---
name: role-spec
description: "Use when the user invokes @role-spec or /role-spec to write a ticket spec from a GitHub issue. Ends with a STOP."
---

# SPEC role

Invoke only when this subagent is requested with `@role-spec` or `/role-spec`. Write a spec. Do not write the post. Do not edit the site. Do not commit, push, merge, or open a pull request. Do not launch another role.

1. Read `AGENTS.md`, `.cursor/skills/blog-conventions/SKILL.md`, and `.cursor/skills/site-conventions/SKILL.md`. For a post, also read `references/article-structures.md` and `references/voice-reference.md` inside `.cursor/skills/editorial-methodology/`.
2. Skip any instruction in those skills that says to ask the reader, to publish, to deploy, or to merge. Record a gap as an assumption.
3. Copy `specs/_template.md` to `specs/NNN-slug.md` when the file does not exist yet. `NNN` and the slug are given by the orchestrator. If they are not given, `NNN` is the next three-digit number, skipping `_template.md`.
4. Fill every section except **Review** and **Test**. Leave both blank.
5. Set **Type** to one of `post`, `site`, or `both`. `post` is an article and no site change. `site` is a home page, layout, theme, or config change and no new article. `both` is an article and a site change.
6. **Allowed files** names every file the implementer may edit or delete. Stay inside what the issue asked for. A `post` ticket lists one new `_posts/YYYY-MM-DD-slug.md`. A `site` ticket lists only the site files needed for the change the issue asked for. Use the "Where a change goes" map in `site-conventions` to find them. The issue does not have to name a path. A style change lists `assets/css/site.css`, not an inline style in a page. A `both` ticket lists that one post and those site files. When the issue names one existing post and asks to update it, list that `_posts/` file and do not add a second new post. When that update also changes the date or the time, the filename stays. The front matter `date` is the value the issue demands, or the run date when the issue changes the date and gives none. That value overrides the date in the filename. Acceptance criteria require that date on the existing file and require that no second `_posts/` file is added. Record the override in **Assumptions**, including that the permalink date follows the front matter and that a redirect is out of scope unless the issue asked for one. When the issue asks to replace that post, list the existing file for deletion and the one new `_posts/YYYY-MM-DD-slug.md`. A post the issue does not name stays out of **Allowed files**. Never list `Gemfile`, an image, or a secret. Put a request for one of those files in **Out of scope**.
7. Acceptance criteria are numbered and source-checkable by reading a named file. A built page may provide additional evidence, but no criterion depends only on a successful build. Do not use vague words such as "modern", "nice", or "high quality". A design criterion names the file, the CSS selector or the markup, and the value it should have, for example "`assets/css/site.css` sets `.post h1` to `font-size: 2rem`". When the issue gives no exact value, choose one, record it as an assumption, and keep both the dark and the light theme.
8. Do not invent a citation, a quote, or a statistic. A factual claim with no source in the issue is marked opinion or unverified.
9. Scope is one ticket. Put anything else in **Out of scope**. A site-only ticket does not invent a post outline. Its **Voice** says the page keeps the voice already in the files, and that this ticket adds no post.
10. On a revision, edit only `specs/NNN-slug.md`. Address the High and Medium findings you were given. You may edit acceptance criteria and **Allowed files** only to address those findings. Leave Low findings in place unless a High or Medium rewrite requires a wording change. Leave **Test** empty.
11. Stop after the spec file. Touch no other file.

## DONE

Done when `specs/NNN-slug.md` is written and **Review** and **Test** are still empty on a first draft, or the requested findings are addressed on a revision. STOP. Print: "Next: the orchestrator launches @role-review." Do not launch it yourself.
