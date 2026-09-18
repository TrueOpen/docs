---
title: Models and profiles
description: Registration, versioning, execution requirements, and lifecycle of AI model profiles.
---

# Models and profiles

TrueOpen separates a **Model**, which identifies a model family, from a **Profile**, which freezes one executable and verifiable configuration of that model.

Every Task selects exactly one `model_id` and `profile_version`. That binding remains unchanged through inference, verification, challenge rounds, settlement, and evidence cleanup.

## What a profile defines

A profile must provide enough information for independent operators to reproduce execution and verification boundaries. Its committed manifest includes or binds:

- Model artifacts and content digests
- Tokenizer identity
- Supported Task types and generation mode
- Runtime class and required capabilities
- Input and output schemas
- Verification algorithm, evidence schema, and thresholds
- Resource requirements and resource tier
- Minimum ServiceBond
- Pricing and Task-limit inputs
- Challenge-window and timeout inputs

Display metadata, logos, README content, and installation advice may exist without becoming consensus fields. They cannot override the on-chain profile projection.

## Registration and versioning

Profiles under a Model use monotonically increasing versions. Registering a new version creates a new immutable profile record; it does not overwrite the old version.

A new version is required whenever a change affects execution, verification, canonical encoding, artifacts, tokenizer behavior, schemas, resource classification, pricing boundaries, or minimum bond. Existing Tasks continue using the snapshot bound when they were accepted.

The profile manifest is content-addressed. Implementations must verify that retrieved manifest material matches its committed hash and the registered projection before using it. Unknown manifest fields or encoding versions fail closed rather than being silently ignored.

## Resource tier and minimum bond

The resource tier describes the Profile, not a node's self-reported hardware. It is derived from factors such as compute scale, memory, context length, precision, modality, runtime constraints, and verification cost.

The minimum ServiceBond is also a Profile-level fact. Candidate selection, Task liability, and related economic checks use the same snapshotted value. Separate components must not invent different minimum-bond values for the same Profile.

One Cortex Node may support multiple Profiles with one ServiceBond. For each Task, the protocol checks whether the node's active bond and declared capability satisfy that Task's Profile.

## Profile lifecycle

A newly registered Profile starts in a registered state. It can accept initial Tasks through the defined cold-start rules, but support declarations alone do not prove active service.

Successful real duties activate support for the corresponding node and Profile. Active support is tracked per node and Profile, while a node's inference and verification capabilities determine which Task duties it may accept.

Governance can freeze, unfreeze, or delist a Profile according to the governance rules:

- A freeze blocks new Tasks while preserving deterministic handling of Tasks already in flight.
- Unfreezing restores future admission without rewriting history.
- Delisting is terminal for new Task admission.

Changing a display field is not a reason to mutate protocol identity. Changing anything that affects Task execution or judgment requires a new Profile version.
