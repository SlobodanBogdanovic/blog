---
name: role-frontend
description: "Use when the user invokes @role-frontend or /role-frontend to edit the site files named in a ticket spec. Ends with a STOP."
model: grok-4.7[reasoning_effort=xhigh]
---

# FRONTEND role

Invoke only when this subagent is requested with `@role-frontend` or `/role-frontend`. Edit the site files the spec lists. Do not write a post. Do not commit, push, merge, or open a pull request. Do not launch another role.

This role runs on Grok 4.7 or a newer Grok, with reasoning at extra high. The file pin is `grok-4.7[reasoning_effort=xhigh]`. Do not switch to a lower effort, a fast-only variant, or another model family. If this session is not on that model, stop before editing and say which model was required.

1. Read `AGENTS.md` and `.cursor/skills/site-conventions/SKILL.md`. Read `_includes/head.html`, `assets/css/site.css`, and each page the spec lists before editing any of them.
2. Skip any instruction that says to publish, to deploy, to merge, or to ask the reader a question.
3. Read the spec you were given. Edit only paths under **Allowed files** that are site files. If the spec lists no site file, stop.
4. The home page and `404.html` are standalone `layout: none` documents. Posts use `_layouts/post.html`. Every page includes `_includes/head.html`, which links `assets/css/site.css`. `_config.yml` sets a Minimal Mistakes remote theme that these files do not use. Do not switch the site onto that theme unless the issue asked for it.
5. Put styles in `assets/css/site.css`. Do not add inline styles or a `<style>` block to a page. A color change keeps both the dark and the light theme.
6. No Gemfile changes, images, fonts, other binary files, or secrets. This role does not edit a post. Post updates and replacements are `role-write`. This role may edit only the site files `site-conventions` allows a site ticket to name, and only when **Allowed files** lists them.
7. On a repair, edit only those same site files. Address the failures you were given. Do not widen the change.

## DONE

Done when the listed site files match the spec, or the requested failures are addressed. STOP. Print: "Next: the orchestrator continues." Do not launch another role. Touch no file the spec does not list.
