---
name: table
category: component
description: Styled data table with mono headers and accent first column.
---

## Usage

Use for reference data, repo listings, quick lookups. First column is auto-accented.

## HTML

```html
<table>
  <thead>
    <tr><th>Name</th><th>Description</th></tr>
  </thead>
  <tbody>
    <tr><td>item-one</td><td>Description of item one</td></tr>
    <tr><td>item-two</td><td>Description of item two</td></tr>
  </tbody>
</table>
```

## CSS

```css
.reveal table {
  width: 100%;
  border-collapse: collapse;
  font-family: 'Source Serif 4', serif;
  font-size: 0.82em;
}

.reveal table th {
  font-family: 'Fira Code', monospace;
  font-size: 0.8em;
  font-weight: 500;
  color: var(--cyan);
  background: var(--panel2);
  padding: 0.7rem 1rem;
  text-align: left;
  letter-spacing: 0.05em;
  border-bottom: 1px solid var(--border);
}

.reveal table td {
  padding: 0.65rem 1rem;
  border-bottom: 1px solid rgba(170,255,0,0.06);
  vertical-align: top;
  color: var(--text);
}

.reveal table tr:last-child td { border-bottom: none; }
.reveal table td:first-child { color: var(--cyan); }
```
