---
name: terminal-embed
category: component
description: Live terminal embedded in a slide via ttyd. Fullscreen or split-panel. Interactive during presentation — type real commands, open files, run demos.
---

## Usage

Embed a live terminal session directly in a slide using [ttyd](https://github.com/tsl0922/ttyd),
a lightweight tool that serves a terminal over HTTP. The presenter can type
live commands during the talk.

**Requires:** `ttyd` installed on the presenter's machine and running before
the presentation starts.

```bash
# Ubuntu/Debian
sudo apt install ttyd
```

### Terminal modes

| Mode | Command | Use case |
|------|---------|----------|
| Blank shell | `ttyd -W -p 7681 bash` | Live demo, ad hoc commands |
| Specific directory | `ttyd -W -p 7681 bash -c "cd /path/to/project && exec bash"` | Project walkthrough |
| Open a file | `ttyd -W -p 7681 vim /path/to/file.php` | Code review, config inspection |
| View a file | `ttyd -W -p 7681 less /path/to/file.json` | Read-only file display |
| Run then stay open | `ttyd -W -p 7681 bash -c "drush status; exec bash"` | Show output, then continue |

### Multiple terminals

Use different ports for different slides:

```bash
ttyd -W -p 7681 bash &                                    # slide {005}
ttyd -W -p 7682 vim /app/web/sites/default/settings.php & # slide {008}
ttyd -W -p 7683 bash -c "cd /app && exec bash" &          # slide {012}
```

### Important: the `-W` flag

ttyd is **read-only by default**. The `-W` (writable) flag is required for
the presenter to type in the terminal. Always include it.

### Presenter tips

- Start all ttyd instances before presenting (`&` to background them)
- Test each terminal iframe loads before going live
- Use a larger font in the terminal: ttyd supports `--font-size` or configure
  via your terminal profile
- Kill all instances after: `pkill ttyd`

## HTML

**Fullscreen terminal (entire slide is the terminal):**
```html
<section data-background-iframe="http://localhost:7681"
         data-background-interactive>
  <div class="terminal-label">
    <span class="terminal-label-text">LIVE TERMINAL</span>
  </div>
  <aside class="notes">
    Live demo — show the audience [describe what you'll do].
    Commands to run: [list key commands as a reminder].
  </aside>
</section>
```

**Fullscreen with overlay caption:**
```html
<section data-background-iframe="http://localhost:7681"
         data-background-interactive>
  <div class="terminal-overlay">
    <h3>Live Demo</h3>
    <p>Configuring DDEV for a new Drupal project</p>
  </div>
  <aside class="notes">
    Click into the terminal to interact. The overlay will stay
    in the corner for context.
  </aside>
</section>
```

**Split slide — terminal on one side, content on the other:**
```html
<section>
  <span class="slide-tag">{NNN}</span>
  <span class="motif-bg" style="position:absolute; top:-40px; right:-20px; color:var(--cyan);">&#9889;</span>
  <h2>Setting Up DDEV</h2>
  <div class="cols-2" style="gap:1.5rem; align-items:stretch;">
    <div>
      <p>Key steps:</p>
      <ul>
        <li>Initialize the project</li>
        <li>Configure PHP version</li>
        <li>Start the containers</li>
      </ul>
      <div class="callout">
        <strong>Try it:</strong> Follow along in the live terminal.
      </div>
    </div>
    <div class="terminal-inline">
      <div class="terminal-chrome">
        <span class="mac-dot red"></span>
        <span class="mac-dot yellow"></span>
        <span class="mac-dot green"></span>
        <span class="terminal-title">bash</span>
      </div>
      <iframe src="http://localhost:7681"
              style="width:100%; height:380px; border:none; border-radius:0 0 6px 6px;">
      </iframe>
    </div>
  </div>
</section>
```

## CSS

```css
/* Label pinned to bottom-left of fullscreen terminal slides */
.terminal-label {
  position: absolute;
  bottom: 1.5rem;
  left: 2rem;
  z-index: 10;
  pointer-events: none;
}

.terminal-label-text {
  font-family: 'Fira Code', monospace;
  font-size: 0.5em;
  color: var(--cyan);
  letter-spacing: 0.15em;
  text-transform: uppercase;
  background: rgba(6,10,18,0.8);
  padding: 0.3em 0.8em;
  border-radius: 3px;
  border: 1px solid var(--border);
}

/* Corner overlay with caption on fullscreen terminal slides */
.terminal-overlay {
  position: absolute;
  bottom: 2rem;
  left: 2rem;
  background: rgba(6,10,18,0.88);
  padding: 0.8rem 1.2rem;
  border-radius: 6px;
  border: 1px solid var(--border);
  z-index: 10;
  max-width: 40%;
  pointer-events: none;
}

.terminal-overlay h3 {
  font-size: 0.9em;
  margin: 0 0 0.3rem 0;
  color: var(--cyan);
}

.terminal-overlay p {
  font-size: 0.65em;
  margin: 0;
  color: var(--muted);
}

/* Inline terminal panel for split slides */
.terminal-inline {
  border: 1px solid var(--border);
  border-radius: 6px;
  overflow: hidden;
  background: #0a0a0a;
}

.terminal-chrome {
  display: flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.4rem 0.7rem;
  background: #1a1a2e;
  border-bottom: 1px solid var(--border);
}

.terminal-title {
  font-family: 'Fira Code', monospace;
  font-size: 0.5em;
  color: var(--muted);
  margin-left: 0.5rem;
}
```
