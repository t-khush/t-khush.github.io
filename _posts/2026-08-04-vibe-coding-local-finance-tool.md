---
layout: post
title: Locally hosting a personal finance tool
description: How I used Codex to build Local Finance, a self-hosted dashboard for tracking assets, liabilities, investments, and retirement goals.
slug: self-hosted-personal-finance-tracker
image: /assets/images/posts/local-finance/retirement-planning.png
image_alt: Local Finance retirement planning dashboard with mock financial data
image_width: 1265
image_height: 712
tags:
  - self-hosting
  - personal-finance
  - homelab
  - codex
read_time: 4
---
## Context
I just canceled my $95/year Copilot subscription this morning and couldn't be happier. I wanted a self-hosted personal finance tracker that I could adapt to how I manage money.

I bought a Mac Mini during the OpenClaw craze and have been using it as my personal assistant. I've been using it for a few things: calendar management, coding via Telegram (though I'm using Codex's harness now), and general projects or notes I think of on the go. I have a separate [paper trading project](https://paper-trading-dashboard-bice.vercel.app/) here.

Lately, I've been falling into the rabbit hole of homelabbing. I think it's a mix of enjoying playing around with hardware and networking, wanting to better understand the technology and its inherent privacy risks, and the ease of development with AI tooling.

I stumbled across [Actual Budget](https://actualbudget.org/) and set up the project locally. However, after playing around with it, I found that I wasn't a huge fan. I wanted less of a budgeting app and more of a net worth and investment account tracker—similar to what Monarch and Copilot were doing for me.

I tried to iterate on top of it—adding a parsing layer for Robinhood and Fidelity statements and creating a separate Investments tab—but the changes kept getting harder to maintain without breaking something else in the process. It would be easier to set something up from scratch rather than iterate on a local fork with functionality it wasn't meant to have.

## Enter: Local Finance

The name isn't too creative, but it's exactly what I wanted: a platform that would aggregate all my finances in one place.

I got to work by enabling voice dictation in Codex and giving it a goal loop for what I wanted:
- Focus on assets and liabilities tracking.
- Manually upload documents (PDFs and CSVs) with automated ways of extracting the relevant information—for example, [Robinhood PDF Statement to CSV](https://github.com/t-khush/robinhood-statement-to-csv).
- Track stock tickers in real time.
- Add a retirement simulation to show how on track a user is.

### Architecture

The app runs in Docker on my Mac Mini and is reachable over my home network or Tailscale. A React interface talks to a FastAPI backend, which coordinates account synchronization, price refreshes, retirement modeling, and statement parsing while persisting data in a Docker volume.

<figure class="article-diagram">
  <a href="{{ '/assets/images/posts/local-finance/architecture.png' | relative_url }}" aria-label="Open the full-size Local Finance architecture diagram">
    <img src="{{ '/assets/images/posts/local-finance/architecture.png' | relative_url }}" alt="Architecture diagram of Local Finance running in Docker on a Mac Mini, with React, FastAPI, financial services, statement parsers, and persistent storage" width="2081" height="829" loading="lazy" decoding="async">
  </a>
  <figcaption>Local Finance architecture, from private network access through the application services and persistent Docker volume. Select the diagram to view it full size.</figcaption>
</figure>

Using 5.6 Sol at high effort was sufficient, and the build used about 40% of my quota. The results are great. Here are some screenshots with mock data:
  
![Local Finance overview dashboard with mock financial data]({{ '/assets/images/posts/local-finance/overview.jpg' | relative_url }})

![Local Finance retirement planning dashboard with mock financial data]({{ '/assets/images/posts/local-finance/retirement-planning.png' | relative_url }})

## Challenges
I couldn't one-shot this with the goal loop. I had to add custom integrations for:

### Robinhood, Fidelity, and Schwab Accounts
- Robinhood doesn't provide CSV files for all holdings in an account, just a monthly statement. I had to work backward to extract the statement's text and generate a CSV of holdings from it.
- Fidelity and Schwab both provide CSVs of current holdings, albeit in different formats. I had to create a custom parser for each format.

### Storage
- I wanted to create this tool with the idea that it could be open source and reusable by other interested homelabbers.
- Because I need to upload PDFs and CSVs to see the investment account overview, that data has to persist somewhere. One option would be to store it in a directory listed in `.gitignore`, but instead I took this as a reason to full-send into Docker and learn about mounted volumes. Everything is currently mounted there, keeping the persisted information outside the application itself.

### Manual vs. Automated
- This is something I thought a lot about. I really wanted an automated way to sync data and actually ported the same SimpleFin API that Actual Budget uses, but I ultimately opted for the manual approach.
- The reason is that this ensures full ownership of my data rather than introducing a third party, and it also gives me more direct visibility into my finances :)

I'm still tinkering with the repo, but I hope to open it up to others soon.

> **Edit, August 8, 2026:** I have now open sourced Local Finance. The code and setup instructions are available in the [t-khush/local-finance repository](https://github.com/t-khush/local-finance).
