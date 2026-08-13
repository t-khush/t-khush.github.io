---
read_time: 5
tags:
  - mcp
  - ai-agents
  - agentic-commerce
image_height: 1360
image_width: 2552
image_alt: |2-
   Menlo Labs Shopping MCP turning a Nike hoodie request into three structured
    product results
image: /assets/images/posts/menlo-labs/product-search-response.png
slug: menlo-labs-shopping-mcp
description: |-
  I built a shopping MCP for Amazon product discovery, found organic users,
    and shut it down after learning how difficult agentic commerce is to monetize
title: " What I learned building and deprecating a shopping MCP"
layout: post
---

## What did I build?
A few months ago, I launched [Menlo Labs](https://menlolabs.dev/) which was an MCP Server to hook into Amazon's product search. The idea was simple: give your AI Agent access to Amazon's catalog to search for products you're interested in, and based off your requirements, it would give you the best product.

<figure class="article-diagram">
  <a href="{{ '/assets/images/posts/menlo-labs/product-search-response.png' | relative_url }}" aria-label="Open the full-size product search response diagram">
    <img src="{{ '/assets/images/posts/menlo-labs/product-search-response.png' | relative_url }}" alt="Example Menlo Labs product search request for a highly rated Nike hoodie under $80 and the three returned products" width="2522" height="1360" loading="lazy" decoding="async">
  </a>
  <figcaption>A product-search request and its structured response. Open the image to view it full size.</figcaption>
</figure>

The contract was pretty simple, and installation was fairly simple as well. Users could send their agent [this]({{ '/assets/files/menlolabs.dev.agents.md' | relative_url }}) markdown file to pickup context/instructions, and from there, they could then hook up to the MCP via having their agent draft up a skill.

## Technicals
I wanted to give users a 0-effort way of adding this tool for their agent. By sending their agent the AGENT.md link mentioned above, they would be allowed to hit our Shopping MCP as such:

<figure class="article-diagram">
  <a href="{{ '/assets/images/posts/menlo-labs/architecture.png' | relative_url }}" aria-label="Open the full-size Menlo Labs Shopping MCP architecture diagram">
    <img src="{{ '/assets/images/posts/menlo-labs/architecture.png' | relative_url }}" alt="Menlo Labs Shopping MCP request flow from an agent through Vercel, FastAPI, OpenRouter, Rainforest API, and Supabase to a structured tool result" width="2236" height="1176" loading="lazy" decoding="async">
  </a>
  <figcaption>The request path from agent onboarding to product results and click attribution. Open the image to view it full size.</figcaption>
</figure>

In terms of how we sourced the data, we used [Rainforest API's Amazon Product Data API](https://trajectdata.com/ecommerce/rainforest-api/). This gave us a bunch of data regarding products including:

- Titles
- ASIN
- Description
- Amazon Links
- Reviews

## Distribution/Analytics
This MCP exposes two tools:

### `search_products`

<figure class="article-diagram">
  <a href="{{ '/assets/images/posts/menlo-labs/search-products-tool.png' | relative_url }}" aria-label="Open the full-size search_products tool reference">
    <img src="{{ '/assets/images/posts/menlo-labs/search-products-tool.png' | relative_url }}" alt="Menlo Labs search_products tool inputs and an abbreviated response containing product data" width="2500" height="1266" loading="lazy" decoding="async">
  </a>
</figure>

### `build_product_kit`

<figure class="article-diagram">
  <a href="{{ '/assets/images/posts/menlo-labs/build-product-kit-tool.png' | relative_url }}" aria-label="Open the full-size build_product_kit tool reference">
    <img src="{{ '/assets/images/posts/menlo-labs/build-product-kit-tool.png' | relative_url }}" alt="Menlo Labs build_product_kit tool inputs and an abbreviated response with planned shopping categories" width="2568" height="1062" loading="lazy" decoding="async">
  </a>
</figure>

The primary mechanism I had for MCP discovery was submitting to directories. I created and submitted this [skill](https://github.com/t-khush/menlo-shopping-skill) to add to this [directory](https://registry.modelcontextprotocol.io/). Also somehow got featured on some blogs according to Vercel Analytics which also helped.

Some interesting analytics include:

1. 567 Products searched for
2. 62 Product Kits generated, rest are via direct searches
3. Some interesting queries included skincare "COSRX snail mucin", "K-beauty skincare routine", sports/outdoors "pickleball paddle single paddle racket", summer camping tent ventilation hot weather", and food "extra virgin olive oil", "raw almonds bulk 1 pound"

## No Path to Monetize + Deprecation
As a part of the tool response, I sent back a shortened link which hit menlolabs.dev, with the intention of redirecting the product link to Amazon.com.

Something strange I noticed-- granted, I did not spend much time investigating it-- was that that out of 300+ search results, I only received 2 clicks: both myself during testing, after explicitly asking the model for the link. My hypothesis after some light debugging was that  the model doesn't like to provide the link from the tool response as a final response since it doesn't know what it is.

Overall, I chose to shut down the project given I was paying ~$23/month for the Rainforest API with no clear way to monetize it. I was originally thinking that monetization could be possible via affiliate links, and potentially having sponsored products. Unfortunately- I full sent into building before doing a better job investigating the business aspect: Amazon/other companies wouldn't allow affiliate links through this kind of distribution (they would prefer it to be a blog/website rather than an API/MCP), and anything sponsored would need to have a "Sponsored" tag associated with it. Most people using agents/building agents for use would probably hate this.

Overall this was still a fun project- it was cool to see organic user growth but MCPs seem to be a hard area to monetize unless there is some strong data moat you can provide (similar to API businesses). Providing a wrapper over something any developer can build might work as a free service to avoid the headache, but I did doubt any hobbyists would want to pay me for this tool when they could just build it straight from Rainforest API themselves (with more customization).

I do think Agentic Shopping has more opportunities though-- I think there is tremendous benefit to just ask an agent about a hobby/idea, and have it source products via that (similar to the product kit endpoint). Definitely super excited to see how that evolves into the future.

Thanks for reading!
