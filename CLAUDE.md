# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Static HTML slide deck repository hosted on GitHub Pages at https://holsee.github.io/slides/. No build step — edit HTML directly and push.

## Structure

- `index.html` — Landing page listing all presentations
- `<talk-name>/index.html` — Individual slide decks, one per subdirectory

## Adding a new presentation

1. Create a new directory (e.g. `my-talk/index.html`)
2. Add a link entry to the root `index.html` inside the `.talk-list` `<ul>`

## Visual theme

All pages share a CRT terminal aesthetic: dark background (`--bg: #020810`), cyan accent (`--accent: #4fc3f7`), Noto Sans Mono font, scanline overlay, vignette, and flicker animation. CSS variables are defined in each file's `:root` block. Keep new pages visually consistent.

## Deployment

Push to `master` — GitHub Pages deploys automatically from the branch root.
