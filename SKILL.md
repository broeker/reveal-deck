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

**Design dependency:** This skill works best with the `frontend-design` skill
installed, which helps Claude make stronger visual decisions when customizing
themes, choosing colors, or handling ad hoc design requests. However, the
skill is fully self-contained — the theme files and component CSS provide all
the design guidance needed for standard builds. If the user asks for significant
design customization and `frontend-design` is not available, note that
installing it would improve results:
`/install-skill https://github.com/anthropics/skills frontend-design`

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
- **Target length and depth** — this shapes everything:
  - Lightning talk (5-10 min) → tight, punchy, 8-12 slides, no basement slides
  - Standard talk (15-25 min) → balanced depth, 15-25 slides, selective basements
  - Deep dive (30-60 min) → comprehensive, 25-40+ slides, basements for extras
  - If the user doesn't have a preference, estimate from the outline length
    (Path A) or topic breadth (Path B) and propose a target
- Any specific points, examples, or stories to include?
- Any slides needing special treatment (heavy visuals, specific layout)?
- Tone — technical deep-dive, casual overview, persuasive pitch?
- Anything in the notes that's unclear or seems incomplete? (Path A only)
- Content voice (Path A only) — see below

**Content voice — how closely to preserve the user's language:**

During the interview for Path A, gauge how polished the outline is and ask
the user where they fall on this spectrum:

- **Preserve** — the outline contains carefully crafted language. Keep the
  user's exact wording on slides wherever possible. Only restructure for
  slide fit (line breaks, bullet formatting). Tighten for space but don't
  rephrase. Speaker notes can use Claude's voice.
- **Refine** (default) — the outline has good ideas but rough language.
  Improve clarity, tighten phrasing, and punch up key points while keeping
  the user's intent and terminology. Don't over-polish into generic
  corporate tone — match the user's voice, just sharpen it.
- **Transform** — the outline is raw notes, brain dumps, or stream of
  consciousness. Claude has full license to rewrite, restructure, and
  craft the slide language from scratch. Preserve the ideas and key terms,
  but the words are Claude's.

If the outline is clearly one extreme (polished prose vs. messy bullets),
propose the appropriate mode and confirm. If ambiguous, ask. Default to
**Refine** if the user doesn't have a preference.

This applies to slide content only — speaker notes always use Claude's voice
since they're not displayed to the audience.

Propose a title and subtitle inferred from the outline or prompt. Let the user
confirm or override.

**Content analysis (Path A only):**
After reading the outline, briefly note any obvious gaps or suggestions:
- Topics the audience would likely expect but aren't covered
- A missing introduction, summary, or closing slide
- Opportunities for a comparison, demo, or example that would strengthen a point
- Sections that feel out of order or could flow better rearranged
- Content that might work better as a basement slide than in the main flow

Keep this to 2-4 concrete suggestions, not a laundry list. Frame them as
proposals ("You might want to add a slide on X" / "Consider moving Y before Z")
and let the user accept, reject, or modify. Don't hold up the build — include
accepted suggestions in the first draft.

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
`step-list`, `file-tree`, `table`, `badge`, `motif`, `filepath`,
`key-item`, `resource-list`, `effects`, `stat-highlight`, `quote`,
`agenda`, `timeline`, `icon-grid`, `terminal-embed`

**Layouts:** `title-slide`, `section-divider`, `content-slide`, `code-slide`,
`comparison-slide`, `resources-slide`, `basement-slide`, `split-slide`,
`closing-slide`

### 5. Content strategy

**Condensing rules — use your judgment on each slide:**
- **Too long for one slide?** Tighten the language first. If still too dense,
  either break it across 2-3 horizontal slides, or move the deep-dive portion
  to a `basement-slide` below the main slide. Use basement slides when the
  detail is supporting/optional rather than essential to the main flow.
- **Too sparse?** Flesh it out with relevant detail. Don't pad — add substance.
- **Topic breaks** — when the subject shifts, insert a `section-divider` layout.
- **Missing topics** — if there's an obvious gap the outline should cover, add
  a slide for it. Flag these with a speaker note: `<!-- ADDED: not in outline -->`
- **Basement slides** — in the outline, `###` sub-headings under a `##` become
  vertical (basement) slides. Claude should also create basement slides on its
  own when content warrants a deeper dive but would slow the main horizontal
  flow — examples, walkthroughs, reference lists, optional detail. See the
  `basement-slide` layout for structure and slug conventions (`{003a}`, `{003b}`).
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
  - `stat-highlight` for impactful numbers and metrics
  - `quote` for pull quotes and testimonials (slide-level, not inline)
  - `agenda` for table of contents (auto-generate from section dividers)
  - `timeline` for roadmaps and chronological progressions
  - `icon-grid` for feature overviews and capability grids
- **External resources** — include links where they add value.
- **Graphics** — use inline SVG for diagrams, charts, or visuals. Don't force
  visuals where text is clearer.
