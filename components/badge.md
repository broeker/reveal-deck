---
name: badge
category: component
description: Small pill label for status indicators like "COMING SOON", "NEW", "BETA".
---

## Usage

Inline pill for status or category labels. Pairs well with table rows and panel headers.

## HTML

```html
<span class="badge">COMING SOON</span>
```

## CSS

```css
.badge {
  display: inline-block;
  font-family: 'Fira Code', monospace;
  font-size: 0.5em;
  padding: 0.15em 0.55em;
  border-radius: 3px;
  background: rgba(255,176,32,0.15);
  color: var(--amber);
  border: 1px solid rgba(255,176,32,0.35);
  vertical-align: middle;
  letter-spacing: 0.05em;
}
```
