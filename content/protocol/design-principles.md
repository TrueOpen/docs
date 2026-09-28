---
title: Design principles
description: The reasoning behind TrueOpen's execution, verification, and accountability boundaries.
---

# Design principles

TrueOpen coordinates inference across independent participants. These principles explain the design; the [V1 rules](v1/README.md) specify the behavior that implements it.

## Off-chain execution, on-chain accountability

Model execution and bulk Task data stay off-chain. The chain records commitments, assignments, deadlines, and accounting. This keeps the consensus workload separate from model computation while giving participants a shared record of responsibility.

## Independent verification

Execution and judgment are distinct duties. A Worker produces output and evidence; independently assigned Verifiers evaluate that material using the frozen Profile. Commit-reveal separates committing to a result from disclosing it. Challenges provide an additional independent round under the protocol's rules.

Verification is bounded by the selected Profile's algorithm and evidence requirements. It does not establish that every generated statement is factually true.

## Freeze inputs before selecting participants

Candidate facts freeze before the selection beacon becomes known. Future randomness limits the ability to tailor a candidate set to a known draw. Domain separation keeps different selection purposes independent. See [Selection and randomness](v1/foundations/randomness.md).

## Make responsibility explicit

An offer of capacity, a transport acknowledgement, and an accepted assignment are different facts. The chain determines when a provider becomes accountable. ServiceBond liability belongs to the service operator, while consensus stake protects a separate responsibility domain.

## Preserve historical meaning

Tasks retain their accepted Profile, order, rule versions, and parameter snapshots. Later changes must not reinterpret work already accepted. This allows independent participants to verify the same result even when software and network settings evolve.

## Settle deterministically

Success, timeout, unavailable data, and failed verification need defined outcomes. Funds remain separated by purpose, and settlement records finality together with the accounting result. Missing facts or violated invariants must not be repaired with local guesses.
