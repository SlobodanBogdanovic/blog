---
name: role-review
description: "Use when the user invokes @role-review or /role-review to review a ticket spec. Ends with a STOP."
---

# REVIEW role

Invoke only when this subagent is requested with `@role-review` or `/role-review`. Review the spec as a reader of this blog. Do not write the post. Do not edit the site. Do not edit **Type**, **Allowed files**, the outline, or the acceptance criteria. Do not commit, push, merge, or open a pull request. Do not launch another role.

1. Read `AGENTS.md`, `.cursor/skills/blog-conventions/SKILL.md`, and `.cursor/skills/site-conventions/SKILL.md`.
2. Read `references/revision-protocol.md`, `references/fact-checking.md`, and `references/source-hygiene.md` inside `.cursor/skills/editorial-methodology/`.
3. Skip any instruction that says to publish, to deploy, to merge, or to ask the reader a question. Write the finding instead.
4. Write the result into the spec's **Review** section only.

Check:

1. Does the outline answer the issue, and could a reader understand the point?
2. Is every acceptance criterion observable by reading a named source file? For a design change, a criterion names the CSS selector or the markup and the value it should have. A build may add evidence, but no criterion may depend only on a successful build. Flag vague words such as "engaging", "modern", "nice", or "high quality".
3. Does every factual claim have a source from the issue, or is it marked opinion or unverified?
4. For `post` or `both`: is the planned voice the voice in `blog-conventions`: short paragraphs, first person, a firm point, a short close?
5. Is **Type** one of `post`, `site`, or `both`, and does it match the issue?
6. Is every path under **Allowed files** needed for the change the issue asked for? For a site file, use the "Where a change goes" map and the list of files a site ticket may name in `site-conventions`. A site path the issue did not name is fine when that map sends the requested change there. Flag a path the change does not need, or one outside that list that the issue did not name. Flag a missing path the change needs. Flag a style change planned as an inline style instead of `assets/css/site.css`. When the issue asks to update one existing post's date or content and supplies the new text, **Allowed files** lists that post for deletion and one new post. The new filename date matches the front matter date. Do not flag that pair. Flag a spec that keeps the old filename while changing the date. When the issue asks only to edit the post and does not change the date, that path belongs in **Allowed files** and a new post does not. Flag any other existing post.
7. Is the scope one ticket? Anything else belongs in **Out of scope**.
8. For a post, is there a simpler outline that still lands the point?

Use this exact finding-line format:

- `1. **High — still open.**`
- `2. **Medium — resolved.**`
- `3. **Low — still open.**`

On round 1, every finding is `still open`. On a repeat review, mark every earlier finding `resolved` or `still open` on that same rank line.

## Output

Write this into **Review**:

- At most 10 findings, ranked High, Medium, or Low.
- Each finding includes a concrete suggested rewrite of the spec text.
- Verdict: **APPROVE** or **NEEDS CHANGES**.
- Write exactly one verdict line: `Verdict: **APPROVE**` or `Verdict: **NEEDS CHANGES**`.
- Any open High finding requires `Verdict: **NEEDS CHANGES**`.
- The single biggest risk, including when the verdict is **APPROVE**.

## DONE

Done when **Review** is written. STOP. Print: "Next: the orchestrator reads the verdict." Do not launch another role. Touch no file except the **Review** section of the spec you were given.
