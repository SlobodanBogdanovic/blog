# AI skills register

Third-party skills are guidance. `AGENTS.md` and the project skills `blog-conventions`, `site-conventions`, and `site-verification` win when they disagree.

Vetting for a third-party skill:

- Prefer an official or well-maintained source. Accept only MIT, Apache-2.0, BSD-2-Clause, BSD-3-Clause, or ISC.
- Copy the license into the skill folder. If it lives at the upstream repo root, copy it next to `SKILL.md` and say so here.
- Reject a skill that tells the agent to download further rules and follow them, run an install script, ask for a secret or a token, override `AGENTS.md` or `blog-conventions`, or hide instructions.
- Vendor accepted files at one commit SHA. Do not auto-update.
- One skill per topic.

## Accepted

### blog-conventions

- Topic: this blog's path, front matter, and voice
- Source: this repo
- License: project-authored
- Date added: 2026-11-21
- Updated: 2026-11-28, so an update that changes a post's date or content deletes the old file and adds one new file whose date matches its filename, and asks one question only when that path cannot be chosen
- Reason: no catalog skill knows `_posts/` or the existing posts
- Review: written for this repo. `role-spec`, `role-review`, and `role-write` read it before the third-party skill. `role-frontend` follows `site-conventions` for site files.

### editorial-methodology

- Topic: planning, structure, voice, citations, revision, and fact-checking
- Source: https://github.com/magnus919/hermes-profiles
- skills.sh: https://www.skills.sh/magnus919/hermes-profiles/editorial-methodology
- Commit: `867a555e13bae53a3945aa5328b1e09d347268cc`
- License: MIT. The license file is at the upstream repo root and is copied to `.cursor/skills/editorial-methodology/LICENSE`.
- Date added: 2026-11-21
- Reason: one editorial skill for spec, review, and the draft. The repo has about 340 stars. It is archived, so the SHA stays pinned.
- Review: read `SKILL.md` and all five files in `references/`. The skill is a short process plus those notes. It does not download further rules, run an install script, ask for a secret, or tell the agent to override `AGENTS.md`. The publish step in the lifecycle is not followed. Opening the pull request ends the run.

### site-conventions

- Topic: the home page, the post layout, the 404 page, the shared head include and stylesheet, the unused remote theme, where a design change goes, and which role may edit which file
- Source: this repo
- License: project-authored
- Date added: 2026-11-22
- Updated: 2026-11-25, to describe `_includes/head.html`, `assets/css/site.css`, and the self-hosted fonts, and to let a site ticket list those files without the issue naming them
- Reason: no catalog skill knows this home page or the split between `index.html` and the Minimal Mistakes setting in `_config.yml`
- Review: written for this repo. `role-spec`, `role-review`, and `role-frontend` read it. It does not download further rules or ask for a secret.

### site-verification

- Topic: the checks that run after a ticket is implemented, and the commands that must not publish
- Source: this repo
- License: project-authored
- Date added: 2026-11-22
- Updated: 2026-11-28, so the post check requires the calendar day in the front matter to match the filename, including after a post is replaced
- Reason: the catalog checks are for other generators, or they end in a publish step
- Review: written for this repo. `role-test` reads it. A local Jekyll build is a check. Deploy, serve, and merge are not.

Who reads which file:

- `role-spec` reads `blog-conventions`, `site-conventions`, and, for a post, `references/article-structures.md` and `references/voice-reference.md`.
- `role-review` reads `blog-conventions`, `site-conventions`, `references/revision-protocol.md`, `references/fact-checking.md`, and `references/source-hygiene.md`.
- `role-write` reads `blog-conventions`, `references/voice-reference.md`, and `references/source-hygiene.md`.
- `role-frontend` reads `site-conventions`.
- `role-test` reads `blog-conventions` and `site-verification`.

## Refused

These were looked up on skills.sh and were not installed.

- **grill-me** and **grilling** (mattpocock/skills). They wait for an answer on every question. This run records assumptions and continues.
- **writing-beats** (mattpocock/skills). It stops after each beat for a human choice.
- **writing-plans** (obra/superpowers) and **implement-spec** (mattpocock/skills). They are for code, tests, and ticket graphs.
- **content-blog** (vstorm-co/content-skills), **editorial-copy** (srstomp/copyskills), **medium-style-blog-writer** (samihalawa/medium-style-blog-writer-skill), and **house-style** (RightBlogger/bloggingskills). They push a marketing or SEO voice, ask which template to use, or ban punctuation this blog already uses. Those source repos are small.
- Pull-request review skills. `role-review` reviews the spec. The human reviews the pull request.
- **frontend-design** (anthropics/skills). It would restyle the page away from the HTML already in this repo.
- **skill-creator** (anthropics/skills). The project skills for this repo are written here. That catalog skill is not installed.
- **pre-publish-checker** (notque/vexjoy-agent). It is Hugo, it is aimed at SEO, and it treats the job as publishing.
- **publishing-checklist** (Christos-Hadjinikolis/Christos-Hadjinikolis.github.io). It is another person's Jekyll site, it calls `make build`, and it is framed as a deploy.
- **jekyll** (n-n-code/n-n-code-skills). It authorizes editing the site beyond the files a spec lists.
- **verify-build** (heyeddi-com/heyeddi-skills). It is npm and Vite.
- **static-seo** (jdevalk/skills), **website-quality-check** (oocx/tfplan2md), **markdown-post-frontmatter-validation** (jacob-balslev/skill-graph), and **write-check-links** (jeffabailey/skills-writing). They target other sites, other generators, or extra tools.
- **docmeta** (hawkeyexl/docmeta). It is a new Node dependency, and its default schema is not this blog's front matter.

## Maintenance

Update `editorial-methodology` only by reading the whole skill at a new SHA and replacing the vendored files. Do not auto-update.
