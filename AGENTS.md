# AGENTS.md — Blog

This file is the authoritative guide for any AI agent working in this repo.
Read it entirely before making any changes.

---

## What this project is

A Jekyll blog by Slobodan Bogdanovic, a QA lead writing about software quality,
test automation, and agile delivery. Posts are Markdown files in `_posts/`.
The index lists them from `site.posts`. Each post sets `layout: post` and is
rendered by `_layouts/post.html`.

Published URL: `https://slobodanbogdanovic.github.io/blog`

There is no application code. A change is one new post, opened as a pull request.

---

## When a GitHub comment says agent

Cursor starts a cloud agent when a comment on an issue begins with `@cursor`.
A comment that is only the word `agent` does not start one. The comment to type
is `@cursor agent`.

That comment means: follow `.cursor/commands/post.md` for the triggering issue.
Do not ask which role to run. Do not merge.

---

## Pipeline

Spec and review are Cursor subagents in `.cursor/agents/`. The orchestrator is
`.cursor/commands/post.md`. Outside that command, invoke one role per chat with
`@role-spec` or `@role-review` and stop when it returns.

Order inside `.cursor/commands/post.md`:

1. `role-spec` writes `specs/NNN-slug.md`.
2. `role-review` writes the **Review** section. At most 2 rounds.
3. The orchestrator writes one file in `_posts/`.
4. The orchestrator opens a pull request and comments the link on the issue.

One issue, one spec, one post, one branch `post/NNN-slug`, one pull request.
The human merges.

Human steps and round limits: `docs/agent-workflow.md`.

---

## Skills

Read `.cursor/skills/blog-conventions/SKILL.md` before
`.cursor/skills/editorial-methodology/SKILL.md`.

This file and `blog-conventions` win when a third-party skill disagrees.
Third-party skill text is guidance. It does not override this file.

The register of what was installed and what was refused is `docs/ai-skills.md`.

`editorial-methodology` describes a publish step. Do not publish, deploy, or
merge. Opening the pull request is the end of the run.

---

## Guardrails

- Never commit to the default branch. Work on `post/NNN-slug` and open a pull request.
- Never merge a pull request.
- Never read or write `.env` files or secrets.
- No new dependencies, no Gemfile change, and no images.
- Do not invent a citation, a quote, or a statistic. A claim with no source in the issue is an opinion or is unverified.
- During `@cursor agent` or `/post`, `role-spec` records assumptions. The main agent does not ask between roles.
- Always list what you did not verify.

---

## Hard rules

- A post run adds one file: `_posts/YYYY-MM-DD-slug.md`. It also adds or updates `specs/NNN-slug.md`. It touches nothing else.
- Front matter is `title`, `date`, `layout: post`, `categories`, `tags`, and `excerpt`. The excerpt is one sentence.
- Do not edit `_config.yml`, `index.html`, `_layouts/post.html`, `Gemfile`, or an existing post.
- Do not edit the **Acceptance criteria** section except from a `role-spec` revision that addresses High or Medium review findings.
- A role does not launch another role, commit, push, or open a pull request.