- **Effects** — read the `effects` component for Reveal.js advanced features.
  Auto-use fragments on dense lists, auto-animate between related slides,
  and r-fit-text on section dividers. All other effects (background images,
  GIFs, video, iframes, parallax, per-slide transitions) are on-request only
  — use them when the user asks or notes them in the outline.
- **Motif placement (mandatory)** — the theme's motif icon is a structural
  element, not optional decoration. On every content slide:
  1. Add a `motif-bg` (huge ghosted icon) with `position:absolute` in a corner
     or centered. Vary the position slide-to-slide (top-right, bottom-left,
     center, mid-right, etc.) so it feels dynamic.
  2. Alternate motif color between `var(--cyan)` and `var(--amber)` across
     consecutive slides.
  3. On ~40-50% of slides, also add a `motif-sm` inline with the `<h2>` heading.
  4. On ~20-30% of slides, add a `motif-corner` for extra presence.
  5. Never stack more than 2 motif treatments per slide (bg + one other).
  The motif should feel omnipresent — like a watermark or brand signature that
  ties every slide together. See the `motif` component for CSS and HTML.

**Slide types:**
- **Title slide** — always first, uses `title-slide` layout
- **Section divider** — for major topic transitions, uses `section-divider` layout
- **Content slide** — the workhorse, uses `content-slide` layout (2-col preferred)
- **Code slide** — uses `code-slide` layout
- **Comparison slide** — uses `comparison-slide` layout
- **Resources slide** — uses `resources-slide` layout
- **Split slide** — uses `split-slide` layout (50/50 visual + content)
- **Closing slide** — uses `closing-slide` layout (CTA, contact, QR code)
- **Terminal slide** (advanced, on-request only) — live interactive terminal
  via ttyd. **Never add unless the user explicitly asks.** When adding one,
  include a speaker note: `<!-- REQUIRES: ttyd -W -p 7681 bash & -->` and
  warn the user that ttyd must be installed and running before presenting.
  See the `terminal-embed` component for setup details.

**Speaker notes — generate automatically on every content slide:**
Speaker notes go in `<aside class="notes">` inside each `<section>`. They should
**add context the slide doesn't show** — not repeat what's already on screen.

Good speaker notes include:
- The "why" behind a bullet point (the slide says what, you explain why)
- A short anecdote, example, or analogy to make the point land
- Transition cues — how to bridge to the next slide
- Stats or details too granular for the slide but useful when speaking
- Anticipated audience questions and how to address them
- Timing hints on dense slides ("spend extra time here")

Bad speaker notes:
- Restating the slide content verbatim
- Generic filler ("talk about this topic")
- Full scripts — these are prompts, not a teleprompter

Keep each note to 2-4 short sentences. The presenter should glance, not read.

**Slug numbering — `{NNN}` format:**
Every content slide (excluding the title slide) gets a zero-padded sequential
slug: `{001}`, `{002}`, etc. Use as the `slide-tag` content and `data-id`.
Basement slides append a letter to their parent: `{003a}`, `{003b}`, etc.
If source content has pre-assigned slugs, honor them.

### 6. Slide overflow prevention

The viewport is 1280x720 with 0.04 margin. Every slide must fit without
scrolling or bleeding off-screen. Apply these content budgets:

**Maximum content per slide (approximate):**
- **Bullet points:** 5-7 items max (single column), 4-5 per column (two-col)
- **Body text:** 4-5 short paragraphs or 2-3 longer ones
- **Code blocks:** 10-12 lines max at 0.62em
- **Panels in cols-2:** 2 panels with 3-4 bullets each
- **Panels in cols-3:** 3 panels with 2-3 bullets each
- **Flow steps:** 5-6 max before wrapping becomes a problem
- **Step-list items:** 4-5 max
- **Table rows:** 5-7 rows max
- **Stats in cols-3:** 3 stats (number + label + optional context)
- **Key-items:** 3-4 max
- **Timeline items:** 4-5 max

**Red flags — if you see these, the slide is likely overflowing:**
- More than 7 bullet points on a single slide
- Two panels each with 5+ bullets
- A code block over 12 lines
- Body text with more than 3 paragraphs plus additional components
- Nested lists (almost always too dense)
- Any combination of h2 + subtitle text + full cols-2 + callout
- `r-fit-text` on titles longer than 3-4 words (use fixed `font-size` instead)
- Flow diagrams with 5+ steps without `flex-wrap: wrap`

**What to do when content exceeds budget:**
1. First: tighten the language — can you say it in fewer words?
2. Second: split into two horizontal slides
3. Third: move the overflow to a basement slide
4. Fourth: switch to a more compact component (bullets → icon-grid, step-list → flow)

**After generating each slide, do a quick mental check:** count the elements,
estimate vertical space, and split proactively. It's better to have one extra
slide than one that bleeds off-screen.

### 7. HTML output


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

