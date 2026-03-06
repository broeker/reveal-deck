---
name: split-slide
category: layout
description: 50/50 split layout where one half is a full-bleed color block, image, or visual and the other is content. Breaks up visual monotony.
---

## Usage

Use for visual variety — especially effective after several standard content
slides in a row. One half carries the visual weight (color, image, large icon),
the other half carries the text. Alternate which side is visual across slides.

## HTML

**Color block + content:**
```html
<section data-background-color="#060A12">
  <span class="slide-tag">{006}</span>
  <div class="split">
    <div class="split-visual" style="background:var(--panel2);">
      <span class="stat-number" style="font-size:5em;">42</span>
      <span class="stat-label">skills created</span>
    </div>
    <div class="split-content">
      <div class="accent-line"></div>
      <h2>By the Numbers</h2>
      <ul>
        <li>Point one with context</li>
        <li>Point two with detail</li>
        <li>Point three with impact</li>
      </ul>
    </div>
  </div>
</section>
```

**Image + content:**
```html
<section data-background-color="#060A12">
  <span class="slide-tag">{007}</span>
  <div class="split">
    <div class="split-visual" style="background-image:url('image.jpg'); background-size:cover; background-position:center;">
    </div>
    <div class="split-content">
      <div class="accent-line"></div>
      <h2>Visual Story</h2>
      <p>Content alongside the image.</p>
    </div>
  </div>
</section>
```

**Reversed (content left, visual right):**
```html
<div class="split split-reverse">
  ...
</div>
```

## CSS

```css
.split {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 0;
  height: 100%;
  margin: -0.5rem -3.5rem -1rem;
}

.split-visual {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  position: relative;
  overflow: hidden;
}

.split-content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 1.5rem 3rem;
}

.split.split-reverse {
  direction: rtl;
}
.split.split-reverse > * {
  direction: ltr;
}
```
