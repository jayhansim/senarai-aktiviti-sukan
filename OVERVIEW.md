# Senarai Aktiviti Sukan — Project Overview

**Source:** eRosa KBS (Kementerian Belia dan Sukan Malaysia)
**Data as of:** March 27, 2026
**Total Records:** 1,453 licensed sports events

---

## What It Does

A single-page web app for browsing and searching licensed sports events registered with Malaysia's Ministry of Youth and Sports. All data processing happens client-side — no backend required.

---

## Files

| File | Size | Purpose |
|------|------|---------|
| `index.html` | ~315 KB | Main application (HTML + CSS + JS + embedded data) |
| `aktiviti_sukan.csv` | ~132 KB | Source data (1,453 rows) |

### CSV Columns

| Column | Description |
|--------|-------------|
| `No` | Record number (1–1453) |
| `No Lesen` | License/permit number (`L202XXXXXX`) |
| `Nama Syarikat` | Event organizer name |
| `Nama Aktiviti` | Event/activity name |
| `Tarikh Aktiviti Mula` | Start date (DD/MM/YYYY) |
| `Tarikh Aktiviti Tamat` | End date (DD/MM/YYYY) |

---

## Architecture

**Single-file SPA** — all HTML, CSS, JS, and data are bundled into one `.html` file for zero-dependency deployment.

### State

```js
let searchTerm = '';       // current search query
let yearFilter = '';       // selected year ('' = all)
let currentPage = 1;       // active page
let rowsPerPage = 50;      // items per page (50 / 100 / 200)
let filteredData = [...];  // filtered subset of ALL_DATA
let searchTimer = null;    // debounce handle
```

### Data Flow

```
User input
  → debounce (250 ms)
  → applyFilters()    // O(n) scan of ALL_DATA
  → render()          // update table rows
  → renderPagination() // update pagination controls
```

### Key Functions

| Function | Purpose |
|----------|---------|
| `applyFilters()` | Filter data by search term and year |
| `render()` | Re-render table and pagination |
| `renderPagination(id, total)` | Smart pagination with ellipsis |
| `goPage(p)` | Navigate to page, scroll to top |
| `highlight(text, term)` | Wrap matches in `<mark>` |
| `escapeHtml(str)` | Prevent XSS |
| `getYear(dateStr)` | Extract year from DD/MM/YYYY |

---

## Features

- **Full-text search** across activity name, company, license number, and dates
- **Year filter** (2019–2026 via dropdown)
- **Debounced input** — 250 ms delay before filtering
- **Search highlighting** — matching text highlighted in yellow
- **Pagination** — 50/100/200 rows per page, smart ellipsis, dual top/bottom controls
- **Year badges** — color-coded by year for quick visual scanning
- **Clear button** — resets all filters in one click
- **XSS-safe** — all data rendered through `escapeHtml()`

### Year Badge Colors

| Year | Color |
|------|-------|
| 2019 | Purple |
| 2020 | Pink |
| 2021 | Red |
| 2022 | Orange |
| 2023 | Yellow |
| 2024 | Green |
| 2025 | Blue |
| 2026 | Indigo |

---

## Data Summary

### Events by Year

| Year | Events |
|------|--------|
| 2019 | 231 |
| 2020 | 130 |
| 2021 | 23 *(COVID low)* |
| 2022 | 203 |
| 2023 | 271 |
| 2024 | 247 |
| 2025 | 293 |
| 2026 | 48 *(as of Mar 2026)* |

### Top Organizers

| Organizer | Events |
|-----------|--------|
| Oriental Global Event Management | 93 |
| MST Golf Management Sdn Bhd | 40 |
| Lumen Sports Sdn Bhd | 27 |
| Score Sports Management Sdn Bhd | 25 |
| IJ Event Management | 24 |

---

## Dependencies (CDN, no npm)

| Library | Version | Use |
|---------|---------|-----|
| Tailwind CSS | 2.3.0 | Utility styling |
| Flowbite | 2.3.0 | UI components |
| Google Fonts (Inter) | — | Typography |

---

## Deployment

Open `index.html` in any browser — no server or build step needed.
