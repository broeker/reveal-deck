# reveal-deck

A Claude Code skill for building production-quality Reveal.js slide decks from markdown outlines. Ships with a named theme, component library, and layout system so you can reference specific pieces by name.

## Install

```
/install-skill https://github.com/broeker/reveal-deck
```

This symlinks the skill into `~/.claude/skills/`. The slash command is `/slides`.

## Quick start

```bash
mkdir ~/decks/my-talk && cd ~/decks/my-talk
```

Write your outline in markdown — one heading per slide, raw notes underneath:

```markdown
## What Is the Thing

A **thing** is a concept that does X. It matters because Y.

Key points:
- Point one
- Point two
- Point three with a lot of detail that might need to be trimmed or
  broken across multiple slides depending on density

## Why It Matters

Without the thing, you lose Z. With it, you gain A and B.
This is a comparison — show it side by side.

## How to Set It Up

Step 1: do this
Step 2: do that
Step 3: verify
```

Then tell Claude:

```
Build a deck from my-outline.md
```

Claude will read your outline, ask 3-5 quick questions (audience, tone, theme), then generate a complete `index.html` in one pass.

## What you get

- A single self-contained `index.html` — no external dependencies beyond CDN links
- Auto-calculated slide count and estimated duration on the title slide
- Section dividers inserted at topic breaks
- Components chosen to match content (code blocks, comparison panels, flow diagrams, etc.)
- Additional slides added where Claude spots gaps — flagged with speaker notes

## Iterating

Reference slides by their `{NNN}` slug:

```
tighten {003}
split {007} into two slides
drop {011}
add a section divider before {005}
switch the flow diagram on {007} to a step-list
```

## Themes

Themes define colors, fonts, backgrounds, and recommended components. Currently ships with:

| Theme | Description |
|-------|-------------|
| `electric-dark` | Dark background, neon lime/amber accents, dot-grid texture, terminal aesthetic (default) |

Specify a theme in your INSTRUCTIONS.md or during the interview. If you don't specify, `electric-dark` is used.

### Creating a new theme

Add a `.md` file to `themes/` with:
- YAML frontmatter: `name`, `category: theme`, `description`
- Font imports and family names
- CSS custom properties (must define `--dark`, `--panel`, `--accent`, `--amber`, `--text`, `--muted`, `--border`)
- Base styles, background treatment
- Recommended components list

## Components

Named, reusable UI elements. Reference by name when talking to Claude.

| Component | Description |
|-----------|-------------|
| `panel` | Bordered card with color accent and optional label |
| `codeblock` | Terminal-style code block with faux macOS dots |
| `callout` | Highlighted box for key takeaways |
| `comparison` | Side-by-side good/bad panels and verdict grids |
| `flow` | Horizontal process/lifecycle diagram |
| `step-list` | Numbered step list with circled numbers |
| `file-tree` | Monospace directory tree |
| `table` | Styled data table with accent headers |
| `badge` | Small pill label (status indicators) |
| `bolt-motif` | Lightning bolt decorative system (multiple treatments) |
| `filepath` | Inline path badge (amber/green variants) |
| `key-item` | Numbered takeaway list with large accent numbers |
| `resource-list` | Categorized link list for references slides |

### Adding a new component

Create a `.md` file in `components/` with:

```yaml
---
name: my-component
category: component
description: What it does and when to use it.
---
```

Then add `## Usage`, `## HTML`, and `## CSS` sections. Commit and push — it's immediately available for future decks.

## Layouts

Slide-level patterns that combine components into complete slide structures.

| Layout | Description |
|--------|-------------|
| `title-slide` | Opening slide with title, meta, auto-calculated stats |
| `section-divider` | Large-text transition between major topics |
| `content-slide` | Standard workhorse (2-column preferred) |
| `code-slide` | Full-width code-focused slide |
| `comparison-slide` | Side-by-side comparison layout |
| `resources-slide` | Categorized links for references/further reading |

## Tips for good results

### Write a good outline

- **One heading per slide idea** — Claude will split or merge as needed
- **Include raw notes** — don't worry about length; too much is better than too little
- **Note special requests inline** — "show this as a comparison", "include a diagram here"
- **Mark what matters** — bold or emphasize key points you don't want lost in condensing

### During the interview

- **Be specific about audience** — "developers who know Git but not CI/CD" is better than "technical audience"
- **State the tone** — casual team talk vs. conference presentation changes how Claude writes
- **Flag tricky slides** — if you know slide 5 is too long, say so up front

### During iteration

- **Use slugs** — `{003}` is faster and more precise than "the third slide"
- **Be direct** — "tighten {003}" works better than "can you maybe make slide 3 a bit shorter?"
- **Request component swaps** — "switch {007} from bullets to a `flow` diagram"
- **Ask for additions** — "add a `callout` to {004} with the key takeaway"

### Previewing

Say "spin it up" and Claude will start a local server at `http://localhost:8765`.

## Decks are standalone

Once generated, a deck is a self-contained `index.html` that doesn't depend on this toolkit at runtime. New components added to the toolkit won't affect existing decks — they're only available for future builds.

## License

MIT
