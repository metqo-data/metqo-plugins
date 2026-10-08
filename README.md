# Metqo Data: review insights for Claude and other AI assistants

Ask your AI assistant *"What do verified buyers complain about most for this Walmart product?"* and get a themed answer from real reviews.

**Tools** (pay per result through Apify; failed items are free):
- **[Walmart Product & Reviews Scraper](https://apify.com/metqo/walmart-product-reviews)**: every review, with verified-only, star, date, keyword and topic-sentiment filters, plus new-review monitoring.
- **[Amazon Reviews & Customers Say Scraper](https://apify.com/metqo/amazon-public-reviews)**: top reviews across 12 marketplaces plus Amazon's "Customers say" topics with sentiment.

## Install in Claude Code

```
/plugin marketplace add metqo-data/metqo-plugins
/plugin install metqo-reviews@metqo-data
```

The plugin adds a `review-insights` skill and connects Apify's MCP server with the two Metqo tools. On first use, sign in to Apify (a free account works).

## Add it to your AI assistant

You need a free Apify account and its API token (apify.com → Settings → API & Integrations). Tools run on your Apify account and are billed per result.

| Assistant | Steps |
|---|---|
| **Claude** (claude.ai, Desktop, mobile) | Settings → Connectors → **Add custom connector** → URL `https://mcp.metqo.com/mcp?apifyToken=YOUR_APIFY_TOKEN` |
| **ChatGPT** | Settings → Apps & Connectors → enable **Developer mode** → **Create** → same URL as Claude, authentication: none |
| **Manus** | Settings → Integrations → **Custom MCP Servers** → **Add Server** → URL `https://mcp.metqo.com/mcp`, auth: Bearer token = your Apify token |
| **Cursor / VS Code / Windsurf** | `{ "mcpServers": { "metqo": { "url": "https://mcp.metqo.com/mcp", "headers": { "Authorization": "Bearer YOUR_APIFY_TOKEN" } } } }` |
| **Claude Code** | `claude mcp add --transport http metqo https://mcp.metqo.com/mcp --header "Authorization: Bearer YOUR_APIFY_TOKEN"` (or install the plugin below) |
| **Smithery** | [smithery.ai/servers/support-yw1p/metqo-reviews](https://smithery.ai/servers/support-yw1p/metqo-reviews), which asks for your token |

The server never logs request URLs or tokens. Prefer the header form wherever your client supports it.

**Metqo's own MCP server** (works in every client, uses your Apify token): `https://mcp.metqo.com/mcp` with header `Authorization: Bearer <Apify API token>`.

**Skill for Manus and other agents:** in Manus → Skills → + Add → **Import from GitHub** → `https://github.com/metqo-data/metqo-plugins` (skill: `skills/metqo-review-insights`).

Then ask: *"What do verified buyers complain about most for Walmart item 10450114? Group by topic."*

Also listed in the official MCP Registry as `io.github.trueleaftech786/metqo-reviews`.

## Pricing

| Tool | Per review | Per product |
|---|---|---|
| Walmart | $0.0008 | $0.003 |
| Amazon | $0.002 | $0.004 per marketplace page |

Support: support@metqo.com
