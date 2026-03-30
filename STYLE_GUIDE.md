# Style Guide
## A Software Engineer's Guide to the Apocalypse

This document is the canonical design reference for every page in this series. Before writing any HTML, read this file in full. New work must be visually indistinguishable from the two published articles (`index.html` and `the-language-stack/index.html`).

---

## Typefaces

All four must be loaded from Google Fonts in every page:

```html
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Serif+Display:ital@0;1&family=IBM+Plex+Mono:wght@400;600&family=Instrument+Sans:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet" />
```

| Font | Use |
|---|---|
| **Bebas Neue** | Hero titles, section numbers, pull quote decorative marks, closing CTAs, read-time stats |
| **DM Serif Display** | Section headings (`h2`, `h3`), pull quote text, article card titles, italic subtitles |
| **IBM Plex Mono** | Eyebrow labels, section labels, meta lines, breadcrumbs, badges, URL slugs, `<code>` elements |
| **Instrument Sans** | All body copy (`p`), navigation, general UI text |

Never use system fonts, Inter, Roboto, or any substitute. If the Google Fonts link fails, the page should still be readable but will not be on-brand.

---

## Color System

Defined as CSS custom properties on `:root`. Copy these exactly:

```css
:root {
  --ink: #0f0e0c;       /* near-black — page background, borders, headings */
  --paper: #f5f0e8;     /* warm cream — content section backgrounds */
  --accent: #c8390a;    /* burnt red — eyebrows, links, active states, CTAs */
  --mid: #6b6560;       /* warm gray — body text, secondary labels */
  --light: #e8e2d8;     /* pale cream — hover states, code backgrounds */
  --rule: #d4cec4;      /* hairline — dividers, borders, subtle rules */
}
```

**Alternate section background:** `#f9f5ef` — used on every other `.section` to create rhythm without a hard color break.

**Branch accent colors** (used in the contents page and any navigation context):

```css
--c-purple:   #534AB7;   --c-purple-l: #EEEDFE;   --c-purple-m: #CECBF6;
--c-teal:     #0F6E56;   --c-teal-l:   #E1F5EE;   --c-teal-m:   #9FE1CB;
--c-amber:    #854F0B;   --c-amber-l:  #FAEEDA;   --c-amber-m:  #FAC775;
--c-blue:     #185FA5;   --c-blue-l:   #E6F1FB;   --c-blue-m:   #B5D4F4;
--c-pink:     #993556;   --c-pink-l:   #FBEAF0;   --c-pink-m:   #F4C0D1;
```

Branch color assignments:
- Root article → `--accent` (red)
- Branch one (Horizons) → `--c-purple`
- Branch two (Language Stack) → `--c-teal`
- Branch three (New Roles) → `--c-amber`
- Branch four (Craft & Judgment) → `--c-blue`
- Branch five (Human Side) → `--c-pink`

---

## Page Shell

Every page uses the same shell. The `body` background is `--ink` (dark). Content sections sit on `--paper` (cream) backgrounds, creating a framed editorial look.

### Noise texture overlay

Every page has a subtle noise texture applied as a fixed pseudo-element over the entire viewport. Copy this exactly — do not simplify or remove it:

```css
body::before {
  content: '';
  position: fixed;
  inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
  pointer-events: none;
  z-index: 100;
  opacity: 0.4;
}
```

### Dashed accent stripe

Used at the bottom of the hero and masthead. Applied as a `::after` pseudo-element:

```css
.hero::after {
  content: '';
  position: absolute;
  bottom: -2px;
  left: 0; right: 0;
  height: 6px;
  background: repeating-linear-gradient(
    90deg,
    var(--accent) 0, var(--accent) 20px,
    transparent 20px, transparent 28px
  );
}
```

---

## Components

### Breadcrumb nav

Appears at the very top of every page except the root `index.html`. Dark background, monospace, muted text. The `a` tag links to the parent page via relative URL (`../`).

