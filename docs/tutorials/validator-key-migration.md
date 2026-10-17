# Safely migrating validator keys

> When migrating validator keys, take your time, do not rush!

There are many scenarios where you need to move the validator keys from one machine to another, here are some examples:

* ⬆️ Upgrading hardware.
* 🔧 Recovering from a hardware failure.
* ☁️ Migrating from a cloud hosting service to a home staking machine.

In any of these cases, the procedure should be the same. The most important thing to remember is that the penalty for being offline is **very low**, so do not optimize for minimum downtime. A slashing event caused by incorrect key migration will incur a penalty equivalent to **MONTHS** of simply being offline.

🚨 _Do not rush_ 🚨

## Definitions

**Source**: Where the keys are coming from.\
**Target**: Where the keys are being migrated to.

## Steps

1. Stop the validator client on the source machine.
2. Stop the validator client on the target machine.
3. Wait a **MINIMUM** of 2 finalized [epochs](../../staking-glossary#epoch) before continuing.
4. Copy the validator keys to the target machine either through intermediate storage (e.g. a USB) or directly from source to target machine (e.g. `scp`, `rsync`, etc.). If the validator keys have been lost due to a hardware failure, [generate them again](../../validator-keys/secure-key-generation).
5. Delete the keys from the source machine. This ensures that even if the source machine restarts unexpectedly, the validator signing keys won't exist so cannot be used by the validator client.
6. If available, export any [slashing protection](../../validator-keys/slashing-protection) from the source machine and import on the target machine.
7. Turn off the source machine and be 100% sure it cannot be restarted.
8. Start the validator client on the target machine.
9. Import the validator keys.
10. Check the validator client logs to confirm everything is working correctly.

Congratulations! You've successfully migrated your validator keys between two machines 🥳
