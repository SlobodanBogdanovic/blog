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
3. **Post, when Allowed files has a post.** For each `_posts/` file that remains, the path is `_posts/YYYY-MM-DD-slug.md`. Front matter has `title`, `date`, `layout: post`, non-empty `categories` and `tags`, and a one-sentence `excerpt`. The date matches the filename. A number, quotation, or named source that the spec does not allow fails. A post the spec says to delete has no remaining file to check.
4. **Existing posts.** A post that existed on the default branch and is not under **Allowed files** is unchanged. Fail if `git diff` lists such a post. An existing post listed under **Allowed files** may be edited or deleted, and only that one.
5. **Site files, when Allowed files has a site file.** Every changed site file is on the list `site-conventions` allows a site ticket to name, or the issue named it. A changed page or include adds no `style=` attribute and no `<style>` block. No font, image, or other binary file is added or changed. When `site.css` changes colors, both the dark and the light theme still define them.
6. **Build.** When `ruby` and `bundle` exist, run `bundle exec jekyll build --disable-disk-cache` with `--destination` set to a temporary directory outside the repo. Set `JEKYLL_CACHE_DIR` to a temporary directory outside the repo too. Use the existing `Gemfile`. Do not edit it. Find the built home page and the changed post by the slug and the title, not by one hardcoded path. Confirm the title is in the built page. For a site ticket, confirm each built page the spec lists links `assets/css/site.css` under the `/blog` base URL. When the spec changes `site.css`, quote the changed rule from the built `assets/css/site.css`. When it changes a page or an include, quote the changed markup from the built page.
7. **Links.** For each URL in a changed file, a clear HTTP 404 fails. A timeout or a refused connection is **Not verified**.
8. **Browser, when one is available.** Open the built pages and check the visible title and the changed text. For a design change, check the changed element in both the dark and the light color scheme when the browser can switch them. Record the local built-page path and quote the visible text, or record a screenshot path. Do not open the live site.

## What is not a failure

A missing Ruby, a failed `bundle install`, or a remote-theme error that does not name the changed file is **Not verified**. Do not edit `_config.yml` or a layout to clear that error. Do not treat the skipped build as a pass.

## After the build

Delete the temporary destination and cache directories outside the repo. The working tree must not contain `_site/`, `.jekyll-cache/`, `.jekyll-metadata`, or `vendor/`. The scope check fails if those paths appear in `git status`.

## Verdict

**FAIL** if any check that ran failed. **PASS** only when every check that ran passed. List what did not run under **Not verified**.
