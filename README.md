# cmdref

A single-file, offline Linux command reference with instant search.

No server, no database, no build step — every command and flag is baked
into one HTML file. Open it in a browser and start typing.

## Why

Made this because remembering every flag for `ss`, `find`, `tar`, etc.
across a bunch of different machines gets old, and copy-pasting from a
search engine every time is slower than it should be. This is a
"save it once, use it anywhere" cheat sheet.

## Features

- **Instant search** — filters ~76 commands / ~380 flag combinations as you type, no lag
- **Plain-English explanations** — e.g. `ls -l` → "long/detail format: shows permissions (rwxr-xr-x), owner, group, size, date"
- **One-click copy** — every command has its own copy button that copies *only* the command, not the explanation
- **Grouped/combo commands** — common real-world combos like `ss -tulpn` are included as their own entries, not just single flags
- **Fully offline** — no CDN, no fonts, no network calls. Works from `file://` with no internet connection
- **Fast** — pure HTML/CSS/JS, no framework, no server round-trip

## Usage

### Option 1 — Just open the file
Download `cmdref.html` and double-click it, or open it in a browser
directly. That's it.

### Option 2 — Host it on GitHub Pages
1. Push `cmdref.html` (rename to `index.html` if you want it at the root URL) to a GitHub repo
2. Go to **Settings → Pages**, set the source branch/folder
3. GitHub gives you a URL like `https://yourusername.github.io/reponame/`
4. Bookmark it and use it from any machine with a browser

### Option 3 — Any static host
Since it's a single self-contained HTML file with no dependencies, it
also works on Netlify, Vercel, a personal server, a USB stick, or a
local `python3 -m http.server`.

## Keyboard shortcuts

| Key | Action |
|-----|--------|
| `/` | Focus the search bar |
| `Esc` | Clear the search |

## Editing / adding commands

All data lives in a single JS array (`const DATA = [...]`) near the top
of the `<script>` section in `cmdref.html`. Each entry looks like:

```js
{cmd:"ss", desc:"Show socket statistics (modern replacement for netstat)", variants:[
  {f:"ss -tulpn", d:"Most common combo: TCP+UDP listening sockets with process name/PID and numeric ports"},
  {f:"ss -tu", d:"Show both TCP and UDP sockets"},
]}
```

To add a command, add a new object to the array. To add a flag to an
existing command, add an entry to its `variants` array. No build step —
just save and refresh the page.

## Tech

Plain HTML, CSS, and vanilla JavaScript. No frameworks, no dependencies,
no external requests.
