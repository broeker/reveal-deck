---
name: comparison
category: component
description: Side-by-side good/bad panels and verdict-style comparison grids. Use for before/after, with/without, or pros/cons.
---

## Usage

Two styles available: **box comparison** (two panels side by side) and **verdict grid** (label + description rows).

### Box comparison

```html
<div class="cols-2">
  <div class="compare bad">
    <span class="label bad">WITHOUT</span>
    <p>Description of the bad state.</p>
  </div>
  <div class="compare good">
    <span class="label good">WITH</span>
    <p>Description of the good state.</p>
  </div>
</div>
```

### Verdict grid

```html
<div class="compare-grid">
  <span class="verdict bad">AVOID</span>
  <span class="compare-text">Description of what to avoid</span>
  <span class="verdict good">PREFER</span>
  <span class="compare-text">Description of what to prefer</span>
</div>
```

## CSS

```css
.compare {
  background: var(--panel);
  border: 1px solid var(--border);
  border-radius: 6px;
  padding: 0.7rem 1rem;
  height: 100%;
  box-sizing: border-box;
}
.compare.bad  { border-left: 3px solid var(--red); }
.compare.good { border-left: 3px solid var(--cyan); }

.label {
  font-family: 'Fira Code', monospace;
  font-size: 0.58em;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  margin-bottom: 0.65rem;
  display: block;
}
.label.bad  { color: var(--red); }
.label.good { color: var(--cyan); }

.compare-grid {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 0.55em 1.2em;
  align-items: center;
}
.verdict {
  font-family: 'Fira Code', monospace;
  font-size: 0.6em;
  font-weight: 500;
  padding: 0.25em 0.5em;
  border-radius: 3px;
  white-space: nowrap;
  text-align: center;
  margin-top: 0.1em;
}
.verdict.bad  { background: rgba(255,80,80,0.12); color: var(--red); border: 1px solid rgba(255,80,80,0.2); }
.verdict.good { background: rgba(170,255,0,0.1);  color: var(--cyan); border: 1px solid var(--border); }
.compare-text {
  font-family: 'Source Serif 4', serif;
  font-size: 0.78em;
  color: var(--text);
  line-height: 1.5;
}
.compare-text em { color: var(--muted); font-style: italic; }
```
