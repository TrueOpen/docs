---
title: Staking and penalties
description: Responsibility domains, Cortex Node bonds, penalties, recovery, and exit.
---

# Staking and penalties

TrueOpen separates consensus security from AI service responsibility. A failure in one responsibility domain must not silently consume funds from another.

## Responsibility domains

| Domain | Participant | Purpose |
|---|---|---|
| Consensus stake | Validator | Consensus participation and governance power |
| ServiceBond | Cortex Node | Service admission, Task liability, business penalties, and exit accountability |
| Builder responsibility | Builder | Coordination and data-availability duties |

In Phase 0, a Builder has no funded BuilderBond. Objective Builder faults can still be recorded for audit and governance, but they do not debit Validator consensus stake or a Cortex Node ServiceBond.

Ordinary inference, verification, or data-availability faults never slash Validator consensus stake.

## Operator and service key

Each Cortex Node has one stable operator address and one currently authorized service key.

- The operator controls the ServiceBond, earnings, claims, exit, and key replacement.
- The service key signs handraises, Task material, and permitted self-rescue transactions.
- A compromised service key cannot withdraw the ServiceBond, claim earnings, or change the operator.

A service-key replacement is allowed only after the node stops accepting new work and all accepted Task liabilities and required submissions have closed. Replacement is atomic: the old key loses authority as soon as the new key becomes active.

## ServiceBond lifecycle

| State | Meaning | New Task eligibility |
|---|---|---|
| `REGISTERED` | Bond and operator identity exist | Not until profile support requirements are met |
| `ACTIVE` | Eligible profile support is current | Yes |
| `STALE` | Required support freshness expired | No |
| `JAILED` | Recoverable service fault is active | Only if the protocol gives a non-zero recovery factor |
| `UNBONDING` | Exit or bond reduction is waiting | No new Tasks |
| `TOMBSTONED` | Permanently removed | No |
| `EXITED` | Bond was withdrawn after all liability closed | No |

One ServiceBond can support several profiles. Eligibility is evaluated separately for each Task profile by comparing the active bond with that profile's minimum bond and checking the relevant inference or verification capability.

## Task liability

Handraising expresses willingness, not assignment. When a Cortex Node is selected, the protocol reserves enough slashable ServiceBond for that Task. A node cannot use the same unreserved amount to accept unlimited concurrent liability.

Later changes to a profile's minimum bond do not rewrite an accepted Task. They affect future eligibility after the configured effective boundary and grace period.

## Penalties and recovery

Only objectively attributable protocol facts can create a business penalty. Examples include missing an accepted duty deadline, submitting contradictory signed material, or being disproved by an independent challenge round.

Penalties follow these rules:

- A unique fault can be applied only once.
- Liability is debited from the responsible operator's slashable service funds.
- Active bond, slashable unbonding funds, and applicable claimable earnings may be consumed only in the defined order.
- A shortfall is recorded but does not create protocol debt or draw from another fund.
- Recoverable faults may increase an operator-global jail count and require successful duties before recovery.
- Tombstoned operators cannot recover.

## Unbonding and exit

Starting unbonding stops new Task eligibility but does not erase existing obligations. The waiting period must cover active Tasks, their challenge windows, evidence-retention responsibilities, and delayed fault application.

Withdrawal is allowed only when all accepted liabilities have ended and the unbonding period has matured. This prevents an operator from exiting before the protocol can evaluate work it already accepted.
