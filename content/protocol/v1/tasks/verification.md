---
title: Verification
description: Independent result checking, commit-reveal, verdict formation, and failure paths.
---

# Verification

Verification checks whether the Worker's committed output satisfies the judgment rules frozen by the Task's Profile.

## Frozen execution context

Every Verifier evaluates the same Task-bound context:

- Input and output commitments
- Model and Profile version
- Manifest, tokenizer, and schema commitments
- Judgment-function and canonical-encoding versions
- Evidence schema
- Effective generation parameters
- Worker's signed inference receipt

A Verifier cannot substitute another Profile, tokenizer, runtime interpretation, or generation default.

## Full-output verification

V1 verification evaluates all committed generated token positions using the Profile's defined prefill or teacher-forcing procedure. Normal verification does not sample a subset of output positions.

This keeps the verification target stable: the Worker commits to one result, and each selected Verifier independently evaluates the same complete committed output.

## Commit then reveal

Verification uses a commit-reveal sequence:

1. A selected Verifier computes its result and commits to the result payload with a private salt.
2. After the commit boundary, it reveals the result material and salt.
3. The chain verifies that the reveal matches the earlier commitment and the Task context.

This prevents a Verifier from waiting for another participant's visible answer and copying it into a valid late commitment.

A commit or reveal is accepted only for the selected operator, current round, expected Profile, active deadline, and current service authorization. Once accepted, the fact belongs to the stable operator even if its service key later changes.

## Verdict formation

Each valid result binds its sample verdict, work-unit count, metric summary, evidence commitment, and Task context. Results with inconsistent counts, invalid evidence commitments, bad signatures, late submissions, or unmatched commits are excluded.

The protocol forms a verdict only from a sufficiently large consistent result cluster. A minority result is not rewritten to match the majority and does not receive the majority's payment eligibility.

If the required threshold is not reached, the round closes through the defined no-consensus or verification-unavailable path rather than inventing a verdict.

## Deadline behavior

Assignment, inference, commit, reveal, and round-close deadlines are expressed in block height. Missing actions are processed by deterministic protocol runners. Local wall clocks and service-side timeout observations do not create the failure fact.

Every deadline path must terminate or advance the Task. A missing transaction submitter cannot leave funds permanently locked; after prioritized submitter windows expire, self-rescue or deterministic runner paths apply the same state transition.
