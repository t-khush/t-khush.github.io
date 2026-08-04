# khush.blog

The source for [t-khush.github.io](https://t-khush.github.io), a small Jekyll site hosted on GitHub Pages.

## Run locally

Ruby 3.2 or newer is recommended.

```sh
bundle install
bundle exec jekyll serve
```

If your system Ruby is older, the build can also run in a Ruby container:

```sh
docker run --rm -p 4000:4000 -v "$PWD:/site" -w /site ruby:3.3-bookworm \
  bash -lc 'bundle install && bundle exec jekyll serve --host 0.0.0.0'
```

Then open `http://localhost:4000`.

## Add a post

Create a Markdown file in `_posts` named `YYYY-MM-DD-post-title.md`:

```yaml
---
layout: post
title: Post title
description: One sentence used in the post list and link previews.
tags:
  - systems
read_time: 5
---
```

GitHub Pages builds and publishes the site whenever changes reach the configured publishing branch.
