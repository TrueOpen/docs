---
title: Participants
description: The participants and task-specific responsibilities in TrueOpen.
---

# Participants

TrueOpen distinguishes long-lived network participants from responsibilities assigned for a single task.

## Network participants

| Participant | Responsibility |
|---|---|
| **User** | Creates sessions, signs and funds task orders, receives results, and may open a challenge. |
| **Validator** | Participates in consensus and chain governance. A Validator is not automatically an AI inference or verification provider. |
| **Builder** | Coordinates task proposals and data delivery through Nexus. A Builder does not execute inference or determine the final verdict. |
| **Cortex Node** | Provides compute capacity, maintains a business bond, and declares supported model profiles and capabilities. |
| **Governance** | Manages permitted parameters, emergency actions, treasury decisions, and protocol upgrades within protocol constraints. |

## Task responsibilities

A Cortex Node may receive one of two responsibilities for a particular task:

- **Worker**, also called Executor in some transitional material, executes the inference and produces the result and supporting commitments.
- **Verifier** independently checks the result using the verification rules bound to the task.

Worker and Verifier are not permanent node types. The same Cortex Node can serve in different capacities on different tasks, but cannot be both Worker and Verifier for the same task.
