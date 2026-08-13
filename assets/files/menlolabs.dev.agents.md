# Shopping MCP instructions for agents

Version: 0.1.0
Last updated: July 11, 2026

Shopping MCP gives AI agents structured access to product search, prices, ratings, review counts, product identifiers, images, and direct product links.

Current coverage is Amazon.com. The tool interface is retailer-neutral, but no other retailer or product source is supported yet.

## Connection

- Transport: Streamable HTTP
- MCP endpoint: https://menlolabs.dev/mcp
- Website: https://menlolabs.dev
- For Humans: https://menlolabs.dev/agents

Discover the server's tools after connecting. No consumer API key is required for the current public MVP.

## Connect your agent

### Codex CLI or app

```bash
codex mcp add shopping-mcp --url https://menlolabs.dev/mcp
```

### Hermes Agent

```bash
hermes mcp add shopping-mcp --url https://menlolabs.dev/mcp
```

When prompted, choose no authentication and enable both discovered tools.

### Generic MCP configuration

```json
{
  "mcpServers": {
    "shopping-mcp": {
      "url": "https://menlolabs.dev/mcp"
    }
  }
}
```

Open a new agent session and verify that `search_products` and `build_product_kit` are available.

## Tool selection

### `search_products`

Use for specific product discovery. `query` is required. Optional inputs include `max_results` (1–10), `sort`, `min_price`, `max_price`, `min_rating`, `exclude_sponsored`, and `amazon_domain`. Only `amazon.com` is supported.

Supported sort values: `best_match`, `featured`, `best_rated`, `bestselling`, `newest`, `price_low_to_high`, `price_high_to_low`.

```json
{
  "query": "wireless mechanical keyboard",
  "max_results": 5,
  "sort": "best_rated",
  "max_price": 120,
  "min_rating": 4.2,
  "exclude_sponsored": true
}
```

### `build_product_kit`

Use for broad shopping goals that require several product categories. `theme` is required. Optional inputs include `budget`, `max_categories` (maximum 3), `products_per_category` (maximum 5), and `sort`. At most two uncached category searches call the upstream product provider.

```json
{
  "theme": "I'm returning to recreational running",
  "budget": 250,
  "max_categories": 3,
  "products_per_category": 3,
  "sort": "best_match"
}
```

## Operating rules

1. Preserve all explicit user constraints. Do not silently relax constraints.
2. Retrieve multiple candidates before recommending a product unless the user explicitly wants one result.
3. Consider rating and review count together.
4. Never invent prices, ratings, review counts, ASINs, images, Prime status, availability, or URLs.
5. Treat price, shipping, Prime status, and availability as time-sensitive.
6. Clearly distinguish retrieved facts from interpretation.
7. Always include the returned `product_url` for every product presented.
8. Do not expose API keys, provider parameters, or internal implementation details.

## Response semantics

Product facts come from the product-data provider or cached provider-derived results. `product_url` is the direct source URL. `tracked_url` is a separate optional Menlo redirect used for click measurement. Fields may be null when unavailable. `cache_status` is `hit` or `miss`. Theme requests may return `partial` when rate or provider-budget limits prevent a category search.

## Example responses

### `search_products`

```json
{
  "request_id": "01f...",
  "status": "success",
  "canonical_query": "wireless mechanical keyboard",
  "cache_status": "hit",
  "products": [
    {
      "asin": "B0EXAMPLE",
      "name": "Example Mechanical Keyboard",
      "product_url": "https://www.amazon.com/dp/B0EXAMPLE",
      "tracked_url": "https://menlolabs.dev/r/a8K2mP",
      "image_url": "https://...",
      "price": {
        "amount": 89.99,
        "currency": "USD",
        "display": "$89.99"
      },
      "rating": 4.6,
      "review_count": 2840,
      "is_prime": true,
      "is_sponsored": false,
      "price_checked_at": "2026-07-11T18:00:00Z"
    }
  ],
  "upstream_request_made": false
}
```

### `build_product_kit`

```json
{
  "theme": "returning to recreational running",
  "status": "success",
  "categories": [
    {
      "category": "Running shoes",
      "reason": "Core footwear for regular running.",
      "search_query": "beginner daily trainer running shoes",
      "products": [
        {
          "asin": "B0EXAMPLE",
          "name": "Example Daily Trainer",
          "product_url": "https://www.amazon.com/dp/B0EXAMPLE",
          "price": { "amount": 89.99, "currency": "USD" },
          "rating": 4.6,
          "review_count": 2840
        }
      ]
    }
  ]
}
```

## Limitations

- Results currently focus on Amazon.com.
- Additional retailers and product-data sources are planned but are not currently supported.
- Prices and availability may change after retrieval.
- Shipping, Prime, and variation-level metadata may be unavailable or incomplete.
- The MCP does not complete checkout.
- Anonymous clients may make 10 searches per UTC day.
- Tracked product links record clicks.
- Affiliate attribution is not currently configured.
