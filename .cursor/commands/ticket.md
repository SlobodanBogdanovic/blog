---
description: Turn the triggering GitHub issue into one spec, implement the post or the site change, test it, and open a pull request.
---

# /ticket

You are the main agent. A GitHub issue comment `agent`, or the command `/ticket`, is the authorization for this pipeline. The issue title and body are the brief. Orchestrate. Do not write the spec, fill **Review** or **Test**, write the post, or edit the site.

Launch `role-spec`, `role-review`, `role-write`, `role-frontend`, and `role-test` with the Task tool, one at a time, and wait for each to finish. If the Task tool is unavailable, stop and report. Do not do that role's work in this chat.

Ignore a role's "Next:" line. A role must not launch another role. Each task prompt starts with the `@role-...` invocation so the role accepts the job, and tells that role not to commit, push, merge, or open a pull request.

Read `AGENTS.md` before any git write. Do not follow the publish step in `editorial-methodology`.

Never read or write `.env` files or secrets. Never merge. Never commit to the default branch. Never push the default branch.

An early stop before implementation commits nothing and pushes nothing. Report the step, the round counts, and the spec path if the spec file exists. After implementation has written or deleted a listed file, a **FAIL** from **Test** still continues to section 6 and opens a pull request.

## 0. Preconditions

1. If `git status --porcelain` prints anything, including untracked files, stop. Do not stash.
2. Read the issue: number, title, and body. If there is no issue body, stop. For an automation-triggered run, also read the triggering comment, author, and the author's repository association. Continue only when that association is `OWNER`, `MEMBER`, or `COLLABORATOR`; if it is missing or anything else, stop before a git write and say the comment was not authorized. A direct `/ticket` or `/post` command from the current Cursor user is authorized without a GitHub comment, but the issue number, title, and body must still be supplied.
3. List `specs/*.md`. Skip `specs/_template.md`. `NNN` is one plus the highest three-digit prefix, zero-padded to 3. If none exist, `NNN` is `001`.
4. Build a slug from the issue title: lowercase, letters and digits, words separated by single hyphens, no leading or trailing hyphen, at most 40 characters.
5. The branch is `ticket/NNN-slug`. The spec path is `specs/NNN-slug.md`. If that branch already exists, or that file exists, stop.
6. Detect the default branch from `origin/HEAD`. If it cannot be detected, stop. Do not guess. Do not fetch or pull.
7. Compare the local default-branch commit with `origin/<default>`. If they differ, stop and report that the checkout is stale. Do not fetch, pull, or guess which commit to use.
8. From the clean, current tree, check out the default branch, then `git checkout -b ticket/NNN-slug`. Do this before any role launch.
9. If `HEAD` is not `ticket/NNN-slug`, stop.

## 1. Spec

Launch `role-spec` once. Do not pass a model. Task prompt:

> You are invoked with `@role-spec`. Write only `specs/NNN-slug.md` for GitHub issue NUMBER, title `TITLE`, body: `BODY`. Copy `specs/_template.md`. Fill every section except **Review** and **Test**. Set **Type** to `post`, `site`, or `both`. List **Allowed files**. When the issue updates one existing post's date or content, follow **Replacing a post** in `blog-conventions`: delete the old file and add one new file whose filename date matches the front matter date. If that section says to ask, write `## Question` with one question, do not set **Type**, and stop. For any other gap, state assumptions in the spec and finish. Do not write the post. Do not edit the site. Do not commit, push, merge, or open a pull request. Touch no other file.

If `specs/NNN-slug.md` contains a `## Question` heading and **Type** is not `post`, `site`, or `both`, stop before review. Do not launch another role. Do not commit, push, or open a pull request. Comment that question on the issue. If the issue comment fails, report the question and stop.

If the subagent fails, or `specs/NNN-slug.md` is missing, or **Type** is not `post`, `site`, or `both`, stop.

## 2. Review — maximum 2 rounds

A round is one `role-review` run. The spec file's **Review** section is the verdict source. If the chat summary and the file disagree, use the file. Require exactly one line matching `Verdict: **APPROVE**` or `Verdict: **NEEDS CHANGES**`. Reject zero or multiple verdict lines. Do not infer a verdict from finding text.

Do not pass a model. Launch prompt, every round:

> You are invoked with `@role-review`. Review only `specs/NNN-slug.md`. Write the **Review** section. Rank findings High, Medium, or Low, each with a suggested rewrite. On a repeat review, mark every earlier finding `resolved` or `still open`. Set the verdict to **APPROVE** or **NEEDS CHANGES**. State the biggest risk. Do not edit **Type**, **Allowed files**, the outline, or the acceptance criteria. Do not write the post. Do not edit the site. Do not commit, push, merge, or open a pull request.

- Round 1 is the review of the new spec.
- A finding line uses exactly `N. **High — still open.**`, `N. **High — resolved.**`, and the equivalent Medium or Low form. On round 1, every finding is `still open`. On a repeat review, every earlier finding is either `resolved` or `still open`.
- After every review round, any High finding whose line is not `**High — resolved.**` is open. An open High finding requires **NEEDS CHANGES**. If the verdict says **APPROVE**, stop because the review is inconsistent.
- **APPROVE** on round 1: go to implementation. Do not revise.
- **NEEDS CHANGES** on round 1: launch `role-spec` to revise that same file, then run review round 2. Do not pass a model. Revision prompt:

