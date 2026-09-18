---
title: Governance
description: Governed actions, hard limits, emergency controls, and protocol upgrades.
---

# Governance

TrueOpen governance converts an accepted on-chain proposal into a typed, deterministic protocol action. Passing a vote grants authorization; it does not allow the action to bypass protocol invariants.

## Voting baseline

Phase 0 uses bonded Validator consensus stake as governance voting power and the Cosmos SDK governance lifecycle for deposits, voting, tallying, and proposal results.

ServiceBonds, Builder status, Profile support, and business revenue do not create governance voting power. Governance deposits use the business asset. Any governance path described as burning a USDC deposit instead transfers the applicable amount to the treasury.

## Governed actions

Governance may authorize:

- Future-effective parameter changes within hard limits
- Model or Profile freeze, unfreeze, and delisting
- Emergency freeze and explicit recovery actions
- Treasury spending
- Full Validator-set changes through the restricted lifecycle
- Full Builder-set replacement
- Bridge signer rotation and bridge cutover
- Scheduled software and protocol upgrades

Each action binds its proposal result, target, type, effective boundary, and deterministic action digest. Exact replay is a no-op; reuse of the same locator with different content is rejected.

## Future-effective changes

Parameters that affect admission, selection, payment, or responsibility apply at a specified future height or epoch. An accepted Task continues using its frozen snapshots.

Governance cannot retroactively reinterpret a signature, change a historical price, replace an assigned participant, recalculate a closed round, or create rewards for an earlier period.

## Emergency controls

Emergency actions are narrow and attributable. A freeze can stop new exposure while preserving the deterministic completion or refund of existing obligations.

An emergency action must not:

- Confiscate funds outside an existing penalty rule
- Skip supply or escrow invariants
- Make an off-chain administrator the final protocol judge
- Automatically unfreeze without a new authorized action and invariant check

## Validator and Builder sets

Phase 0 uses a governed Validator set and a governed fixed Builder set.

Builder membership changes use a complete future-effective replacement, not an add/remove delta or automatic score-based rotation. Existing Tasks retain the Builder set they locked at admission, including its remaining data and submission responsibilities.

Validator membership and bridge-signer membership are coupled by the bridge safety rules. A change that affects the set must coordinate bridge freeze and signer cutover before normal bridge operation resumes.

## Protocol upgrades

A regular parameter proposal cannot change message types, signed encodings, state schema, randomness proofs, judgment-function inputs, or account structures. Those changes require a versioned software upgrade with deterministic migration and invariant checks.

An upgrade must preserve or explicitly migrate historical verification and accounting facts. New code cannot reinterpret an old signature, settlement, or claim using new rules.
