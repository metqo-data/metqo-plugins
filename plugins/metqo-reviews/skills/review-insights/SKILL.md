---
name: review-insights
description: Analyse Walmart or Amazon product reviews into a complaints and topic-sentiment report. Use when the user asks what customers complain about, why a product's rating is dropping, how a product compares with a competitor's reviews, or wants to monitor new reviews for a Walmart item ID/URL or Amazon ASIN/URL.
---

# Review insights with Metqo scrapers

You have two tools through the `metqo` MCP server (Apify). Each call runs a scraper and is billed per result to the user's Apify account, so keep requests no bigger than the question needs.

| Tool | Use for | Key input |
|---|---|---|
| `metqo/walmart-product-reviews` | Walmart items: every review, deep history | `products` (item IDs or URLs), `maxReviewsPerProduct`, `stars`, `verifiedOnly`, `topics`, `reviewsSince`, `keywords`, `onlyNewReviews` |
| `metqo/amazon-public-reviews` | Amazon: top reviews per marketplace + Amazon's "Customers say" topics | `products` (ASINs or URLs), `marketplaces` (e.g. `["US","CA","UK"]`) |

## How to answer

1. **Pick the smallest useful request.**
   - Complaints: `stars: [1, 2]`, `verifiedOnly: true`, `maxReviewsPerProduct: 100–200`, `sort: "submission-desc"`.
   - One theme (Walmart): run once with `maxReviewsPerProduct: 20` to read the product's `topics` from the summary row, then rerun with `topics: ["<name>"]`.
   - Amazon complaints: read the `topics` with `sentiment: "negative"` or `"mixed"` from the product record. Public pages show only ~8–13 mostly positive reviews per marketplace, so don't promise more.
2. **Tell the user the cost before large runs.** Walmart: $0.0008 per review, $0.003 per product. Amazon: $0.002 per review, $0.004 per product page per marketplace. Ask before anything above about $1.
3. **Read the summary row** (`recordType: "summary"`) to report what was available versus delivered, and why the run stopped. Never present a partial set as complete.
4. **Report themes, not walls of text:**
   - Top complaint themes with counts and share of reviews analysed
   - Whether each theme is recent or long-running (use `submittedAt`)
   - 1–2 short, representative quotes per theme
   - What it suggests (product fix, listing fix, shipping, seller issue via `sellerName`/`fulfilledBy`)
5. **Privacy:** don't request `includePersonalInfo` unless the user needs reviewer names and has a lawful basis. Don't name reviewers in reports.

## Monitoring

For "alert me to new bad reviews", use Walmart with `onlyNewReviews: true`, `sort: "submission-desc"`, `stars: [1, 2]`, and suggest scheduling it daily in Apify (Schedules) or with n8n/Make. Repeat runs return only reviews not delivered before; quiet days cost nothing.
