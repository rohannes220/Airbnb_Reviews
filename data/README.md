# Data card

## Source

- **URL:** https://insideairbnb.com/get-the-data/ (Boston section)
- **Publisher:** Inside Airbnb
- **How the data was collected:** Inside Airbnb scrapes public Airbnb listing pages for Boston and
  publishes each scrape as a dated snapshot. The files are a scrape, not a sample: listings that
  Airbnb hides, removes or never shows are not included. We use the published files only and do not
  scrape Airbnb ourselves. Column definitions are in the Inside Airbnb data dictionary.

## Snapshots

| Role | Snapshot date | Inside Airbnb scrape ID | Folder | Download root |
| --- | --- | --- | --- | --- |
| Build (develop the analysis) | 2026-06-15 | 20260615212204 | `data/raw/build/` | https://data.insideairbnb.com/united-states/ma/boston/2026-06-15/ |
| Test (check the finding still holds) | 2026-09-19 | 20260919134146 | `data/raw/test/` | https://data.insideairbnb.com/united-states/ma/boston/2026-09-19/ |

`make data` downloads both snapshots from those roots (`data/` for the CSV files,
`visualisations/` for the GeoJSON). If the portal no longer serves them, it falls back to the
files attached to the GitHub release `v0.1-proposal`.

## License

[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).
Attribution requires crediting Inside Airbnb (https://insideairbnb.com) as the source, linking the
license and saying if the data was changed. We cite Inside Airbnb in this file, in the main README
and on the project site.

## Files

Row counts come from `make counts` on the downloaded files (data rows, header excluded).

| File | Grain | Rows: build (2026-06-15) | Rows: test (2026-09-19) | Main use |
| --- | --- | --- | --- | --- |
| `listings.csv.gz` | one row per listing | 4,378 | 4,368 | outcome: `review_scores_rating` (listing's overall rating) |
| `reviews.csv.gz` | one row per review | 252,910 | 267,731 | review text (`comments`) used to predict low ratings |
| `calendar.csv.gz` | one row per listing per day (365 days) | 1,611,110 | 1,594,327 | availability and minimum/maximum nights (no price column) |
| `neighbourhoods.geojson` | one polygon per neighbourhood | 26 | 26 | grouping listings by area, optional maps |

## Known limits

- **Review selection bias:** only guests who choose to write a review are represented, so the text
  may not reflect every stay, and reviews skew positive.
- **Missing ratings and reviews:** listings without reviews have no rating. In the build snapshot
  3,477 of 4,378 listings have a `review_scores_rating`; in the test snapshot 3,579 of 4,368 do.
  Our question applies only to listings that have both reviews and a rating.
- **Ratings are concentrated near the top**, so "low-rated" listings are a small group and the
  cutoff we choose affects the result.
- **One listing has many reviews:** splitting reviews instead of listings would put the same
  listing in both training and test sets.
- **Repeated review IDs:** the test snapshot's `reviews.csv.gz` has 267,731 rows but 266,845
  unique review `id` values. To be checked in the data audit.
- **Scraped-data coverage:** each snapshot shows only listings visible on the scrape date, and
  columns can change between snapshots.

## Checksums

`MANIFEST.sha256` at the repository root has one SHA-256 checksum per file in `data/raw/`.
`make data` downloads and verifies in one step. To verify files already downloaded:

```bash
make verify
```

which is the same as:

```bash
grep -v '^#' MANIFEST.sha256 | sha256sum -c -        # Linux
grep -v '^#' MANIFEST.sha256 | shasum -a 256 -c -    # macOS
```

Every line must report `OK`.
