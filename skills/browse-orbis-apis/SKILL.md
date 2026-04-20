---
name: browse-orbis-apis
description: Search and browse 2,200+ x402-enabled APIs on the Orbis marketplace. Use when you need to find an external API or service, want to know what APIs are available, or need to discover a paid API for a specific task. Covers "find an API for...", "what APIs does Orbis have?", "search for...", "show me available services".
user-invocable: true
disable-model-invocation: false
---

# Browsing the Orbis API Marketplace

Orbis has 2,200+ x402-enabled APIs across AI/ML, data, utilities, finance, and more. All APIs support pay-per-call in USDC on Base via x402, with free tier options available.

## Search via MCP (Recommended)

The Orbis MCP server is the fastest way to browse and call APIs. Configure it once:

**Claude Desktop** — add to `claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "orbis": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://orbisapi.com/mcp?key=YOUR_ORBIS_KEY"]
    }
  }
}
```

**Cursor / Windsurf** — add MCP server URL:
```
https://orbisapi.com/mcp?key=YOUR_ORBIS_KEY
```

Get your key at: https://orbisapi.com/for-agents

## Search via REST API (No Auth Required)

```bash
# Search by keyword
curl "https://orbisapi.com/api/marketplace/apis?search=<query>&limit=10"

# Browse by category
curl "https://orbisapi.com/api/marketplace/apis?category=<slug>&limit=20"

# Get full API details
curl "https://orbisapi.com/api/marketplace/apis/<slug>"
```

## Available Categories

`ai-ml` · `data` · `utilities` · `finance` · `media` · `communication` · `developer-tools` · `blockchain`

## Response Fields

| Field | Description |
|---|---|
| `slug` | Unique API identifier — use for subscription and calls |
| `shortDescription` | What the API does |
| `pricePerCall` | Cost in USDC per call (most are $0.001) |
| `hasFreeTier` | Whether a free tier is available |
| `isVerified` | Verified and guaranteed by Orbis |

## Examples

```bash
# Find sentiment analysis APIs
curl "https://orbisapi.com/api/marketplace/apis?search=sentiment&limit=5"

# Browse AI/ML APIs
curl "https://orbisapi.com/api/marketplace/apis?category=ai-ml&limit=10"
```

## Next Steps

Once you find an API, use the `subscribe-to-api` skill to get an API key, or `call-orbis-api` to pay per call via x402.
