# Changelog

Structural changes only: new folders, reorganizations, dedup passes, metadata schema
changes. Document additions go in `MANIFEST.md`, not here.

## 2026-07-06 — Phase 1: Repository skeleton initialized

- Created `raw_education/` with 14 topic subfolders (01_Finance_Fundamentals through
  14_Glossary) per CONTEXT.md Section 2.
- Created `raw_market/` with 10 topic subfolders (company_annual_reports through
  company_metadata) per CONTEXT.md Section 2. Replaced a pre-existing, differently-named
  subfolder structure (01_Company_Data, 02_Filings, 03_Announcements, 04_News,
  05_Research_Reports, 06_API_Data, 07_Market_Datasets, 08_Sectors) that predated this
  repo and did not match the spec; all replaced subfolders were empty, so no data was lost.
- Created `metadata/` with README.md, MANIFEST.md, SOURCES.md, TODO.md, CHANGELOG.md
  (this file) as templates.
- Created `scripts/` (empty, placeholder for future ingestion/dedup tooling).
- Initialized Git in the repository root.
- Left the pre-existing `data/` folder (8GB, 3,382 files) and 8 legacy top-level folders
  (`01_Finance_Fundamentals`, `02_PSX_Guides`, `03_SECP_Guides`, `04_Books`,
  `05_Articles`, `06_Research_Papers`, `07_YouTube_Transcripts`, `08_Notes`) untouched on
  disk and excluded from Git tracking for now. These will be vetted and ingested per
  Section 10 during Phase 2, folder-by-folder — not part of this skeleton commit.
