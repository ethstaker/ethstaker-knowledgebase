# Validator Queues & Execution-Layer Actions (Post-Pectra)

This document details the types of queues involved in validator lifecycle operations and how execution-layer-triggered actions are processed.

## Consensus-Layer Queues

| Queue                  | Purpose                               | Limit                     |
|------------------------|----------------------------------------|----------------------------|
| Entry Queue            | Validator activations & top-ups        | 256 ETH/epoch              |
| Exit Queue             | Full exits & EL-triggered withdrawals  | Churn-limited              |
| Withdrawability Delay  | Delay after exit before funds are sweep-eligible | ~27 hours           |
| Consolidation Queue    | Validator merges (new in Pectra)       | 2 per block                |

- All **exits** and **manual partial withdrawals** go through the **exit queue**.
- **Automatic withdrawals** (via sweep) are not subject to the exit queue.
- **Sweep cycle** processes up to 16 automatic withdrawals per block.

## Execution-Layer Triggered Actions (EIP-7002)

Only available to validators with 0x01 or 0x02 withdrawal credentials.

| Action Type               | Validator Types | Queue Used     | Notes                                           |
|---------------------------|-----------------|----------------|-------------------------------------------------|
| Manual Partial Withdrawal | 0x02 only       | Exit Queue     | Requires gas, deducted after queue processing   |
| Full Exit (EL-triggered)  | 0x01 and 0x02   | Exit Queue     | Equivalent to voluntary exit from validator keys|

## Smart Contract Enforcement

Execution-layer-triggered actions (via [EIP-7002](https://eips.ethereum.org/EIPS/eip-7002)) are enforced using smart contract queues:

- **Minimum gas fee logic** exists to prevent spam.
- If the EL fee is too low, the transaction is rejected (no revert message).
- These smart contract queues act as a rate-limiting interface between EL and consensus.

## Monitoring Tools

- [validatorqueue.com](https://www.validatorqueue.com/): Tracks exit/withdrawal queue length.
- [pectrified.com](https://pectrified.com/mainnet): Monitors pending consolidations, top-ups, withdrawals.
