---
title: "Automating My Portfolio with GitHub Actions"
date: 2026-06-26T22:00:00-03:00
draft: false
tags: ["DevOps", "CI/CD", "Hugo", "GitHub Actions"]
---

## Automating My Portfolio with GitHub Actions

Building a portfolio site is one thing, but as a DevOps Engineer, deploying it manually feels like a crime. In this post, I'll walk you through how I automated the deployment of this very Hugo site to GitHub Pages using GitHub Actions.

## The Pipeline

The goal was simple: push to `main` and have the site automatically build and deploy. With the newer GitHub Pages deployment methods, we don't even need a separate `gh-pages` branch anymore. We can deploy directly using artifacts.

Here is the core of the workflow:

```yaml
name: Deploy Hugo site to Pages
on:
  push:
    branches: ["main"]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v3
        with:
          hugo-version: 'latest'
          extended: true
      - name: Build
        run: hugo --minify
```

## Why Hugo?

I chose Hugo primarily for its speed and the amazing `hugo-theme-shell` which gives this site its terminal aesthetic. Combine that with a solid CI/CD pipeline, and I have a low-maintenance, high-performance portfolio.

Until next time, keep automating!
