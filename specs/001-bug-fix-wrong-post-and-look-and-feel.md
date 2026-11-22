# 001 — Quality & Delivery Lead

## Brief

GitHub issue 5 is titled `BUG - fix wrong post and look and feel`. Its body asks for a site cleanup: delete one post, change the public headline to `Quality & Delivery Lead`, and restyle layouts, CSS, and fonts. It also says not to write a post.

This file is the spec for one post. The headline sentence and the existing writing line are the only wording the issue contributes. The deletion, the theme, and every layout or config edit are out of scope.

## Reader

Someone who already reads this blog for notes on software quality and delivery. The issue names no audience. That reader is an assumption.

## Point

The line under the name should read Quality & Delivery Lead. The blog line stays "Writing about software quality and engineering." The post states both in the first person. It may add one opinion sentence: the keyword line is the wrong line under the name. That sentence is a preference. It does not argue that the old phrases misdescribe the work, and it cites no study, quote, or count. It does not narrate a bug fix, a deletion, or a redesign.

## Outline

Short personal note. Two paragraphs and a close. No Markdown headings. Paragraph shape follows `2026-04-11-testing-vs-qa.md`: first person, one idea per paragraph. There is no evidence section and no counter-argument.

Target length: 110 to 170 words in the body, excluding front matter.

Front matter, exact:

```yaml
---
title: "Quality & Delivery Lead"
date: 2026-11-22
layout: post
categories:
  - Quality Engineering
tags:
  - QA
  - Career
excerpt: "The line under my name should read Quality & Delivery Lead, and this blog still writes about software quality and engineering."
---
```

1. **First paragraph.** Two or three sentences. Open with the claim in the first person: the line under the name should read Quality & Delivery Lead. Do not add an employer, a start date, or a promotion story. The issue does not give one. In the same paragraph, the issue names `QA Lead`, `Test Automation`, and `Agile Delivery` as the tagline to replace where it describes him. Say that this keyword line is the wrong line under the name. The issue also lists a `Quality Engineering | ...` search pattern. That pattern was not found in the working tree. Omit it. Do not say the keyword phrases are false descriptions of the work. Do not say the site files have already been edited. Write the headline as a preference: the line should read that. Do not write that the site already shows it.
2. **Second paragraph.** Include this sentence once, on its own: `Writing about software quality and engineering.` Present it as the line that still describes the blog, separate from the headline.
3. **Close.** One or two sentences. The headline names the role. The writing stays about the work. No request to restyle a page, and no further-reading line. The issue gave no sources.

## Claims and sources

The post may use only the claims in this table. Anything marked opinion stays in the author's voice and is not dressed up as a finding. Anything marked unverified is omitted.

| Claim | Standing | Source |
| --- | --- | --- |
| The public headline he wants is `Quality & Delivery Lead`. | From the issue. The post may say this in the first person. | Issue 5, Step 2. |
| The blog line to keep is `Writing about software quality and engineering.` | From the issue. Use that sentence once. | Issue 5, Step 2. |
| `QA Lead`, `Test Automation`, and `Agile Delivery` are the tagline he does not want under his name. | From the issue. Preference only. Not a claim that the phrases are inaccurate. The current description and tagline use this wording. | Issue 5, Step 2. `_config.yml` description; `index.html` tagline. The post does not name those files. |
| A `Quality Engineering \| ...` pattern is a line under the name. | Not found in the working tree. Omit. | Issue 5 lists it as a search string. Ripgrep on 2026-11-22 found it only in this spec. |
| `_config.yml` description and bio, and the tagline in `index.html`, still contain "QA Lead" wording. | Verified in the working tree while writing this spec. | `_config.yml` description and bio; `index.html` tagline. The post does not name those files. |
| A post titled "The Line Under My Name", slug `look-and-feel-improvement`, is in the repo or its history. | Not found. Omit. | Ripgrep of the working tree, and `git log -S` for both strings, on 2026-11-22. No matches. |
| Why the new headline is a better description than "QA Lead". | Optional one sentence, first person. Do not expand it into a comparison. | No source in the issue. |
| Catppuccin hex values, font coverage, contrast ratios, and a Lighthouse score of at least 95. | Implementation targets in the issue. Not measurements. Omit. | Issue 5, Step 4 and Done when. No result is attached. |

