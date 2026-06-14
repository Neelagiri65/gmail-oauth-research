# HANDOFF — gmail-oauth-research

**Last updated:** 2026-06-14
**State:** clean working tree, on `main`. Single commit (`efba1f6` — initial research report).
**Remote:** github.com/Neelagiri65/gmail-oauth-research · published via GitHub Pages → https://neelagiri65.github.io/gmail-oauth-research/

## What this is
A code-pattern audit across 2M+ public repos (Sourcegraph) finding **124 open-source projects that key Google OAuth on the `email` claim instead of the stable `sub` claim** — i.e. accounts break / get hijacked when a user renames their Gmail. Static report site (`index.html`, `og-image.svg`, `README.md`).

## Current state
- Research complete and published. No build step — plain static site.
- Sibling product: `authdrift` (the tool that detects this pattern) — keep the two cross-linked.

## NEXT
- No active task — this is a finished, published artifact (baseline HANDOFF).
- If revisiting: re-run the Sourcegraph audit to refresh the 124-repo count; expand the severity/methodology tables; ensure the report links to `authdrift` (the productised detector) and vice-versa.
