---
name: filepath
category: component
description: Inline path badge for displaying file paths and directory locations.
---

## Usage

Use to highlight file paths or directory locations inline. Available in amber (default) and green variants.

## HTML

```html
<span class="filepath">~/.claude/skills/</span>
<span class="filepath green">.claude/skills/</span>
```

## CSS

```css
.filepath {
  font-family: 'Fira Code', monospace;
  font-size: 0.68em;
  color: var(--amber);
  background: rgba(255,176,32,0.07);
  border: 1px solid rgba(255,176,32,0.2);
  padding: 0.2em 0.55em;
  border-radius: 3px;
  display: inline-block;
  margin-bottom: 0.4em;
}
.filepath.green {
  color: var(--cyan);
  background: rgba(170,255,0,0.06);
  border-color: rgba(170,255,0,0.2);
}
```
