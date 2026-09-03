# Scattered Stars Design — 2026-09-03

## Goal
Add small subtle scattered stars across GitHub profile README for polish, without changing layout or adding dependencies.

## Decisions
- Placement: random-feel across profile (header, dividers, trailing accents)
- Style: subtle unicode only — `✦ ˖ ˚ ⋆ ·`
- Approach: static scatter (approved). No JS (GitHub strips it), no SVG banner, no Action.

## Design
- Architecture: single-file markdown change in `README.md` only.
- Components:
  1. Header suffix on `## Hi, I'm Amir Asyraf` line: add `˖ ˚ ✦`
  2. Section dividers: replace 2-3 `---` with `· ✦ · ─ ─ ─ · ✦ ·` style subtle divider text, or keep `---` and add star line above.
  3. Trailing accents: append 1 sparkle (`˖`, `⋆`, `˚`) to 3-4 existing lines (What I Do bullets, Tech Stack header, Pinned Highlights).
- Data flow: none (static markdown).
- Error handling: ensure unicode renders on GitHub light/dark; keep to common glyphs only.
- Testing: visual check of rendered README, no broken markdown.

## Out of scope
- Animated stars, SVG banner, daily-shuffle Action, layout rework.
