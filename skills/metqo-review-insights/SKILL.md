---
name: metqo-review-insights
description: Turn Walmart and Amazon product reviews into a complaints and topic-sentiment report. Use when asked what customers complain about, why a rating is dropping, how two products' reviews compare, or to monitor new reviews, for a Walmart item ID/URL or an Amazon ASIN/URL. Requires the Metqo MCP server (https://mcp.metqo.com/mcp) connected with an Apify API token.
---

# Metqo review insights

## Setup (once)

Connect the Metqo MCP server:
- **URL:** `https://mcp.metqo.com/mcp`
- **Auth header:** `Authorization: Bearer <your Apify API token>` (free account at apify.com; token under Settings → API & Integrations)

Where: Manus → Settings → Integrations → Custom MCP Servers · Claude → Settings → Connectors · ChatGPT → Apps & Connectors (Developer mode) · Cursor/VS Code → MCP config.

Tools: `walmart_reviews`, `walmart_product`, `amazon_reviews`. Each call runs a pay-per-result scraper on the user's Apify account.

## Choosing the call

| Question | Call |
|---|---|
| Top complaints (Walmart) | `walmart_reviews(product, stars="1,2", verified_only=true, max_reviews=100)` |
| One theme (Walmart) | `walmart_product(product)` to read the topic list, then `walmart_reviews(product, topic="<name>", stars="1,2")` |
| Recent problems only | add `since="YYYY-MM-DD"` |
| Amazon overview | `amazon_reviews(product, marketplaces="US,CA,UK")`; use the product's `topics` with `sentiment` negative/mixed |

Amazon shows only ~8-13 mostly positive reviews per marketplace without sign-in: rely on its "Customers say" topics for complaints, and say so.

## Cost (tell the user before large runs)

Walmart $0.0008/review + $0.003/product · Amazon $0.002/review + $0.004/product page per marketplace. Ask before anything above about $1.

## Report format

1. Top complaint themes with counts and % of reviews analysed
2. New vs long-running for each theme (from review dates)
3. One or two short quotes per theme; never name reviewers
4. Likely cause and suggested fix (product, listing, packaging, shipping, seller)
5. Coverage line from the `summary`: reviews available vs analysed, and why the run stopped
