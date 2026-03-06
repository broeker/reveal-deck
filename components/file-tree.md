---
name: file-tree
category: component
description: Monospace directory tree listing with color-coded dirs, files, and comments.
---

## Usage

Use to display file/directory structures. Color-code directories, files, comments, and symlink arrows.

## HTML

```html
<div class="file-tree">
  <span class="ft-dir">my-project/</span><br>
  &nbsp;&nbsp;<span class="ft-dir">src/</span><br>
  &nbsp;&nbsp;&nbsp;&nbsp;<span class="ft-file">index.js</span> <span class="ft-cmnt"># entry point</span><br>
  &nbsp;&nbsp;<span class="ft-file">package.json</span><br>
  &nbsp;&nbsp;<span class="ft-file">symlink</span> <span class="ft-arr">-></span> <span class="ft-cmnt">target/path</span>
</div>
```

## CSS

```css
.file-tree {
  font-family: 'Fira Code', monospace;
  font-size: 0.68em;
  background: var(--dark);
  border: 1px solid var(--border);
  border-radius: 5px;
  padding: 0.6rem 0.9rem;
  line-height: 1.65;
}

.ft-dir  { color: var(--cyan); }
.ft-file { color: var(--text); }
.ft-cmnt { color: var(--muted); font-style: italic; }
.ft-arr  { color: var(--amber); }
```