```html
<nav class="breadcrumb">
  <a href="../">A Software Engineer's Guide to the Apocalypse</a>
  <span>/</span>
  <span>The Language Stack</span>
</nav>
```

```css
.breadcrumb {
  background: var(--ink);
  padding: 16px 40px;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: rgba(245,240,232,0.35);
  display: flex;
  align-items: center;
  gap: 10px;
}
.breadcrumb a { color: rgba(245,240,232,0.5); text-decoration: none; }
.breadcrumb a:hover { color: var(--accent); }
.breadcrumb span { color: rgba(245,240,232,0.2); }
```

---

### Hero (full article pages)

Used on articles, not on the contents/sitemap page. Large Bebas Neue display title with one line in `--accent`. Italic DM Serif subtitle. IBM Plex Mono meta row.

```html
<header class="hero">
  <div class="container">
    <div class="eyebrow">Engineering Leadership · March 2026</div>
    <h1 class="hero-title">
      The
      <span>Language</span>
      Stack
    </h1>
    <p class="hero-subtitle">
      Your subtitle here — italic, DM Serif, warm gray.
    </p>
    <div class="hero-meta">
      <span>10 MIN READ</span>
      <span>LANGUAGE · ENGINEERING · COMMUNICATION</span>
      <span>BY BRIAN BUNKER &amp; CLAUDE SONNET 4.6</span>
    </div>
  </div>
</header>
```

Key CSS values:
- `hero-title`: Bebas Neue, `clamp(56px, 10vw, 112px)`, `line-height: 0.92`, `letter-spacing: -0.01em`
- `hero-title span`: `color: var(--accent); display: block`
- `hero-subtitle`: DM Serif Display, italic, `22px`, `color: var(--mid)`, `max-width: 640px`
- `eyebrow`: IBM Plex Mono, `11px`, `font-weight: 600`, `letter-spacing: 0.2em`, uppercase, `color: var(--accent)`, with a `32px × 2px` red bar before it via `::before`
- `hero-meta`: IBM Plex Mono, `11px`, `color: var(--mid)`, `letter-spacing: 0.1em`, flex row with `gap: 32px`

Hero entrance animation (apply to title, subtitle, meta with staggered delays):
```css
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(24px); }
  to   { opacity: 1; transform: translateY(0); }
}
.hero-title    { animation: fadeUp 0.7s ease both; }
.hero-subtitle { animation: fadeUp 0.7s ease 0.15s both; }
.hero-meta     { animation: fadeUp 0.7s ease 0.25s both; }
```

---

### Content section

The standard content wrapper. Alternates between `--paper` and `#f9f5ef` backgrounds. Max content width `860px` via `.container`.

```css
.section {
  background: var(--paper);
  padding: 72px 40px;
  border-bottom: 1px solid var(--rule);
}
.section:nth-child(even) { background: #f9f5ef; }
.container { max-width: 860px; margin: 0 auto; padding: 0 40px; }
```

Section label (always appears before `h2`):
```css
.section-label {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  font-weight: 600;
  letter-spacing: 0.25em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 28px;
}
```

Body typography:
```css
h2 {
  font-family: 'DM Serif Display', serif;
  font-size: clamp(30px, 4vw, 44px);
  line-height: 1.15;
  color: var(--ink);
  margin-bottom: 28px;
}
h3 {
  font-family: 'DM Serif Display', serif;
  font-size: 22px;
  color: var(--ink);
  margin: 36px 0 12px;
}
p {
  font-size: 17px;
  line-height: 1.75;
  color: #2a2724;
  margin-bottom: 20px;
  max-width: 680px;
}
code {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 0.85em;
  background: var(--light);
  border: 1px solid var(--rule);
  border-radius: 2px;
  padding: 0.1em 0.4em;
  color: var(--accent);
}
```

---

### Pull quote

Dark ink background section with a large decorative quotation mark. Used between content sections for emphasis.

