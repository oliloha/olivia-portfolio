# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

A static personal portfolio website for Olivia — a marketer transitioning into product. No build toolchain, no dependencies, no package manager. Everything runs directly in the browser.

To preview locally, open `index.html` in a browser or use a simple static server:

```bash
python3 -m http.server 8080
```

## File structure

- `index.html` — the live portfolio (current design)
- `before.html` — the previous dark/space-themed version (kept as reference, not linked)

## Architecture

Both files are fully self-contained: all CSS lives in a `<style>` block in `<head>`, and all JavaScript is inline at the bottom of `<body>` before `</body>`. There are no external JS/CSS files (only Google Fonts loaded via CDN).

### Design system (`index.html`)

The current design uses a **journal/scrapbook aesthetic** — warm paper tones, hand-drawn SVG doodles, slightly-rotated cards with tape accents. CSS custom properties define the palette:

- `--paper` / `--paper-2` / `--paper-3` — background layers
- `--ink` / `--ink-2` / `--ink-dim` — text hierarchy
- `--peach`, `--pink`, `--yellow`, `--sage`, `--lavender`, `--sky` — accent colors used on cards
- `--tape-*` variants (e.g. `--tape-yellow`) — semi-transparent versions used for decorative tape strips
- Fonts: `Caveat` (handwritten, headings/accents), `Space Grotesk` (body), `Space Mono` (labels/mono)

The previous design (`before.html`) used a **dark space/cosmic** palette (`--teal`, `--violet`, dark `--space-*` backgrounds) — relevant if restoring that aesthetic.

### Sections

`index.html` has these sections in order: Hero → About (`#about`) → AI & Tools (`#ai-tools`) → Work (`#work`) → Contact (`#contact`) → Footer.

The Skills section exists in both files but is commented out (`<!-- ── SKILLS (removed) ── -->`).

### Animation patterns

- **Scroll reveal**: Elements get `.reveal` class; an `IntersectionObserver` adds `.visible` when they enter the viewport. Stagger via `.reveal-delay-1` through `.reveal-delay-6`.
- **Counter animation**: `.stat-num` elements animate their numeric value on scroll via a second `IntersectionObserver` + eased `requestAnimationFrame` loop.
- **Canvas background**: `index.html` uses a geometric network (nodes + connecting lines); `before.html` uses a star-field with shooting stars. Both are drawn on `#bg-canvas` (fixed, `pointer-events: none`).
- **Custom cursor**: Pencil SVG cursor set on `body`, with a dot + ring overlay (hidden on mobile via CSS).

### Responsive breakpoints

- `max-width: 900px` — collapses grids to 1 column, hides desktop nav, shows hamburger
- `max-width: 520px` — further collapses stats grid, reduces hero font size
