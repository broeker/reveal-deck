---
name: quote
category: component
description: Large pull quote with attribution. Use for impactful statements, testimonials, or provocative framing. Different from inline blockquotes — this is the star of the slide.
---

## Usage

Use when a quote IS the content of the slide — not a supporting element but
the main event. Works for speaker quotes, user testimonials, provocative
statements to set up the next section, or key principles.

## HTML

**Standard quote:**
```html
<div class="pull-quote">
  <blockquote class="pull-quote-text">
    The best way to predict the future is to invent it.
  </blockquote>
  <cite class="pull-quote-cite">Alan Kay</cite>
</div>
```

**Quote with role/source:**
```html
<div class="pull-quote">
  <blockquote class="pull-quote-text">
    Skills turned our hard-won workflows into institutional knowledge.
  </blockquote>
  <cite class="pull-quote-cite">
    Sarah Chen <span class="pull-quote-role">— Senior Developer, Electric Citizen</span>
  </cite>
</div>
```

## CSS

```css
.pull-quote {
  max-width: 85%;
  margin: 1.5rem auto;
  text-align: center;
}

.pull-quote-text {
  font-family: 'Source Serif 4', serif;
  font-size: 1.4em;
  font-style: italic;
  color: var(--text);
  line-height: 1.45;
  border: none;
  background: none;
  padding: 0;
  margin: 0 0 0.8rem;
  position: relative;
}

.pull-quote-text::before {
  content: '\201C';
  font-family: 'Rajdhani', sans-serif;
  font-size: 3em;
  color: var(--cyan);
  opacity: 0.3;
  position: absolute;
  top: -0.35em;
  left: -0.5em;
  line-height: 1;
}

.pull-quote-cite {
  font-family: 'Fira Code', monospace;
  font-size: 0.6em;
  color: var(--cyan);
  font-style: normal;
  letter-spacing: 0.05em;
  display: block;
}

.pull-quote-role {
  color: var(--muted);
  font-weight: 400;
}
```
