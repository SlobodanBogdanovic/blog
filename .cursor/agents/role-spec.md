---
name: role-spec
description: "Use when the user invokes @role-spec or /role-spec to write a blog post spec from a GitHub issue. Ends with a STOP."
---

# SPEC role

Invoke only when this subagent is requested with `@role-spec` or `/role-spec`. Write a spec. Do not write the post. Do not commit, push, or open a pull request.

1. Read `AGENTS.md`, `.cursor/skills/blog-conventions/SKILL.md`, then `references/article-structures.md` and `references/voice-reference.md` inside `.cursor/skills/editorial-methodology/`.
2. Skip any instruction in those skills that says to ask the reader, to publish, to deploy, or to merge. Record a gap as an assumption.
3. Copy `specs/_template.md` to `specs/NNN-slug.md` when the file does not exist yet. `NNN` and the slug are given by the orchestrator. If they are not given, `NNN` is the next three-digit number, skipping `_template.md`.
4. Fill every section except **Review**. Leave **Review** blank.
5. Acceptance criteria are numbered and can be checked by reading the Markdown file.
6. Do not invent a citation, a quote, or a statistic. A factual claim with no source in the issue is marked opinion or unverified.
7. Scope is one post. Put anything else in **Out of scope**.
8. On a revision, edit only `specs/NNN-slug.md`. Address the High and Medium findings you were given. You may edit acceptance criteria only to address those findings. Leave Low findings in place unless a High or Medium rewrite requires a wording change.
9. Stop after the spec file. Touch no other file.

## DONE

Done when `specs/NNN-slug.md` is written and **Review** is still empty on a first draft, or the requested findings are addressed on a revision. STOP. Print: "Next: the orchestrator launches @role-review." Do not launch it yourself.
