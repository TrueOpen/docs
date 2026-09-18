---
title: Task lifecycle
description: The complete TrueOpen V1 Task lifecycle and its protocol boundaries.
---

# Task lifecycle

The Task protocol turns a signed inference order into one final on-chain outcome. It coordinates off-chain compute and data without treating an off-chain service as the final judge.

## Five stages

```mermaid
flowchart LR
    A[Open Task] --> B[Inference]
    B --> C[Open Verify]
    C --> D[Verification]
    D --> E[Settlement]
```

1. **Open Task** accepts one signed order version, freezes its budget and snapshots, gathers Worker handraises, and selects one Worker.
2. **Inference** lets the selected Worker retrieve input, execute the bound Profile, and submit a signed receipt plus output and evidence commitments.
3. **Open Verify** gathers eligible Verifier handraises and selects the Verifier set using future randomness.
4. **Verification** has the selected Verifiers independently compute, commit, reveal, and submit results.
5. **Settlement** includes the challenge window and any challenge round, then applies one final accounting plan.

A challenge is a subdivision of Settlement, not a sixth Task stage. Settlement and finality are written together.

## Follow a Task

The stage walkthroughs explain cross-component exchanges, accepted transitions, and recovery paths. They illustrate the rules linked below; they do not define additional protocol stages.

1. [Task submission](task-01-open-task.md)
2. [Inference](task-02-inference.md)
3. [Verification assignment](task-03-open-verify.md)
4. [Verification](task-04-verification.md)
5. [Challenges](task-05-challenge.md)
6. [Settlement](task-06-settlement.md)

The final two walkthroughs expand the Settlement stage. Challenges remain part of Settlement in the five-stage protocol model.

## Governing rules

| Page | Covers |
|---|---|
| [Orders and task identity](orders-and-identity.md) | Sessions, order sequencing, signed orders, stable Task identity, and escrow admission |
| [Candidate selection](candidate-selection.md) | Eligibility, handraises, immutable snapshots, and Worker/Verifier assignment |
| [Data and evidence](data-and-evidence.md) | Task Builders, data commitments, access, retention, and availability responsibility |
| [Verification](verification.md) | Full-output checking, commit-reveal, result formation, and deadlines |
| [Challenges and settlement](challenges-and-settlement.md) | Permissionless challenge rounds, effective verdict, accounting, and finality |

## Lifecycle invariants

- One accepted Task uses one order hash and one Profile version.
- Its Task Builders remain fixed until all data responsibility ends.
- Candidate and parameter snapshots do not change retroactively.
- A selected node's duty is attached to its stable operator, not to a replaceable service key.
- Every accepted Task has a deterministic terminal path, including timeout and unavailable-data paths.
- No Task earnings become claimable before finality.