Not verified, and therefore not material for the post:

- The live URL `https://slobodanbogdanovic.github.io/blog/2026/11/22/look-and-feel-improvement/`.
- Comments on issue 5 beyond the body pasted into this task.
- A formal job title outside that issue text.
- Rendered contrast, font files, or a Lighthouse run.
- History on any remote other than the pickaxe search above.

## Voice

- First person, contractions, short paragraphs, one idea each. Same register as `2026-04-11-testing-vs-qa.md`.
- Plain sentences. No marketing language and no hype.
- No shell session, no code block, no CSS, no palette names.
- No link. The issue cites nothing. Descriptive link text does not create a source.
- Close in one or two sentences. No further-reading line.
- The visible ampersand is the character `&`. The HTML entity `&amp;` is for templates, which this post is not.

## Acceptance criteria

1. The post file is `_posts/2026-11-22-bug-fix-wrong-post-and-look-and-feel.md` and its front matter matches the YAML block in **Outline**, including `layout: post` and a one-sentence excerpt.
2. The body, excluding front matter, is between 110 and 170 words, contains no Markdown headings, and is two paragraphs plus a close of one or two sentences.
3. The source contains the character sequence `Quality & Delivery Lead` in the title, the excerpt, and the body, and it does not contain `Quality &amp; Delivery Lead`.
4. The body contains the sentence `Writing about software quality and engineering.` once.
5. The body is first person: it uses `I` or `my`.
6. If a surname appears, it is `Bogdanović` (ć, U+0107). The unaccented string `Bogdanovic` does not appear.
7. The file contains no `http://` or `https://`, no fenced code block, and no image.
8. The file does not contain `look-and-feel-improvement`, `The Line Under My Name`, `git rm`, `_config.yml`, `_layouts`, `index.html`, `Catppuccin`, `prefers-color-scheme`, `Lighthouse`, or `woff2`.
9. The file states no percentage, contrast ratio, or other statistic, and it attributes no quote to a named person.
10. The file does not say that a post was deleted, that a URL was removed, or that the site theme, config, or headline was changed. It does not state that the line under the name already reads Quality & Delivery Lead.

## Out of scope

- Deleting, moving, or editing any existing post, including a file for `look-and-feel-improvement` or "The Line Under My Name".
- Removing links, feed entries, sitemap rows, search indexes, tag pages, redirects, or committed build output.
- Editing `_config.yml`, `index.html`, layouts, includes, CSS, fonts, or the feed.
- A Catppuccin palette, `prefers-color-scheme`, self-hosted fonts, a shell-prompt home page, a top bar, or any other visual theme.
- JavaScript, images, a Gemfile change, or a new dependency.
- Changing an existing post URL, or any URL other than the one the issue says should stop existing. That URL change is also out of scope here.
- Lighthouse, WCAG measurement, and viewport checks.
- A second post, a changelog of the site, or a how-to for the theme.
- Publishing, deploying, or merging. Those are not this spec's job.

## Assumptions

- The pasted issue title and body are the whole brief. No other comment was read. The instruction in that body to skip the post, to stop and ask, and to ignore the repo's post rules is not followed. The site work it asks for is listed under **Out of scope**.
- The issue author is writing as the blog's author. The headline is his requested wording. It was not checked against a contract, a staff page, or any source outside the issue.
- The reader named above was not asked. Recorded here instead of a question.
- The post date is 2026-11-22, the date of this run. The slug is the one assigned with this spec: `bug-fix-wrong-post-and-look-and-feel`.
- `QA` and `Career` are existing tags on posts already in `_posts/`. `Quality Engineering` is an existing category.
- No citation, quote, or statistic was added. The optional sentence, that the keyword line is the wrong line under the name, is a preference. It is not a comparison.

