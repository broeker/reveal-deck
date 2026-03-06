---
name: codeblock
category: component
description: Terminal-style code container with faux macOS dots header. Use for commands, file contents, and code snippets.
---

## Usage

Use for any terminal commands, code snippets, or file contents. The faux dot header gives it a terminal/IDE feel.

## HTML

```html
<div class="codeblock">
  <div class="codeblock-header">
    <span class="codeblock-dot" style="background:#FF5F56"></span>
    <span class="codeblock-dot" style="background:#FFBD2E"></span>
    <span class="codeblock-dot" style="background:#27C93F"></span>
  </div>
  <pre><code>your code here</code></pre>
</div>
```

## CSS

```css
.reveal pre {
  width: 100%;
  margin: 0;
  box-shadow: none;
  background: transparent;
  border: none;
}

.codeblock {
  background: var(--dark);
  border: 1px solid var(--border);
  border-radius: 6px;
  overflow: hidden;
}

.codeblock-header {
  background: var(--panel2);
  padding: 0.4rem 0.9rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  border-bottom: 1px solid var(--border);
}

.codeblock-dot {
  width: 8px; height: 8px;
  border-radius: 50%;
}

.codeblock pre {
  padding: 0.7rem 1rem;
  font-size: 0.62em;
  line-height: 1.65;
  color: var(--cyan);
  white-space: pre-wrap;
  word-break: break-all;
}

.codeblock pre code {
  background: transparent;
  border: none;
  padding: 0;
  color: inherit;
  white-space: pre-wrap !important;
  overflow-wrap: break-word !important;
  max-height: none !important;
  overflow: visible !important;
}
```
