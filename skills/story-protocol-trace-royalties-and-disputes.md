---
name: Trace royalties and disputes for an IP asset
description: Follow royalty payments to and from a Story Protocol IP asset and inspect any disputes raised against it.
api: openapi/story-protocol-openapi-original.json
operations:
  - "POST /api/v3/royalties/payments"
  - "POST /api/v3/disputes"
  - "GET /api/v3/disputes/{disputeId}"
---

# Trace royalties and disputes for an IP asset

Read-only flow against the Story Protocol API (`https://api.storyapis.com`).

## Auth
Send `X-Api-Key` and `X-Chain` (`mainnet` = 1514, `aeneid` = 1315) on every request. See `authentication/story-protocol-authentication.yml`.

## Steps
1. **List royalty payments** — `POST /api/v3/royalties/payments` with a query-options body filtered by `receiverIpId = {ipId}` (money in) or `payerIpId = {ipId}` (money out). Each `RoyaltyPay` records `amount`, `token`, `sender`.
2. **List disputes for the IP** — `POST /api/v3/disputes` with a query-options body filtered by `targetIpId = {ipId}`. Note each dispute's `status`, `currentTag`, and `arbitrationPolicy`.
3. **Get a single dispute** — `GET /api/v3/disputes/{disputeId}` for full detail including `evidenceHash`, `counterEvidenceHash`, `liveness`, and `umaLink`.

## Conventions
- List endpoints are POST with a query/pagination body (`conventions/story-protocol-conventions.yml`).
- Entity relationships (RoyaltyPay -> IPAsset, Dispute -> IPAsset) are captured in `data-model/story-protocol-data-model.yml`.
