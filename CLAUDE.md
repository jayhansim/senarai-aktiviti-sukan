# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Single-page web app for browsing 1,453 licensed sports events from Malaysia's Ministry of Youth and Sports (eRosa KBS). No build step, no backend, no package manager — open `aktiviti_sukan.html` directly in a browser.

## Commands

There are no build, lint, or test commands. To preview changes, open the HTML file in a browser or use a local static server:

```bash
python3 -m http.server 8080
# then open http://localhost:8080/aktiviti_sukan.html
```

## Architecture

Everything lives in **`aktiviti_sukan.html`** — markup, styles, JavaScript, and all 1,453 data records embedded as a JS array (`ALL_DATA`). The CSV (`aktiviti_sukan.csv`) is the original data source; changes to data require re-embedding it into the HTML.

### Data flow

```
ALL_DATA (embedded JSON array)
  → applyFilters()     filter by searchTerm + yearFilter
  → filteredData[]     filtered subset
  → render()           slice by page, write table rows
  → renderPagination() build pagination controls (top + bottom)
```

### State variables (all module-level `let`)

| Variable | Purpose |
|----------|---------|
| `searchTerm` | Current search query |
| `yearFilter` | Selected year string, `''` = all |
| `currentPage` | 1-based active page |
| `rowsPerPage` | 50 / 100 / 200 |
| `filteredData` | Result of last `applyFilters()` call |
| `searchTimer` | Handle for 250 ms debounce |

### Key functions

- **`applyFilters()`** — O(n) scan; resets `currentPage = 1`; calls `render()`
- **`render()`** — slices `filteredData`, builds table HTML, calls `renderPagination()` twice
- **`highlight(text, term)`** — wraps matches in `<mark>`; safe because input goes through `escapeHtml()` first
- **`escapeHtml(str)`** — used on every data value before inserting into DOM

### Dependencies (CDN only)

- Tailwind CSS 2.3.0
- Flowbite 2.3.0
- Google Fonts — Inter

### Localization

UI text is in Malay (MS). Date format throughout is `DD/MM/YYYY`; `getYear()` parses this by splitting on `/` and taking index 2.
