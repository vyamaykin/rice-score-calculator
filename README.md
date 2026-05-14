# RICE Score Calculator — Jira Plugin

A zero-dependency, single-file web app for prioritizing Jira projects using the **RICE scoring framework**. Load issues directly from your Jira workspace, score them inline, and export a ranked CSV — no build step required.

![RICE Score Calculator screenshot](https://img.shields.io/badge/type-single--file%20HTML-blue) ![No dependencies](https://img.shields.io/badge/dependencies-none-brightgreen) ![License: MIT](https://img.shields.io/badge/license-MIT-lightgrey)

---

## What is RICE Scoring?

RICE is a product prioritization framework developed by Intercom. It scores each item on four dimensions:

```
RICE Score = (Reach × Impact × Confidence%) ÷ Effort
```

| Factor | Definition | Unit |
|---|---|---|
| **Reach** | How many users will this affect? | Users per quarter |
| **Impact** | How much will it move the needle per user? | 0.25 / 0.5 / 1 / 2 / 3 |
| **Confidence** | How certain are you about your estimates? | Percentage (e.g. 80) |
| **Effort** | How much work does this require? | Person-months |

Higher RICE score = higher priority.

---

## Features

- **Inline scoring table** — edit all four RICE inputs directly in the table; scores recalculate instantly
- **Edit items** — click the pencil icon on any row to open a full edit modal (name, type, description, Jira URL, all RICE scores)
- **Clickable Jira keys** — paste a URL like `https://mersgoodwill.atlassian.net/browse/SB-2161` and the key `SB-2161` renders as a live link back to the Kanban board; the key is auto-extracted from the URL as you type
- **Auto-ranking** — sidebar shows a live priority ranking of all scored items
- **Sort** — sort the table by RICE Score, Name, or Effort
- **Export CSV** — downloads a date-stamped CSV sorted by RICE score, including all fields
- **Persistence** — items and scores are saved to `localStorage` and survive page refresh
- **No build step** — open `index.html` directly in any modern browser

---

## Getting Started

### 1. Clone the repo

```bash
git clone https://github.com/your-org/rice-score-calculator.git
cd rice-score-calculator
```

### 2. Open in a browser

```bash
open index.html
# or double-click the file in your file manager
```

No server, no npm install, no build. It runs entirely client-side.

### 3. (Optional) Use a local dev server

If you prefer to avoid any browser file-access restrictions:

```bash
# Python 3
python3 -m http.server 8080

# Node (npx)
npx serve .
```

Then visit `http://localhost:8080`.

---

## Manual Scoring (no Jira required)

1. Click **Add Item**
2. Fill in the name, optional Jira key, type, and description
3. **Paste a full Jira URL** (e.g. `https://mersgoodwill.atlassian.net/browse/SB-2161`) — the key `SB-2161` is extracted automatically and will render as a clickable link back to that board ticket
4. Optionally enter RICE scores in the modal, or fill them in directly in the table after adding
5. Scores calculate automatically as you type

## Editing Items

Click the **pencil icon** on any row to open the Edit modal. You can update:

- Name, type, description
- Jira URL (auto-extracts and updates the key)
- All four RICE inputs

You can also delete the item from the Edit modal using the **Delete item** button.

---

## Exporting Results

Click **Export CSV** to download a `.csv` file sorted by RICE score descending. The file includes:

```
Rank, Key, Name, Type, Description, Reach, Impact, Confidence %, Effort (person-months), RICE Score
```

The filename is date-stamped: `rice-scores-2026-04-21.csv`.

---

## RICE Score Interpretation

| Range | Priority | Recommended action |
|---|---|---|
| ≥ 50 | 🟢 High | Strong candidate — schedule and resource |
| 20 – 49 | 🟡 Medium | Evaluate tradeoffs; consider sequencing |
| < 20 | 🔴 Low | Deprioritize, reduce scope, or cut |

---

## Impact Scale Reference

The standard Intercom impact scale used in this tool:

| Value | Label |
|---|---|
| 3.0 | Massive |
| 2.0 | High |
| 1.0 | Medium |
| 0.5 | Low |
| 0.25 | Minimal |

---

## File Structure

```
rice-score-calculator/
├── index.html    # The entire app — one self-contained file
└── README.md     # This file
```

Everything is in `index.html`: HTML structure, CSS (custom properties, no framework), and vanilla JavaScript (no libraries). `localStorage` is used for persistence.

---

## Browser Compatibility

Works in all modern browsers:

- Chrome / Edge 88+
- Firefox 85+
- Safari 14+

Not tested in Internet Explorer.

---

## Contributing

1. Fork the repo
2. Make your changes in `index.html`
3. Test: open the file in a browser, add items, score them, export CSV, load from Jira
4. Open a pull request with a clear description of what changed and why

### Development guidelines

- Keep it a single file — no build pipeline, no external CSS/JS dependencies
- Use CSS custom properties for all colors
- Escape all user-provided strings before inserting into the DOM (`escHtml()`)
- Persist state changes to `localStorage` via `saveItems()` after every mutation

---

## License

MIT — free to use, modify, and distribute. See [LICENSE](LICENSE) for details.

---

## Acknowledgements

- RICE framework originally described by [Sean McBride at Intercom](https://www.intercom.com/blog/rice-simple-prioritization-for-product-managers/)
- Jira integration powered by the [Anthropic API](https://docs.anthropic.com) + [Atlassian Rovo MCP](https://www.atlassian.com/platform/rovo)
