# 001 — The Line Under My Name

## Brief

GitHub issue 1, "Look and feel improvement", is an implementation brief for the GitHub Pages site. It asks for a new headline, a Linux-desktop reading theme, self-hosted fonts, and a shell-style home page. This pipeline produces one post. The post is a short first-person argument that records the presentation decisions in that issue. It does not implement them.

Working title from the issue: "Look and feel improvement". Post title: "The Line Under My Name". Slug: `look-and-feel-improvement`. Path: `_posts/2026-11-22-look-and-feel-improvement.md`. Date: 2026-11-22.

The post states three strings exactly as the issue states them:

- The headline under the name becomes `Quality Engineering | Agile Delivery`.
- The name stays `Slobodan Bogdanović`, with the character ć (U+0107).
- The existing sentence stays: `Writing about software quality and engineering.`

The post then says, as his decision, that a Linux-desktop frame is only there so a long post stays comfortable to read, and that the page stays a name, that headline, GitHub and LinkedIn, then the posts.

## Reader

Someone who already reads this blog for notes on quality engineering and agile delivery, and who will notice the line under the name. Not an implementer looking for CSS, font files, or a build guide.

## Point

The line under the name should name the work, `Quality Engineering | Agile Delivery`, and the rest of the page should stay a reading page. The shell, the monospace chrome, and the palette are a frame for that reading, not a new section of the site.

## Outline

Short argument, in the shape of `_posts/2026-04-11-testing-vs-qa.md`. Prose paragraphs. No bullet list. No fenced code. Two `##` headings. A reader who only reads the headings and the first sentence still gets the decision.

1. **Opening, no heading.** First sentence states the decision in the first person, as a change he is making: the line under the name becomes `Quality Engineering | Agile Delivery`. Do not describe the live page as already showing that line. Do not quote the tagline from `index.html` or `_config.yml`. The same opening keeps the name `Slobodan Bogdanović` and the sentence `Writing about software quality and engineering.` One following paragraph, opinion: a role label is a narrower description than the subjects the blog already writes about. Do not define quality engineering, testing, or agile. Do not summarize or quote the existing posts.

2. **`## A frame for reading`.** Two short paragraphs. First: the Linux-desktop chrome, including a home page that reads like a short shell session, is his choice so a long post stays comfortable to read, and this post is not a claim that the theme is already on the site. Second: he wants body text in Inter, JetBrains Mono only for the chrome and for code, type at 18px with line height 1.7 and a measure of about 68ch as written in issue 1, and light and dark following the system with the Catppuccin palette he named (Mocha in the dark, Latte in the light). Do not inventory every monospace slot, do not print either font stack, and do not print the hex table. One sentence may say that text below WCAG AA (4.5:1) has to be adjusted, that 4.5:1 is the threshold he named, and that this post is not that check.

3. **`## What stays`.** Name, the new headline, links to GitHub and LinkedIn only, then the list of posts. No email. No new sections. He is not rewriting published posts and he is not changing their URLs. Those are his rules from the issue, not a crawl result. Do not list post titles or URLs.

4. **Close, one or two sentences, no new heading.** The shell chrome is a frame. The post is the part a reader should be able to finish. Do not add a further-reading line. The issue gave no sources.

## Claims and sources

The issue is the only source. No citation, quote, or statistic that the issue does not contain. No hyperlinks. No further-reading line.

