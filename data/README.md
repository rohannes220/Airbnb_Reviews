# Data

## Source

[Inside Airbnb](https://insideairbnb.com/get-the-data/) and web scraping.

City: Boston, Massachusetts.

<!-- TODO(team): confirm whether "web scraping" means Inside Airbnb's own scraping of public
     Airbnb pages or additional scraping by this team. -->

## Snapshots

We use two frozen snapshots and never re-download "latest" data.

| Snapshot | Folder | Scrape date | Use |
| --- | --- | --- | --- |
| Build | `data/raw/build/` | _TBD: exact earlier 2026 date from the course files_ | building and exploring |
| Test | `data/raw/test/` | September 19, 2026 | held-out testing |

Download URLs: _TBD: the exact course-assigned URLs (set `BUILD_BASE_URL` and `TEST_BASE_URL` in the Makefile)._

## License

Inside Airbnb data is licensed under
[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).
Attribution: data from Inside Airbnb (https://insideairbnb.com). Any report or figure that uses
this data must credit Inside Airbnb.

## Files

Each snapshot folder has the same four files. Row counts must come from the downloaded files
(`make counts`); they are blank until the frozen files are available.

| File | Grain (one row per…) | Rows: build | Rows: test | Purpose |
| --- | --- | --- | --- | --- |
| `listings.csv.gz` | listing at the scrape date | _TBD_ | _TBD_ | listing attributes, review scores and review counts |
| `reviews.csv.gz` | review (with listing, date, reviewer and text) | _TBD_ | _TBD_ | main review data for Track 4 |
| `calendar.csv.gz` | listing per calendar day | _TBD_ | _TBD_ | availability and price context |
| `neighbourhoods.geojson` | neighbourhood (one polygon feature each) | _TBD_ | _TBD_ | grouping listings by area and mapping |

## Known limits

- **Review selection bias:** only guests who choose to write a review are represented, and
  reviews skew positive.
- **Missing ratings and reviews:** many listings have no reviews or blank review-score fields.
- **Scraped-data coverage:** the data is a scrape of public listing pages at one point in time;
  listings that were hidden, removed or not reachable at scrape time are missing, and fields can
  change between snapshots.

## Checksums

`MANIFEST.sha256` at the repository root holds the SHA-256 hash of every file in `data/raw/`.

To verify:

```bash
make verify
```

which is the same as:

```bash
grep -v '^#' MANIFEST.sha256 | sha256sum -c -        # Linux
grep -v '^#' MANIFEST.sha256 | shasum -a 256 -c -    # macOS
```

Every line must report `OK`. `make data` downloads and verifies in one step. To create the
manifest the first time, place the frozen files in `data/raw/build/` and `data/raw/test/`, run
`make manifest`, check the output and commit `MANIFEST.sha256`.
