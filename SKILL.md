---
name: slides
description: >
  Use this skill when building, generating, or iterating on a Reveal.js slide
  deck or presentation. Triggers on requests like "build a slideshow", "create
  a deck", "make a presentation", "turn this into slides", "generate reveal.js",
  "spin up the deck", or "make a deck about X". Also triggers when the user
  provides a notes/outline file and asks to turn it into slides, OR when the
  user describes a topic and wants a deck built from scratch without an outline.
---

# Slides Skill

Builds production-quality Reveal.js slide decks using a library of named
themes, components, and layouts. Supports two entry points: building from a
markdown outline, or generating a deck from scratch given just a topic/prompt.
Always pairs with the `frontend-design` skill for aesthetic direction.

## Workflow

### 1. Determine the entry point

**Path A — From an outline file:**
Look for content files in the current directory:
- `INSTRUCTIONS.md` — project-specific overrides (takes precedence over defaults)
- `*.md` — notes, outlines, or structured content to turn into slides

If no `INSTRUCTIONS.md` exists, auto-generate one from the template at
`templates/INSTRUCTIONS.template.md` in this skill's directory. Fill in what
you can infer from the outline; leave the rest for the interview step.

Proceed to step 2 (Interview).

**Path B — From a prompt (no outline):**
The user describes a topic, audience, or goal but has no written outline.

1. Ask a short interview (step 2) to clarify scope, audience, tone, and theme
2. Generate a proposed outline in markdown — slide titles with brief content
   notes for each, organized into logical sections
3. Present the outline to the user for approval. They may:
   - Approve as-is — proceed to build
   - Edit/rearrange — incorporate changes, then proceed
   - Add detail to specific slides — incorporate, then proceed
4. Save the approved outline as `OUTLINE.md` in the deck directory for reference
5. Proceed to build (step 3 onward) using the approved outline as source material

### 2. Interview (before building)

After reading the outline (Path A) or hearing the topic (Path B), ask a short
round of targeted questions (3-5 max). Only ask what you actually need — skip
anything already clear.

Good questions:
- Audience and their familiarity with the topic?
- Preferred theme? (default: `electric-dark`)
- Approximate scope — how many slides / how long? (or let Claude decide)
- Any specific points, examples, or stories to include?
- Any slides needing special treatment (heavy visuals, specific layout)?
- Tone — technical deep-dive, casual overview, persuasive pitch?
- Anything in the notes that's unclear or seems incomplete? (Path A only)

Propose a title and subtitle inferred from the outline or prompt. Let the user
confirm or override.

### 3. Load the theme

Read the selected theme file from `themes/` in this skill's directory.
Default to `electric-dark` if none specified. The theme defines:
- CSS custom properties (colors)
- Font imports
- Base styles (background, typography, links, lists)
- Background treatment
- Recommended components

### 4. Load components and layouts

Read only the component and layout files you'll actually use. Don't load
everything — read them from `components/` and `layouts/` as needed based
on the content.

Every piece is referenced by its kebab-case name:

**Components:** `panel`, `codeblock`, `callout`, `comparison`, `flow`,
`step-list`, `file-tree`, `table`, `badge`, `bolt-motif`, `filepath`,
`key-item`, `resource-list`

**Layouts:** `title-slide`, `section-divider`, `content-slide`, `code-slide`,
`comparison-slide`, `resources-slide`

### 5. Content strategy

**Condensing rules — use your judgment on each slide:**
- **Too long for one slide?** Tighten the language first. If still too dense,
  break it across 2-3 slides. Don't lose key information — condense, don't cut.
- **Too sparse?** Flesh it out with relevant detail. Don't pad — add substance.
- **Topic breaks** — when the subject shifts, insert a `section-divider` layout.
- **Missing topics** — if there's an obvious gap the outline should cover, add
  a slide for it. Flag these with a speaker note: `<!-- ADDED: not in outline -->`
