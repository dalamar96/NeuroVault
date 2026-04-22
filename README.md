# NeuroVault

A single-file bookmark manager that runs entirely in your browser — no server, no install, no account. Import your browser's exported bookmarks HTML, score and tag each link, and explore your collection through four views.

## Features

- **Explorer** — bookmarks grouped by folder, sorted by value score, collapsible
- **Dashboard** — top-value links, most-clicked links, score distribution, tag frequency charts
- **Graph** — interactive force-directed graph; nodes connected by shared domain or tag; draggable
- **Tags** — cluster view showing every tag group with average score and item count

### Import

- Upload a browser bookmarks `.html` file (Chrome, Firefox, Edge, Safari all export the same Netscape format)
- Drag and drop a file onto the drop zone
- Paste raw bookmark HTML directly into the text area

### AI Scoring & Tagging (optional)

Connect any OpenAI-compatible local inference server (e.g. LM Studio, Ollama) to automatically score each bookmark 1–5 and suggest tags on import. Falls back gracefully if the endpoint is unreachable.

### Smart Merge

When an incoming bookmark shares the same base domain as an existing one, a side-by-side merge panel appears. Choose to keep both, replace the existing entry, skip the incoming one, or stop the import.

### Editing

Each bookmark card has inline actions:

| Action | Description |
|--------|-------------|
| Open | Opens the URL in a new tab and increments the click counter |
| Edit | Full edit modal for title, URL, folder path, score, tags, and notes |
| +Score | Bumps the value score by 1 (max 5) |
| +Tag | Prompts for a new tag and appends it |
| Delete | Removes the bookmark after confirmation |

### Export

| Format | Contents |
|--------|----------|
| HTML | Standard Netscape bookmarks file, re-importable in any browser |
| JSON | Full bookmark data with scores, tags, notes, and usage stats |
| Obsidian Bundle | Markdown index + one `.md` file per bookmark, ready to drop into a vault |

## Usage

1. Download `favorites.html`
2. Open it in any modern browser — it works offline
3. Import your bookmarks and start exploring

No build step. No dependencies. No data leaves your machine.

## Data Storage

All data is saved to `localStorage` under two keys:

- `neurovault_bookmarks_v3` — bookmark array
- `neurovault_ui_v2` — UI state (current view, AI settings)

Use **Clear Saved Data** in the sidebar to wipe everything, or **Export JSON** to back up before clearing.

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl/Cmd + K` | Focus the search bar |
| `Escape` | Close open modal or cancel in-progress merge |

## Auto-Tagging Rules

Tags are inferred from the bookmark's title, URL, and notes without any AI:

| Keyword match | Tag applied |
|---------------|-------------|
| github, gitlab, npm, repo | `dev` |
| azure, aws, gcp, cloudflare | `cloud` |
| youtube, course, tutorial, learn | `learning` |
| stripe, billing, checkout | `payments` |
| analytics, seo, ga4 | `marketing` |
| art, photo, camera | `creative` |
| book, story, novel, obsidian | `writing` |

## Browser Compatibility

Requires a browser with `localStorage`, `Canvas 2D`, `DOMParser`, `Fetch`, and `File API` — any evergreen browser released after 2020 will work.
