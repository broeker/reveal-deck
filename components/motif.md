---
name: motif
category: component
description: Repeating visual icon system with multiple size/opacity treatments. The icon itself is defined by the theme (emoji, SVG, or image). This component defines how to display it.
---

## Usage

Every theme can define a **motif** — a repeating visual icon that acts as a
brand element across slides. The theme specifies *what* the icon is; this
component defines *how* to display it at different sizes and opacities.

The motif icon is set by the theme. Examples:
- `electric-dark` uses `&#9889;` (lightning bolt)
- A space theme might use `&#128640;` (rocket)
- A corporate theme might use an inline SVG logo

### Treatments

| Class | Purpose | Typical placement |
|-------|---------|-------------------|
| `motif-bg` | Huge ghosted icon, nearly invisible, creates depth | `position:absolute` in a slide corner or center |
| `motif-sm` | Small inline icon | Next to h2 titles |
| `motif-md` | Medium standalone accent | Between content sections |
| `motif-corner` | Medium-opacity icon anchored to a slide corner | `position:absolute` top-right or bottom-right |

### Rules

- Never use the same treatment on consecutive slides — rotate through them
- Alternate accent colors (e.g. `cyan` and `amber`) across slides
- Background motifs use inline `style="color:var(--cyan)"` or `style="color:var(--amber)"`
- Not every slide needs a motif — use on ~60-70% of slides
- The motif should feel like a brand element, not decoration for its own sake

## HTML

Replace `ICON` with the theme's motif icon (emoji entity, inline SVG, or `<img>`).

```html
<!-- Huge ambient background motif -->
<span class="motif-bg" style="position:absolute; top:-40px; right:-20px; color:var(--cyan);">ICON</span>

<!-- Small inline motif next to a heading -->
<h2><span class="motif-sm cyan">ICON</span> Slide Title</h2>

<!-- Medium standalone motif -->
<span class="motif-md cyan">ICON</span>

<!-- Corner motif -->
<span class="motif-corner" style="top:10px; right:30px; color:var(--amber);">ICON</span>
```

### Example: lightning bolt (electric-dark)

```html
<span class="motif-bg" style="position:absolute; top:-40px; right:-20px; color:var(--cyan);">&#9889;</span>
<h2><span class="motif-sm cyan">&#9889;</span> Slide Title</h2>
```

### Example: inline SVG logo

```html
<span class="motif-sm cyan">
  <svg width="1em" height="1em" viewBox="0 0 24 24" fill="currentColor">
    <!-- SVG path data -->
  </svg>
</span>
```

## CSS

```css
.motif-bg {
  position: absolute;
  font-size: 18em;
  opacity: 0.03;
  pointer-events: none;
  user-select: none;
  line-height: 1;
  z-index: 0;
}
.motif-bg.amber { opacity: 0.035; }

.motif-sm {
  font-size: 0.85em;
  opacity: 0.65;
  display: inline-block;
  vertical-align: middle;
}
.motif-sm.cyan  { color: var(--cyan); }
.motif-sm.amber { color: var(--amber); }

.motif-md {
  font-size: 2.2em;
  line-height: 1;
  opacity: 0.45;
  display: block;
}
.motif-md.cyan  { color: var(--cyan); }
.motif-md.amber { color: var(--amber); }

.motif-corner {
  position: absolute;
  font-size: 6em;
  opacity: 0.07;
  pointer-events: none;
  user-select: none;
  line-height: 1;
}
```

## Theme integration

Themes define their motif in a `## Motif` section:

```markdown
## Motif
- **Icon:** `&#9889;` (lightning bolt emoji)
- **Fallback:** none
- **Notes:** Fits the electric/terminal aesthetic. Alternate cyan and amber.
```

During the interview, the user can also override the motif: "use a rocket
instead of the bolt" — just swap the icon entity in the HTML.
