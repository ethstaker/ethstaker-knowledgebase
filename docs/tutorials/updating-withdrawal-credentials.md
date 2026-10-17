# Updating Withdrawal Credentials

As described in [Validator sweeping](../../getting-started/withdrawal-process-explained#validator-sweeping), the only way to receive rewards from the [Beacon chain](../../staking-glossary#beacon-chain) or the initial 32 ETH deposit upon a [validator exiting](../../staking-glossary#5-exiting-validator) is for a validator to have set a [Withdrawal address](../../staking-glossary#withdrawal-address) changing their Withdrawal Credentials from `0x00` to `0x01`.

It is possible upon validator creation to specify a withdrawal address and, if you have done so, there is no need to update your credentials. In fact, **once your credentials have been set to 0x01 it will not be possible to change them in the future**. This is why it is imperative that when you choose a withdrawal address, you **choose one that you have full control over such as a hardware wallet**. It is heavily recommended to **NOT** choose a wallet on an exchange or third party where you do not control the private keys.

**Please note**: If at any point you are confused as to what to do, please ask the EthStaker community for guidance. There are no stupid questions and we always strive to be welcoming first and knowledgeable second.

**eth-docker users:** There is a standalone guide if you use eth-docker [here](https://github.com/ethstaker/eth-docker/tree/main/.eth/ethdo). The following guide can be considered a companion as the steps are very similar.

## Warnings

* **Choose an address you have full control over:** Hardware wallets are preferred and exchange wallets **MUST NOT BE USED**. You may think it is clever to send to a hot wallet or an exchange to avoid extra transaction fees, but you are risking not only your rewards but the initial 32 ETH deposit.
* **Once your withdrawal credentials have changed from 0x00 to 0x01 they can not be changed in the future.**
* **Your mnemonic is required to change your credentials:** Your funds will be locked indefinitely as long as your withdrawal credentials are `0x00`. Without your mnemonic, it will not be possible to update your credentials. Except for extremely rare cases of controlling the withdrawal private key **and** keystores, we recommend searching thoroughly and retracing your steps if you are having trouble locating your mnemonic.
* **Go offline! Security is important:** When making this change, you will be exposing your mnemonic so it is heavily encouraged to perform this action **offline**. Failing to do so could result in the theft of the mnemonic and your validators.
* **All Beacon chain rewards and the initial deposit will go to the specified address automatically without user interaction:** The address specified will be the only location rewards and the initial deposit can go once set. If the specified address becomes compromised, it is advised to work with a White Hat group to recover your funds.
* **Do not throw away your mnemonic after updating your credentials:** Even after the credentials are changed, you are still advised to hold on to your mnemonic as it can be used to regenerate your keystore files if those files become lost. Your mnemonic can be passed on to your heirs. &#x20;

## Choose your tool

There are two primary tools that are used to make the credential change and both have different requirements. Look at both options and choose based on your situation. Normally if you have multiple validators associated with a single mnemonic, ethdo is the preferred approach.&#x20;

#### Waygu KeyGen

A GUI application that provides the functionality available with the Ethereum Staking CLI tool. If you are a non-technical user, this is a perfect choice. It is easy to use and less error-prone than attempting the Staking CLI directly. There is a [standalone video guide](https://www.youtube.com/watch?v=EMQoVtxNaxo) for this tool.

#### ethdo

An extremely powerful CLI tool that is ideal for technical users or those who have multiple validators associated with the same mnemonic. This tool has also proved to be very effective with users who have run into issues with Waygu KeyGen, normally due to misunderstandings. Due to the technical barrier of this tool, the rest of the guide will be centered around how to use it.

## Preparation

In order for ethdo to make the necessary changes, there are a number of things you will need:

* **The ethdo tool**: [https://github.com/wealdtech/ethdo/releases](https://github.com/wealdtech/ethdo/releases)
* **Offline Preparation File:** This is a file that contains information on all validators in the Beacon chain such as the public key, validator index, and current credentials (called the Beacon chain state). This data is required for the tool to make the necessary signature. To generate this file, you can run the following command on your Beacon chain client: \
  \
  `./ethdo validator credentials set --prepare-offline`
* Note: You may not have `ethdo` on your machine and will need to download it\
  \
  If you do not have access to your validator or are using a third party, you can ask the community for a version or [download an older one here](https://github.com/benjaminchodroff/ConsensusLayerWithdrawalProtection/blob/main/offline-preparation.json.mainnet.2023-03-04.tar.gz).
* **The validator mnemonic:** When you generated your validator, you created or provided a [mnemonic key](../../staking-glossary#validator-seed-phrase-mnemonic). If you do not have ownership of this key or have lost it, you will not be able to continue further and make the necessary signature.
* **Offline air-gapped machine:** Because you are going to be exposing the mnemonic to sign this operation, it is recommended to use an offline machine to perform the operation. There are numerous guides on how to create an air-gapped machine and you can [view an example here](https://ubuntu.com/tutorials/create-a-usb-stick-on-ubuntu#1-overview).
* **An execution layer address:** In order to receive funds, you need to specify an execution layer address that you fully control. This would preferably be a hardware wallet such as a ledger but you certainly want to choose an address that has the highest security. After an address is set, if the corresponding wallet were to be compromised, you would have a high likelihood of losing your rewards and initial deposit.
* **A USB flash drive:** The machine you are going to perform this change on will not have access to the internet and thus you will not be able to download or upload anything directly. In order to get the necessary information to the machine and the results from the machine, you will need a flash drive to store said information and results. On this flash drive you should put the `ethdo` cli tool, the `offline-preparation.json` file, and the `address` you wish to set.



## Change your credentials

Before you start this process, understand that until you move your results to an online computer and submit them, you can not mess up this step. Take a breath and relax, we'll get through it together.

**Warning:** It's worth repeating - Please go through the effort of performing this operation on a fully offline computer. A user reported that they made the change online on their work computer and they received a message from their IT staff with their mnemonic included. Luckily for that individual, whoever discovered the mnemonic was a good person and warned them. Please take security seriously.

### Start the offline computer

With the **Live USB** that you created during the preparation step, plug it into your offline machine and boot the computer. You will want to choose the "Try Ubuntu without installing" option. If you get stuck you can follow [this guide](https://ubuntu.com/tutorials/try-ubuntu-before-you-install#3-boot-from-usb-flash-drive).  With the computer online, be sure to shut off all network capabilities by looking in the upper right of the screen for the network icon. Clicking on the icon will give you the option to turn off connection to the internet.

### Get the tools on the computer

Now that you have the offline operations system running, plug in your USB that has `ethdo`, your `address`, and `offline-preparation.json` file. You will likely see a notification appear that the device was detected and clicking on that device will open the file explorer to that device.\
\
At this point, we are going to be operating in a **Terminal** which will allow us to execute the `ethdo CLI` and create the operation. You can open the Terminal by clicking on `Activities` in the top left and then typing `terminal`. If you get stuck, you can follow a guide [here](https://ubuntu.com/tutorials/command-line-for-beginners#3-opening-a-terminal).&#x20;

In the terminal, we are going to copy the contents of the flash drive to your local device to avoid any permission issues. To do so, you first need to locate your drive contents. Usually running these commands will find it:

```bash
cd /media/usb/
ls -la
```

Once found, you can run :

```bash
pwd
```

and copy the resulting location along with the usd drive name.

Now to copy the contents, we can navigate back to our `home` and run a command to copy the contents and fix the permissions:

```bash
cd ~
cp <PWD_RESULT>/* ~
chmod 777 *
```

Where `<PWD_RESULT>` is the result of your command above. Something similar to:

```
cp /media/usb/my-usb/* ~
```

At this point, running:

```
./ethdo
```

should result in the CLI executing and providing a list of all the commands it has to offer.

### Create the operation

Now with your address and mnemonic on hand, you can run the following command and fill in the necessary information:

```
./ethdo validator credentials set --offline --withdrawal-address="0x12341234...12341234" --mnemonic="test ocean pyramid my 24 words pyrmaid ocean test"
```

Where the `withdrawal-address` is the execution address you **FULLY CONTROL** and the `mnemonic` is the 24 word phrase that was used or created when you made your validators.

This should output a `change-operations.json` file with your changes. If you run into any issues, please view the [#faq](#faq) or ask us on Discord. We are always happy to help in any way we can.

### Submit the operation

In order to submit the operation, we need to transfer the `change-operations.json` file to a computer with a connection to the internet. Copy the `change-operations.json` file to your USB through the file explorer or the following command:

```bash
cp change-operations.json <PWD_RESULT>/
```

again, should be similar to:

```bash
cp change-operations.json /media/usb/my-usb/
```

You can now safely shut off the air-gapped computer.&#x20;

Plug in the USB to a computer you are comfortable with that has an internet connection.

Open the `change-operations.json` file and look for an attribute called `to_execution_address`. That is the address your Beacon chain rewards will go to. **Be absolutely sure this is the address you specified and have full control over.** Sending a test transaction to and from the address is advised.

Once you have verified the address, you can submit using Beaconchain's [broadcasting tool](https://beaconcha.in/tools/broadcast) or you can transfer the file to your Beacon chain node and run the following command:

```bash
curl -X POST -H 'Content-Type: application/json' -d @change-preparation.json http://<IP>:5052/eth/v1/beacon/pool/bls_to_execution_changes
```

Where `<IP>` is the address of your node, most likely `localhost`

### Verifying changes

At this point, the submission process and propagation should be near instantaneous. Look up your validator on the [beaconcha.in](https://beaconcha.in/) and see if the withdrawal credentials have been updated. When viewing a validator, there is a `Deposits` section which should note the change of your credentials.&#x20;

At this point, your credentials have been updated and you will automatically receive your Beacon chain rewards as described [here](../../getting-started/withdrawal-process-explained#validator-sweeping).

## FAQ

#### My credentials are 0x01. Do I have to do anything?

Nope. You are all set! You will periodically receive your rewards as defined [here](../../getting-started/withdrawal-process-explained#validator-sweeping).

#### How can I change my withdrawal address again?

After you have set a withdrawal address, changing your credentials from 0x00 to 0x01, it is **NOT** possible to change them again. If you would like to have your rewards and deposit go to a different address, you will need to exit the validator and reenter with the desired address specified.

#### I have my deposit mnemonic. Can I change my credentials?

The only way to submit a valid credential change is if the operation is signed by the **Mnemonic you created the validators with**. This is normally a 24-word phrase. Your deposit account is irrelevant unless you specified your deposit mnemonic when creating your validators.&#x20;

#### I lost my mnemonic. Won't the funds go back to the deposit address?

We are sorry to say no.  Beacon chain rewards and the initial deposit can only go to the set address or will remain locked indefinitely if the credentials are 0x00. During the development of the Beacon chain and at the time of its launch, it was expected that 0x00 credentials could be used to handle withdrawals directly. But due to changes in future development plans, it was decided that an execution layer address would need to be specified forced the `0x00` to `0x01` change.

#### I'm 100% certain I have the correct mnemonic. Why is the credentials set command failing?

`ethdo` works by searching the Beacon chain state for the public keys corresponding to the mnemonic provided. It attempts 1024 different indices (also known as paths or positions) before failing. If you use a third party such as **StakeFish** or **Staked.Us**, it is possible the public key will not match. You can get around this by using your private key instead. Please follow these instructions and get in contact with the EthStaker community if you have issues:

```bash
./ethdo account derive --mnemonic="pyramid 24 words test" --show-private-key --path="m/12381/3600/0/0"h
```

This will output the `private key` of the 0th path. Copy that value and try this command:

```bash
./ethdo validator credentials set --offline --withdrawal-address="0xADDRESS_YOU_CONTROL" --private-key="PRIVATE_KEY_FROM_ABOVE"
```

Then follow the same [submission instructions](#submit-the-operation).

#### The change-operations.json is showing a weird 0x010000000 value! What is that?

When you have set a withdrawal address, the credentials have a pattern of `0x01` followed by 22 `0` and then your address without the `0x` prefix. So if your address was `0x123456789abcdeedcba987654321012345789abc` your credentials would be `0x010000000000000000000000123456789abcdeedcba987654321012345789abc` after it was successfully changed.
