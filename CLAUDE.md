# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Static HTML slide decks hosted on GitHub Pages at https://holsee.github.io/slides/. No build step — edit HTML directly and push to `master`.

## Structure

- `index.html` — Landing page listing all presentations (same CRT theme)
- `<talk-name>/index.html` — Individual slide decks, one per subdirectory

## Creating a new presentation

1. Create `<talk-name>/index.html` as a single self-contained HTML file
2. Use the design system below — reference `configuring-your-coding-agent/index.html` as the canonical example
3. Add a `.talk-item` link to root `index.html` inside the `.talk-list` `<ul>`
4. Each presentation is unique — choose components that fit the content, don't force every slide into the same layout

## Design system

### Theme: CRT Terminal

All presentations use a dark CRT terminal aesthetic. Single-file HTML with no external dependencies except Google Fonts.

**Font:** Noto Sans Mono (all weights 400-700) via Google Fonts import  
**Effects:** CRT scanlines (`body::before`), vignette (`body::after`), subtle flicker animation

### CSS variables (`:root`)

```
--bg: #020810          /* main background */
--bg-alt: #0a1628      /* alternate bg */
--bg-card: #0c1a2e     /* card/panel bg */
--accent: #4fc3f7      /* primary cyan */
--accent2: #29b6f6     /* secondary cyan */
--accent3: #81d4fa     /* tertiary cyan */
--green: #4dd0e1
--amber: #80deea
--rose: #e0f7fa
--text: #b3e5fc        /* body text */
--muted: #4a6a7a       /* subdued text */
--dim: #1a3050         /* decorative/borders */
--border: #1e3a5f
--glow-strong: 0 0 8px #4fc3f780, 0 0 20px #4fc3f730
--glow-text: 0 0 6px #4fc3f750
```

### Fixed UI elements (present on every presentation)

- `a.author-handle` — top-right, links to https://x.com/holsee
- `div.progress` — top progress bar
- `div.counter` — bottom-right slide counter `[ 3 / 19 ]`
- `div.nav-arrows` — bottom-center prev/next buttons
- `div.kb-hint` — bottom-left keyboard shortcut hint

### Slide basics

```html
<div class="deck" id="deck">
  <div class="slide">...</div>
  <div class="slide">...</div>
</div>
```

- Slides use `position: absolute; inset: 0` with `justify-content: flex-start`
- Padding: `8vh 6vw`
- Add `anim` class to direct children of `.slide` for staggered fade-in (up to 6 children auto-staggered)

### Title slide (first slide only)

```html
<div class="slide title-slide">
  <div class="section-label anim">Section Label</div>
  <div class="mega-title anim">Talk Title</div>
  <div class="mega-subtitle anim">Subtitle text.</div>
  <div class="tag-line anim">Date &middot; Tags</div>
</div>
```

The title slide centers vertically, has a gradient panel on the right, and a blinking cursor after the mega-title.

### Standard content slide

```html
<div class="slide">
  <div class="section-label anim">Section</div>
  <div class="slide-title anim">Title</div>
  <div class="slide-subtitle anim">Optional paragraph.</div>
  <!-- layout component(s) -->
  <div class="callout anim">Optional takeaway.</div>
</div>
```

### Available components

**Card grid** — feature lists, grouped concepts. 2-5 columns via `.cols-{2,3,4,5}`.
```html
<div class="card-grid cols-3 anim">
  <div class="card" data-accent="green">
    <div class="card-title green">Title</div>
    <div class="card-desc">Description text.</div>
  </div>
</div>
```
Accent colors: `accent` (default cyan), `green`, `amber`, `rose`, `violet`, `sky`. Set both `data-accent` on `.card` and color class on `.card-title`.

**Stat grid** — up to 3 big numbers.
```html
<div class="stat-grid anim">
  <div class="stat-card"><div class="stat-num">60%</div><div class="stat-label">Description</div></div>
</div>
```

**Flow grid** — up to 5 numbered process steps (horizontal).
```html
<div class="flow-grid anim">
  <div class="flow-step"><div class="flow-num">1</div><div class="flow-title">Step</div><div class="flow-desc">Detail</div></div>
</div>
```

**Step list** — vertical numbered steps with descriptions.
```html
<div class="step-list anim">
  <div class="step-item"><div class="step-num">1</div><div><div class="step-content-title">Title</div><div class="step-content-desc">Description</div></div></div>
</div>
```

**Comparison table** — feature grids.
```html
<table class="comparison-table anim">
  <tr><th>Feature</th><th>Tool A</th><th>Tool B</th></tr>
  <tr><td>Item</td><td>Value</td><td>Value</td></tr>
</table>
```

**Code tree** — directory/file structure display.
```html
<div class="code-tree anim">
  <div class="tree-header">project/</div>
  <div class="tree-line">&boxvr;&boxh;&boxh; <span>file.txt</span></div>
  <div class="tree-line">&boxur;&boxh;&boxh; <span>last-file.txt</span></div>
</div>
```

**Resource list** — links with arrow bullets.
```html
<ul class="resource-list anim">
  <li><strong>url.com</strong> &mdash; Description</li>
</ul>
```

**Tip box** — highlighted advice.
```html
<div class="tip-box anim"><span class="tip-icon">&gt;</span> Tip content.</div>
```

**Callout** — key takeaway, prefixed with `> `.
```html
<div class="callout anim">Important point.</div>
```

**Permission rows** — allow/ask/deny patterns.
```html
<div class="perm-row"><div class="perm-label">Allow</div><div class="perm-desc">Description</div></div>
<div class="perm-row ask"><div class="perm-label">Ask</div><div class="perm-desc">Description</div></div>
<div class="perm-row deny"><div class="perm-label">Deny</div><div class="perm-desc">Description</div></div>
```

**Hook timeline** — 4-column event cards.
```html
<div class="hook-flow anim">
  <div class="hook-card"><div class="hook-name">Name</div><div class="hook-desc">Description</div></div>
</div>
```

### Speaker notes panel

Orange terminal theme, toggles with `N` key. Place inside `.notes-content`:
```html
<div class="note-section" data-slide="0">
  <div class="note-heading">Topic</div>
  <div class="note-point">Talking point.</div>
  <div class="note-emphasis">Emphasized text inline.</div>
  <div class="note-data">Data/code block in notes.</div>
  <div class="note-cue">Transition cue (italic, prefixed with //).</div>
</div>
```
`data-slide` is 0-indexed. Notes panel is open by default and pushes the deck to 58vh.

### Navigation (JS boilerplate)

Every presentation needs the same JS block:
- `show(idx)` — activates slide, updates progress/counter/hash/notes
- `slideFromHash()` — parses `#N` from URL (1-indexed, human-friendly)
- `hashchange` listener for browser back/forward
- Keyboard: arrows/space navigate, Home/End jump, N toggles notes
- Touch swipe support
- Notes panel toggle with deck push

Reference the `<script>` block in `configuring-your-coding-agent/index.html` and replicate it exactly for new presentations.

### Lucide icons

Icons are inlined as SVG path data in a `const ICONS = {}` map — no CDN. Use `<i data-lucide="icon-name"></i>` in HTML. Add new icons to the map as needed. The JS at the bottom replaces `[data-lucide]` elements with SVGs.

## Design principles

- Every slide should be scannable — avoid walls of text
- Use cards and grids to structure information visually
- Keep content within the visible area (especially with notes open at 58vh)
- Color accents should be meaningful, not decorative — use them to group or distinguish
- Each presentation should feel like it belongs to the same family but have its own structure suited to its content