> You are invoked with `@role-spec`. Revise only `specs/NNN-slug.md` to address these High and Medium findings: `FINDINGS`. You may edit acceptance criteria and **Allowed files** only to address those findings. Leave Low findings in place unless a High or Medium rewrite requires a wording change. Do not ask questions. Do not write the post. Do not edit the site. Do not commit, push, merge, or open a pull request. Touch no other file. Leave **Test** empty.

- Round 2 is the last review. Do not launch a third.
- After round 2, a High finding is still open unless that finding's rank line is marked `resolved`. A High entry with no status, or marked `still open`, is open. If any High finding is still open, stop before implementation.
- Medium and Low findings that remain do not block implementation. Copy them into the pull request under **Spec**.
- If a review launch changes **Type**, **Allowed files**, or **Acceptance criteria**, stop. Only a `role-spec` launch may change those sections. Do not restore them yourself.

## 3. Implement

Read **Type** from the spec. Do not reclassify the issue yourself.

`role-write` and `role-frontend` run on Grok 4.7 or a newer Grok, with reasoning at extra high. Pass model `grok-4.7-xhigh` on each launch of those two roles, including the one repair launch in section 5. If the Task tool lists a newer Grok slug that is 4.7 or later and extra high (`xhigh`), pass that slug instead. Do not pass `cursor-grok-4.6-high-fast`, a fast-only slug, or a lower effort. Do not invent a slug.

If that launch fails because the model is missing, stop before either role edits a file. Do not retry on another model. Say that implementation required Grok 4.7 or newer at extra-high reasoning and that the ticket was not implemented.

If the launcher has no model field, omit it. The agent file pin is `grok-4.7[reasoning_effort=xhigh]`. Do not implement the post or the page yourself.

- **post:** launch `role-write` only.
- **site:** launch `role-frontend` only.
- **both:** launch `role-write`, wait, then launch `role-frontend`.

`role-write` prompt:

> You are invoked with `@role-write`. Implement the post files listed under **Allowed files** in `specs/NNN-slug.md`. That is the new post, and the one existing post the spec lists for an update or a deletion. Follow that spec. Do not edit a site file. Do not commit, push, merge, or open a pull request. Touch no other file.

`role-frontend` prompt:

> You are invoked with `@role-frontend`. Edit only the site files listed under **Allowed files** in `specs/NNN-slug.md`. Follow that spec. Do not write a post. Do not commit, push, merge, or open a pull request. Touch no file that the spec does not list.

If the launched role fails, or an allowed file it was supposed to add is missing, or an existing post it was supposed to delete is still present, stop.

## 4. Test

Launch `role-test`. Do not pass a model. Prompt:

> You are invoked with `@role-test`. This is test round 1. Test the work against `specs/NNN-slug.md`. Write only the **Test** section. Run every check you can run. For each check, write pass or fail and quote the line or the command output that proves it. Do not edit the post, the site, **Type**, **Allowed files**, the outline, or the acceptance criteria. Do not publish, deploy, serve the site, push, merge, or open a pull request. Do not open https://slobodanbogdanovic.github.io/blog as proof.

The **Test** section is the verdict source. Require exactly one line matching `Verdict: **PASS**` or `Verdict: **FAIL**`. Reject zero or multiple verdict lines. Do not infer a verdict from check text.

## 5. Repair — one more test at most

On **PASS**, go to section 6.

On **FAIL**, repair only a file an implementer just wrote:

- If a failing check is in a post file listed under **Allowed files**, launch `role-write` once with model `grok-4.7-xhigh` (or the newer extra-high Grok slug you used in section 3). Prompt:

> You are invoked with `@role-write`. Fix only the post files listed under **Allowed files** in `specs/NNN-slug.md`. Failures: `FAILURES`. Do not edit a site file. Do not commit, push, merge, or open a pull request. Touch no other file. A listed deletion stays deleted.

- If a failing check is in a site file that role wrote, launch `role-frontend` once with the same model. Prompt:

> You are invoked with `@role-frontend`. Fix only the site files listed under **Allowed files** in `specs/NNN-slug.md`. Failures: `FAILURES`. Do not write a post. Do not commit, push, merge, or open a pull request. Touch no file that the spec does not list.

- If both kinds of file failed, launch `role-write` once, then `role-frontend` once, each with that model.
- If the failure is not in a file those roles wrote, or the fix would need a file outside **Allowed files**, do not repair. Go to section 6.
- If a repair role or its required Grok model fails to launch, do not repair again. Go to section 6. The pull request body includes that operational failure.

Then launch `role-test` once more. Do not pass a model. This is round 2. Do not launch a third test.

> You are invoked with `@role-test`. This is test round 2. Re-test `specs/NNN-slug.md` after the repair. Write the **Test** section. Mark each earlier failing check `resolved` or `still open`, with fresh evidence. Do not edit the post, the site, or the acceptance criteria. Do not publish, deploy, serve, push, merge, or open a pull request.

