# Ethereum Validator Types & Lifecycle

The Pectra upgrade introduced significant enhancements to validator roles, behaviors, and transitions. This document supplements the core withdrawals explainer by outlining validator types, lifecycle actions, and related mechanisms.

## Validator Types

| Type   | Description                                                                 |
|--------|-----------------------------------------------------------------------------|
| 0x00   | Legacy BLS withdrawal credentials (non-upgradable, no EL-triggered actions) |
| 0x01   | ETH1 (execution layer) withdrawal credentials                               |
| 0x02   | Compounding validator — supports EL-triggered exits, partial withdrawals, and consolidations |

- `0x00` can be upgraded to `0x01` using an exit and withdrawal credentials change.
- `0x01` can be upgraded to `0x02` via the `switch_to_compounding_validator` mechanism.
- `0x02` validators are eligible for advanced features like top-ups and consolidations.

## Lifecycle Transitions

### 0x01 → 0x02 (Compounding Upgrade)

- Can be triggered via execution layer.
- Effective balance (EB) is retained.
- Any balance above EB is queued as a top-up via the **entry queue**.
- Top-ups are subject to churn limits.

### Top-Ups (0x02 Only)

- Additional ETH can be added to 0x02 validators via the **entry queue**.
- Entry queue is governed by the churn limit (256 ETH/epoch).
- Top-ups increase effective balance incrementally (hysteresis applies).

### Consolidation (New in Pectra)

- Merge one validator into another `0x02` validator.
- Initiated via execution layer (from withdrawal address).
- Effective balance is transferred directly to the target validator.
- Any excess balance is **swept to the withdrawal address** (not added to the target).
- Consolidations bypass the standard exit queue and instead use the **consolidation queue** (2 per block limit).
