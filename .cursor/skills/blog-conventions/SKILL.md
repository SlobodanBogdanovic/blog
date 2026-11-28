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

## Replacing a post

When the issue names one existing post and asks to update its date, its content, or both, and the new text is in the issue or in an attachment, do this and do not ask:

Delete that file. Add one new `_posts/YYYY-MM-DD-slug.md`. `YYYY-MM-DD` is the date the issue gives. If the issue changes the date and gives none, use the run date. The slug stays the existing slug unless the issue gives a new one. The front matter `date` is that same calendar day. Do not keep the old filename. Do not put a different day in `date` than the day in the filename.

The body is the supplied text. Do not invent a different article. If that text starts with a `#` title, put that title in the front matter and leave it out of the body. Include each picture the issue attached, using the URL the issue gave. Do not add a file under `assets/` unless the issue names that path. Keep the categories and tags already on the post unless the issue changes them. A redirect from the old URL is out of scope unless the issue asked for one.

Ask one question and stop, with no implementable spec, only when one of these is true:

- The issue does not show which existing post to change.
- The issue asks for new content and supplies no text and no attachment.
- The issue says to keep the old filename or the old URL and also to change the date.
- The issue names more than one post.

Write `## Question` with that one question. Do not set **Type**. Do not write the post. For any other gap, record an assumption and continue.

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
