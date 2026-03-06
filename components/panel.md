---
name: panel
category: component
description: Bordered card with optional color accent and label. Use for grouping related content.
---

## Usage

Use panels to group related content into visual cards. Supports color-coded left borders and an optional label header. Works well in 2-col and 3-col layouts.

## HTML

```html
<div class="panel panel-cyan">
  <div class="panel-label" style="color:var(--cyan)">LABEL TEXT</div>
  <p>Panel content goes here.</p>
</div>
```

**Variants:**
```html
<div class="panel panel-cyan">...</div>   <!-- lime/green left border -->
<div class="panel panel-amber">...</div>  <!-- amber left border -->
<div class="panel panel-red">...</div>    <!-- red left border -->
<div class="panel">...</div>              <!-- no colored border -->
```

## CSS

```css
.panel {
  background: var(--panel);
  border: 1px solid var(--border);
  border-radius: 6px;
  padding: 0.7rem 1rem;
}

.panel-cyan  { border-left: 3px solid var(--cyan); }
.panel-amber { border-left: 3px solid var(--amber); }
.panel-red   { border-left: 3px solid var(--red); }

.panel-label {
  font-family: 'Fira Code', monospace;
  font-size: 0.58em;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  padding-bottom: 0.35rem;
  margin-bottom: 0.35rem;
  border-bottom: 1px solid var(--border);
}
```
