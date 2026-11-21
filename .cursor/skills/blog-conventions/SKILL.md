---
name: blog-conventions
description: "Front matter, file path, and voice for posts on this Jekyll blog. Use when writing or reviewing a spec or a post in _posts."
disable-model-invocation: true
---

# Blog conventions

Read this before `editorial-methodology`. This file wins on conflict.

## Path

One new post per issue:

`_posts/YYYY-MM-DD-slug.md`

`YYYY-MM-DD` is the run date. The slug is lowercase, hyphens, at most 40 characters. The index lists `site.posts`. Do not edit the index.

## Front matter

```yaml
---
title: "Post title"
date: YYYY-MM-DD
layout: post
categories:
  - Quality Engineering
tags:
  - QA
excerpt: "One sentence."
---
```

`layout: post` is required. `excerpt` is one sentence. Categories and tags stay short, in the style of the existing posts: Quality Engineering, Development, Books, QA, Testing, Agile.

## Voice

Match the posts already in `_posts/`. Read them before drafting.

- First person. Short paragraphs. One idea per paragraph.
- A firm point in plain sentences. No marketing language and no hype.
- A short argument looks like `2026-04-11-testing-vs-qa.md`. A grouped list looks like `2026-10-01-my-book-reading-list.md`.
- Link with descriptive text. Do not invent a citation, a quote, or a statistic.
- Close in a sentence or two. A further-reading line is appropriate when the issue gave sources.

## Do not touch

`_config.yml`, `index.html`, `_layouts/post.html`, `Gemfile`, and existing posts.
