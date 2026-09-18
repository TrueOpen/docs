---
title: Candidate selection
description: Eligibility, handraises, snapshots, and deterministic Task assignments.
---

# Candidate selection

Candidate selection separates four ideas that must not be conflated:

1. An eligible Cortex Node satisfies the on-chain requirements for a Profile and duty.
2. A handraise is that node's signed willingness to accept one Task duty.
3. A candidate set is the frozen union of valid handraises.
4. A selected Worker or Verifier is an assigned participant chosen from that frozen set.

A handraise is not an assignment, a reputation score, or proof that a node failed when it did not volunteer.

## Eligibility

Common eligibility checks include:

- The Model and Profile allow new Tasks.
- The Cortex Node is not tombstoned or actively exiting.
- Its ServiceBond satisfies the Profile minimum and has capacity for Task liability.
- Its support declaration is fresh and matches the exact `model_id` and `profile_version`.
- It declares the required inference or verification capability.
- It is not assigned both Worker and Verifier responsibility for the same Task.
- Any jail factor permits participation under the defined recovery rules.

Local benchmarks, GPU utilization, self-reported hardware, HTTP latency, heartbeats, and Builder arrival order are not consensus eligibility or weight inputs.

## Handraises

A handraise binds the chain, Task, duty, Profile, relevant Task commitment, candidate snapshot, operator, expiry, and signing domain. A Builder may collect and relay handraises but cannot edit them or turn its private ordering into protocol priority.

Valid handraises are merged monotonically into an authoritative on-chain union. A later proposal may add newly validated candidates but cannot remove previous candidates, switch order versions, or substitute a different candidate index.

## Immutable snapshots

At the selection cutoff, the protocol freezes:

- The membership mapping and candidate set
- Each candidate's stable operator identity
- Bond and support facts used for eligibility
- The candidate-weight method and inputs
- The relevant randomness height

Later stake, support, jail, or Profile changes do not rewrite that historical set. A newly disqualifying terminal condition may force the Task down a defined failure and refund path, but it cannot authorize choosing someone outside the frozen candidates.

## Worker and Verifier selection

The Worker is chosen by a weighted, unbiased draw after the Worker set freezes and a future beacon becomes available.

Verifier selection uses two future beacons. The first produces a bounded candidate window from a previously frozen eligibility source. Valid handraises are then collected and frozen. A later beacon selects the required Verifiers without replacement from that legal set.

Challenge rounds exclude participants from earlier rounds so the new result is independently produced.
