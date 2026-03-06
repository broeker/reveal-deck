---
name: agenda
category: component
description: Table of contents / agenda showing deck structure with optional "you are here" highlight. Auto-generate from section dividers.
---

## Usage

Use near the beginning of a deck (after the title slide) and optionally
repeat at section transitions with the current section highlighted. Most
valuable for decks with 10+ slides or 3+ major sections.

Claude should auto-generate this from the section dividers in the deck.

## HTML

**Full agenda:**
```html
<div class="agenda">
  <div class="agenda-item active">
    <span class="agenda-num">01</span>
    <span class="agenda-title">What Are Skills?</span>
  </div>
  <div class="agenda-item">
    <span class="agenda-num">02</span>
    <span class="agenda-title">Building Your First Skill</span>
  </div>
  <div class="agenda-item">
    <span class="agenda-num">03</span>
    <span class="agenda-title">Sharing and Collaboration</span>
  </div>
  <div class="agenda-item">
    <span class="agenda-num">04</span>
    <span class="agenda-title">Resources</span>
  </div>
</div>
```

**Compact horizontal variant (for repeating at section breaks):**
```html
<div class="agenda-bar">
  <span class="agenda-bar-item done">Intro</span>
  <span class="agenda-bar-sep">/</span>
  <span class="agenda-bar-item active">Building</span>
  <span class="agenda-bar-sep">/</span>
  <span class="agenda-bar-item">Sharing</span>
  <span class="agenda-bar-sep">/</span>
  <span class="agenda-bar-item">Resources</span>
</div>
```

## CSS

```css
/* Vertical agenda */
.agenda {
  max-width: 70%;
}

.agenda-item {
  display: flex;
  align-items: baseline;
  gap: 1.2em;
  padding: 0.6em 0;
  border-bottom: 1px solid rgba(170,255,0,0.07);
  opacity: 0.5;
  transition: opacity 0.3s;
}
.agenda-item:last-child { border-bottom: none; }
.agenda-item.active { opacity: 1; }
.agenda-item.done { opacity: 0.35; }

.agenda-num {
  font-family: 'Rajdhani', sans-serif;
  font-size: 1.6em;
  font-weight: 700;
  color: var(--muted);
  min-width: 1.5em;
  line-height: 1;
}
.agenda-item.active .agenda-num { color: var(--cyan); }

.agenda-title {
  font-family: 'Source Serif 4', serif;
  font-size: 0.9em;
  color: var(--text);
}
.agenda-item.active .agenda-title { color: var(--text); }

/* Horizontal compact bar */
.agenda-bar {
  font-family: 'Fira Code', monospace;
  font-size: 0.55em;
  display: flex;
  align-items: center;
  gap: 0.6em;
  margin-bottom: 1rem;
  letter-spacing: 0.05em;
}

.agenda-bar-item {
  color: var(--muted);
  opacity: 0.4;
}
.agenda-bar-item.active {
  color: var(--cyan);
  opacity: 1;
}
.agenda-bar-item.done {
  color: var(--muted);
  opacity: 0.6;
  text-decoration: line-through;
}

.agenda-bar-sep {
  color: var(--muted);
  opacity: 0.25;
}
```
