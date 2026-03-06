---
name: content-slide
category: layout
description: Standard workhorse slide with slug, accent line, and title. Prefer 2-column layout.
---

## Usage

The default slide type for most content. Every content slide gets a `{NNN}` slug, accent line, and h2 title. Prefer 2-column layouts; use single column with a panel or callout to fill visual weight when needed.

## HTML

```html
<section data-background-color="#060A12">
  <span class="slide-tag">{001}</span>
  <div class="accent-line"></div>
  <h2>Slide Title</h2>

  <!-- 2-column layout (preferred) -->
  <div class="cols-2">
    <div>
      <p>Left column content.</p>
    </div>
    <div>
      <div class="panel panel-cyan">
        <div class="panel-label" style="color:var(--cyan)">KEY POINT</div>
        <p>Right column content in a panel.</p>
      </div>
    </div>
  </div>
</section>
```

**Single column variant:**
```html
<section data-background-color="#060A12">
  <span class="slide-tag">{002}</span>
  <div class="accent-line"></div>
  <h2>Slide Title</h2>
  <p>Content paragraph.</p>
  <div class="callout">Key takeaway here.</div>
</section>
```

## CSS

```css
.cols-2 {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.75rem;
  align-items: start;
}
.cols-2 > *, .cols-3 > * { min-width: 0; }

.cols-3 {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 1.25rem;
}

.accent-line {
  width: 2.5rem; height: 3px;
  background: var(--cyan);
  border-radius: 2px;
  margin-bottom: 0.5rem;
}

.slide-tag {
  font-family: 'Fira Code', monospace;
  font-size: 0.55em;
  color: var(--muted);
  display: block;
  margin-bottom: 0.25rem;
}
```
