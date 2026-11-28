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

`YYYY-MM-DD` is the run date. The slug is lowercase, hyphens, at most 40 characters. The index lists `site.posts`. A post does not edit the index.

A new post uses that same calendar day in the front matter `date`. When the issue gives a time of day, `date` may be `YYYY-MM-DD HH:MM:SS` and the calendar day still matches the filename.

## Date override on an update

When the issue names one existing post and asks to update it, the filename stays. When that issue also asks to change the date or the time, the front matter `date` is the new value and overrides the date in the filename. Jekyll uses that value for ordering and for `permalink: /:year/:month/:day/:title/`. Do not add a second file, and do not rename the post, to make the filename match.

If the issue asks for a new date and does not give one, use the run date. If the issue gives a time, include it. If it does not, write the date only.

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

`role-write` may add the one new post, and may edit or delete the one existing post the spec lists. It does not edit `_config.yml`, `index.html`, `404.html`, anything in `_layouts/`, `_includes/`, or `assets/`, `Gemfile`, or a post the spec does not list. A site ticket follows `site-conventions`. `role-frontend` may edit the site files `site-conventions` allows, only when the spec lists that path. It never edits `Gemfile` or a post.
