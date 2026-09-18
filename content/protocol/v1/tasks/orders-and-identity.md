---
title: Orders and task identity
description: Sessions, signed orders, Task identity, replacement, and budget admission.
---

# Orders and task identity

A User submits work through a Session. The Session owns an ordered sequence of Task positions and prevents an old order from being replayed as a new request.

## Session and sequence

A Session has one owner and a monotonically increasing expected order sequence. Creating a Session is an on-chain action, so the User account and public key are available before any offline order signature is evaluated.

For a new Task, the submitted sequence must equal the Session's next expected sequence. The sequence is consumed only when the first valid Open Task proposal is accepted. Failed local uploads or rejected proposals do not advance it.

## Stable position and signed version

TrueOpen distinguishes:

- `task_id`, the stable position derived from the Session and order sequence.
- `task_hash`, the digest of one exact TaskOrder version.

This distinction allows a User to replace an unaccepted order at the same Task position while preserving a stable reference. Once the first proposal is accepted, its `task_hash` becomes authoritative and competing versions are rejected.

A signed order binds at least the User, Session, order sequence, chain, model Profile, generation constraints, price bid, maximum fee, expiration, and the anchor inputs needed to determine the Task Builders. The signature does not become a general transaction authorization.

## Admission is atomic

The first accepted Open Task proposal must validate all of these before changing state:

- User signature and Session ownership
- Expected sequence and unexpired order
- Model and Profile admission state
- Budget arithmetic and User balance
- Candidate-pool and Builder-set snapshots
- At least one valid Worker handraise

Only after all checks pass does the protocol consume the sequence, freeze `max_fee` in Task escrow, lock the order version, and record the Task snapshots. Partial admission is forbidden.

## Historical stability

The Task freezes the Profile version, pricing inputs, verification rules, maintenance rate, gas-reimbursement policy, candidate source, Builder set, and other versioned rules used by later stages.

Governance or market changes after admission affect future Tasks. They do not change the price, judgment rule, candidate weight, or Task Builder group of an accepted Task.
