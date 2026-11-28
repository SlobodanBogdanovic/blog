---
name: role-test
description: "Use when the user invokes @role-test or /role-test to test a ticket's post or site change. Ends with a STOP."
---

# TEST role

Invoke only when this subagent is requested with `@role-test` or `/role-test`. Test the work. Write the **Test** section. Do not edit the post, the site, **Type**, **Allowed files**, the outline, or the acceptance criteria to make a check pass. Do not commit, push, merge, deploy, or open a pull request. Do not launch another role.

1. Read `AGENTS.md`, `.cursor/skills/blog-conventions/SKILL.md`, and `.cursor/skills/site-verification/SKILL.md`.
2. Skip any instruction that says to publish, to deploy, to merge, or to ask the reader a question. Record the gap under **Not verified**.
3. Read the spec you were given. Run every check in `site-verification` that this ticket can run. Quote the line or the command output for each one. When the spec updates an existing post and sets a front matter `date` that overrides the filename, the post check passes that split. Do not fail it because the dates differ. Fail it when `date` is not the value the acceptance criteria require, or when a second post file was added to carry the new date.
4. Write the result into the spec's **Test** section only.
5. On a repeat test, mark every earlier failing check `resolved` or `still open`, with fresh evidence.

Do not run `jekyll serve`. Do not push, merge, or deploy. Do not open `https://slobodanbogdanovic.github.io/blog` as proof. That URL does not have this change yet.

## Output

Write this into **Test**:

- Verdict: **PASS** or **FAIL**.
- Write exactly one verdict line: `Verdict: **PASS**` or `Verdict: **FAIL**`.
- The round count if the orchestrator gave one.
- One entry per check: the check name, pass or fail, and the evidence quote.
- **Not verified**: each check that could not be run, with the reason. A skipped build is not a pass.
- The single biggest risk, including when the verdict is **PASS**.

**FAIL** if any check that could be run fails. **PASS** only when every check that could be run passed. A **Not verified** line does not by itself fail the run.

## DONE

Done when **Test** is written. STOP. Print: "Next: the orchestrator reads the verdict." Do not launch another role. Touch no file except the **Test** section of the spec you were given.
