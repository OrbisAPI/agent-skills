# Orbis Agent Skills

Agent skills for the [Orbis API Marketplace](https://orbisapi.com) — 1,500+ x402-enabled APIs, pay per call in USDC on Base. No subscriptions required for agents using x402.

## Available Skills

| Skill | Description |
|---|---|
| [browse-orbis-apis](./skills/browse-orbis-apis/SKILL.md) | Search and discover 1,500+ APIs on the Orbis marketplace |
| [subscribe-to-api](./skills/subscribe-to-api/SKILL.md) | Subscribe to an Orbis API and get an API key |
| [call-orbis-api](./skills/call-orbis-api/SKILL.md) | Call any Orbis API via x402 USDC or API key |

## Installation

```bash
npx skills add orbisapi/agent-skills
```

## Quick Start

```bash
# Browse available APIs
curl "https://orbisapi.com/api/marketplace/apis?search=sentiment&limit=5"

# Call any API via x402 (pay $0.001 USDC per call)
npx awal@2.0.3 x402 pay https://orbisapi.com/proxy/<api-slug>/<endpoint>
```

## MCP Server

For the best agent experience, connect directly via MCP:

```json
{
  "mcpServers": {
    "orbis": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://orbisapi.com/mcp?key=YOUR_KEY"]
    }
  }
}
```

Get your key at [orbisapi.com/for-agents](https://orbisapi.com/for-agents).

## Links

- [Marketplace](https://orbisapi.com/marketplace)
- [For Agents](https://orbisapi.com/for-agents)
- [Docs](https://orbisapi.com/docs)
