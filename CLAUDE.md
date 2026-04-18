# zabrain — Shared second brain

Shared knowledge base maintained by **Zaid** and **Anas** via a Telegram bot. Every raw entry is authored by one of us; the LLM organizes, clusters, and synthesizes over time.

## Structure

- `raw/` — one file per dump, with author in frontmatter. Immutable.
- `wiki/sources/` — one summary per raw file.
- `wiki/clusters/` — emergent groupings of related thoughts (2+ items).
- `wiki/themes/` — concepts that recur across 3+ sources.
- `index.md` — content catalog, updated on every ingest.
- `log.md` — chronological append-only record.

## Ownership

- **Users write**: raw only, via Telegram `/c <thought>`.
- **LLM writes**: everything in `wiki/`, plus `index.md` and `log.md`.
- Never modify raw files. Quote verbatim when citing.

## Conventions

**File names:** kebab-case, lowercase (e.g. `attention-as-currency.md`).

**Links:** Obsidian wikilinks, e.g. `[[clusters/attention]]`.

**Raw frontmatter:**
```yaml
---
author: zaid | anas
date: YYYY-MM-DD
---
```

**Wiki page frontmatter:**
```yaml
---
type: source-summary | cluster | theme
created: YYYY-MM-DD
updated: YYYY-MM-DD
authors: [zaid, anas]   # whoever contributed sources under this page
---
```

## Query behavior (for the Telegram bot)

1. Read CLAUDE.md + `index.md` first.
2. Drill into wiki pages as needed.
3. Cite with `[[wiki-path]]` wikilinks.
4. Respect both authors' voices — quote verbatim when the phrasing matters. Don't average them together.

## Ingest behavior (for the Telegram bot)

When handling a capture:
- Write to `raw/{date}-{slug}.md` with `author:` in frontmatter.
- Commit + push.
- Do NOT auto-create wiki pages from single captures. Wiki creation happens separately (future distiller / manual desktop ingest).

## Tone

Both authors have distinct voices. Preserve them. The wiki should feel like *their shared thinking organized*, not a single homogenized voice.
