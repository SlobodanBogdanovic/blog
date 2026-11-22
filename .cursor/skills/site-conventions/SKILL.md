---
name: site-conventions
description: "What this Jekyll site is made of, and which role may edit which file. Use when writing a site spec or editing index.html, the post layout, or _config.yml."
disable-model-invocation: true
---

# Site conventions

Read this before changing the site. `AGENTS.md` wins on conflict. For a post, `blog-conventions` still wins on voice and front matter.

## What the pages are

`index.html` is the home page. It sets `layout: none` and does not use a theme layout. The visible header is the name, a tagline, and links to GitHub and LinkedIn. The post list is `site.posts`. CSS is in that file. The type is IBM Plex, loaded from Google Fonts.

`_layouts/post.html` is the post page. A post sets `layout: post`. The page has a back link to the home page, the date, the title, and the body. CSS is in that file. It uses the same IBM Plex pairing.

`_config.yml` sets `remote_theme` to Minimal Mistakes and a default `layout: single` for posts. The home page and the post layout above do not use that theme. Do not switch the site onto Minimal Mistakes unless the issue asked for it. Do not "fix" the split.

`url` is `https://slobodanbogdanovic.github.io` and `baseurl` is `/blog`.

## Who may edit what

`role-write` may add the one new post listed under **Allowed files**. It does not edit the files in the next list.

`role-frontend` may edit a file only when the spec's **Allowed files** names it. The files a site ticket may name are `index.html`, `_layouts/post.html`, and `_config.yml`, plus a path the issue itself named.

Neither role edits `Gemfile`, an image, a secret, or an existing post. This pipeline has no implementation route for those files.

`role-spec` and `role-review` do not edit these files. `role-test` does not edit them to make a check pass.

## When editing

Read `index.html` and `_layouts/post.html` before changing either. Match the type, the measure, and the quiet page that are already there, unless the issue asks for a different look. Keep the post list driven by `site.posts`. Do not add a second copy of a post title by hand.

No new gems. No images. No secrets.
