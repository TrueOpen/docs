---
title: Configure profiles and capabilities
description: Configure the Profiles, capabilities, capacity, and local policy offered by a compute provider.
---

# Configure profiles and capabilities

Cortex can operate multiple Profiles concurrently. Each configured Profile has independent runtime, readiness, pricing, and Task state. On-chain support and capability declarations are keyed by Model.

## Provider configuration

For each Profile, select:

- `model_id` and `profile_version`
- Expected manifest and runtime-capability digests
- Runtime or adapter binding
- Inference capability, verification capability, or both
- Capacity limits
- A local minimum price for production work

Entries must be unique by `(model_id, profile_version)`, and at least one capability must be enabled. The local minimum price controls whether this node signs a handraise. It is private operator policy, not a protocol price or a modification of the registered Profile.

The integrator-facing format and behavior of the manifest are documented in [Profile and capability manifest](model-integration/profile-manifest.md).

## Validate before declaring support

Run the adapter readiness check for each Profile and capability. Cortex validates the returned Profile binding, artifacts, runtime digest, and evidence requirements. A successful local check means the node is technically ready; it does not activate support on-chain.

## Declare and activate support

Declare support and capabilities for the Model, then confirm the declaration on-chain. Support must remain fresh according to the network schedule. Expired support prevents new selection but does not erase an existing duty. A new Profile version needs its own local readiness check, not a new on-chain support declaration.

New support becomes active after the required real-duty activation path. Worker and Verifier duties may provide different activation evidence, but an operator counts at most once as an active supporter for a Model. See [Model and node activation](model-and-node-activation.md).

## Understand the four states

| View | Meaning |
|---|---|
| Provider configuration | What the operator intends to offer |
| Chain support state | Whether support is declared, active, fresh, frozen, or stale |
| Runtime observation | Whether the local runtime is loading, ready, draining, or failed |
| Task Profile lease | The immutable Profile and capacity binding for one accepted duty |

Do not collapse these into one status flag. A healthy runtime does not prove active chain support, and a chain declaration does not prove the local runtime is ready.

## Change or remove a Profile

Adding a Profile requires readiness validation before handraises. Changing or removing one starts a drain:

1. Stop new handraises for that Profile.
2. Preserve existing Task leases.
3. Finish or reach terminal state for accepted duties.
4. Retain evidence through cleanup eligibility.
5. Unload the Profile runtime after responsibility ends. Stop refreshing Model support only when the operator no longer supports any of that Model's versions.

Changing inference or verification semantics requires a new registered Profile version. Local configuration cannot rewrite a Task already bound to an older version.
