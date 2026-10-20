# Balloon Fiesta Live! — Stream Statistics

Public stats page for the Balloon Fiesta Live! YouTube and Facebook streams, hosted on Cloudflare Pages.

## Layout
- `index.html` — the page (charts and tables, reads the CSVs on load)
- `data/youtube-2026.csv` — per-show YouTube stats (15 live shows + Awards Ceremony)
- `data/facebook-2026.csv` — per-show Facebook stats (14 live shows)
- `assets/d3.min.js` — charting library (d3 v7), bundled so the site has no outside dependencies
- `_headers` — tells Cloudflare not to cache the data files, so refreshes show up right away

## Updating
Replace the CSV files in `data/` with new numbers and commit. Cloudflare Pages republishes automatically.
Column names must stay the same; the page reads them by name.

## Sources
YouTube Studio (Advanced mode and per-video analytics), Meta Business Suite, and Facebook Live Producer.
Facebook peak live viewers are read from Live Producer charts and are approximate (about ±5%).

## Years
The page has a 2026 / 2025 switch (also linkable as `?year=2025`).
- 2026: `data/youtube-2026.csv` and `data/facebook-2026.csv`
- 2025: `data/youtube-2025.csv` and `data/facebook-2025.csv`. Facebook deletes live videos after 30 days; the 2025 Facebook file comes from snapshots recorded before deletion (views, reach, 3-second live views, partial average play time).
  2025 YouTube figures are lifetime totals; the Farewell row combines the live stream with its same-day replacement upload.

## Points in time

The page has an End of Fiesta / +1 week / +1 month / To date switch so years can be compared at the same point after the event.

- End of Fiesta = through the day after the last show; +1 week and +1 month count from there.
- 2025: `youtube-2025-end.csv` (through Oct 13, 2025), `-week.csv` (Oct 19), `-month.csv` (Nov 12), rebuilt from YouTube Studio's daily figures. `youtube-2025.csv` is To date.
- 2026: `youtube-2026-week.csv` (through Oct 18) added Oct 20. `youtube-2026-end.csv` / `facebook-2026-end.csv` (through Oct 12, 2026). Add `youtube-2026-week.csv` after Oct 18 and `youtube-2026-month.csv` after Nov 11, then set their `stats` paths in the `YEARS` map at the top of `index.html`. `youtube-2026.csv` / `facebook-2026.csv` are To date.
- Unique viewers and external % are lifetime-only, so they're blank in the milestone files.