## Review

Round 2. Acceptance criteria were not edited.

### 1. High — resolved — The outline treats a search pattern as a line on the site

Outline item 1 now calls `Quality Engineering | ...` a search pattern, says it was not found in the working tree, and says to omit it. The claims table gives that pattern its own row with standing "Not found in the working tree. Omit." The tagline row is `QA Lead`, `Test Automation`, and `Agile Delivery`. Checked again on 2026-11-22: the `_config.yml` description is `QA Lead | Test Automation | Agile Delivery`, the home-page tagline is `QA Lead · Test Automation · Agile Delivery`, and `Quality Engineering |` appears in this spec only. `git log -S` for that pattern is empty.

**Suggested rewrite.** None. The round 1 rewrite is in the outline and the claims table.

### 2. Medium — resolved — Three headings and a 180-word floor repeat two sentences

The outline is a short note: two paragraphs and a close, no Markdown headings, 110 to 170 words. Acceptance criterion 2 matches that shape. A reader can follow the point in that length: the role line he wants, the keyword line that should not sit under the name, the blog sentence that stays, and a short close.

**Suggested rewrite.** None. The round 1 rewrite is in the outline and in acceptance criterion 2.

### 3. Medium — resolved — The point forbids an argument the claims table allows

The point now allows one preference sentence, that the keyword line is the wrong line under the name, and it says that sentence does not argue the old phrases misdescribe the work. The claims-table standing is "Optional one sentence, first person. Do not expand it into a comparison." Outline item 1 tells the writer to use that preference. The claim label still says "better description." That remainder is finding 6.

**Suggested rewrite.** None for this finding. The round 1 rewrite is in the point and in the standing cell.

### 4. Medium — resolved — A present-tense headline would be a false claim, and the criteria allow it

Outline item 1 now says to write the headline as a preference and not to write that the site already shows it. Acceptance criterion 10 rejects a claim that the line under the name already reads Quality & Delivery Lead. The home-page tagline is still `QA Lead · Test Automation · Agile Delivery`. Issue 5, Step 2, is an instruction to change that line. It is not a report that the change is done.

**Suggested rewrite.** None. The round 1 rewrite is in outline item 1 and in acceptance criterion 10.

### 5. Low — still open — The surname rule is only in the acceptance criteria

Voice still does not mention the surname. Acceptance criterion 6 does. Issue 5, Step 2, spells the name `Slobodan Bogdanović`. `_config.yml` and `index.html` spell it `Bogdanovic`. A drafter who copies those files fails criterion 6. A drafter who skips the name passes.

**Suggested rewrite.** Add to **Voice**:

> Do not use the surname. If a sentence needs it, spell it `Bogdanović` (ć, U+0107). Do not write `Bogdanovic`.

### 6. Low — new — The claims row still names a comparison

The point, the assumptions, and outline item 1 allow one preference: the keyword line is the wrong line under the name. The claims table still lists "Why the new headline is a better description than QA Lead" as a claim the post may use. That is a comparison, and it has no source in the issue. No acceptance criterion rejects it, so a draft can pass the criteria with that sentence in it.

**Suggested rewrite.** Replace that claims-table row with:

> | The keyword line is the wrong line under the name. | Optional one sentence, first person. A preference about placement. Do not argue that the old phrases misdescribe the work, and do not compare the two headlines. | No source in the issue. |

### Verdict

**APPROVE**

### Biggest risk

The draft says Quality & Delivery Lead is a better description than QA Lead. That comparison has no source. The point allows only the preference that the keyword line is the wrong line under the name, and no acceptance criterion rejects the comparison.

Not verified: the live site was not opened, issue comments were not read, and the site was not built.
