---
layout: post
title: New projects and onwards
description: A life update on running, homelabbing, and making more time for new hobbies.
slug: new-projects-and-onwards
image: /assets/images/posts/new-projects-and-onwards/workout-tracker-heatmap.png
image_alt: Workout Tracker heatmap of running routes around a neighborhood park
image_width: 990
image_height: 894
tags:
  - running
  - homelab
  - life
read_time: 3
---

Hi!

Last time I wrote here, I deprecated the Menlo Labs Shopping MCP. I think I want to start turning this site into my public diary. Not just technical projects but general life updates.

I recently came across this image of the Ouroboros

![Black-and-white illustration of an ouroboros, a snake eating its own tail]({{ '/assets/images/posts/new-projects-and-onwards/ouroboros.png' | relative_url }})

which is this scary image of a snake eating its tail. I first came across this image on a random meme site in middle school and thought it was disgusting to look at but have started to appreciate it. It represents both eternity and infinity as well as death/rebirth. I've been thinking about it-- as one chapter closes, another opens.

I want to spend more time "life-maxxing." It's been a few years since I've been out of college and I feel like besides work, I haven't accomplished much.

Fairly recently it feels like my life has taken a lot of turns. I've been trying to ask myself the inwards what is it I want to do, and what that means to be happy. There are a lot of hobbies, and bucket-list items I want to start crossing off, and personal accomplishments and achievements I want to chase.

So for now, my most recent interest has been fitness.

It's still in the early stages, but I've *consistently* been running for the last few weeks, and it's been going great. In New Jersey, I've been running around my neighborhood, going to parks, running on streets I've never been on. It's been meditative, and being the numbers/metrics guy I am, it's been cool to track my runs, see HR, pacing, and geo-analytics, and build on top of it.

Recently, I've gotten into homelabbing. Given my [personal finance tracker project]({{ '/blog/self-hosted-personal-finance-tracker/' | relative_url }}) I've explored a few projects which also can help me track my runs. Lately I've been using this simple open-source [workout-tracker](https://github.com/jovandeginste/workout-tracker) as a part of my homelab stack. Through a HealthSync app, I sync up my Apple Health metrics every few hours to my Mac Mini which runs the workout tracker in a Docker container. From there, I have access to all my metrics (I know September looks a little dry right now).

![Workout Tracker calendar showing three runs in early September 2026]({{ '/assets/images/posts/new-projects-and-onwards/workout-tracker-calendar.png' | relative_url }})

What I like is that there's this cool feature on the repo for heatmaps.

![Workout Tracker heatmap of running routes around a neighborhood park]({{ '/assets/images/posts/new-projects-and-onwards/workout-tracker-heatmap.png' | relative_url }})

I think Strava has something similar, but Strava is so heavily paywalled that this will do. The repo uses OpenStreetMap to pull from the route uploaded from Apple Health and documents the run route here. Hoping I can slowly populate a lot of NJ/NYC points!

I also forked the repository to make it more running oriented. I have a few local commits (which I'm procrastinating pushing to GitHub) to properly track Running PRs, Rolling Pace over the last N runs, distance, and more.

Immediate goals are to get to a healthy 5K pace by end of the year. I doubt I'll ever be interested in running marathons/those kinds of distances, but a 5K seems likes a healthy amount to run.

So as a part of lifemaxxing, my goal will be to hobbymax. Next up on the agenda, will be electronics/tinkering with hardware.

Thanks for reading and getting this far!
