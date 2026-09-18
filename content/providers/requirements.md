---
title: Requirements
description: Identity, infrastructure, storage, and connectivity required to provide compute.
---

# Requirements

Confirm that you can satisfy the identity, compute, storage, connectivity, and operational requirements before bonding or accepting Tasks.

## Identity and keys

Prepare two account roles:

- The **operator account** is the stable economic identity. It controls the ServiceBond, claims, support management, service-key rotation, and exit. Keep it offline or under strongly restricted custody.
- The **service key** is the online key Cortex uses for handraises, Task material, and permitted self-rescue transactions. Store it separately from the model runtime and evidence data.

One operator represents one logical and economic Cortex Node. Adding machines behind it expands local capacity but does not create additional protocol identities or support votes.

## Compute and model runtime

Capacity is Profile-specific. The runtime must satisfy the selected Profile's model artifacts, tokenizer, precision, context, memory, inference, and verification requirements.

Before declaring a Profile, confirm that the runtime can produce the committed material and evidence it requires. Signed output and evidence digests for an identical completed Task binding must not depend on local paths, retry counters, or wall-clock time.

See the [model integrator guide](model-integration/README.md) when the runtime does not yet expose a compatible adapter.

## Durable storage

Cortex needs durable storage for:

- Task leases and responsibility state
- Signed material persisted before transmission
- Input, output, and evidence objects required by active duties
- Deduplication and submission records
- Chain observation cursors
- Evidence retained through challenge and cleanup windows

Size storage for concurrent Tasks and the longest required retention period. A successful network send is not a substitute for local persistence.

## Connectivity

The node needs outbound access to:

- Chain query, event, and transaction endpoints
- Builder coordination and Task data endpoints
- Its model adapter
- Operator-controlled monitoring and management services

Remote production connections must be authenticated and encrypted. Cortex must validate the chain ID, endpoint identity, and Builder descriptors before it signs or transfers Task material. A public inbound endpoint is not required by the Cortex architecture.

## Time and operations

Protocol deadlines use chain height rather than local wall-clock time. A healthy clock is still required for logs and TLS. The provider must also be able to respond to deadline alerts, storage failures, chain lag, model failures, release upgrades, and security incidents.

## Pre-bond checklist

- Operator and service keys are separated and backed up appropriately.
- The expected chain ID and synchronized chain state can be verified.
- Builder coordination and data endpoints are reachable.
- Evidence storage is durable and covered by backup planning.
- The adapter passes health, capability, and Profile readiness checks.
- At least one Profile has an explicit local price floor and sufficient capacity.
- Alerts cover chain lag, submission acceptance, deadline risk, storage, and runtime health.
- The operator understands the duties and potential bond impact of accepted work.
