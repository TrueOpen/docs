---
title: Overview
description: An introduction to TrueOpen, its architecture, and its participants.
---

# Overview

TrueOpen is a purpose-built Cosmos SDK application chain for AI inference. A user submits and funds a Task, the network selects a compute provider, independent Verifiers check the result, and the chain settles the final outcome after the challenge process closes.

The design combines off-chain computation and data delivery with on-chain coordination, accountability, and settlement. Transactions, deadlines, and consensus transitions accepted by the chain establish protocol facts. Off-chain services transport data and coordinate work within those rules.

## System map

- [Architecture](architecture.md) introduces the chain, Nexus, Cortex, and SDK.
- [Participants](participants.md) explains Users, Validators, Builders, and Cortex Nodes.
- [Task lifecycle](../protocol/v1/tasks/README.md) follows a Task from admission through finality.

## Choose your path

- [Providers](../providers/README.md): operate Cortex and supply inference or verification capacity.
- [Developers](../developers/README.md): integrate TrueOpen Tasks into applications.
- [Network Operators](../operators/README.md): operate Validator and Builder infrastructure.
- [Protocol](../protocol/README.md): understand design principles, mechanisms, algorithms, and versioned rules.
- [Reference](../reference/README.md): look up terminology and published interface information.

## V1 scope

V1 covers a single application chain, Task execution and verification, challenges, settlement, service bonds, model registration, and governance. It is not a general-purpose EVM chain. Future multi-chain designs are outside the documented V1 behavior.