```html
<div class="pull-quote">
  <div class="container">
    <blockquote>
      The quote text here — serif, large, cream colored.
      <cite>— Attribution label</cite>
    </blockquote>
  </div>
</div>
```

```css
.pull-quote {
  background: var(--ink);
  color: var(--paper);
  padding: 72px 40px;
  position: relative;
  overflow: hidden;
}
.pull-quote::before {
  content: '"';
  font-family: 'Bebas Neue', sans-serif;
  font-size: 280px;
  line-height: 1;
  color: rgba(255,255,255,0.05);
  position: absolute;
  top: -20px; left: 20px;
  pointer-events: none;
}
.pull-quote blockquote {
  font-family: 'DM Serif Display', serif;
  font-size: clamp(24px, 3.5vw, 38px);
  line-height: 1.3;
  color: var(--paper);
  max-width: 740px;
  margin: 0 auto;
  position: relative;
  z-index: 1;
}
.pull-quote cite {
  display: block;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 11px;
  font-style: normal;
  letter-spacing: 0.15em;
  color: var(--accent);
  margin-top: 24px;
}
```

---

### Split grid (two-column comparison)

Used for the workshop/factory comparison in article one. Left column is neutral, right column gets the accent color on its label.

```css
.split-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 0;
  margin-top: 48px;
  border: 2px solid var(--ink);
}
.split-col { padding: 40px 36px; }
.split-col:first-child { border-right: 2px solid var(--ink); }
.split-col-label {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 36px;
  letter-spacing: 0.02em;
  margin-bottom: 24px;
  padding-bottom: 16px;
  border-bottom: 2px solid var(--rule);
}
.split-col:last-child .split-col-label { color: var(--accent); }
.split-item {
  padding: 12px 0;
  border-bottom: 1px solid var(--rule);
  font-size: 14.5px;
  line-height: 1.6;
}
.split-item strong {
  display: block;
  font-weight: 600;
  font-size: 12px;
  font-family: 'IBM Plex Mono', monospace;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--mid);
  margin-bottom: 3px;
}
```

---

### Horizon/feature card grid

Used for the six horizons in article one and the dialect cards in article two. Auto-fill grid, bordered cells.

```css
.horizons-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 0;
  margin-top: 48px;
  border: 2px solid var(--ink);
}
.horizon-card {
  padding: 32px 28px;
  border-right: 1px solid var(--ink);
  border-bottom: 1px solid var(--ink);
  transition: background 0.2s;
}
.horizon-card:hover { background: var(--light); }
/* Current horizon gets inverted treatment */
.horizon-card.current {
  background: var(--ink);
  color: var(--paper);
}
.horizon-num {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  font-weight: 600;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 8px;
}
.horizon-badge {
  display: inline-block;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  font-weight: 600;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  background: var(--accent);
  color: white;
  padding: 3px 8px;
  margin-bottom: 10px;
}
.horizon-title {
  font-family: 'DM Serif Display', serif;
  font-size: 20px;
  color: var(--ink);
  margin-bottom: 14px;
  line-height: 1.2;
}
.horizon-card.current .horizon-title { color: var(--paper); }
.horizon-tasks {
  list-style: none;
  margin-top: 12px;
}
.horizon-tasks li {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 12px;
  padding: 5px 0;
  border-top: 1px solid rgba(0,0,0,0.08);
  display: flex;
  gap: 8px;
  align-items: flex-start;
  line-height: 1.5;
}
.horizon-tasks li::before {
  content: '→';
  color: var(--accent);
  flex-shrink: 0;
  font-size: 11px;
  margin-top: 1px;
}
```

---

### Translation stack (stacked before/after blocks)

Used in article two to show the same message rewritten across dialects. Bordered blocks connected by a directional arrow.

