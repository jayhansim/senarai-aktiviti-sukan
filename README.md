# Senarai Aktiviti Sukan

A single-page web app for browsing 1,453 licensed sports events from Malaysia's Ministry of Youth and Sports (eRosa KBS). 
Link: https://erosa.kbs.gov.my/carian_pelesenan/aktivitisukan_list.php

## Reason of building this

I'm a runner and as Malaysian we can enjoy tax relief from participating in races, provided that the competition organiser is approved and licensed by the Commissioner of Sports. Then I found the list on eRosa KBS website. The user experience of the website wasn't optimal. Hence with the help of AI, I recreate the table and made some enhancements by adding filters and more responsive search capabilities using modern web tech. 

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
