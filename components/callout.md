---
name: callout
category: component
description: Highlighted box for key takeaways, tips, or important notes.
---

## Usage

Use callouts to draw attention to a key point, takeaway, or rule of thumb. Available in accent (default) and amber variants.

## HTML

```html
<div class="callout">
  Key takeaway or important note here.
</div>

<div class="callout callout-amber">
  Warning or secondary emphasis here.
</div>
```

## CSS

```css
.callout {
  background: rgba(170,255,0,0.05);
  border: 1px solid rgba(170,255,0,0.25);
  border-radius: 5px;
  padding: 0.5rem 0.8rem;
  font-family: 'Source Serif 4', serif;
  font-size: 0.82em;
  color: var(--text);
  margin-top: 0.6rem;
}

.callout-amber {
  background: rgba(255,176,32,0.06);
  border-color: rgba(255,176,32,0.3);
}
```
