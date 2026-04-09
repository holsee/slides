---
name: new-slides
description: Generate a new slide deck presentation from a topic or outline
arguments:
  - name: topic
    description: The talk topic, title, or outline to generate slides for
    required: true
---

# New Slides

Create a new presentation slide deck.

## Instructions

1. Read `CLAUDE.md` for the full design system reference (CSS variables, components, conventions)
2. Read `configuring-your-coding-agent/index.html` as the canonical implementation reference for the exact CSS, JS, speaker notes panel, and Lucide icon system
3. Derive a kebab-case directory name from the topic (e.g. "Intro to MCP Servers" → `intro-to-mcp-servers`)
4. Generate `<dir-name>/index.html` as a single self-contained HTML file:
   - Copy the full CSS block (all styles including notes panel) from the reference presentation
   - Copy the full JS block (navigation, notes, hash routing, icons) from the reference presentation
   - Copy the fixed UI elements (author handle, progress, counter, nav arrows, kb hint with clickable N toggle, notes panel structure)
   - Create a title slide and content slides tailored to the topic
   - Choose the right component for each slide's content — don't force everything into cards
   - Write speaker notes for every slide
   - Only include Lucide icons that are actually used in slides — add their SVG paths to the ICONS map
5. Add a `.talk-item` entry to the root `index.html` inside the `.talk-list` `<ul>`
6. Show the user the final slide count and directory name

## Guidelines

- Aim for 10-20 slides depending on topic depth
- Every slide should be scannable — no walls of text
- Vary the layout components across slides (cards, stats, flows, tables, steps, code trees)
- Speaker notes should contain what the presenter would actually say, not just repeat the slide
- Keep content within visible area especially with notes panel open (deck is 58vh when notes shown)
- Speaker notes default to open on desktop (>=900px) and closed on mobile — the N key/button toggles
- The clickable N kbd in the kb-hint uses classes `kb-orange clickable` with `onclick="toggleNotes()"`
- Nav buttons, counter, and kb-hint get `z-index: 200` when notes are open (above notes panel z-index 150)
- Mobile (<=900px): slides use `overflow-y: auto` so content can scroll, card grids collapse to single column
- The argument may be a short topic ("MCP Servers") or a detailed outline — adapt accordingly
- If the topic is vague, make reasonable choices rather than asking — the user can iterate
