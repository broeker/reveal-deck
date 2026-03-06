---
name: step-list
category: component
description: Numbered step list with circled numbers. Use for ordered procedures or instructions.
---

## Usage

Use when content has a clear numbered sequence — installation steps, procedures, ranked items.

## HTML

```html
<div class="step">
  <span class="step-n">1</span>
  <div class="step-body">
    <strong>Step title</strong> — description of what to do.
  </div>
</div>
<div class="step">
  <span class="step-n">2</span>
  <div class="step-body">
    <strong>Next step</strong> — continue the process.
  </div>
</div>
```

## CSS

```css
.step {
  display: flex;
  gap: 0.9rem;
  align-items: flex-start;
  margin-bottom: 0.85rem;
}

.step-n {
  font-family: 'Rajdhani', sans-serif;
  font-weight: 700;
  font-size: 0.75em;
  min-width: 1.5em; height: 1.5em;
  border-radius: 50%;
  background: var(--cyan);
  color: var(--dark);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  margin-top: 0.05em;
}

.step-body { flex: 1; font-size: 0.84em; }
.step-body strong { color: var(--cyan); }
```
