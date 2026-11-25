---
name: site-conventions
description: "What this Jekyll site is made of, where a design change goes, and which role may edit which file. Use when writing a site spec or editing index.html, the post layout, the head include, site.css, or _config.yml."
disable-model-invocation: true
---

# Site conventions

Read this before changing the site. `AGENTS.md` wins on conflict. For a post, `blog-conventions` still wins on voice and front matter.

## What the pages are

The site looks like a terminal. Each section of a page starts with a shell prompt line such as `slobodan@blog:~$ ls posts/`.

`index.html` is the home page. It sets `layout: none` and does not use a theme layout. It shows `whoami` (the name, the role, a tagline), `ls links/` (GitHub, LinkedIn, and the feed), and `ls posts/`. The post list is `site.posts`.

`_layouts/post.html` is the post page. A post sets `layout: post`. The page has a prompt bar with links home, to GitHub, to LinkedIn, and to the feed, then the date, the tags, the title, and the body.

`404.html` is the not-found page. It sets `layout: none` and shows a terminal error with a link home.

`_includes/head.html` is the `<head>` of every page: the page title, the description and social meta tags, the favicon (`assets/favicon.png`), the feed link, and the stylesheet link.

`assets/css/site.css` holds all the CSS for every page. No page has inline styles. It defines the Catppuccin Mocha (dark) and Latte (light) colors, switched with `prefers-color-scheme`, and its header comment records the contrast fixes. The type is Inter for text and JetBrains Mono for the prompt and code. Both are self-hosted in `assets/fonts/` and loaded by `@font-face` rules in `site.css`.

`_config.yml` sets `remote_theme` to Minimal Mistakes and a default `layout: single` for posts. The home page and the post layout above do not use that theme. Do not switch the site onto Minimal Mistakes unless the issue asked for it. Do not "fix" the split.

`url` is `https://slobodanbogdanovic.github.io` and `baseurl` is `/blog`.

## Where a change goes

An issue describes what should look or read differently. It does not have to name a file. Map the request to files like this:

- Colors, type, sizes, spacing, borders, the dark or light theme, the look of the post list or the post body: `assets/css/site.css`.
- The page title, the description, or a social meta tag: `_includes/head.html`.
- What the home page shows, its sections, its wording, its links: `index.html`.
- What the post page shows around the body: `_layouts/post.html`.
- What the not-found page shows: `404.html`.
- Site title, description, permalinks, or plugins: `_config.yml`.

A change that needs new markup and new styles lists both files.

## Who may edit what

`role-write` may add the one new post listed under **Allowed files**, and may edit or delete the one existing post that list names.

`role-frontend` may edit a file only when the spec's **Allowed files** names it. A site ticket may list these files when the map above sends the requested change there, whether or not the issue names the path:

- `index.html`
- `404.html`
- `_layouts/*.html`
- `_includes/*.html`
- `assets/css/site.css`
- `_config.yml`

A new file is allowed only under `_layouts/`, `_includes/`, or `assets/css/`, and only when **Allowed files** lists it. Any other path needs the issue to name it.

Neither role edits `Gemfile`, an image, the favicon, a font file, any other binary file, a secret, or a post the spec does not list. Neither role adds a font, an image, or any other binary file. This pipeline has no implementation route for those files.

`role-spec` and `role-review` do not edit these files. `role-test` does not edit them to make a check pass.

## When editing

Read `_includes/head.html`, `assets/css/site.css`, and each page the spec lists before changing any of them. Match the terminal look, the type, the measure, and the quiet page that are already there, unless the issue asks for a different look. Put styles in `assets/css/site.css`, not inline in a page. A color change keeps both the dark and the light theme and keeps text contrast at WCAG AA 4.5:1 or better. Keep the post list driven by `site.posts`. Do not add a second copy of a post title by hand.

No new gems. No new fonts. No secrets. A post may include a photograph the author placed in `assets/images/`. A ticket does not add one unless the issue names that file.
