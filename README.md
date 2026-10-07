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

## Use with any MCP client (Claude desktop, Cursor, VS Code)

Remote MCP server URL:

```
https://mcp.apify.com?tools=metqo/walmart-product-reviews,metqo/amazon-public-reviews
```

## Pricing

| Tool | Per review | Per product |
|---|---|---|
| Walmart | $0.0008 | $0.003 |
| Amazon | $0.002 | $0.004 per marketplace page |

Support: support@metqo.com
