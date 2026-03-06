---
name: resource-list
category: component
description: Categorized link list for resources slides. Groups links under mono-styled category headers.
---

## Usage

Use on resources/references slides to organize links by category.

## HTML

```html
<span class="res-cat">Official Documentation</span>
<ul class="res-list">
  <li><a href="https://example.com">Resource title</a> — brief description</li>
  <li><a href="https://example.com">Another resource</a></li>
</ul>

<span class="res-cat">Community</span>
<ul class="res-list">
  <li><a href="https://example.com">Community resource</a></li>
</ul>
```

## CSS

```css
.res-cat {
  font-family: 'Fira Code', monospace;
  font-size: 0.55em;
  letter-spacing: 0.10em;
  text-transform: uppercase;
  color: var(--cyan);
  margin: 0.2rem 0 0.15rem;
  display: block;
}

.res-list { list-style: none; padding: 0; }
.reveal .res-list li { font-size: 0.65em; margin-bottom: 0.2em; padding: 0; }
.reveal .res-list li::before { content: none; }
```
