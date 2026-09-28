---
title: Cross-chain assets
description: The canonical USDC route, bridge security, supply conservation, and operational controls.
---

# Cross-chain assets

Phase 0 uses one canonical USDC route as the source of the TrueOpen `business_denom`. The route connects USDC collateral locked on its origin chain with a synthetic voucher minted on TrueOpen.

## Canonical route

The route identity commits to both chains, domains, origin token, routers, mailboxes, local token identifiers, decimals, and the resulting business denomination. It is frozen at genesis.

Changing any identity field creates a different asset route and requires a protocol upgrade and, where applicable, an asset migration. Ordinary governance cannot point the existing denomination at a different token or router.

Both sides use the same integer base-unit precision. V1 does not scale decimals or create rounding residuals.

## Mint and burn boundary

The only valid mint path for the business asset is successful processing of an authenticated canonical bridge deposit. The only valid burn path is a canonical withdrawal through the bridge.

Business penalties, governance deposits, and residuals are transferred to the treasury; they do not burn USDC.

The protocol maintains the conservation relationship:

```text
total on-chain business asset
  = cumulative bridge mint
  - cumulative bridge burn
  + explicit genesis allocation
```

Supply counters survive export and import. Current supply must never be relabeled as a new genesis allocation.

## Bridge authorization

Bridge messages use a multisignature security module whose signer set is derived from the current Validator registrations. Each Validator has a separate bridge-signing key and proves possession when it is registered or rotated.

The bridge signer key is distinct from both the consensus key and operator account key. Reusing one private key or one storage slot across these roles is prohibited because compromise has different consequences.

The bridge remains frozen whenever the local signer set, confirmed origin-chain signer set, and registered Validator projection do not match.

## Set changes and cutover

A Validator or bridge-signer change cannot be atomic across two chains. The protocol therefore uses a staged cutover:

1. Pause new inbound origin-chain dispatch and drain earlier inbound messages.
2. Freeze the TrueOpen bridge.
3. Apply the local Validator or signer change and switch the local security module atomically.
4. Drain already dispatched outbound messages and update the origin-chain security module.
5. Confirm the new deployment and signer-set commitments on TrueOpen.
6. Recheck route, signer, supply, and in-flight invariants before a separate unfreeze action.

No interface may present this sequence as a cross-chain atomic update.

## Limits and freeze

Governance can freeze inbound and outbound bridge transfers without freezing ordinary on-chain USDC use. During a bridge freeze, existing balances can still be transferred, bonded, used for Tasks, settled, and claimed.

Inbound and outbound epoch limits bound the loss surface of a bridge failure. A transfer that exceeds the remaining limit is rejected in full; it is not partially executed. Limit changes are future-effective.

Relayers have no protocol privilege. Any address may submit a correctly authenticated message and pay its transaction fee. Relayer failure affects latency, not bridge authorization.

## Withdrawal finality

A successful TrueOpen-side withdrawal burn is final on TrueOpen. Receipt of unlocked assets on the origin chain is a separate cross-chain outcome and must not be displayed as complete merely because the local burn succeeded.

V1 does not support a second asset route, TrueOpen-side collateral USDC, decimal scaling, permanent bridge fee bypass, ownership renunciation, or automatic on-chain compensation for an origin-chain delivery failure.
