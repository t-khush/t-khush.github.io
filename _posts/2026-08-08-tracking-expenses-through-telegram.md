---
layout: post
title: Tracking expenses through Telegram
description: I built a small MCP that lets my personal assistant record expenses in Local Finance.
slug: tracking-expenses-through-telegram
image: /assets/images/posts/local-finance/telegram-mcp-expense.jpg
image_alt: Telegram conversation showing a personal assistant recording an expense in Local Finance through MCP
image_width: 591
image_height: 1280
tags:
  - personal-finance
  - mcp
  - homelab
read_time: 2
---
## A small update

Earlier this week, I wrote about [building Local Finance]({{ '/blog/self-hosted-personal-finance-tracker/' | relative_url }}). I have since [open sourced the project](https://github.com/t-khush/local-finance).

I wanted to make it easier to keep my transactions current without opening the app every time. Since I already use a Telegram bot as my personal assistant, I built a small MCP server that connects it to Local Finance.

The MCP can list eligible spending accounts, read transaction history, and add, edit, or delete manually tracked expenses. I intentionally kept the surface area small. It cannot change balances, holdings, synced transactions, or retirement data.

## How I use it

The screenshot below is a simple example. I told the bot to add a CHF 1.85 iced tea purchase to the same card I had been using. It looked up the exchange rate, converted the amount to USD, asked for approval, and called the Local Finance MCP to record the expense.

<figure class="article-phone-shot">
  <img src="{{ '/assets/images/posts/local-finance/telegram-mcp-expense.jpg' | relative_url }}" alt="Telegram conversation showing a personal assistant converting a Swiss franc purchase to dollars and recording the expense through the Local Finance MCP" width="591" height="1280" loading="lazy" decoding="async">
  <figcaption>Recording a foreign-currency expense from Telegram.</figcaption>
</figure>

This is mostly for my own personal finance workflow. I can record something while it is still fresh without switching apps, and the transaction still lands in the self-hosted tool running on my Mac Mini.

The MCP lives in the [Local Finance repository](https://github.com/t-khush/local-finance/tree/main/integrations/hermes).