- **Display choices** — pick the right component for the content. Don't default
  to bullet lists when a visual component would be stronger:
  - Bullet lists for sequences and simple enumerations
  - `panel` for grouped concepts
  - `callout` for key takeaways
  - `codeblock` for commands/syntax
  - `comparison` for before/after or good/bad
  - `flow` for processes and lifecycles
  - `step-list` for ordered procedures
  - `key-item` for numbered takeaways
  - `file-tree` for directory structures
  - `table` for reference data
- **External resources** — include links where they add value.
- **Graphics** — use inline SVG for diagrams, charts, or visuals. Don't force
  visuals where text is clearer.

**Slide types:**
- **Title slide** — always first, uses `title-slide` layout
- **Section divider** — for major topic transitions, uses `section-divider` layout
- **Content slide** — the workhorse, uses `content-slide` layout (2-col preferred)
- **Code slide** — uses `code-slide` layout
- **Comparison slide** — uses `comparison-slide` layout
- **Resources slide** — uses `resources-slide` layout

**Slug numbering — `{NNN}` format:**
Every content slide (excluding the title slide) gets a zero-padded sequential
slug: `{001}`, `{002}`, etc. Use as the `slide-tag` content and `data-id`.
If source content has pre-assigned slugs, honor them.

### 6. HTML output

Generate a single self-contained `index.html`. Use Reveal.js from CDN:

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reveal.js@5.1.0/dist/reveal.css">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reveal.js@5.1.0/dist/theme/black.css">
<script src="https://cdn.jsdelivr.net/npm/reveal.js@5.1.0/dist/reveal.js"></script>
<script src="https://cdn.jsdelivr.net/npm/reveal.js@5.1.0/plugin/notes/notes.js"></script>
<script src="https://cdn.jsdelivr.net/npm/reveal.js@5.1.0/plugin/highlight/highlight.js"></script>
```

**Reveal.js init:**
```js
Reveal.initialize({
  hash: true,
  slideNumber: 'c/t',
  progress: true,
  transition: 'fade',
  transitionSpeed: 'fast',
  backgroundTransition: 'fade',
  center: false,
  width: 1280,
  height: 720,
  margin: 0.04,
  plugins: [ RevealNotes, RevealHighlight ]
});
```

Combine all CSS from the theme + used components + used layouts into a single
`<style>` block in `<head>`. The output must be fully self-contained.

### 7. Title slide auto-calculation

After generating all slides, update the title slide with:
- **Slide count** — total content slides (excluding title)
- **Estimated duration** — based on slide complexity:
  - Section dividers: ~30 seconds
  - Standard content slides: ~1 minute
  - Dense slides (code, comparisons, diagrams): ~1.5 minutes
- Display as: `15 slides` / `~18 min`

Recalculate after every editing pass.

### 8. Serving and previewing

When the user says "spin it up" or asks to preview:

```bash
cd /path/to/deck && python3 -m http.server 8765 &
```

Confirm with `curl -s -o /dev/null -w "%{http_code}" http://localhost:8765/`
and report: **http://localhost:8765**

### 9. Iteration

After the first draft, expect iteration. Common requests:
- **"Tighten {003}"** — reduce text, increase visual contrast
- **"Split {007}"** — duplicate section structure, split content
- **"Drop {011}"** — remove the slide, renumber subsequent slugs
- **"Add a section divider before {005}"** — insert and renumber
- **"Switch the flow on {007} to a step-list"** — swap component
- **"Change the theme"** — update CSS variables and fonts; layout stays
- **"Add speaker notes"** — `<aside class="notes">` inside each section
- **"Make it more visual"** — replace bullet lists with panel grids or flow diagrams

When iterating, use `Edit` (not `Write`) to make targeted changes to `index.html`.
Always recalculate title slide stats after changes.

## Adding new components

To add a new component to this toolkit:
1. Create a `.md` file in `components/` following the standard format (YAML frontmatter with `name`, `category`, `description` + Usage + HTML + CSS sections)
2. Use a unique kebab-case name
3. Commit and push — it's immediately available for future decks

Same process for new layouts (`layouts/`) and themes (`themes/`).
