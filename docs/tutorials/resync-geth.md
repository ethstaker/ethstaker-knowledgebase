# How to resync Geth

A common reason for Geth to fail can be an unexpected shutdown of a validator machine. Geth uses RAM for temporary memory and during a graceful shutdown some important information will be written to disk. However, during an unexpected shutdown, there isn't time to write to disk (e.g. due to a sudden loss of power) so important data is lost. This loss of data leads to a corruption of the `chaindata` folder, requiring a resync.

* [File Locations](#file-locations)
* [Steps (If the ancient folder exists)](#steps-if-the-ancient-folder-exists)
* [Steps (If the ancient folder does not exist)](#steps-if-the-ancient-folder-does-not-exist)

## File Locations

*   Standard location of the `chaindata` folder.

    ```bash
    /var/lib/goethereum/geth/chaindata/
    ```
*   Standard location of the `ancient` folder.

    ```bash
    /var/lib/goethereum/geth/chaindata/ancient
    ```

## Steps (If the ancient folder exists)

Good news! The required resync can be made much faster than a full resync simply by keeping the `ancient` folder. The ancient folder contains files that are not corrupted during an unexpected shutdown.

1. Stop Geth.
2.  Move the `ancient` folder.

    ```bash
    sudo mv /var/lib/goethereum/geth/chaindata/ancient /var/lib/goethereum/geth/
    ```
3.  Delete the `chaindata` directory and recreate it.

    ```bash
    sudo rm -rf /var/lib/goethereum/geth/chaindata
    sudo mkdir /var/lib/goethereum/geth/chaindata
    ```
4.  Move the ancient folder back to the now empty chaindata directory.

    ```bash
    sudo mv /var/lib/goethereum/geth/ancient /var/lib/goethereum/geth/chaindata
    ```
5.  Change the ownership of the `chaindata` directory to the Geth user.

    ```bash
    sudo chown -R goeth:goeth /var/lib/goethereum/geth/chaindata
    sudo chmod 755 /var/lib/goethereum/geth/chaindata
    sudo chmod 755 /var/lib/goethereum/geth/chaindata/ancient
    ```
6. Start Geth.

Congratulations! You've successfully started a Geth resync 🥳

## Steps (If the ancient folder does not exist)

If the ancient folder does not exist, that's not a problem. It just means you will need to resync Geth from scratch, which will take a bit longer.

1. Stop Geth.
2.  Delete the `chaindata` directory and recreate it.

    ```bash
    sudo rm -rf /var/lib/goethereum/geth/chaindata
    sudo mkdir /var/lib/goethereum/geth/chaindata
    ```
3.  Confirm the ownership and permissions for the `chaindata` directory are set to the Geth user.

    ```bash
    sudo chown -R goeth:goeth /var/lib/goethereum/geth/chaindata
    sudo chmod 755 /var/lib/goethereum/geth/chaindata
    ```
4. Start Geth.

Congratulations! You've successfully started a Geth resync 🥳
