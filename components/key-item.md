---
name: key-item
category: component
description: Numbered takeaway list with large accent numbers. Use for key points, benefits, or ranked items.
---

## Usage

Use for key takeaways, numbered benefits, or ranked items where each point deserves visual weight.

## HTML

```html
<div class="key-item">
  <span class="key-num">01</span>
  <span class="key-text"><strong>Key point title</strong> — supporting description of why this matters.</span>
</div>
<div class="key-item">
  <span class="key-num">02</span>
  <span class="key-text"><strong>Another point</strong> — more detail here.</span>
</div>
```

## CSS

```css
.key-item {
  display: flex;
  align-items: flex-start;
  gap: 0.8em;
  padding: 0.18em 0;
  border-bottom: 1px solid rgba(170,255,0,0.07);
}
.key-item:last-child { border-bottom: none; }

.key-num {
  font-family: 'Rajdhani', sans-serif;
  font-size: 1.4em;
  font-weight: 700;
  color: var(--cyan);
  min-width: 1.5em;
  line-height: 1.1;
}

.key-text {
  font-family: 'Source Serif 4', serif;
  font-size: 0.78em;
  color: var(--text);
  line-height: 1.55;
}
.key-text strong { font-weight: 600; }
```
