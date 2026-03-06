---
name: bolt-motif
category: component
description: Lightning bolt decorative system with multiple size/opacity treatments. Recurring brand element across slides.
---

## Usage

Use the lightning bolt emoji as a recurring decorative motif. Vary the treatment across slides so it never feels repetitive. Rotate through sizes, positions, and colors.

### Treatments

| Class | Purpose | Typical placement |
|-------|---------|-------------------|
| `bolt-bg` | Huge ghosted bolt, nearly invisible, creates depth | `position:absolute` in a slide corner or center |
| `bolt-sm` | Small inline bolt | Next to h2 titles |
| `bolt-md` | Medium standalone accent | Between content sections |
| `bolt-corner` | Medium-opacity bolt anchored to a slide corner | `position:absolute` top-right or bottom-right |

### Rules

- Never use the same treatment on consecutive slides — rotate through them
- Alternate `cyan` and `amber` coloring
- Background bolts use inline `style="color:var(--cyan)"` or `style="color:var(--amber)"`
- Not every slide needs a bolt — use on ~60-70% of slides

## HTML

```html
<!-- Huge ambient background bolt -->
<span class="bolt-bg" style="position:absolute; top:-40px; right:-20px; color:var(--cyan);">&#9889;</span>

<!-- Small inline bolt next to a heading -->
<h2><span class="bolt-sm cyan">&#9889;</span> Slide Title</h2>

<!-- Medium standalone bolt -->
<span class="bolt-md cyan">&#9889;</span>

<!-- Corner bolt -->
<span class="bolt-corner" style="top:10px; right:30px; color:var(--amber);">&#9889;</span>
```

## CSS

```css
.bolt-bg {
  position: absolute;
  font-size: 18em;
  opacity: 0.03;
  pointer-events: none;
  user-select: none;
  line-height: 1;
  z-index: 0;
}
.bolt-bg.amber { opacity: 0.035; }

.bolt-sm {
  font-size: 0.85em;
  opacity: 0.65;
  display: inline-block;
  vertical-align: middle;
}
.bolt-sm.cyan  { color: var(--cyan); }
.bolt-sm.amber { color: var(--amber); }

.bolt-md {
  font-size: 2.2em;
  line-height: 1;
  opacity: 0.45;
  display: block;
}
.bolt-md.cyan  { color: var(--cyan); }
.bolt-md.amber { color: var(--amber); }

.bolt-corner {
  position: absolute;
  font-size: 6em;
  opacity: 0.07;
  pointer-events: none;
  user-select: none;
  line-height: 1;
}
```