| Claim in the post | How to treat it |
| --- | --- |
| Headline becomes `Quality Engineering | Agile Delivery` | Author's instruction in issue 1. State it as his decision. |
| Name is `Slobodan Bogdanović`, with ć | Author's instruction in issue 1. Use that spelling. |
| Keep `Writing about software quality and engineering.` | Author's instruction in issue 1. Quote it as the sentence he is keeping. |
| Home page stays name, headline, GitHub, LinkedIn, then posts. No email, no new sections. | Author's instruction in issue 1. |
| Inter for body text; JetBrains Mono only for the chrome and for code. | Author's font rule in issue 1. Name the two faces and say monospace is limited to the chrome and to code. Do not claim the files are in the repo or that a Latin Extended subset was built. |
| Body at 18px, line height 1.7, width about 68ch | Author's reading rule in issue 1. Do not cite a readability study or call these values an optimum. |
| Catppuccin Mocha for dark and Latte for light, switched with `prefers-color-scheme` | Author's palette choice in issue 1. Do not reproduce hex codes. Do not describe them as contrast-tested. |
| Text below WCAG AA (4.5:1) has to be adjusted. | His bar in issue 1. Unverified. The post may mention 4.5:1 only as the threshold he named. It must not say a color was measured, adjusted, or found to pass. |
| Lighthouse accessibility of at least 95 | A done-when line for the theme work. Not a result. Do not mention a score. |
| Existing post URLs still resolve | A done-when line for the theme work. Not checked for this spec. The post may say he does not want those URLs changed. It must not say they were requested or that they resolve. |
| Current home tagline is `QA Lead · Test Automation · Agile Delivery` plus the writing sentence | Verified only in `index.html` in this repo. `_config.yml` uses `QA Lead \| Test Automation \| Agile Delivery` and spells the name without ć. The published site was not opened. The post may say, in the first person, that the line he has been using names a role. It must not quote the tagline from `index.html` or `_config.yml`, and it must not claim the live page was inspected. |
| He is a QA lead, the blog is Jekyll, the public URL is `https://slobodanbogdanovic.github.io/blog` | In `AGENTS.md` and `_config.yml`, not in the issue. Leave them out of the post. |

Opinion, labeled as his judgment, not as a finding: a role label is narrower than the subjects of the blog; the shell chrome is a frame and the article is the part that has to read well.

## Voice

First person. Contractions throughout. Short paragraphs, one idea each. Plain sentences, the way `_posts/2026-04-11-testing-vs-qa.md` argues, without that post's outside links. No marketing words, no hype, no slogan stack. Do not address the reader as "you" until the close, and then only if the closing sentence needs it. No imperatives and no tutorial steps. No headings written as prompts (`slobodan@blog`). The name ć is the Unicode character, not an HTML entity and not `Bogdanovic`.

## Acceptance criteria

1. The post file is `_posts/2026-11-22-look-and-feel-improvement.md` and no other post file is added.
2. Front matter sets `title: "The Line Under My Name"`, `date: 2026-11-22`, `layout: post`, a `categories` list that includes `Quality Engineering`, a `tags` list that includes `Agile`, and an `excerpt` of one sentence.
3. The excerpt does not claim a contrast ratio, a Lighthouse score, or that the theme is already on the site.
4. The body contains the exact string `Quality Engineering | Agile Delivery`.
5. The body contains `Slobodan Bogdanović` with the character ć (U+0107), and it does not contain `Bogdanovic`.
6. The body contains the exact sentence `Writing about software quality and engineering.`
7. The body has exactly two `##` headings: `A frame for reading` and `What stays`.
8. The body has no bullet list, no numbered list, no image, no hyperlink, and no fenced code block.
9. The body does not contain a hex color, `@font-face`, a `Lighthouse` score, the digit sequence `95` as an accessibility result, or a statement that a contrast ratio was measured or met.
10. The body does not say that existing post URLs were checked or that they resolve.
11. The body does not quote or name Michael Bolton, Catppuccin's documentation, a font foundry, or a work issue 1 does not name. The body may name Inter, JetBrains Mono, Catppuccin, Mocha, Latte, and WCAG AA, because issue 1 names them.
12. The close is one or two sentences after `## What stays` and does not add a source.
13. The body contains a first-person sentence that the theme in this post is not already on the site. It does not describe the live page as already using the new headline, Inter, JetBrains Mono, or Catppuccin.

## Out of scope

- Any change to `_config.yml`, `index.html`, `_layouts/post.html`, `Gemfile`, CSS, font files, or an existing post.
- The shell-session home page, the top bar, `prefers-reduced-motion`, focus styles, tables, syntax colors, and responsive layout. Those belong to the theme work in issue 1, not to this post.
- Self-hosting Inter or JetBrains Mono, including any Latin Extended subset.
- Checking contrast, running Lighthouse, building the site, or requesting the live URLs.
- A second post, a screenshot, or a design ticket pasted as the article.
- Publishing, deploying, or merging. This role does not commit, push, or open a pull request.

## Assumptions

- Issue 1 has no reader, no thesis, and no sources. The gap is filled by the Point and Reader above. The theme checklist is not the article.
- The run date is 2026-11-22, so that is the post date.
- Readers of the existing posts are the audience. Nobody was asked.
- `index.html` in the repo shows the role line and the writing sentence, loads IBM Plex from Google Fonts, and spells the visible name without ć. `_config.yml` sets `remote_theme` to Minimal Mistakes while the home page is a standalone `index.html`. The post does not explain that split.
- Publication is out of scope. Editorial methodology's publish step is skipped.

