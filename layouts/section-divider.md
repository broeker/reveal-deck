---
name: section-divider
category: layout
description: Large-number section transition slide for major topic breaks.
---

## Usage

Insert between major topic groups to orient the audience. Uses a large section number/label and minimal content.

## HTML

```html
<section data-background-color="#060A12">
  <span class="slide-tag">{NNN}</span>
  <span class="section-label">SECTION</span>
  <h1 style="font-size:3.5em; color:var(--cyan);">Section Title</h1>
  <p style="font-size:0.85em; color:var(--muted); max-width:60%;">
    Brief one-line description of what this section covers.
  </p>
</section>
```

## CSS

```css
.section-label {
  font-family: 'Fira Code', monospace;
  font-size: 0.6em;
  color: var(--muted);
  letter-spacing: 0.2em;
  text-transform: uppercase;
  display: block;
  margin-bottom: 0.75rem;
}
```