A second **FAIL** still goes to section 6. Commit, push, and open the pull request. The body includes the verdict and the failing evidence. Do not merge.

## 6. Describe, commit, push, and pull request

Run the commit and pull request steps when implementation wrote or deleted a file under **Allowed files** and `HEAD` is `ticket/NNN-slug`. Do this when **Test** says **PASS** and when **Test** says **FAIL**. If a role already made commits, stop and report. Do not amend, reset, or push them. Do not commit or open a pull request when implementation did not run.

Write the description yourself from the spec and from **Test**. Do not ask another role. Do not retell the evidence. Copy it.

**What changed.** A few sentences someone can read without knowing the pipeline. Say what a reader of the site or the post will notice. Then one line per file that changed. Do not mention roles, branches, or commands in this part. Do not claim a check that **Test** marks failed or not verified. In particular, do not say the site was built, or that the live site changed, unless **Test** recorded that check as pass.

**Test.** The verdict and the rounds used. Then one line per check: the check name, pass or fail, and the evidence quote from **Test**. Put a check the machine could not run under **Not verified**, with the reason. Do not turn a skipped build into a pass. Say that the live site was not opened and that this run did not merge.

**Spec.** `specs/NNN-slug.md`, branch `ticket/NNN-slug`, and any Medium or Low review findings still open.

When the verdict is **FAIL**, still commit, push, and open the pull request. The body includes the failing evidence. Do not merge.

Before committing, inspect `git status`, `git diff`, and recent `git log` messages.

- Commit 1: `specs/NNN-slug.md` only.
- Commit 2: the implemented files only. Stage each path under **Allowed files** that exists, and stage a deletion when **Allowed files** lists an existing post the spec says to remove. Do not stage the spec again.

If commit 2 would be empty, stop. Do not push.

Do not stage `_site/`, `.jekyll-cache/`, `.jekyll-metadata`, `vendor/`, `.env`, `.env.*`, `credentials.json`, `*.pem`, `*.key`, or any other secret filename. If a secret path is in the status list, stop before that commit. If `git status` shows a path outside the spec and **Allowed files**, stop before that commit.

Do not update git config. Do not skip hooks. Do not use `git commit --amend` or interactive git.

Commit messages, one or two sentences about why:

```bash
git commit -m "Record the spec for the ticket."
git commit -m "Implement the ticket."
```

Push only when both commits succeeded and `HEAD` is `ticket/NNN-slug`:

```bash
git push -u origin HEAD:ticket/NNN-slug
```

Never push the default branch. Never force-push. Never merge.

Open the pull request. The title is the issue title.

Write the body to a temporary file outside the repository. Never interpolate issue text or a multiline body directly into a shell command.

```bash
gh pr create --title "$TITLE" --body-file "$PR_BODY_FILE"
```

The body is **What changed**, then **Test**, then **Spec**, in that order.

If the push fails, stop and report the error. Do not merge.

If `gh pr create` fails with `Resource not accessible by integration`, open the pull request with the automation action `open_git_pr` for this repository. Pass the same title and description, the branch `ticket/NNN-slug`, the default branch as the base, and draft false. The run is not done until that pull request URL exists. If both attempts fail, stop and report both errors. Do not merge. When the commits are already on the remote branch, do not end the run without a pull request URL.

Post one short comment on the new pull request:

Write the comment to a temporary file outside the repository.

```bash
gh pr comment "$PR_URL" --body-file "$PR_COMMENT_FILE"
```

Keep the comment to 3–6 short lines:

- `Implemented:` one plain sentence saying what a reader will notice.
- `Files:` the changed implementation paths, comma-separated.
- `Test:` the verdict and the number of test rounds.
- `Evidence:` one compact line copied from the strongest passing build or acceptance-criteria evidence in **Test**.
- `Not verified:` one compact line when **Test** has anything not verified; otherwise omit it.
- `Spec:` the spec path.

Do not paste the full **Test** section into the comment. It is already in the pull request body and the spec. Do not claim the live site changed. If the PR comment fails, report the error and stop; the pull request remains open. Do not retry by editing the pull request body.

Comment on the triggering issue. The comment is the **What changed** paragraph, the verdict, the failing evidence if the verdict is **FAIL**, and the pull request URL. Do not rewrite the issue body.

Write the issue comment to a temporary file outside the repository.

```bash
gh issue comment "$NUMBER" --body-file "$ISSUE_COMMENT_FILE"
```

If the issue number cannot be determined, leave the description in the pull request body when a pull request exists, and say so. Do not guess a number.

If the issue comment fails, report the error and stop. When a pull request already exists, leave it open and include its URL in the report. Do not merge and do not rewrite the issue body.

On **FAIL**, the pull request stays open. The issue comment includes the verdict, the failing evidence, and the pull request URL.

## 7. Stop

When the pull request is open, its short comment is posted, and the issue comment is posted, end with the pull request URL and nothing after it.

When the verdict is **FAIL** and the pull request is open, end with the pull request URL.

When a question stopped the run before implementation, end with the question.
