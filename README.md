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

Server URL (the same everywhere):

```
https://mcp.apify.com?tools=metqo/walmart-product-reviews,metqo/amazon-public-reviews
```

| Assistant | Steps |
|---|---|
| **Claude** (claude.ai, Desktop, mobile) | Settings → Connectors → **Add custom connector** → paste the URL → sign in to Apify |
| **ChatGPT** | Settings → Apps & Connectors → enable **Developer mode** → **Create** → paste the URL, auth: OAuth |
| **Manus** | Settings → Integrations → **Custom MCP Servers** → **Add Server** → paste the URL |
| **Cursor / VS Code / Windsurf** | Add to your MCP config: `{ "mcpServers": { "metqo": { "url": "<server URL>" } } }` |
| **Claude Code** | `/plugin marketplace add metqo-data/metqo-plugins` then `/plugin install metqo-reviews@metqo-data` |

Then ask: *"What do verified buyers complain about most for Walmart item 10450114? Group by topic."*

Also listed in the official MCP Registry as `io.github.trueleaftech786/metqo-reviews`.

## Pricing

| Tool | Per review | Per product |
|---|---|---|
| Walmart | $0.0008 | $0.003 |
| Amazon | $0.002 | $0.004 per marketplace page |

Support: support@metqo.com
