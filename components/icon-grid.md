---
name: icon-grid
category: component
description: Grid of icon + label + description blocks. Use for feature overviews, capability lists, or category breakdowns.
---

## Usage

Use when presenting multiple features, capabilities, or categories that are
peers — each gets equal visual weight. More compact and visual than panels.
Works best with 3, 4, or 6 items.

Icons can be emoji, inline SVG, or single characters.

## HTML

```html
<div class="icon-grid">
  <div class="icon-grid-item">
    <span class="icon-grid-icon">&#9889;</span>
    <span class="icon-grid-label">Fast</span>
    <span class="icon-grid-desc">Skip the setup, get to the work.</span>
  </div>
  <div class="icon-grid-item">
    <span class="icon-grid-icon">&#128736;</span>
    <span class="icon-grid-label">Flexible</span>
    <span class="icon-grid-desc">Works with any project or tool.</span>
  </div>
  <div class="icon-grid-item">
    <span class="icon-grid-icon">&#129309;</span>
    <span class="icon-grid-label">Shareable</span>
    <span class="icon-grid-desc">Team-wide skills from day one.</span>
  </div>
</div>
```

**With inline SVG icons:**
```html
<div class="icon-grid-item">
  <span class="icon-grid-icon">
    <svg width="1.2em" height="1.2em" viewBox="0 0 24 24" fill="currentColor">
      <!-- path data -->
    </svg>
  </span>
  <span class="icon-grid-label">Feature</span>
  <span class="icon-grid-desc">Description here.</span>
</div>
```

## CSS

```css
.icon-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
  margin: 1rem 0;
}

.icon-grid-item {
  text-align: center;
  padding: 0.8rem 0.5rem;
}

.icon-grid-icon {
  font-size: 2em;
  display: block;
  margin-bottom: 0.4rem;
  color: var(--cyan);
  line-height: 1.2;
}

.icon-grid-label {
  font-family: 'Rajdhani', sans-serif;
  font-weight: 600;
  font-size: 0.9em;
  color: var(--text);
  display: block;
  margin-bottom: 0.2rem;
}

.icon-grid-desc {
  font-family: 'Source Serif 4', serif;
  font-size: 0.68em;
  color: var(--muted);
  line-height: 1.35;
  display: block;
}
```
