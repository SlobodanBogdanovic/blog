# Agent workflow

A GitHub issue is the brief. A comment starts spec, then review, then one new post, then a pull request. You merge it if the post is right. Nothing merges itself.

## What you do

1. Install the Cursor GitHub app on this repo and allow cloud agents to open pull requests.
2. Put this pipeline on the default branch. A cloud agent checks out that branch. It cannot see uncommitted files.
3. Open a GitHub issue. The title is the working title. The body is the brief: who it is for, the point, what to cover, and any sources. Do not write the post yourself.
4. Comment `@cursor agent` on that issue. A comment that is only the word `agent` does not start Cursor.
5. Read the pull request. Merge it if you are happy with the post.

## What the agent does

The comment follows `.cursor/commands/post.md`.

1. **Spec.** `role-spec` writes `specs/NNN-slug.md` from `specs/_template.md`. It records assumptions. It does not ask you questions.
2. **Review.** `role-review` writes the **Review** section. Verdict: **APPROVE** or **NEEDS CHANGES**.
3. **Revise, at most once.** **NEEDS CHANGES** sends High and Medium findings back to `role-spec`, then review runs again. An open High finding after the second review stops the run before a post is written. Medium and Low findings that remain are copied into the pull request body.
4. **Post.** One file, `_posts/YYYY-MM-DD-slug.md`.
5. **Pull request.** Branch `post/NNN-slug`. The agent comments the pull request URL on the issue and stops.

One issue, one spec, one post, one branch, one pull request.

A dirty tree, including untracked files, stops the run. The agent does not stash.

## One role, one chat

Outside `@cursor agent` and `/post`, start a new chat and type one of:

- `@role-spec` and the issue text. The agent writes the spec and stops.
- `@role-review` and the spec path. The agent writes **Review** and stops.

When the subagent returns, the parent reports the result and stops.

## Skills

`blog-conventions` is the voice and the file format for this blog. `editorial-methodology` is the vendored writing skill. `AGENTS.md` and `blog-conventions` win if they disagree. The register is `docs/ai-skills.md`.
