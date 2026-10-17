# Withdrawal process explained

### Staking rewards

Reward payments are automatically processed for active validator accounts with a maxed-out effective balance (32 ETH for legacy validators, 2048 ETH for compounding 0x02 validators).

Any balance above the effective balance cap earned through rewards does not actually contribute to a validator’s weight on the network, and is thus automatically withdrawn as a reward payment every few days. These are called **partial withdrawals**.

These automatic partial withdrawals are initiated on the consensus layer via the sweep process, which continuously scans validator indices and includes eligible withdrawals in block proposals. No action is required by the validator operator, and no gas (transaction fee) is needed.

Validators using **execution-layer (0x01 or 0x02) withdrawal credentials** may also manually trigger partial withdrawals via the execution layer, using the withdrawal address (not validator keys). These **manual partial withdrawals** still require the validator to wait in the exit queue before being processed.

### Exiting staking entirely

Providing a withdrawal address is required before _any_ funds can be transferred out of a validator account balance.

Users looking to exit staking entirely and withdraw their full balance must either:

- Submit a **voluntary exit** using their validator keys (via the validator client), or  
- Trigger a **full exit** via an **execution-layer transaction** from the withdrawal address (supported for 0x01 and 0x02 validators via [EIP-7002](https://eips.ethereum.org/EIPS/eip-7002)).

Either approach initiates the validator's removal from the active set. This action does **not** require gas if done via validator keys (consensus-layer), but **does** use gas if triggered from the execution layer.

The process of a validator exiting takes a variable amount of time, depending on how many others are exiting or withdrawing at the same time. All exits and EL-triggered partial withdrawals are processed in the same **exit/withdrawal queue**, which can become congested. You can check the current queue at [validatorqueue.com](https://www.validatorqueue.com/).

Once the validator reaches the front of the queue and completes the **withdrawability delay** (~27 hours), the validator’s full balance becomes eligible to be withdrawn.

At that point, there is nothing more a user needs to do. The validator is automatically swept, and its entire balance is transferred to the withdrawal address during the next [sweep](https://ethereum.org/en/staking/withdrawals/#validator-sweeping). This is known as a **full withdrawal**.

### How do withdrawal payments work?

Whether a given validator is eligible for a withdrawal is determined by the state of the validator account. No user input is needed during normal operation — the process is automatically coordinated by the consensus layer.

However, users with 0x01 or 0x02 withdrawal credentials may optionally **trigger withdrawals manually via the execution layer**, using their withdrawal address. This includes:

- **Manual partial withdrawals** (only for 0x02)
- **EL-triggered full exits** (for 0x01 or 0x02)

These require gas and must pass through the **exit/withdrawal queue**.

#### Validator "sweeping"

When a validator is scheduled to propose the next block, it is required to build a withdrawal list of up to 16 eligible withdrawals. This is done by sequentially scanning validator indices, starting where the last block left off.

Validators are checked for **automatic** withdrawals (either partial or full). Manual withdrawals (triggered via the EL) are not included in this sweep — they are processed directly after passing through the shared exit/withdrawal queue.

!!! info "Info"

    Think about an analogue clock. The hand on the clock points to the hour, progresses in one direction, doesn’t skip any hours, and eventually wraps around to the beginning again after the last number is reached.\
    \
    Now instead of 1 through 12, imagine the clock has 0 through N _(the total number of validator accounts that have ever been registered on the Beacon Chain)._\
    \
    The hand on the clock points to the next validator that needs to be checked for automatic withdrawals. It starts at 0, and progresses all the way around without skipping any accounts.

**Automatic withdrawal eligibility checks:**

While a proposer is sweeping through validators for possible automatic withdrawals, each validator is evaluated against the following:

1. **Has a withdrawal address been provided?**  
   If no withdrawal address has been provided, the validator is skipped.

2. **Is the validator exited and withdrawable?**  
   If yes, a **full withdrawal** is triggered, transferring the validator’s entire balance to the withdrawal address.

3. **Is the validator active and its effective balance maxed out?**  
   If yes, and the actual balance exceeds the effective balance cap, a **partial withdrawal** is made to transfer only the excess.

### Manual withdrawals and exits

With the introduction of [EIP-7002](https://eips.ethereum.org/EIPS/eip-7002), validators with `0x01` or `0x02` withdrawal credentials can:

- Trigger a **partial withdrawal** (0x02 only) from the execution layer.
- Trigger a **full exit** (0x01 or 0x02) from the execution layer.

These actions require an on-chain transaction from the withdrawal address and consume gas. After being submitted, they are queued in the shared **exit/withdrawal queue** and processed in order.

Once dequeued and processed by the consensus layer, the funds are transferred to the withdrawal address. These manual withdrawals **do not** wait for the sweeping cycle — they are processed directly after exiting the queue.

### Gas free

For automatic withdrawals (partial or full), no transaction is required. This means:

- **No gas (transaction fee)** is required.
- Withdrawals do not compete for block space on the execution layer.

### How frequently will I get my staking rewards?

A maximum of 16 **automatic withdrawals** can be included in each consensus block. This means up to 115,200 validator withdrawals per day can be processed (assuming no missed slots).

Withdrawals are only made if the validator meets the automatic withdrawal criteria. Validators without eligible balances are skipped, which increases the efficiency of the sweep.

Estimated sweep duration:

| Number of validators | Time to sweep once |
|:--------------------:|:------------------:|
|       800,000        |      7.0 days      |
|       900,000        |      7.8 days      |
|     1,000,000        |      8.7 days      |
|     1,100,000        |      9.6 days      |

For real-time queue status and forecasts, see [validatorqueue.com](https://www.validatorqueue.com/) or [pectrified.com](https://pectrified.com/mainnet).

**Source:** [https://ethereum.org/en/staking/withdrawals/](https://ethereum.org/en/staking/withdrawals/)
