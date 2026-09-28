---
title: Economics
description: Phase 0 assets, Task budgets, payouts, challenge economics, and treasury boundaries.
---

# Economics

Phase 0 uses canonical USDC as its sole business and transaction-fee asset. It has no transferable native token and no protocol emission rewards.

The genesis-defined `business_denom` is used for Task budgets, ServiceBonds, registration fees, challenge funds, claimable earnings, treasury balances, and transaction fees. Validator `ubond` exists only for consensus and governance accounting and cannot enter a business payment path.

## Isolated funds

| Fund | Purpose |
|---|---|
| User balance | Funds orders, bonds, challenges, and transaction fees |
| Task escrow | Holds the maximum fee of an accepted, unfinished Task |
| Rewards | Holds finalized but unclaimed service earnings and eligible gas reimbursement |
| Service bond | Holds slashable Cortex Node responsibility funds |
| Challenge bond | Holds the opener bond and challenge-round verification budget |
| Treasury | Holds maintenance fees, registration fees, and penalty residuals |

Funds cannot cover one another's shortfalls. The protocol does not create debt, mint missing balances, or borrow from the treasury to complete a payout.

## Task budget

At admission, the order freezes a maximum output size, price bid, maximum fee, verification ratio, transaction-fee reserve, maintenance rate, and applicable calculation versions.

The chain derives maximum Worker and Verifier amounts using checked integer arithmetic. It rejects the Task before consuming the Session sequence or moving funds if the order is below the Profile minimum, exceeds `max_fee`, uses an unsupported rule version, or overflows.

The full `max_fee` moves to Task escrow. Unused funds are not revenue; they return to the User at finality.

## Work measurement and payment

The Worker's signed generated-token count is bounded by the order and must be independently confirmed by a sufficient cluster of valid Verifier results. If the counts do not agree, the protocol does not silently truncate or average them.

At final settlement:

- A successful, non-disproved Worker is paid for the confirmed work units at the frozen price.
- Only eligible round-1 Verifiers in the effective consensus cluster receive Task verification fees.
- Missing, invalid, minority, or disproved slots are not redistributed to other participants.
- Maintenance is deducted from each applicable gross payment and sent to the treasury.
- Eligible recorded Task transaction fees can be reimbursed within frozen per-transaction and per-Task caps.
- Every remaining escrow unit is refunded.

Failed assignment, Worker timeout, unavailable verification, or no consensus produces the defined zero-service-payment and refund path, less only explicitly eligible recorded costs.

## Claims and issuance

Service earnings become claimable only after Task finality. Task submission, a provisional verdict, or a closed first round does not create withdrawable income.

Phase 0 issuance is always zero. Validators may receive transaction fees through the standard fee collector; that is not an emission reward. Builders receive no issuance reward and only the narrowly permitted Task transaction-fee reimbursements.

## Treasury

The treasury receives maintenance fees, registration fees, and defined bond or penalty residuals. Spending requires an accepted typed governance action. The treasury cannot automatically subsidize a Task, challenge, bridge transfer, bond withdrawal, or service payout.

Every fund has a supply-to-ledger invariant. A mismatch is a consensus error and must not be repaired by silently minting, burning, transferring between funds, or clearing state.
