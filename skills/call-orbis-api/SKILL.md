---
name: call-orbis-api
description: Call any Orbis API using either an API key or x402 USDC payment on Base. Use when you want to make an actual API call to an Orbis service, invoke a paid API, run an Orbis endpoint, or use a subscribed service. Supports both key-based auth and x402 pay-per-call.
user-invocable: true
disable-model-invocation: false
allowed-tools: ["Bash(npx awal@2.0.3 x402 pay *)"]
---

# Calling an Orbis API

Two ways to call any Orbis API: with an API key (if subscribed) or via x402 pay-per-call in USDC.

## Option A: x402 Pay-Per-Call (No Key Needed)

Call any Orbis API endpoint directly — pays $0.001 USDC per call automatically.

```bash
# GET request
npx awal@2.0.3 x402 pay https://orbisapi.com/proxy/<slug>/<endpoint>

# POST request with body
npx awal@2.0.3 x402 pay https://orbisapi.com/proxy/<slug>/<endpoint> \
  -X POST \
  -d '{"key": "value"}'
```

**Prerequisites for x402:**
- Wallet authenticated: `npx awal@2.0.3 status`
- USDC balance on Base: `npx awal@2.0.3 balance`
- If not funded, use the `fund` skill from `coinbase/agentic-wallet-skills`

## Option B: API Key (Subscribed Users)

If you subscribed via the `subscribe-to-api` skill:

```bash
# GET request
curl "https://orbisapi.com/proxy/<slug>/<endpoint>" \
  -H "X-API-Key: <YOUR_ORBIS_KEY>"

# POST request
curl -X POST "https://orbisapi.com/proxy/<slug>/<endpoint>" \
  -H "X-API-Key: <YOUR_ORBIS_KEY>" \
  -H "Content-Type: application/json" \
  -d '{"key": "value"}'
```

## Find Endpoint Paths

```bash
# Get full API spec including available endpoints
curl "https://orbisapi.com/api/marketplace/apis/<slug>"
# Check the `endpoints` array in the response
```

Or inspect payment requirements (no cost):
```bash
npx awal@2.0.3 x402 details https://orbisapi.com/proxy/<slug>/<endpoint>
```

## Example: Call the LLM API

```bash
npx awal@2.0.3 x402 pay https://orbisapi.com/proxy/orbis-llm-api/chat \
  -X POST \
  -d '{"model": "llama-3.3-70b", "messages": [{"role": "user", "content": "Hello"}]}'
```

## Example: Call Embeddings API

```bash
npx awal@2.0.3 x402 pay https://orbisapi.com/proxy/orbis-embeddings-api/embed \
  -X POST \
  -d '{"input": "text to embed", "model": "text-embedding-3-small"}'
```

## Browse All Available APIs

```bash
curl "https://orbisapi.com/api/marketplace/apis?limit=20"
```

Or visit: https://orbisapi.com/marketplace

## MCP Integration

For seamless agent integration, use the Orbis MCP server — it combines browse, subscribe, and call into one interface:
```
https://orbisapi.com/mcp?key=YOUR_ORBIS_KEY
```
