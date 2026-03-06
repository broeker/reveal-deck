---
name: timeline
category: component
description: Horizontal timeline with milestones, dates, or phases. Use for roadmaps, project history, or chronological progression.
---

## Usage

Use for anything with a chronological or phased sequence — project roadmaps,
historical context, release timelines, migration plans. Different from `flow`
(which shows a repeatable process); timeline shows progression through time.

## HTML

```html
<div class="timeline">
  <div class="tl-item">
    <span class="tl-date">Q1 2025</span>
    <div class="tl-dot"></div>
    <span class="tl-label">Research &amp; planning</span>
  </div>
  <div class="tl-item active">
    <span class="tl-date">Q2 2025</span>
    <div class="tl-dot"></div>
    <span class="tl-label">Build &amp; test</span>
  </div>
  <div class="tl-item">
    <span class="tl-date">Q3 2025</span>
    <div class="tl-dot"></div>
    <span class="tl-label">Team rollout</span>
  </div>
  <div class="tl-item">
    <span class="tl-date">Q4 2025</span>
    <div class="tl-dot"></div>
    <span class="tl-label">Full adoption</span>
  </div>
</div>
```

## CSS

```css
.timeline {
  display: flex;
  align-items: flex-start;
  gap: 0;
  position: relative;
  margin: 1.5rem 0;
  padding-top: 0.5rem;
}

/* Connecting line */
.timeline::before {
  content: '';
  position: absolute;
  top: calc(0.5rem + 1.6em + 0.4rem + 5px);
  left: 5%;
  right: 5%;
  height: 2px;
  background: var(--border);
}

.tl-item {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  position: relative;
}

.tl-date {
  font-family: 'Fira Code', monospace;
  font-size: 0.55em;
  color: var(--muted);
  letter-spacing: 0.05em;
  margin-bottom: 0.4rem;
}
.tl-item.active .tl-date { color: var(--cyan); }

.tl-dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: var(--panel2);
  border: 2px solid var(--muted);
  margin-bottom: 0.5rem;
  position: relative;
  z-index: 1;
}
.tl-item.active .tl-dot {
  background: var(--cyan);
  border-color: var(--cyan);
  box-shadow: 0 0 10px var(--glow);
}

.tl-label {
  font-family: 'Source Serif 4', serif;
  font-size: 0.7em;
  color: var(--text);
  line-height: 1.3;
  max-width: 90%;
}
.tl-item.active .tl-label { color: var(--text); font-weight: 600; }
```