Not verified:

- The live site at `https://slobodanbogdanovic.github.io/blog` was not opened.
- Contrast for the issue's Catppuccin colors was not calculated.
- No Lighthouse run was made.
- No font file was inspected. The repo has no Inter or JetBrains Mono files.
- GitHub and LinkedIn links in `index.html` were not requested.
- Existing post URLs were not requested.

## Review

Round 2. Revised spec after round 1. Voice matches the blog: first person, short paragraphs, a firm point, a short close. Scope is one post. The theme work sits in **Out of scope**. Claims are tied to issue 1, marked as his judgment, or listed under **Not verified**. Every acceptance criterion is a check in the Markdown file. No new findings.

1. **Medium — resolved.** Outline item 2 now leads with the shell as a reading frame, forbids a monospace inventory, font stacks, and the hex table, and uses "about 68ch" as issue 1 writes it. The close no longer hangs on the word "prompt." The Inter row matches that compression.

   Suggested rewrite, already the spec text:

   > 2. **`## A frame for reading`.** Two short paragraphs. First: the Linux-desktop chrome, including a home page that reads like a short shell session, is his choice so a long post stays comfortable to read, and this post is not a claim that the theme is already on the site. Second: he wants body text in Inter, JetBrains Mono only for the chrome and for code, type at 18px with line height 1.7 and a measure of about 68ch as written in issue 1, and light and dark following the system with the Catppuccin palette he named (Mocha in the dark, Latte in the light). Do not inventory every monospace slot, do not print either font stack, and do not print the hex table. One sentence may say that text below WCAG AA (4.5:1) has to be adjusted, that 4.5:1 is the threshold he named, and that this post is not that check.

2. **Medium — resolved.** Criterion 11 names what the body must not cite and the names issue 1 allows, so a post can follow the outline and pass the check.

   Suggested rewrite, already the spec text:

   > 11. The body does not quote or name Michael Bolton, Catppuccin's documentation, a font foundry, or a work issue 1 does not name. The body may name Inter, JetBrains Mono, Catppuccin, Mocha, Latte, and WCAG AA, because issue 1 names them.

3. **Medium — resolved.** The opening is a change he is making, and it forbids treating the live page as already showing the line or quoting the tagline from `index.html` or `_config.yml`. Criterion 13 requires a first-person sentence that the theme is not already on the site, and it forbids describing the live page as already using the new headline, Inter, JetBrains Mono, or Catppuccin.

   Suggested rewrite, already the spec text:

   > First sentence states the decision in the first person, as a change he is making: the line under the name becomes `Quality Engineering | Agile Delivery`. Do not describe the live page as already showing that line. Do not quote the tagline from `index.html` or `_config.yml`.
   >
   > 13. The body contains a first-person sentence that the theme in this post is not already on the site. It does not describe the live page as already using the new headline, Inter, JetBrains Mono, or Catppuccin.

4. **Low — resolved.** The WCAG row states issue 1's bar, allows 4.5:1 as the threshold he named, and forbids a measured, adjusted, or passing result.

   Suggested rewrite, already the spec text:

   > Text below WCAG AA (4.5:1) has to be adjusted. | His bar in issue 1. Unverified. The post may mention 4.5:1 only as the threshold he named. It must not say a color was measured, adjusted, or found to pass.

5. **Low — still open.** Outline item 3 still starts with "Name, the new headline," which the opening already requires. It does not tell the writer to leave that string in the opening. The page order, GitHub and LinkedIn only, and the rule against rewriting posts or changing URLs are in the section, and the headline can still be quoted there a second time.

   Suggested rewrite of outline item 3:

   > 3. **`## What stays`.** The page stays a name, that headline, links to GitHub and LinkedIn only, then the list of posts. No email. No new sections. He is not rewriting published posts and he is not changing their URLs. Those are his rules from the issue, not a crawl result. Do not quote the headline again, and do not list post titles or URLs.

**Verdict: APPROVE**

**Biggest risk:** **What stays** can quote the headline again, so the new rules in that section — GitHub and LinkedIn only, no email, no rewritten posts, no changed URLs — carry less of the piece than a second pass over the line under the name.
