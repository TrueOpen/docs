---
title: FAQ
description: Frequently asked questions about TrueOpen.
---

# Frequently asked questions

## Is TrueOpen a general-purpose EVM chain?

No. TrueOpen V1 is a purpose-built Cosmos SDK application chain for AI inference tasks.

## Is AI inference performed on-chain?

No. Inference and verification compute run on Cortex Nodes. The chain coordinates selection, deadlines, commitments, accountability, funds, settlement, and finality.

## Are Worker and Verifier different node types?

No. They are responsibilities assigned to Cortex Nodes for a particular task. A node may take different responsibilities on different tasks, but cannot be both Worker and Verifier for the same task.

## Does a Builder decide whether a result is valid?

No. Builders coordinate proposals and data delivery. Protocol state and accepted on-chain actions determine selection, verdict processing, and settlement.

## Where are API endpoints and network parameters?

They will be added to the developer and reference sections after the corresponding public network and interfaces are released. Internal defaults are not treated as public configuration.
