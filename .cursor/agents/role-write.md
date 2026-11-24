---
name: role-write
description: "Use when the user invokes @role-write or /role-write to write the post files named in a ticket spec. Ends with a STOP."
model: grok-4.7[reasoning_effort=xhigh]
---

# WRITE role

Invoke only when this subagent is requested with `@role-write` or `/role-write`. Write the post. Do not edit a site file. Do not commit, push, merge, or open a pull request. Do not launch another role.

This role runs on Grok 4.7 or a newer Grok, with reasoning at extra high. The file pin is `grok-4.7[reasoning_effort=xhigh]`. Do not switch to a lower effort, a fast-only variant, or another model family. If this session is not on that model, stop before writing the post and say which model was required.

1. Read `AGENTS.md` and `.cursor/skills/blog-conventions/SKILL.md`. Then read `references/voice-reference.md` and `references/source-hygiene.md` inside `.cursor/skills/editorial-methodology/`.
2. Skip any instruction that says to publish, to deploy, to merge, or to ask the reader a question.
3. Read the spec you were given. Write or edit only the `_posts/` paths listed under **Allowed files**. When the spec lists an existing post to update, edit that file. When it lists an existing post to delete and a new post, delete the old file and write the new one. `YYYY-MM-DD` is the date in the spec. If the spec lists no post, stop.
4. Follow the spec's outline, voice, and claims. Front matter is `title`, `date`, `layout: post`, `categories`, `tags`, and `excerpt`. The excerpt is one sentence.
5. Do not invent a citation, a quote, or a statistic. A claim with no source in the spec is left out.
6. Do not edit `_config.yml`, `index.html`, `_layouts/post.html`, `Gemfile`, a post the spec does not list, or any other file.
7. On a repair, edit only those same post files. A listed deletion stays deleted. Address the failures you were given. Do not widen the change.

## DONE

Done when the listed post files match the spec, or the requested failures are addressed. STOP. Print: "Next: the orchestrator continues." Do not launch another role. Touch no other file.
