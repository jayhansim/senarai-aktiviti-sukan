# Senarai Aktiviti Sukan

A single-page web app for browsing 1,453 licensed sports events from Malaysia's Ministry of Youth and Sports (eRosa KBS). 
Link: https://erosa.kbs.gov.my/carian_pelesenan/aktivitisukan_list.php

## Usage

Open `index.html` directly in a browser, or serve it locally:

```bash
python3 -m http.server 8080
# open http://localhost:8080/index.html
```

No build step, no backend, no dependencies to install.

## Features

- Full-text search across activity name, organizer, license number, and dates
- Year filter (2019–2026)
- Pagination with 50/100/200 rows per page
- Search term highlighting
- Color-coded year badges

## Files

| File | Purpose |
|------|---------|
| `index.html` | Main app — markup, styles, JS, and all data embedded |
| `aktiviti_sukan.csv` | Source data (1,453 rows) |

For detailed documentation, see [OVERVIEW.md](OVERVIEW.md).
