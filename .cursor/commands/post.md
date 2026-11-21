---
description: Turn the triggering GitHub issue into one blog post spec, review it, write the post, and open a pull request.
---

# /post

You are the main agent. A GitHub comment `@cursor agent`, or the command `/post`, is the authorization for this pipeline. The issue title and body are the brief. Orchestrate. Do not write the spec, fill **Review**, or ask which role to run.

Launch `role-spec` and `role-review` with the Task tool, one at a time, and wait for each to finish. If the Task tool is unavailable, stop and report. Do not do that role's work in this chat.

Ignore a role's "Next:" line. A role must not launch another role. Each task prompt starts with the `@role-...` invocation so the role accepts the job, and tells that role not to commit, push, or open a pull request.

Read `AGENTS.md` and `.cursor/skills/blog-conventions/SKILL.md` before any git write. When you write the post, also read `references/voice-reference.md` and `references/source-hygiene.md` in `.cursor/skills/editorial-methodology/`. Do not follow that skill's publish step.

Never read or write `.env` files or secrets. Never merge. Never commit to the default branch.

An early stop commits nothing and pushes nothing. Report the step, the round counts, and the spec path if the spec file exists.

## 0. Preconditions

1. If `git status --porcelain` prints anything, including untracked files, stop. Do not stash.
2. Read the triggering issue: number, title, and body. If there is no issue body, stop.
3. List `specs/*.md`. Skip `specs/_template.md`. `NNN` is one plus the highest three-digit prefix, zero-padded to 3. If none exist, `NNN` is `001`.
4. Build a slug from the issue title: lowercase, letters and digits, words separated by single hyphens, no leading or trailing hyphen, at most 40 characters.
5. The branch is `post/NNN-slug`. The spec path is `specs/NNN-slug.md`. If that branch already exists, or that file exists, stop.
6. Detect the default branch from `origin/HEAD`. If it cannot be detected, stop. Do not guess. Do not fetch or pull.
7. From the clean tree, check out the default branch, then `git checkout -b post/NNN-slug`. Do this before any role launch.
8. If `HEAD` is not `post/NNN-slug`, stop.

## 1. Spec

Launch `role-spec` once. Task prompt:

> You are invoked with `@role-spec`. Write only `specs/NNN-slug.md` for GitHub issue NUMBER, title `TITLE`, body: `BODY`. Copy `specs/_template.md`. Fill every section except **Review**. Do not ask questions. State assumptions in the spec and finish. Do not write the post. Do not commit, push, or open a pull request. Touch no other file.

If the subagent fails, or `specs/NNN-slug.md` is missing, stop.

## 2. Review — maximum 2 rounds

A round is one `role-review` run. The spec file's **Review** section is the verdict source. If the chat summary and the file disagree, use the file. If the file has no **APPROVE** or **NEEDS CHANGES** verdict, stop. Do not invent a verdict.

Launch prompt, every round:

> You are invoked with `@role-review`. Review only `specs/NNN-slug.md`. Write the **Review** section. Rank findings High, Medium, or Low, each with a suggested rewrite. On a repeat review, mark every earlier finding `resolved` or `still open`. Set the verdict to **APPROVE** or **NEEDS CHANGES**. State the biggest risk. Do not edit the outline or the acceptance criteria. Do not write the post. Do not commit, push, or open a pull request.

- Round 1 is the review of the new spec.
- **APPROVE** on round 1: go to the post. Do not revise.
- **NEEDS CHANGES** on round 1: launch `role-spec` to revise that same file, then run review round 2. Revision prompt:

> You are invoked with `@role-spec`. Revise only `specs/NNN-slug.md` to address these High and Medium findings: `FINDINGS`. You may edit acceptance criteria only to address those findings. Leave Low findings in place unless a High or Medium rewrite requires a wording change. Do not ask questions. Do not write the post. Do not commit, push, or open a pull request. Touch no other file.

- Round 2 is the last review. Do not launch a third.
- After round 2, a High finding is still open unless that finding's rank line is marked `resolved`. A High entry with no status, or marked `still open`, is open. If any High finding is still open, stop before the post. Do not write the post.
- Medium and Low findings that remain do not block the post. Copy them into the pull request body.
- If a review launch changes the **Acceptance criteria** section, stop. Only a `role-spec` launch may change that section. Do not restore it yourself.

## 3. Post

Read `blog-conventions`, `references/voice-reference.md`, and `references/source-hygiene.md`. Write exactly one file: `_posts/YYYY-MM-DD-slug.md`. `YYYY-MM-DD` is today's date. Follow the spec's outline, voice, and claims. Do not invent a citation, a quote, or a statistic. Do not edit any other file in this step.

## 4. Commit, push, and pull request

Run this section only after the post file exists and review did not stop the run.

If `HEAD` is not `post/NNN-slug`, stop. If a role already made commits, stop and report. Do not amend, reset, or push them.

Before committing, inspect `git status`, `git diff`, and recent `git log` messages.

- Commit 1: `specs/NNN-slug.md` only.
- Commit 2: `_posts/YYYY-MM-DD-slug.md` only.

If commit 2 would be empty, stop. Do not push.

Do not stage `.env`, `.env.*`, `credentials.json`, `*.pem`, `*.key`, or any other secret filename. If a secret path is in the status list, stop before that commit.

Do not update git config. Do not skip hooks. Do not use `git commit --amend` or interactive git.

Commit messages, one or two sentences about why:

```bash
git commit -m "Record the spec for the post."
git commit -m "Add the draft post for review."
```

Push only when both commits succeeded and `HEAD` is `post/NNN-slug`:

```bash
git push -u origin HEAD:post/NNN-slug
```

Never push the default branch. Never force-push. Never merge.

Open the pull request:

```bash
gh pr create --title "TITLE" --body "BODY"
```

The body includes:

- **Spec** — `specs/NNN-slug.md` and branch `post/NNN-slug`
- **Review** — verdict, rounds used, unresolved findings
- **Assumptions** — from the spec
- **Not verified** — the post was not published, and the site was not built

If the push or the pull request fails, stop and report the error.

Comment on the triggering issue with the pull request URL:

```bash
gh issue comment NUMBER --body "Pull request: URL"
```

If the issue number cannot be determined, leave the URL in the pull request body and say so. Do not guess a number.

## 5. Stop

When the pull request is open and the issue comment is posted, end with the pull request URL and nothing after it.
