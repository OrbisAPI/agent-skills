---
name: subscribe-to-api
description: Subscribe to an Orbis API and get an API key for authenticated access. Use when the user wants to subscribe to an API, needs an API key, or wants to set up recurring access to a paid Orbis API. Many APIs have a free tier — subscribe first to get a key before making calls.
user-invocable: true
disable-model-invocation: false
---

# Subscribing to an Orbis API

Subscribing gives you an API key for authenticated access. Most APIs include a free tier — subscribe first, then use your key.

## Step 1: Find the API slug

If you don't know the slug, use the `browse-orbis-apis` skill first:

```bash
curl "https://orbisapi.com/api/marketplace/apis?search=<query>&limit=5" | python3 -c "
import json, sys
apis = json.load(sys.stdin).get('apis', [])
for a in apis:
    print(a['slug'], '-', a['shortDescription'])
"
```

## Step 2: Subscribe (via MCP — Recommended)

If you have the Orbis MCP configured, simply ask:
> "Subscribe me to the [API name] API on Orbis"

The MCP `call_api` tool handles subscription automatically.

## Step 3: Subscribe (via REST API)

Requires a wallet address (from user) and Orbis account:

```bash
# 1. Check free tier details
curl "https://orbisapi.com/api/marketplace/apis/<slug>"

# 2. Subscribe
curl -X POST "https://orbisapi.com/api/subscriptions" \
  -H "Content-Type: application/json" \
  -H "x-wallet-address: <USER_WALLET_ADDRESS>" \
  -d '{"apiSlug": "<slug>", "tier": "free"}'

# Response includes your API key:
# { "key": "orbis_...", "tier": "free", "callsRemaining": 100 }
```

## Step 4: Store the API Key

Save the returned key for use in `call-orbis-api`:
```
orbis_xxxxxxxxxxxx
```

## Subscription Tiers

| Tier | Description |
|---|---|
| `free` | Free calls per month (varies by API) |
| `paid` | Pay per call via Stripe (credit card) |
| `x402` | Pay per call in USDC on Base — no subscription needed |

## Next Steps

Use the `call-orbis-api` skill to make calls using your new key.
