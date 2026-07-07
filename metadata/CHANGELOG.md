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

## 2026-07-06 — Schema change: added 15_Regulations_Compliance

- Added `raw_education/15_Regulations_Compliance/` to CONTEXT.md Section 2 and created
  the folder. Needed while inspecting `data/unstructured/` for Phase 2 ingestion: the PSX
  Rule Book and an SECP regulatory circular (Market Development Fund mechanism) are
  general regulatory/compliance material that didn't fit any of the original 14
  raw_education topics or any raw_market folder. Approved by user before creation, per
  CONTEXT.md's "never invent new top-level folders without asking first" rule.

## 2026-07-06 — Schema change: batch rows for large bulk ingests

- Section 8 specifies one MANIFEST.md row per document. For the first Phase 2 ingest
  (`data/` local staging folder), two categories are large, uniform batches: company
  annual/quarterly filings (1,632 files, 190 tickers x up to 5 years each) and PSX daily
  announcement sheets (1,605 files, one per trading day). Per user decision, these two
  categories get one MANIFEST.md summary row per batch instead of one row per file, to
  keep MANIFEST.md readable. Every individual file is still fully indexed in a companion
  CSV in `metadata/` (`company_annual_reports_index.csv`, `company_quarterly_reports_index.csv`,
  `psx_daily_announcements_index.csv`), with the same fields (source, file type, date
  added) as a MANIFEST row would carry. All other categories (smaller, non-uniform) keep
  one MANIFEST row per document as specified.

## 2026-07-06 — Phase 2 ingest: first `data/` local staging folder populated

- Populated all 10 `raw_market/` folders and 2 `raw_education/` folders
  (`07_Investing`, `15_Regulations_Compliance`) from the pre-existing local `data/`
  staging folder, per the mapping confirmed with the user and the dedup report
  confirmed before any copying. Full detail in `metadata/TODO.md`'s ingest entry and
  per-document/per-batch rows in `MANIFEST.md`.
- Bulk transfer for the two largest categories (company annual/quarterly filings, PSX
  daily announcements — ~2,850 files combined) was done via `robocopy`, run natively by
  the user, after reads through the connected project folder proved too slow and
  inconsistent for practical bulk copying from this side. Flattening nested
  year/ticker folders and applying the Section 7 naming convention was done afterward
  using fast in-place renames (metadata-only operation, unaffected by the slow-read
  issue). This is the recommended pattern for any future large local ingest into this
  repo.
- Caught and corrected a data integrity issue from an earlier partial-copy attempt (see
  `metadata/TODO.md`) — 64 truncated annual-report files were detected by size mismatch
  against the robocopy'd source and replaced before logging anything in MANIFEST.md.
- `data/` itself is left untouched on disk (copied, not moved) per Section 10.

## 2026-07-06 — Switched to Git LFS for PDFs at ~8.6 GB

- Repo size reached ~8.6 GB after the Phase 2 ingest (mostly PDF filings and
  announcements), well past the "several gigabytes" threshold Section 1 flagged as the
  point to revisit plain Git tracking. Per that section's instruction to ask before
  making this change rather than doing it unilaterally, confirmed with the user before
  switching.
- Enabled Git LFS (`git lfs install`) and added `.gitattributes` tracking `*.pdf` and
  `*.Z` (the compressed PSX company-announcements feed) — the two binary file types
  making up nearly all of the repo's size. All other tracked files (CSV, JSON, MD)
  remain plain Git objects.
- Motivation beyond repo size: plain `git push` was repeatedly failing on a slow,
  unstable connection — pushes over ~800MB were dropping mid-transfer (connection
  resets, intermittent DNS failures), and GitHub also hard-rejects any single push pack
  over 2 GB. LFS uploads each file individually over plain HTTP, so a dropped
  connection only costs that one file's retry instead of restarting an entire
  multi-hundred-MB (or multi-GB) pack transfer.
- Ten speculative non-LFS commits from an earlier chunked-push attempt (splitting
  annual/quarterly filings by year to stay under the 2GB pack limit) were reset and
  discarded before making this switch — none of them had successfully reached the
  remote, so no history was lost.
- Going forward, any new PDF (or `.Z`) additions to this repo will automatically be
  tracked via LFS per `.gitattributes` — no extra step needed when adding future
  documents, `git add`/`git commit` handle it transparently.
