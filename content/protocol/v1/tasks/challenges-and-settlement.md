---
title: Challenges and settlement
description: Challenge rounds, effective verdicts, final accounting, and Task finality.
---

# Challenges and settlement

TrueOpen uses optimistic settlement: the first verification-round verdict stands unless a challenge opens another independent verification round. No accounting is applied until the challenge opportunity and all opened rounds have closed.

## Challenge window

The challenge window begins when round 1 closes. Opening a challenge is permissionless: any address can lock the required challenge bond and prepay the maximum verification budget for the new round.

The opener does not choose the Verifiers, submit a replacement verdict, or need access to private Task data. The protocol selects a new Verifier set, excluding participants from previous rounds, and those Verifiers independently retrieve and evaluate the frozen Task material.

V1 allows only the configured bounded number of rounds. A Task cannot be delayed indefinitely by repeatedly opening challenges.

## Round result

Every closed round records an immutable facts commitment covering its Task, round number, accepted inference receipt, ordered Verifier results, frozen execution context, failure class, and verdict.

The latest closed round's verdict is effective. Votes are never aggregated across rounds. A challenge that reaches the same conclusion confirms the earlier result; a challenge that reaches the opposite conclusion replaces it for final settlement.

An inconclusive or unavailable challenge does not automatically prove that the previous round was wrong. Its own missing-duty and availability rules apply independently.

## Economic effect of a challenge

- If the new round diverges, the opener's bond is returned. Objectively disproved Workers or earlier Verifiers lose payment eligibility and may incur the defined ServiceBond penalty.
- If the new round concurs, the opener pays for the additional verification and forfeits the challenge bond to the treasury.
- If the round is inconclusive, the configured portion of the bond is charged and the remainder is returned.

Challenge Verifiers are paid from the opener's separate challenge budget. The User's original Task verification budget is not charged a second time.

## Settlement

Settlement is derived entirely from accepted immutable state. The transaction submitter does not supply an alternative bill, verdict, or participant list.

The settlement plan:

1. Selects the latest effective verdict.
2. Determines which Worker and round-1 Verifier slots remain payable.
3. Applies maintenance fees and recorded eligible gas reimbursements.
4. Credits claimable earnings.
5. Returns every unused unit of Task escrow to the User.
6. Records the immutable settlement facts and finality height.

All transfers and state writes occur atomically. A failure rolls back the entire plan; partial settlement is forbidden.

## Finality

A Task is final only when no round remains open, no further challenge can be opened, required fault effects are complete, and settlement succeeds. Settlement and finality are the same transition. There is no state in which a Task has paid out but can still be challenged.
