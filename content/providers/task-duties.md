---
title: Worker and Verifier duties
description: Understand when a compute provider accepts responsibility and how Cortex completes it.
---

# Worker and Verifier duties

Cortex discovers Task opportunities through Builder messages, but provider responsibility begins only after chain confirmation.

## Before offering capacity

Cortex evaluates inexpensive checks before downloading Task data:

- Chain synchronization and signer availability
- Order identity, Profile, budget, anchor, and deadline
- Candidate membership and role separation
- Profile support, capability, and runtime digest
- Available capacity and ServiceBond liability
- Local price floor and deadline risk

Declining to sign a handraise affects only this provider. It does not reject the User's Task or create a penalty. Before sending a handraise, Cortex persists the Task Profile lease and signed digest; retries reuse the same material.

## Worker duty

After the chain confirms Worker assignment, Cortex:

1. Reconciles the Task, order hash, Profile, and operator assignment.
2. Downloads and verifies the input from the Task Builders.
3. Calls the adapter's `Infer` capability.
4. Validates the returned bindings and evidence.
5. Persists output, evidence, and the signed receipt before sending them.
6. Streams signed output to the Task Builders.
7. Submits the receipt through a Builder and watches for chain acceptance.
8. Uses the permitted self-rescue path if relay acceptance approaches its deadline.
9. Retains Worker evidence through challenge and cleanup.

A Nexus acknowledgement proves transport, not completion. The duty is accepted only after chain reconciliation.

## Verifier duty

After the chain confirms Verifier assignment, Cortex:

1. Persists the round-specific Task lease.
2. Downloads and validates the input, output, Worker evidence, and frozen Profile context.
3. Reports data unavailability through the protocol path if no Task Builder provides a complete valid set.
4. Calls `Verify` for every committed generated position.
5. Validates the metric summary, root, evidence bundle, and candidate result.
6. Persists and submits the result commitment.
7. Waits for the chain reveal phase, then submits the matching reveal.
8. Retains Verifier evidence until final cleanup eligibility.

Round 1 and challenge-round leases are isolated. Material from one round cannot be reused in another.

## Deadlines and fallback

Cortex tracks chain-height deadlines and begins fallback before the cutoff:

1. Retry the current Builder.
2. Try another fixed Task Builder where permitted.
3. Submit the same material through the service-key self-rescue path where permitted.
4. Stop producing new conflicting material after the deadline.

Self-rescue does not authorize Cortex to alter a receipt, commitment, or result after failed relay. See the [inference](../protocol/v1/tasks/task-02-inference.md), [open verification](../protocol/v1/tasks/task-03-open-verify.md), and [verification](../protocol/v1/tasks/task-04-verification.md) pages for cross-component sequences.
