# Claude Code Instructions
## A Software Engineer's Guide to the Apocalypse

This file is read automatically by Claude Code at the start of every session. Follow these instructions for all work on this repository.

---

## Before Writing Any HTML

**Always read these files first, in this order:**

1. `STYLE_GUIDE.md` — the complete design system: CSS variables, typefaces, components, editorial conventions
2. The most relevant existing article — either `index.html` (root) or `the-language-stack/index.html`

Do not write a single line of HTML until you have read both. The visual quality of this series depends entirely on consistency with what already exists. When in doubt about how something should look, the answer is in one of those two files.

---

## What This Series Is

A multi-article editorial series about the changing nature of software engineering work in the AI era. Written by Brian Bunker in collaboration with Claude Sonnet 4.6. Published as static HTML via GitHub Pages.

The tone is: direct, honest, not alarmist. It doesn't tell people what to feel — it gives them a map. The writing is the product. The design serves the writing.

Two articles are published. The structure, design system, and folder conventions are established. New work extends what exists — it does not reinvent it.

---

## Writing New Articles

### Content first

Drafting an article means writing the full content — sections, pull quotes, examples, suggested reading — before touching HTML. Get the argument right before thinking about layout.

Each article should have:
- A clear single thesis stated early
- 3–6 named sections, each with a `.section-label` that names the section's function (not just its topic)
- One or two pull quotes — short claims, not summaries
- A "The Practical Part" section with 4–6 bolded action items
- A closing statement (goes in the `.closing` red CTA section)
- 3–5 suggested reading items with source attribution

### Structure

Follow the exact HTML structure of the existing articles:

```
breadcrumb nav
hero (with eyebrow, h1 with accent span, subtitle, meta)
content sections (alternating paper/slightly-darker backgrounds)
pull quote(s) (dark background, large serif quote)
closing CTA (accent red background)
suggested reading section
footer
```

### Tone and voice

- Present tense, declarative sentences
- Uses "we" and "you" — not "engineers" as a distant third party
- Honest about difficulty and uncertainty without being defeatist
- Technical vocabulary is used precisely, not avoided
- Analogies are developed fully — not just named and dropped
- Sections end with forward momentum, not summary

---

## Design Rules (summary — full detail in STYLE_GUIDE.md)

- **Four fonts only:** Bebas Neue (display), DM Serif Display (headings/quotes), IBM Plex Mono (labels/meta/code), Instrument Sans (body). Load all four from Google Fonts. No others.
- **Six core CSS variables:** `--ink`, `--paper`, `--accent`, `--mid`, `--light`, `--rule`. Copy them from STYLE_GUIDE.md verbatim.
- **Noise texture overlay** on `body::before` — copy the exact SVG data URI from STYLE_GUIDE.md
- **Dashed accent stripe** on `.hero::after` — copy the exact gradient from STYLE_GUIDE.md
- **Body text max-width: 680px.** Never wider.
- **Section labels** before every `h2`. IBM Plex Mono, uppercase, `--accent` colored.
- **Alternating section backgrounds** — `--paper` and `#f9f5ef`
- New design patterns are not invented. If a component doesn't exist in STYLE_GUIDE.md, ask before creating it.

---

## File Conventions

- New articles go in their own subfolder: `branch-name/article-name/index.html`
- All internal links use relative paths: `../../` to reach root, `../` to reach branch
- Breadcrumb on every page except root `index.html`
- Footer format: `[Article Title] · [Section if applicable] · [Month Year]`

See STYLE_GUIDE.md for the full proposed folder structure.

---

## Contents Page

The series navigation lives at `contents/index.html`. Update it whenever a new article is published:

1. Change the article's `.seq-item` from `is-next` or `is-forthcoming` to `is-live`
2. Add an `href` to the `<a>` tag
3. Change the `.seq-url` class from `muted` to `live`
4. Update the masthead stats (published count)
5. Update the "Read next" bridge below the root card if the newly published article is the logical next read

---

## What Not to Do

- Do not use system fonts, Inter, Roboto, or any font not in the Google Fonts import
- Do not invent new color variables — use only what's in STYLE_GUIDE.md
- Do not make the hero smaller or larger than the existing articles without a specific reason
- Do not use bullet point lists in body copy — use prose, or the `horizon-tasks` pattern with `→` arrows
- Do not summarize what you're about to write — write it
- Do not add decorative elements (gradients, shadows, icons) not present in the existing articles
- Do not change the folder naming pattern or link structure without updating contents/index.html

---

## Collaboration Model

This repo is maintained by Brian Bunker using Claude Code (Claude Sonnet 4.6) for structure, content drafting, and file management. Visual refinement and design review happens in claude.ai. The two tools are complementary:

- Claude Code: article drafting, HTML scaffolding, repo management, contents page updates
- Claude.ai: visual QA, new component design, design system decisions

If a visual output looks off, note it and flag for review in claude.ai rather than trying to fix it by guessing at CSS.
