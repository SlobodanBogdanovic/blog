---
name: site-verification
description: "Checks for a ticket before a pull request. Use when role-test writes the Test section. Does not publish."
disable-model-invocation: true
---

# Site verification

`AGENTS.md` wins on conflict. Run the checks. Quote the evidence. Do not edit the post or the site to make a check pass.

## Do not

- `jekyll serve`
- `git push`, `git commit`, `git merge`
- `gh pr create`, `gh pr merge`
- a GitHub Pages deploy, or any other deploy
- opening `https://slobodanbogdanovic.github.io/blog` as proof of this change

That URL does not have the change yet. Publishing from this skill is a failed run.

## Checks

1. **Scope.** `git status --porcelain` and `git diff --name-only` against the default branch list only `specs/NNN-slug.md` and the paths under **Allowed files**. Fail if any other path appears, including `_site/`, `.jekyll-cache/`, `.jekyll-metadata`, `vendor/`, `Gemfile`, or a file the spec did not list.
2. **Acceptance criteria.** Every numbered criterion, pass or fail, with the source line or the command that shows it. Every criterion must be source-checkable. A criterion that cannot be checked from the named source file fails closed. An unavailable build is reported separately under **Not verified**.
3. **Post, when Allowed files has one.** The path is `_posts/YYYY-MM-DD-slug.md`. Front matter has `title`, `date`, `layout: post`, non-empty `categories` and `tags`, and a one-sentence `excerpt`. The date matches the filename. A number, quotation, or named source that the spec does not allow fails.
4. **Existing posts.** All existing posts are unchanged. Fail if `git diff` lists a post that existed on the default branch.
5. **Build.** When `ruby` and `bundle` exist, run `bundle exec jekyll build --disable-disk-cache` with `--destination` set to a temporary directory outside the repo. Set `JEKYLL_CACHE_DIR` to a temporary directory outside the repo too. Use the existing `Gemfile`. Do not edit it. Find the built home page and the changed post by the slug and the title, not by one hardcoded path. Confirm the title is in the built page.
6. **Links.** For each URL in a changed file, a clear HTTP 404 fails. A timeout or a refused connection is **Not verified**.
7. **Browser, when one is available.** Open the built pages and check the visible title and the changed text. Record the local built-page path and quote the visible text, or record a screenshot path. Do not open the live site.

## What is not a failure

A missing Ruby, a failed `bundle install`, or a remote-theme error that does not name the changed file is **Not verified**. Do not edit `_config.yml` or a layout to clear that error. Do not treat the skipped build as a pass.

## After the build

Delete the temporary destination and cache directories outside the repo. The working tree must not contain `_site/`, `.jekyll-cache/`, `.jekyll-metadata`, or `vendor/`. The scope check fails if those paths appear in `git status`.

## Verdict

**FAIL** if any check that ran failed. **PASS** only when every check that ran passed. List what did not run under **Not verified**.