**Always include these overflow prevention rules in the base CSS:**
```css
.reveal section {
  padding: 0.5rem 3.5rem 1rem;
  box-sizing: border-box;
  overflow: hidden;
  max-width: 100%;
}
.reveal section h1, .reveal section h2 {
  word-wrap: break-word;
  overflow-wrap: break-word;
}
.reveal .slides section > * { max-width: 100%; }
```

### 8. Title slide auto-calculation

After generating all slides, update the title slide with:
- **Slide count** — total content slides (excluding title)
- **Estimated duration** — based on slide complexity:
  - Section dividers: ~30 seconds
  - Standard content slides: ~1 minute
  - Dense slides (code, comparisons, diagrams): ~1.5 minutes
- Display as: `15 slides` / `~18 min`

Recalculate after every editing pass.

### 9. Serve script

After generating `index.html`, copy the launch script into the deck directory:

```bash
cp /path/to/skill/templates/serve.sh /path/to/deck/serve.sh
chmod +x /path/to/deck/serve.sh
```

This script handles:
- Starting a local server (`python3 -m http.server`)
- Checking if the port is available
- Detecting terminal-embed slides and warning if ttyd isn't running
- Cross-platform (Linux and macOS)

When the user says "spin it up" or asks to preview:

```bash
cd /path/to/deck && ./serve.sh &
```

Confirm with `curl -s -o /dev/null -w "%{http_code}" http://localhost:8765/`
and report: **http://localhost:8765**

If the user runs it themselves, the script provides all the guidance needed.

### 10. Iteration

After the first draft, expect iteration. Common requests:
- **"Tighten {003}"** — reduce text, increase visual contrast
- **"Split {007}"** — duplicate section structure, split content
- **"Drop {011}"** — remove the slide, renumber subsequent slugs
- **"Move {005} to a basement slide under {004}"** — convert to vertical slide
- **"Promote {004a} to the main flow"** — move basement slide to horizontal
- **"Add a section divider before {005}"** — insert and renumber
- **"Switch the flow on {007} to a step-list"** — swap component
- **"Change the theme"** — update CSS variables and fonts; layout stays
- **"Improve notes on {003}"** — richer speaker notes for a specific slide
- **"Make it more visual"** — replace bullet lists with panel grids or flow diagrams
- **"Fullscreen gif on {005}"** — apply GIF background (see `effects` component)
- **"Embed this URL as an iframe on {010}"** — iframe background
- **"Auto-animate {003} to {004}"** — smooth morph between related slides
- **"Add fragments to {006}"** — progressive reveal on list items

When iterating, use `Edit` (not `Write`) to make targeted changes to `index.html`.
After every editing pass:
- **Renumber all slugs** — keep `{NNN}` sequential with no gaps. If you drop
  `{004}`, what was `{005}` becomes `{004}`, etc. Basement suffixes follow
  their parent: if `{004}` moves to `{003}`, then `{004a}` becomes `{003a}`.
- **Recalculate title slide stats** — update slide count and estimated duration.

### 11. Markdown export

When the user asks to "export as markdown", "give me a markdown version", or
"convert this deck to markdown", generate a clean `.md` file from the finished
`index.html`:

**Structure:**
```markdown
# Deck Title
*Subtitle — Presenter, Date*
*15 slides / ~18 min*

---

## {001} Slide Title

Slide content converted to clean markdown — bullet lists, bold, inline code,
links all preserved. Component-specific markup (panels, callouts, etc.)
converted to the closest markdown equivalent:

- `panel` → blockquote or indented section with bold label
- `callout` → blockquote prefixed with **Key takeaway:**
- `codeblock` → fenced code block
- `comparison` → two blockquotes labeled **Without:** / **With:**
- `flow` → inline: Step 1 → Step 2 → Step 3
- `step-list` → numbered list
- `file-tree` → fenced code block
- `table` → markdown table
- `stat-highlight` → **87%** — label text
- `quote` → blockquote with attribution
- `timeline` → table or list with dates
- `icon-grid` → bullet list with bold labels

> **Speaker notes:** The note content goes here, separated from slide
> content so the reader gets the extra context.

---

## {002} Next Slide Title
...
```

**Rules:**
- Speaker notes are included as blockquotes at the end of each slide section
- Section dividers become `---` with a `## Section Title` heading
- Basement slides are indented under their parent (use `###` headings)
- Links are preserved as markdown links
- SVG graphics and decorative elements (motifs, accent lines) are omitted
- Save as `DECK-TITLE.md` in the deck directory (kebab-case filename)

## Adding new components

To add a new component to this toolkit:
1. Create a `.md` file in `components/` following the standard format (YAML frontmatter with `name`, `category`, `description` + Usage + HTML + CSS sections)
2. Use a unique kebab-case name
3. Commit and push — it's immediately available for future decks

Same process for new layouts (`layouts/`) and themes (`themes/`).
