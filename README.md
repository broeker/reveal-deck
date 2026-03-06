# reveal-deck

A Claude Code skill for building production-quality Reveal.js slide decks. Works two ways: from a markdown outline, or from scratch given just a topic. Ships with a named theme, component library, and layout system so you can reference specific pieces by name.

## Install

```
/install-skill https://github.com/broeker/reveal-deck
```

This symlinks the skill into `~/.claude/skills/`. The slash command is `/slides`.

## Quick start

### Option A — From a markdown outline

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

Claude reads your outline, asks 3-5 quick questions, then generates a complete `index.html` in one pass.

### Option B — From a prompt (no outline)

```bash
mkdir ~/decks/my-talk && cd ~/decks/my-talk
```

Just describe what you want:

```
Build a deck about Git rebasing best practices for a team of junior devs
```

Claude will interview you (audience, tone, scope), then generate a proposed outline for your approval. Once you sign off, it builds the full deck. The outline is saved as `OUTLINE.md` for reference.

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
| `motif` | Repeating visual icon system — icon defined by theme (bolt, rocket, logo, etc.) |
| `filepath` | Inline path badge (amber/green variants) |
| `key-item` | Numbered takeaway list with large accent numbers |
| `resource-list` | Categorized link list for references slides |
| `effects` | Reveal.js advanced features — fragments, auto-animate, backgrounds, transitions |

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
| `basement-slide` | Vertical (down) slides for deeper dives beneath a main slide |

## Effects and advanced features

Reveal.js has powerful features beyond static slides. Some are used automatically; others are available on request.

### Automatic (Claude decides)

These are applied where they clearly help — you don't need to ask:

| Effect | What it does | When Claude uses it |
|--------|-------------|---------------------|
| **Fragments** | Reveals list items one at a time on click | Dense slides with 5+ bullets |
| **Auto-animate** | Smooth morph between two related slides | Slides that build on each other (growing code, expanding lists) |
| **r-fit-text** | Auto-scales text to fill slide width | Section dividers and single-phrase impact slides |

### On request

Ask for these in your outline notes or during iteration:

| Effect | How to request | Example |
|--------|---------------|---------|
| **Image background** | "fullscreen image on {005}" | Full-bleed photo behind slide content |
| **GIF background** | "fullscreen gif on {007}" | Animated GIF as slide background |
| **Video background** | "video background on {003}" | Auto-playing muted video behind content |
| **iframe background** | "embed this URL as an iframe on {010}" | Live webpage as the slide |
| **Parallax** | "add parallax scrolling" | Subtle depth effect as slides change (global) |
| **Transition override** | "zoom into {008}" or "hard cut to {012}" | Per-slide transition style |
| **Background transition** | "zoom the background on {006}" | Animate just the background independently |

**Transitions available:** `fade` (default), `slide`, `convex`, `concave`, `zoom`, `none`

**Fragment styles available:** `fade-in` (default), `fade-up`, `fade-down`, `fade-left`, `fade-right`, `highlight-current-blue`, `semi-fade-out`

You can also note these inline in your outline:

```markdown
## The Big Reveal

[fullscreen gif: https://example.com/mind-blown.gif]

This changes everything.

## Live Demo

[iframe: https://my-app.example.com]
```

For the full list of Reveal.js features, see the [official demo](https://revealjs.com/) and [documentation](https://revealjs.com/markup/).

## Tips for good results

### Write a good outline

- **One `##` heading per slide idea** — Claude will split or merge as needed
- **Use `###` for deeper dives** — sub-headings become basement (vertical) slides below their parent
- **Include raw notes** — don't worry about length; too much is better than too little
- **Note special requests inline** — "show this as a comparison", "include a diagram here"
- **Mark what matters** — bold or emphasize key points you don't want lost in condensing

```markdown
## Main Topic              <-- horizontal slide
Core points here.

### Detailed Example        <-- basement slide (navigate down)
Extended walkthrough...

### Reference Commands      <-- second basement slide
More detail...

## Next Topic              <-- back to horizontal flow
```

Claude will also create basement slides on its own when content warrants a deeper dive but would slow the main flow. Basement slides use letter suffixes: `{003a}`, `{003b}`.

### During the interview

- **Be specific about audience** — "developers who know Git but not CI/CD" is better than "technical audience"
- **State the tone** — casual team talk vs. conference presentation changes how Claude writes
- **Flag tricky slides** — if you know slide 5 is too long, say so up front

### During iteration

- **Use slugs** — `{003}` is faster and more precise than "the third slide"
- **Be direct** — "tighten {003}" works better than "can you maybe make slide 3 a bit shorter?"
- **Request component swaps** — "switch {007} from bullets to a `flow` diagram"
- **Ask for additions** — "add a `callout` to {004} with the key takeaway"
- **Request effects** — "fullscreen gif on {005}", "auto-animate {003} to {004}", "add fragments to {006}", "embed this URL as an iframe on {010}"
- **Move slides vertically** — "move {005} to a basement slide under {004}" or "promote {004a} to the main flow"

### Previewing

Say "spin it up" and Claude will start a local server at `http://localhost:8765`.

## Decks are standalone

Once generated, a deck is a self-contained `index.html` that doesn't depend on this toolkit at runtime. New components added to the toolkit won't affect existing decks — they're only available for future builds.

## License

MIT
