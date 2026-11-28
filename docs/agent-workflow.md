# Agent workflow

A GitHub issue is the brief. A comment starts the ticket pipeline. The agent implements the post, the site change, or both, tests it, and opens a pull request. You merge it if the change is right. Nothing merges itself.

## What you do

1. Install the Cursor GitHub app on this repo and allow cloud agents to open pull requests.
2. Put this pipeline on the default branch. A cloud agent checks out that branch. It cannot see uncommitted files.
3. Save the Cursor Automation in the Agents Window after that. The draft is below. This file does not turn the automation on.
4. Open a GitHub issue. The title is the task. The body says who it is for, what to change, and any sources. Add the issue to the GitHub Project if you track work there. Adding the issue to the project, assigning it, or moving its card does not start the agent. Only the `agent` comment in the next step does.
5. Comment on that issue with the single word `agent`. Do not also write `@cursor` in that comment. `@cursor` at the start of a comment starts a second, built-in cloud agent.
6. Read the issue comment, the pull request body, and the short comment on the pull request. The body contains the full test evidence. The PR comment gives you the result in a few lines. Merge the pull request yourself when you want GitHub Pages to update.

## Writing a design issue

A design issue is a ticket of type `site`. You do not need to name files. `role-spec` maps the request to files with `site-conventions`. Styles go to `assets/css/site.css`.

Say three things in the body:

- Which page: the home page, the post page, the 404 page, or every page.
- What should look different, with a value when you have one, for example "post titles one step larger" or "links in the green accent".
- How you would check it by looking at the page.

When you give no value, the spec picks one and records it as an assumption. Read the **Assumptions** in the pull request before you merge. A design ticket cannot add a font, an image, or a gem.

## Automation

Save this in the Agents Window. Name it **Site ticket**. Trigger it on a GitHub issue comment for this repository only. Set the model to Grok 4.7 with reasoning at extra high, not the fast variant. When a newer Grok with extra-high reasoning is available, use that instead. If that model cannot be selected, do not save a fallback.

The automation opens a pull request. It does not need Slack or any other connection.

Instructions:

If the comment body is not `agent`, stop and change nothing. If the author is `cursor`, stop, so the agent's own issue comment does not start another run. Continue only when GitHub reports the author as this repository's OWNER, MEMBER, or COLLABORATOR; otherwise stop before a git write. Then follow `.cursor/commands/ticket.md` for that issue. Open a pull request only after the test passes. Put the full explanation and test evidence in the pull request body. Add one 3–6 line PR comment with the implementation summary, files, PASS verdict, strongest evidence, anything not verified, and the spec path. Comment the result and pull request URL on the issue. Do not merge. Do not push the default branch.

The command file has to be on the default branch before you save this. A cloud agent cannot see uncommitted files.

## What the agent does

The comment follows `.cursor/commands/ticket.md`.

1. **Spec.** `role-spec` writes `specs/NNN-slug.md` from `specs/_template.md`. **Type** is `post`, `site`, or `both`. **Allowed files** lists every file the implementer may edit. It records assumptions. It does not ask you questions.
2. **Review.** `role-review` writes the **Review** section. Verdict: **APPROVE** or **NEEDS CHANGES**.
3. **Revise, at most once.** **NEEDS CHANGES** sends High and Medium findings back to `role-spec`, then review runs again. An open High finding after the second review stops the run before implementation. Medium and Low findings that remain are copied into the pull request.
4. **Implement.** `role-write` adds the post when the type is `post` or `both`. When the issue names one existing post and asks to update or replace it, `role-write` edits that file, or deletes it and adds the new one. When that update changes the date or the time, the filename stays and the front matter `date` overrides the filename date. The test passes that override. `role-frontend` edits the listed site files when the type is `site` or `both`. Both run on Grok 4.7 or a newer Grok, with reasoning at extra high. If that model is missing, the run stops and does not implement the ticket on another model.
5. **Test.** `role-test` writes **Test**. It checks the diff, the acceptance criteria, and a local Jekyll build when the machine can build. It does not deploy, serve, or merge. A failed check in a file just written may be repaired once. A second failure stops the run. Nothing is pushed.
6. **Pull request.** On **PASS**, branch `ticket/NNN-slug`. The pull request body says what changed, in plain language, then gives the full test evidence. A 3–6 line PR comment summarizes the implementation and strongest evidence. The issue comment carries the same explanation, the verdict, and the pull request URL. On **FAIL**, the issue comment explains the change, quotes the failing check, and says no pull request was opened.

One issue, one spec, one branch, one pull request.

A dirty tree, including untracked files, stops the run. The agent does not stash.

## One role, one chat

Outside `/ticket` and `/post`, start a new chat and type one of:

- `@role-spec` and the issue text. The agent writes the spec and stops.
- `@role-review` and the spec path. The agent writes **Review** and stops.
- `@role-write` and the spec path. The agent writes the post and stops.
- `@role-frontend` and the spec path. The agent edits the listed site files and stops.
- `@role-test` and the spec path. The agent writes **Test** and stops.

When the subagent returns, the parent reports the result and stops.

## Skills

`blog-conventions` is the voice and the file format for posts. `site-conventions` is the home page, the post layout, and which role may edit which file. `site-verification` is the test checklist. `editorial-methodology` is the vendored writing skill. `AGENTS.md` and the project skills win if a third-party skill disagrees. The register is `docs/ai-skills.md`.
