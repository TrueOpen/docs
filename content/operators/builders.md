---
title: Builders
description: Coordination, relay, and data availability responsibilities of a TrueOpen Builder.
---

# Builders

Builders run Nexus to coordinate Task proposals, deliver Task data, and relay signed participant actions. They support off-chain progress while the chain determines assignments, verdicts, and settlement.

## Responsibilities

- Coordinate Task proposals and participant handraises.
- Deliver input, output, and evidence under the accepted Task bindings.
- Relay signed material and distinguish relay acknowledgement from chain acceptance.
- Preserve required Task data through the retention and cleanup windows.
- Continue serving accepted Tasks whose fixed Builder group includes the operator.

Phase 0 uses a governed Builder set. A replacement applies at its defined future boundary; it does not replace the Task Builders already fixed for historical Tasks.

## Operating boundaries

Builder operation requires reliable chain connectivity, authenticated data transport, durable Task storage, and monitoring of pending relays and retention obligations. Public deployment commands and endpoint configuration will accompany supported Nexus releases.

Builders do not execute inference merely by running Nexus. See [Data and evidence](../protocol/v1/tasks/data-and-evidence.md), [Task submission](../protocol/v1/tasks/task-01-open-task.md), and [Governance](../protocol/v1/governance.md) for the governing responsibilities.
