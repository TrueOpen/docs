---
title: Selection and randomness
description: The proposer-VRF beacon and deterministic selection rules in TrueOpen V1.
---

# Selection and randomness

This page explains the randomness used for assignment. [Candidate selection](../tasks/candidate-selection.md) defines eligibility, candidate snapshots, handraises, weights, and assignment rules.

TrueOpen uses a proposer-generated, validator-verified VRF beacon as the only source of consensus randomness for Task assignment.

## Beacon chain

At every required height, the block proposer includes a canonical beacon carrier containing the height, proposer identity, VRF output, and proof. Other validators verify it before accepting the block.

The VRF input binds:

- A protocol domain
- The chain ID
- The block height
- The previous verified beacon output
- The proposer's consensus identity

Each Validator registers a separate VRF key. The consensus key is not reused as the VRF key. Key activation and rotation occur at deterministic epoch boundaries so every validator resolves the same active key for a height.

An invalid or missing required proof rejects the block. The protocol does not substitute a block hash, local random value, wall clock, indexer observation, or off-chain service.

## Domain separation

A raw beacon value is never used directly. Each consumer derives randomness with a purpose-specific domain and context that binds the Task, candidate snapshot, selection stage, and version.

Worker selection, Verifier-window construction, Verifier selection, and any future reward marking use separate derivation domains. Signature bytes, map iteration order, local arrival order, and nonces that a participant can manipulate are excluded.

## Future-beacon rule

Candidate facts must freeze before the beacon used to select from them becomes known.

For Worker assignment, the handraise union and candidate weights freeze first. A later beacon selects one Worker from that immutable set using unbiased weighted integer sampling.

Verifier assignment uses two later beacons:

1. Beacon A derives a bounded window from a previously frozen eligible population.
2. Valid handraises close and form an immutable legal set.
3. Beacon B selects the Verifiers without replacement from that set.

Challenge rounds follow the same anti-prediction principle and exclude participants from earlier rounds.

## Task Builder selection

Task Builders must be known before an order is submitted, so their selection does not wait for a future beacon. It is a deterministic, domain-separated function of the signed order's fresh chain anchor, Task identity, and Builder-set commitment.

The resulting Builder group is fixed when the Task is accepted and reused for all Task stages.

## Missing randomness

If a required future beacon is unavailable, the protocol may delay the indexed transition or use a specifically defined conservative failure and refund path. It must not switch to another random source or choose a participant outside the frozen set.

V1 does not enable VDF or BLS randomness paths.
