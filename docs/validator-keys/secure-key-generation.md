# Secure key generation

=== "Download CLI app"
    **Step 1:** Download the [deposit command line interface app↗](https://github.com/ethereum/staking-deposit-cli/releases/) for your operating system.

    !!! info "Info"
        Please make sure that you are downloading from the official Ethereum Foundation GitHub account by verifying the url: **<https://github.com/ethereum/staking-deposit-cli/releases/>**
    

    <figure><img src="/assets/img/gitbook/image (16).png" alt=""><figcaption></figcaption></figure>

    **Step 2:** Generate deposit keys using the Ethereum Foundation deposit tool

    !!! info "Info"
        For security, we recommend you disconnect from the internet to complete this step.
    

    * Decompress the file you just downloaded.
    * Use the terminal to move into the directory that contains the deposit executable.
    * Run the following command to launch the app.

    `./deposit new-mnemonic --chain mainnet`&#x20;

    Please make sure you have set `--chain mainnet` for Mainnet, otherwise the deposit will be invalid.&#x20;

    Now follow the instructions presented to you in the terminal window to generate your keys.


=== "Download Key Gen GUI app"
    TODO


=== "Build from source"
    TODO




These tools can be used as an alternative to the [Staking Deposit CLI ↗](https://github.com/ethereum/staking-deposit-cli/) to help with key generation.

| Wagyu Key Gen                                                                                                             | ethdo                                                                                                                     | Avado                                                                                                                     |
| ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| `Linux` `macOS` `Windows` `GUI`                                                                                           | `Linux` `Windows` `CLI`                                                                                                   | `Browser` `GUI`                                                                                                           |
| <p>✅ OPEN SOURCE</p><p>✅ AUDITED</p><p>❌ BUG BOUNTY</p><p>✅ BATTLE TESTED</p><p>✅ PERMISSIONLESS</p><p>✅ SELF CUSTODY</p> | <p>✅ OPEN SOURCE</p><p>✅ AUDITED</p><p>❌ BUG BOUNTY</p><p>✅ BATTLE TESTED</p><p>✅ PERMISSIONLESS</p><p>✅ SELF CUSTODY</p> | <p>✅ OPEN SOURCE</p><p>❌ AUDITED</p><p>❌ BUG BOUNTY</p><p>✅ BATTLE TESTED</p><p>✅ PERMISSIONLESS</p><p>✅ SELF CUSTODY</p> |
| [Get started ↗](https://wagyu.gg/)                                                                                        | [Get started ↗](https://github.com/wealdtech/ethdo)                                                                       | [Get started ↗](https://ava.do/)                                                                                          |

[Source ↗](https://ethereum.org/en/staking/solo/#key-generators)
