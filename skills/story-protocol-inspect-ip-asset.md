---
name: Inspect an IP asset and its licensing
description: Look up a Story Protocol IP asset, read its onchain metadata, and enumerate the license terms and license tokens attached to it.
api: openapi/story-protocol-openapi-original.json
operations:
  - "GET /api/v3/assets/{assetId}"
  - "GET /api/v3/assets/{assetId}/metadata"
  - "GET /api/v3/licenses/ip/terms/{ipId}"
  - "POST /api/v3/licenses/tokens"
---

# Inspect an IP asset and its licensing

Read-only flow against the Story Protocol API (`https://api.storyapis.com`).

## Auth
Send two headers on every request:
- `X-Api-Key: <key>` — use a Story public key or a higher-limit key.
- `X-Chain: <network>` — `mainnet` (chain 1514) or `aeneid` (testnet, chain 1315).

See `authentication/story-protocol-authentication.yml` and `sandbox/story-protocol-sandbox.yml` for published public keys.

## Steps
1. **Get the IP asset** — `GET /api/v3/assets/{assetId}` with the asset's `ipId`. Note `parentCount`, `childrenCount`, `isGroup`, and `rootIpIds` to understand its derivative lineage.
2. **Get metadata** — `GET /api/v3/assets/{assetId}/metadata` for the asset's onchain/NFT metadata.
3. **List attached license terms** — `GET /api/v3/licenses/ip/terms/{ipId}` to see which license terms govern the IP.
4. **List issued license tokens** — `POST /api/v3/licenses/tokens` with a query-options body filtered by `licensorIpId = {ipId}` to enumerate minted license tokens (each references `licenseTemplate` and `licenseTermsId`).

## Conventions
- List endpoints are POST with a JSON query/pagination body (see `conventions/story-protocol-conventions.yml`).
- The API is read-only; issuing licenses or registering IP is done via the SDKs/contracts, not this API.
