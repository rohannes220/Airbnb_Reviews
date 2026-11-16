# Airbnb_Reviews

DS5110 Final Project, Track 4: Reviews. This repository is being prepared for
**Milestone 1 (Proposal)**, release `v0.1-proposal`. No machine learning model has been built yet.

## Research question

<!-- TODO(team): paste the existing 100–150-word research question here, unchanged.
     It was not in this file when the repository was set up. -->

_To be added._

## Team

| Role | Name | GitHub |
| --- | --- | --- |
| Data lead | _TBD_ | _TBD_ |
| Model lead | _TBD_ | _TBD_ |
| Delivery lead | _TBD_ | _TBD_ |

### Actual contributions

List what each person actually did, with links to the pull requests or commits.

| Name | Contribution | PR / commit links |
| --- | --- | --- |
| _TBD_ | _TBD_ | _TBD_ |

## Repository layout

```text
data/README.md   data source, snapshots, license, files, known limits, checksums
data/raw/        downloaded frozen snapshots (not tracked by git)
data/derived/    files built from data/raw/ (not tracked by git)
sql/             SQL queries and schema
src/             Python source code
tests/           automated tests
reports/         figures and milestone reports
docs/            project documents
Makefile         data download and verification (make data)
requirements.txt pinned Python dependencies
MANIFEST.sha256  SHA-256 checksums of the raw data files
```

## Getting started

```bash
python3 -m venv .venv && source .venv/bin/activate
make install
make data      # download the frozen snapshots into data/raw/ and verify SHA-256 checksums
```

See [data/README.md](data/README.md) for where the data comes from and how it is verified.

## Workflow

All changes to the default branch go through reviewed pull requests.
