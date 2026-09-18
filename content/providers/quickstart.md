---
title: Provider quickstart
description: Follow the end-to-end sequence for bringing a Cortex Node online.
---

# Provider quickstart

This page shows the complete provider sequence. It intentionally does not invent unreleased binary names, container tags, configuration keys, or network values.

## 1. Select Profiles

Choose the exact model and Profile versions you intend to support. For each one, decide whether the node will provide inference, verification, or both. Validate the hardware, artifacts, evidence requirements, and deadline budget before continuing.

## 2. Prepare identities and funds

Create the offline operator account and a separate online service key. Fund the operator account for the required ServiceBond and transactions. Do not copy either private key into the model runtime.

## 3. Install Cortex

Install a supported Cortex release from the public release channel. Record the version and verify its published integrity information before execution. Run it under a dedicated operating-system identity with access limited to its configuration, signer, Task state, and evidence storage.

## 4. Configure network connections

Configure the expected chain ID, chain endpoints, and Builder discovery or Nexus endpoints. Start Cortex without enabling new work and confirm that it can query synchronized state, follow events, and resolve current Builder descriptors.

## 5. Connect the model adapter

Connect Cortex to the adapter and run its health, capability, and readiness checks. Confirm that returned Profile identifiers and runtime-capability digests exactly match the intended configuration.

If you own the adapter implementation, follow the [model adapter interface](model-integration/adapter-interface.md) and [conformance testing](model-integration/conformance-testing.md) guides.

## 6. Configure local policy

For every Profile, configure the enabled capabilities, runtime binding, capacity limits, and local minimum price. Local policy determines whether Cortex offers work; it does not change the registered Profile or protocol rules.

## 7. Bond and declare support

Deposit the required ServiceBond, authorize the service key, and declare support for each exact Profile and capability set. Confirm each action from authoritative chain state rather than a transport acknowledgement.

## 8. Complete activation

New support becomes active only after the required real-duty activation path. Keep the node healthy and observe its declared, fresh, and active status on-chain. See [Model and node activation](model-and-node-activation.md).

## 9. Verify production readiness

Before enabling routine handraises, verify that:

- Chain and event cursors are current.
- Profile readiness and runtime digests match.
- Task and evidence stores are writable and have sufficient capacity.
- Pending submissions and deadlines are monitored.
- Restart reconciliation and backups have been tested.
- The operator can stop new work without abandoning accepted duties.

The node is operational only when local health and on-chain support state agree.