```css
.translation-stack {
  margin: 40px 0;
  display: flex;
  flex-direction: column;
  gap: 0;
  max-width: 680px;
}
.translation-block {
  border: 2px solid var(--ink);
  border-bottom: none;
  padding: 28px 32px;
}
.translation-block:last-child { border-bottom: 2px solid var(--ink); }
.translation-label {
  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  font-weight: 600;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 10px;
}
.translation-arrow {
  width: 2px;
  background: var(--ink);
  height: 28px;
  margin: 0 0 0 40px;
  position: relative;
}
.translation-arrow::after {
  content: '↓';
  font-family: 'IBM Plex Mono', monospace;
  font-size: 14px;
  color: var(--mid);
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  background: var(--paper);
  padding: 0 4px;
}
```

---

### Closing CTA section

Accent red background, centered, large Bebas Neue heading, white body text. Always the last section.

```css
.closing {
  background: var(--accent);
  padding: 80px 40px;
  text-align: center;
}
.closing h2 {
  font-family: 'Bebas Neue', sans-serif;
  font-size: clamp(42px, 7vw, 80px);
  letter-spacing: 0.02em;
  color: white;
  margin-bottom: 20px;
  line-height: 1;
}
.closing p {
  font-size: 18px;
  color: rgba(255,255,255,0.85);
  max-width: 600px;
  margin: 0 auto 16px;
  line-height: 1.7;
}
```

---

### Footer

Dark ink background, centered, monospace, very muted. Same on every page.

```css
footer {
  background: var(--ink);
  padding: 32px 40px;
  text-align: center;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 11px;
  letter-spacing: 0.1em;
  color: rgba(245,240,232,0.3);
}
footer a { color: rgba(245,240,232,0.4); text-decoration: none; }
footer a:hover { color: var(--accent); }
```

Footer text format: `[Article Title] · [Section if applicable] · [Month Year]`

---

## Editorial Conventions

**Section structure.** Every content section opens with a `.section-label` (IBM Plex Mono, uppercase, red) before the `h2`. No exceptions. The label names the function of the section, not its topic — e.g. "The Stakes", "The Framework", "The Analogy That Lands", "The Practical Part".

**Body text width.** Body `p` elements have `max-width: 680px`. Content sections have `max-width: 860px` via `.container`. Never let body text run full width.

**Alternating section backgrounds.** Content sections alternate between `--paper` (#f5f0e8) and `#f9f5ef`. This creates rhythm on long scrolling pages.

**Pull quotes.** Used once or twice per article to break up dense text. Always a single sentence or short claim — not a summary of the surrounding argument. The `<cite>` is a short label describing what the quote represents, not a person's name.

**Lists in body copy.** The articles use `<ul>` inside `.horizon-tasks` with `→` arrow prefixes. In regular body sections, prefer prose over bullet lists.

**Bold in body copy.** Used for the opening word or phrase of a key action item in "practical" sections — e.g. `<strong>Think product first.</strong>` followed by the explanation. Never bold random words mid-paragraph.

**Code inline.** Used sparingly for technical terms being presented as terms — e.g. `<code>SegmentationFault</code>`, `<code>/bug-report</code>`. Color is `--accent`.

**Internal links.** Use `style="color:var(--accent);text-decoration:none;border-bottom:1px solid currentColor;"` for inline prose links within article body copy.

---

## Responsive Breakpoints

```css
@media (max-width: 640px) {
  .split-grid { grid-template-columns: 1fr; }
  .split-col:first-child { border-right: none; border-bottom: 2px solid var(--ink); }
  .section, .horizons-section, .split-section, .pull-quote, .closing { padding: 48px 24px; }
  .hero { padding: 56px 24px 48px; }
  .breadcrumb { padding: 16px 24px; }
  .container { padding: 0 24px; }
}
```

---

## File & Folder Conventions

- Root article: `index.html`
- Each article in its own subfolder: `the-language-stack/index.html`
- Folder names are lowercase, hyphenated, descriptive of content
- All internal links use relative paths (`../`, `../the-language-stack/`)
- The contents/sitemap page lives at `contents/index.html`
