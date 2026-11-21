# AI skills register

Third-party skills are guidance. `AGENTS.md` and `.cursor/skills/blog-conventions/SKILL.md` win when they disagree.

Vetting for a third-party skill:

- Prefer an official or well-maintained source. Accept only MIT, Apache-2.0, BSD-2-Clause, BSD-3-Clause, or ISC.
- Copy the license into the skill folder. If it lives at the upstream repo root, copy it next to `SKILL.md` and say so here.
- Reject a skill that tells the agent to download further rules and follow them, run an install script, ask for a secret or a token, override `AGENTS.md` or `blog-conventions`, or hide instructions.
- Vendor accepted files at one commit SHA. Do not auto-update.
- One skill per topic.

## Accepted

### blog-conventions

- Topic: this blog's path, front matter, and voice
- Source: this repo
- License: project-authored
- Date added: 2026-11-21
- Reason: no catalog skill knows `_posts/` or the existing posts
- Review: written for this repo. Both roles read it before the third-party skill.

### editorial-methodology

- Topic: planning, structure, voice, citations, revision, and fact-checking
- Source: https://github.com/magnus919/hermes-profiles
- skills.sh: https://www.skills.sh/magnus919/hermes-profiles/editorial-methodology
- Commit: `867a555e13bae53a3945aa5328b1e09d347268cc`
- License: MIT. The license file is at the upstream repo root and is copied to `.cursor/skills/editorial-methodology/LICENSE`.
- Date added: 2026-11-21
- Reason: one editorial skill for spec, review, and the draft. The repo has about 340 stars. It is archived, so the SHA stays pinned.
- Review: read `SKILL.md` and all five files in `references/`. The skill is a short process plus those notes. It does not download further rules, run an install script, ask for a secret, or tell the agent to override `AGENTS.md`. The publish step in the lifecycle is not followed. Opening the pull request ends the run.

Who reads which file:

- `role-spec` reads `references/article-structures.md` and `references/voice-reference.md`.
- `role-review` reads `references/revision-protocol.md`, `references/fact-checking.md`, and `references/source-hygiene.md`.
- The orchestrator, when it writes the post, reads `references/voice-reference.md` and `references/source-hygiene.md`.

## Refused

These were looked up on skills.sh and were not installed.

- **grill-me** and **grilling** (mattpocock/skills). They wait for an answer on every question. This run records assumptions and continues.
- **writing-beats** (mattpocock/skills). It stops after each beat for a human choice.
- **writing-plans** (obra/superpowers) and **implement-spec** (mattpocock/skills). They are for code, tests, and ticket graphs.
- **content-blog** (vstorm-co/content-skills), **editorial-copy** (srstomp/copyskills), **medium-style-blog-writer** (samihalawa/medium-style-blog-writer-skill), and **house-style** (RightBlogger/bloggingskills). They push a marketing or SEO voice, ask which template to use, or ban punctuation this blog already uses. Those source repos are small.
- Pull-request review skills. `role-review` reviews the spec. The human reviews the pull request.
- **skill-creator** (anthropics/skills) and **frontend-design** (anthropics/skills). This setup does not author more skills, and it does not change the layout.

## Maintenance

Update `editorial-methodology` only by reading the whole skill at a new SHA and replacing the vendored files. Do not auto-update.
