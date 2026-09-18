---
title: Glossary
description: Core TrueOpen terms and their meanings.
---

# Glossary

## Builder

A network participant that runs Nexus to coordinate task proposals and task data delivery. A Builder is neither the inference executor nor the final protocol judge.

## Cortex Node

A compute participant that can declare inference and verification capabilities for supported model profiles. For a particular task, it may be selected as a Worker or Verifier.

## Finality

The point after all applicable verification rounds and the challenge window have closed and the task has been settled. A finalized task cannot be challenged again.

## Model

A registered AI model or model family that can have one or more executable profiles.

## Nexus

The off-chain service operated by a Builder. It coordinates proposals, transports control messages, stores task data, relays outputs, and submits transactions.

## Profile

An executable specification for a Model, including the runtime, resource, capability, and verification boundaries needed to process tasks consistently.

## Session

An ordered stream of requests owned by a User. It provides sequencing and replay protection; it is not a wallet and does not hold funds.

## Task

One inference request across submission, execution, verification, possible challenge rounds, settlement, and finality.

## Task Builders

The Builders assigned to a Task. They remain associated with that Task across its lifecycle and coordinate the required proposal and data-delivery duties.

## Validator

A participant responsible for consensus and governance. Validator status does not automatically grant inference or verification responsibilities.

## Verifier

A task-specific responsibility performed by a selected Cortex Node to independently check an inference result. It is not a permanent node type.

## Worker

A task-specific responsibility performed by a selected Cortex Node to execute inference and produce the result and required commitments. Some transitional material uses the alias Executor.
