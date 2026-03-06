---
name: electric-dark
category: theme
description: Dark electric theme with neon lime accents, dot-grid background, and terminal aesthetic
default: true
---

## Fonts

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Rajdhani:wght@500;600;700&family=Source+Serif+4:ital,opsz,wght@0,8..60,400;0,8..60,600;1,8..60,400&family=Fira+Code:wght@400;500&display=swap" rel="stylesheet">
```

- **Heading:** Rajdhani (500/600/700) — geometric, condensed
- **Body:** Source Serif 4 (400/600, italic) — warm serif
- **Mono:** Fira Code (400/500) — for code, labels, UI chrome

## CSS Variables

```css
:root {
  --dark:   #060A12;
  --panel:  #0D1526;
  --panel2: #101E35;
  --cyan:   #AAFF00;
  --amber:  #FFB020;
  --red:    #FF4D4D;
  --text:   #DCE8F5;
  --muted:  #4E6A8A;
  --border: rgba(170,255,0,0.15);
  --glow:   rgba(170,255,0,0.25);
}
```

## Base styles

```css
.reveal-viewport { background: var(--dark); }

.reveal-viewport::before {
  content: '';
  position: fixed; inset: 0;
  background-image:
    radial-gradient(circle, rgba(170,255,0,0.04) 1px, transparent 1px);
  background-size: 36px 36px;
  pointer-events: none;
  z-index: 0;
}

.reveal .slides { text-align: left; }
.reveal section { padding: 0.5rem 3.5rem 1rem; box-sizing: border-box; overflow: hidden; }
```

## Typography

```css
.reveal h1, .reveal h2, .reveal h3, .reveal h4 {
  font-family: 'Rajdhani', sans-serif;
  font-weight: 700;
  color: var(--text);
  text-transform: none;
  letter-spacing: 0.01em;
  line-height: 1.05;
  margin: 0;
  text-shadow: none;
}
.reveal h1 { font-size: 5em; }
.reveal h2 { font-size: 1.7em; }
.reveal h3 { font-size: 1.2em; font-weight: 600; color: var(--cyan); }

.reveal p, .reveal li, .reveal td {
  font-family: 'Source Serif 4', serif;
  color: var(--text);
  line-height: 1.35;
  font-size: 0.75em;
}

.reveal .panel p, .reveal .panel li,
.reveal .callout p, .reveal .callout li,
.reveal .compare p, .reveal .compare li {
  font-size: 0.80em;
  line-height: 1.3;
}

.reveal code, .reveal pre {
  font-family: 'Fira Code', monospace;
}

.reveal strong { color: var(--cyan); font-weight: 600; }
.reveal em { color: var(--text); font-style: italic; }
```

## Links

```css
.reveal a {
  color: var(--cyan);
  text-decoration: none;
  border-bottom: 1px solid rgba(170,255,0,0.3);
  transition: border-color .2s;
}
.reveal a:hover { border-bottom-color: var(--cyan); }
```

## Lists

```css
.reveal ul { list-style: none; padding-left: 0; }
.reveal ul li {
  padding-left: 1.4em;
  position: relative;
  margin-bottom: 0.3em;
}
.reveal ul li::before {
  content: '\25B8';
  position: absolute;
  left: 0;
  color: var(--cyan);
  font-size: 0.85em;
  top: 0.08em;
}
```

## Inline code

```css
.reveal p code, .reveal li code, .reveal td code {
  font-size: 0.85em;
  padding: 0.1em 0.4em;
  background: rgba(170,255,0,0.1);
  border: 1px solid rgba(170,255,0,0.2);
  border-radius: 3px;
  color: var(--cyan);
}
```

## Highlight inline

```css
mark {
  background: rgba(170,255,0,0.15);
  color: var(--cyan);
  padding: 0.05em 0.3em;
  border-radius: 3px;
}
mark.amber {
  background: rgba(255,176,32,0.15);
  color: var(--amber);
}
```

## Blockquote

```css
blockquote {
  margin: 0;
  padding: 0.8rem 1.1rem;
  background: var(--panel2);
  border-left: 3px solid var(--amber);
  border-radius: 0 5px 5px 0;
  font-family: 'Source Serif 4', serif;
  font-style: italic;
  font-size: 0.88em;
  color: var(--text);
}
```

## Progress and controls

```css
.reveal .progress { color: var(--cyan); height: 2px; }
.reveal .slide-number {
  font-family: 'Fira Code', monospace;
  background: transparent;
  color: var(--muted);
  font-size: 0.5em;
}
```

## Bottom accent bar

```css
.bottom-bar {
  position: fixed; bottom: 0; left: 0; right: 0;
  height: 2px;
  background: linear-gradient(90deg, var(--cyan), var(--amber));
  z-index: 9999;
  opacity: 0.45;
}
```

```html
<!-- Place immediately inside <body>, before .reveal -->
<div class="bottom-bar"></div>
```

## Glow effect (for emphasis text)

```css
.glow {
  color: var(--cyan);
  text-shadow: 0 0 40px rgba(170,255,0,0.4);
}
```

## Motif

- **Icon:** `&#9889;` (lightning bolt emoji, renders as ⚡)
- **Component:** `motif` (defines the size/opacity treatments)
- **Required:** Yes — the lightning bolt is the signature of this theme. Every
  content slide must include at least a `motif-bg` (huge ghosted bolt in a corner).
  Many slides should also include a `motif-sm` inline with the heading. The bolt
  should feel omnipresent — a watermark-like brand element on every slide, not
  occasional decoration.
- **Colors:** Alternate `var(--cyan)` and `var(--amber)` across slides.
- **Positions:** Vary corner placement — top-right, bottom-left, center, mid-right —
  so the bolt feels dynamic, not stamped in the same spot.

## Recommended components

- `motif` — repeating visual icon system (this theme uses the lightning bolt)
- `codeblock` — terminal-style code blocks match the dark theme
- `panel` — bordered cards use accent/border variables
- `callout` — highlighted boxes with accent glow
- `comparison` — good/bad panels with color-coded borders
- `flow` — lifecycle diagrams with glowing active states
- `file-tree` — monospace directory listings
- `badge` — pill labels in amber
- `filepath` — path badges in amber/green
- `key-item` — numbered takeaway lists
