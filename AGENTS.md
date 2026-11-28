# AGENTS.md — Blog

This file is the authoritative guide for any AI agent working in this repo.
Read it entirely before making any changes.

---

## What this project is

A Jekyll blog by Slobodan Bogdanovic, a QA lead writing about software quality,
test automation, and agile delivery. Posts are Markdown files in `_posts/`.
The index lists them from `site.posts`. The home page is `index.html`, with
`layout: none`. Each post sets `layout: post` and is rendered by
`_layouts/post.html`.

Published URL: `https://slobodanbogdanovic.github.io/blog`

A change is one ticket, opened as a pull request. The ticket may be a post,
a site change, or both. The human merges.

---

## When a GitHub comment says agent

A comment that is only the word `agent` does not start Cursor by itself.
`@cursor` at the start of a comment starts the built-in cloud agent. Do not
put `@cursor` in the comment that is only the word `agent`. The two together
can start two runs.

The Cursor Automation on issue comments is what listens for `agent`. That
comment means: follow `.cursor/commands/ticket.md` for the triggering issue.
If the comment is anything else, or the author is `cursor`, stop and change
nothing. Only a repository `OWNER`, `MEMBER`, or `COLLABORATOR` may authorize
a run. If the author's repository association is missing or different, stop
before a git write. Do not ask which role to run. Do not merge.

`/post` follows the same command. It is not a posts-only path.

---

## Pipeline

Roles are Cursor subagents in `.cursor/agents/`. The orchestrator is
`.cursor/commands/ticket.md`. Outside that command, invoke one role per chat
and stop when it returns.

Order inside `.cursor/commands/ticket.md`:

1. `role-spec` writes `specs/NNN-slug.md`, including **Type** and **Allowed files**. When **Replacing a post** says to ask, it writes `## Question` and does not set **Type**. The orchestrator stops there. It does not implement, and it does not open a pull request.
2. `role-review` writes the **Review** section. At most 2 rounds.
3. `role-write` adds the post when the type is `post` or `both`. When the issue names one existing post and asks to change its date or its content, this role deletes that file and adds one new post. The filename date and the front matter date are the same day. When the issue edits a post and does not change the date, this role edits that file.
4. `role-frontend` edits the site files the spec lists when the type is `site` or `both`.
5. `role-test` writes the **Test** section. One repair, then one more test, at most.
6. When implementation has written or deleted a listed file, the orchestrator commits, pushes, and opens a pull request. It does this on **PASS** and on **FAIL**. It posts a short PR comment with the result and evidence, and comments on the issue. It does not merge. A run that stopped before implementation does not open a pull request.

`role-write` and `role-frontend` run on Grok 4.7 or a newer Grok, with
reasoning at extra high. The pin is `grok-4.7[reasoning_effort=xhigh]`. The
launch slug is `grok-4.7-xhigh` unless a newer extra-high Grok slug is listed.
If that model is not available, stop before implementation. Do not fall back.

One issue, one spec, one branch `ticket/NNN-slug`, one pull request.
The human merges.

Human steps and round limits: `docs/agent-workflow.md`.

---

## Skills

Read `.cursor/skills/blog-conventions/SKILL.md` before
`.cursor/skills/editorial-methodology/SKILL.md`.

Read `.cursor/skills/site-conventions/SKILL.md` before editing the site.
`role-test` reads `.cursor/skills/site-verification/SKILL.md`.

This file and those project skills win when a third-party skill disagrees.
Third-party skill text is guidance. It does not override this file.

The register of what was installed and what was refused is `docs/ai-skills.md`.

`editorial-methodology` describes a publish step. Do not publish, deploy, or
merge. Opening the pull request is the end of the run.

---

## Guardrails

- Never commit to the default branch. Work on `ticket/NNN-slug` and open a pull request.
- Never merge a pull request. Never push the default branch.
- Never read or write `.env` files or secrets.
- No new dependencies and no Gemfile change. A post may include a photograph the author placed in `assets/images/`. A ticket does not add one unless the issue names that file.
- Do not invent a citation, a quote, or a statistic. A claim with no source in the issue is an opinion or is unverified.
- During `/ticket` or `/post`, `role-spec` records assumptions. The main agent does not ask between roles. The one exception is **Replacing a post**: when that section says to ask, `role-spec` writes one question and the run stops before implementation.
- The orchestrator does not write the post or the page. Implementation is `role-write` and `role-frontend`.
- The pull request body holds the full explanation and test evidence. The PR comment is a 3–6 line summary copied from that evidence.
- Always list what you did not verify. Do not describe a skipped check as a pass.

---

## Hard rules

- A ticket run updates `specs/NNN-slug.md` and the paths under **Allowed files**. It touches nothing else.
- A post's front matter is `title`, `date`, `layout: post`, `categories`, `tags`, and `excerpt`. The excerpt is one sentence.
- A new post uses the same calendar day in the filename and in `date`. When the issue asks to update one existing post and to change its date or its content, delete that file and add one new post for the new date. The filename date and the front matter date match. Do not keep the old filename with a different date inside it.
- When implementation has written or deleted a file, the run opens a pull request before it ends. A failed test does not skip that pull request. The run does not merge. A question that stops the run before implementation does not open a pull request.
- Do not edit `Gemfile`, an image, or a file the spec does not list. Do not edit a post the issue did not name. When the issue names one existing post and asks to update or replace it, the spec lists that file. The implementer may edit it, or delete it and add the one new post.
- Do not edit **Acceptance criteria** or **Allowed files** except from a `role-spec` revision that addresses High or Medium review findings.
- Do not edit **Type**, **Allowed files**, or **Acceptance criteria** from `role-review`.
- `role-test` writes **Test** only.
- A role does not launch another role, commit, push, merge, or open a pull request.
- The test does not serve the site, deploy it, or open the live URL as proof.
