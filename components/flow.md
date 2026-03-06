---
name: flow
category: component
description: Horizontal lifecycle/flow diagram with connected steps. Use for processes, workflows, and sequential stages.
---

## Usage

Use for any multi-step process or lifecycle. Steps connect with arrows. One step can be highlighted as `.active`.

## HTML

```html
<div class="flow">
  <span class="flow-step">Step 1</span>
  <span class="flow-arrow">-></span>
  <span class="flow-step active">Step 2</span>
  <span class="flow-arrow">-></span>
  <span class="flow-step">Step 3</span>
</div>
```

## CSS

```css
.flow {
  display: flex;
  align-items: center;
  gap: 0;
  flex-wrap: nowrap;
  margin: 1.25rem 0;
}

.flow-step {
  font-family: 'Fira Code', monospace;
  font-size: 0.65em;
  padding: 0.5em 0.9em;
  background: var(--panel2);
  border: 1px solid var(--border);
  border-radius: 4px;
  color: var(--cyan);
  white-space: nowrap;
}

.flow-step.active {
  background: rgba(170,255,0,0.12);
  border-color: var(--cyan);
  box-shadow: 0 0 12px var(--glow);
}

.flow-arrow {
  font-family: 'Fira Code', monospace;
  color: var(--muted);
  padding: 0 0.6em;
  font-size: 0.9em;
}
```
