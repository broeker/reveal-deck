---
name: image
category: component
description: Image handling for slides — background images, inline images, Unsplash stock photos, and user-provided local files. Includes browser-frame treatment for screenshots.
---

## Usage

Images can appear in slides as full-bleed backgrounds, inline content, or
framed screenshots. This component covers all image patterns.

### Image sources

| Source | How to reference | Notes |
|--------|-----------------|-------|
| **Unsplash** | `https://images.unsplash.com/photo-ID?w=1280&q=80` | Free, no API key, no attribution required. Use `w=` to control width. |
| **Local files** | `./images/photo.jpg` | User places files in an `images/` folder in the deck directory |
| **Any URL** | Direct image URL | Hotlinking — works but less reliable long-term |
| **Inline SVG** | `<svg>` in the HTML | Claude can generate diagrams, charts, abstract visuals |
| **Giphy** | `https://media.giphy.com/media/ID/giphy.gif` | For GIF backgrounds |

### Finding Unsplash images

When the user asks for an image on a slide, search Unsplash for a relevant
photo and use the direct image URL format:

```
https://images.unsplash.com/photo-{ID}?w=1280&q=80
```

Common size parameters:
- `w=1280` — full slide width (backgrounds)
- `w=800` — half-width (inline, split slides)
- `w=400` — thumbnails, small inline
- `q=80` — quality (80 is good balance of size/quality)

Unsplash images are free for commercial use, no attribution required.

## HTML

**Full-bleed background image (darkened for readability):**
```html
<section data-background-image="https://images.unsplash.com/photo-1555066931-4365d14bab8c?w=1280&q=80"
         data-background-size="cover"
         data-background-opacity="0.25">
  <h2 style="color:#fff; text-shadow: 0 2px 20px rgba(0,0,0,0.5);">Slide Title</h2>
  <p>Content over the image.</p>
</section>
```

**Background image with higher opacity (image-forward):**
```html
<section data-background-image="URL"
         data-background-size="cover"
         data-background-opacity="0.6">
  <div style="background:rgba(6,10,18,0.7); padding:1.5rem 2rem; border-radius:8px; display:inline-block;">
    <h2>Title in a box</h2>
    <p>Content stays readable over busy images.</p>
  </div>
</section>
```

**Inline image (in content area):**
```html
<div class="cols-2">
  <div>
    <h3>Description</h3>
    <p>Text content alongside the image.</p>
  </div>
  <div>
    <img src="URL" alt="Description"
         style="width:100%; border-radius:6px; border:1px solid var(--border);">
  </div>
</div>
```

**Screenshot in browser frame:**
```html
<div class="screenshot-frame">
  <div class="screenshot-chrome">
    <span class="mac-dot red"></span>
    <span class="mac-dot yellow"></span>
    <span class="mac-dot green"></span>
    <span class="screenshot-url">example.com</span>
  </div>
  <img src="URL" alt="Screenshot of example.com"
       style="width:100%; display:block;">
</div>
```

**GIF background:**
```html
<section data-background-image="https://media.giphy.com/media/ID/giphy.gif"
         data-background-size="cover"
         data-background-opacity="0.2">
  <h2>Slide Title</h2>
</section>
```

## CSS

```css
/* Browser-frame treatment for screenshots */
.screenshot-frame {
  border: 2px solid var(--border);
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 0 30px rgba(170,255,0,0.06);
}

.screenshot-chrome {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.4rem 0.7rem;
  background: #1a1a2e;
  border-bottom: 1px solid var(--border);
}

.screenshot-url {
  font-family: 'Fira Code', monospace;
  font-size: 0.45em;
  color: var(--muted);
  margin-left: 0.5rem;
  background: rgba(0,0,0,0.3);
  padding: 0.15em 0.6em;
  border-radius: 3px;
  border: 1px solid rgba(255,255,255,0.05);
}
```

## Tips

- **Background images:** keep opacity at 0.2-0.3 for readability over dark themes.
  If the image IS the point, go to 0.5-0.7 and put text in a semi-transparent box.
- **Unsplash search:** when the user says "add a photo", search for a relevant
  Unsplash image. Prefer dark, moody images that work with the theme.
- **Local files:** remind the user to create an `images/` folder in their deck
  directory and place files there before referencing them.
- **Screenshots:** use the browser-frame treatment to make screenshots look
  polished. This is also the recommended fallback when iframe embedding is
  blocked by a site's X-Frame-Options headers.
- **Alt text:** always include meaningful `alt` attributes for accessibility.
