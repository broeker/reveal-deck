---
name: stat-highlight
category: component
description: Large number or statistic with label and optional context line. Use for data points, metrics, percentages, or any number that needs to land with impact.
---

## Usage

Use when a single number or metric is the main point of a slide or section.
Works standalone, in pairs (cols-2), or in a row of three (cols-3). The number
should be large enough to read from the back of the room.

## HTML

**Single stat:**
```html
<div class="stat">
  <span class="stat-number">87%</span>
  <span class="stat-label">of teams report faster deploys</span>
</div>
```

**Stat with context line:**
```html
<div class="stat">
  <span class="stat-number">3x</span>
  <span class="stat-label">faster onboarding</span>
  <span class="stat-context">compared to manual documentation</span>
</div>
```

**Multiple stats in a row:**
```html
<div class="cols-3">
  <div class="stat">
    <span class="stat-number">87%</span>
    <span class="stat-label">adoption rate</span>
  </div>
  <div class="stat">
    <span class="stat-number">3x</span>
    <span class="stat-label">faster deploys</span>
  </div>
  <div class="stat">
    <span class="stat-number">42</span>
    <span class="stat-label">skills created</span>
  </div>
</div>
```

## CSS

```css
.stat {
  text-align: center;
  padding: 0.5rem 0;
}

.stat-number {
  font-family: 'Rajdhani', sans-serif;
  font-weight: 700;
  font-size: 4em;
  line-height: 1;
  color: var(--cyan);
  display: block;
  margin-bottom: 0.1em;
}

.stat-label {
  font-family: 'Source Serif 4', serif;
  font-size: 0.85em;
  color: var(--text);
  display: block;
  line-height: 1.3;
}

.stat-context {
  font-family: 'Fira Code', monospace;
  font-size: 0.55em;
  color: var(--muted);
  display: block;
  margin-top: 0.3em;
  letter-spacing: 0.03em;
}

/* Amber variant for secondary stats */
.stat.amber .stat-number { color: var(--amber); }
```
