---
title: Data and evidence
description: Task data commitments, access control, availability, and retention.
---

# Data and evidence

Task inputs, outputs, and evidence remain off-chain. The chain stores commitments and responsibility facts needed to coordinate access, detect inconsistency, and settle the Task.

## Confidentiality boundary

V1 transfers Task data in plaintext over authenticated TLS. The assigned Task Builders can read the input, output, and evidence they store. Selected Workers and Verifiers receive the material needed for their duties.

V1 does not claim end-to-end confidentiality from Builders. Sensitive data that requires Builder-blind encryption is outside the V1 protocol.

## Fixed Task Builders

Each Task is assigned a fixed Builder group when its order is accepted. That group remains responsible across Open Task, Inference, Open Verify, Verification, challenge rounds, Settlement, and the evidence-retention period.

The User sends the order and input to the Task Builders as one logical operation. Each Builder independently stores and authenticates the material. Redundant confirmations improve availability but do not replace on-chain Task admission.

## Commitments

Protocol material binds at least:

| Material | Commitment purpose |
|---|---|
| Input | `input_hash` binds the exact bytes sent after the User signs the order |
| Output | Binds the Worker's delivered result and streaming order |
| Worker evidence | Two required commitments bind token IDs and per-token values separately |
| Verifier evidence | Binds independently produced values, comparison metrics, and the aggregate proof |
| Profile snapshot | Fixes tokenizer, schemas, judgment function, and encoding versions |
| Generation parameters | Prevents a runtime from silently changing decoding behavior |

Implementations retrieving data must verify both size and commitment before consuming it. A valid authorization to download is not proof that the returned bytes are complete or correct.

For the V1 text verification profile, the Worker supplies two evidence bundles:

1. The token opening contains input token IDs, generated token IDs, and the exact canonical generation-parameter bytes. The two token artifacts have flat hashes; the generation-parameter artifact must hash to the Task's `generation_params_digest`. Its bytes do not add to the token opening's `encoded_size_bytes`.
2. The value opening contains the Worker's per-token value tree. Its root and encoded size are committed separately from the token opening.

Each bundle has its own manifest and storage confirmation. A Verifier retrieves and checks both commitments before comparing values. Its own bundle contains verifier values, comparison leaves, and an aggregate proof. The aggregate proof artifact's content hash must equal the result's `aggregate_proof_hash`.

## Access

Candidates receive metadata sufficient to decide whether to handraise. They do not receive full Task data merely for being candidates.

The selected Worker may retrieve the input. Selected Verifiers may retrieve the input, output, and required evidence after assignment. A challenge round grants equivalent bounded access to its newly selected Verifiers.

## Availability responsibility

Availability faults must be attributed from accepted protocol facts, not from one service's access log or claim that a request timed out. A Builder's formal data-ready declaration and threshold reports from selected participants can create attributable responsibility where the protocol defines it.

The protocol does not invent a parallel request-timeout consensus mechanism for every download. Participants retry across the fixed Builder group while their existing duty deadline continues to run.

## Retention and cleanup

Data responsibility outlives result delivery. Required evidence remains available through verification, the challenge window, any challenge round, settlement, and the configured cleanup gate.

Cleanup can remove large data after responsibility ends, but must retain enough immutable commitments, versions, verdict summaries, and accounting references to audit final settlement.
