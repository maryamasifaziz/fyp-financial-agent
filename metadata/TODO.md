# TODO

Anything missing, deferred, or flagged for later review. Updated at the end of every
session (CONTEXT.md Section 4, Section 8).

## Open items

- [x] Confirm GitHub repository is created and connected — done, pushed to
      github.com/maryamasifaziz/fyp-financial-agent.
- [ ] The 8 legacy top-level folders (`01_Finance_Fundamentals`, `02_PSX_Guides`,
      `03_SECP_Guides`, `04_Books`, `05_Articles`, `06_Research_Papers`,
      `07_YouTube_Transcripts`, `08_Notes`) are still untouched on disk and excluded from
      Git. Not yet scoped — revisit separately from the `data/` ingest below.
- [x] `data/` folder ingest (Section 10) — COMPLETE as of 2026-07-06. All categories
      copied, verified, and logged in MANIFEST.md:
        - `raw_market/api_data/`, `raw_market/historical_datasets/worldbank/` — done
          earlier, hash-verified on copy.
        - `raw_market/company_annual_reports/` (383 files) and
          `raw_market/company_quarterly_reports/` (1,249 files) — bulk-copied via
          `robocopy` (native Windows tool, run by user) into nested year/ticker
          subfolders, then flattened and renamed to `TICKER_Annual_Report_YYYY.pdf` /
          `TICKER_Quarterly_Report_YYYY-MM-DD.pdf` using fast in-place renames. **Note:**
          an earlier partial attempt (before the robocopy handoff) had left 67 annual +
          9 quarterly files copied via a slower method; several of these (64 of the 67
          annual ones) turned out to be truncated/corrupted, almost certainly from
          copy processes being killed mid-write when a command timed out. All of these
          were detected via size mismatch against the trustworthy robocopy'd source and
          replaced. A 20-file random hash sample post-fix matched source exactly.
        - `raw_market/psx_announcements/` (1,605 daily sheets, bulk-copied via robocopy
          then renamed to `PSX_Announcement_Sheet_YYYY-MM-DD.pdf`; plus the compressed
          company-announcements feed and the misfiled PSX Daily Stock Market Report from
          `secp/investor_alerts/`) — done.
        - `raw_market/corporate_actions/`, `raw_market/research_reports/`,
          `raw_market/market_news/`, `raw_education/07_Investing/`,
          `raw_education/15_Regulations_Compliance/` — the 8 remaining one-off files,
          copied directly and hash-verified byte-for-byte against source.
      Excluded entirely, not copied (per user decision): `secp/struck_off_companies/`
      blank SECP registration forms (Company Profile, BOD Resolution, GR/security
      clearance for foreign nationals, document checklist) and the unrelated blank
      "Security Clearance Form for Directors of Security Co." — none add knowledge value.
      **Lesson for future large ingests:** reading/writing many individual files through
      the connected project folder from here is slow and inconsistent (likely
      OneDrive/cloud-sync related) — for bulk transfers, use `robocopy`/`xcopy` run
      natively by the user, then handle renaming (fast, metadata-only) and
      verification/logging from here.
- [ ] World Bank CSVs in `raw_market/historical_datasets/worldbank/` are Tier 3
      (international) sourced for Pakistan-specific macro facts (GDP, inflation,
      unemployment) — Section 5 prefers Tier 1 (Pakistan Bureau of Statistics, Ministry of
      Finance) for this. Kept as an interim source; replace with a Tier 1 source when
      available. Note this caveat in the MANIFEST.md entry once it's written.
- [ ] 2025-05-19.pdf in `data/unstructured/psx_announcements/daily_announcements/` is
      byte-identical to 2025-03-19.pdf — likely a genuine upstream data error (same report
      saved under two dates). Only 2025-03-19.pdf will be copied into the repo; noting the
      anomaly here rather than silently dropping it.
- [ ] CSV/JSON files intentionally kept out of Git LFS (current max ~300KB, total ~9MB).
      Revisit only if a future source produces individual files in the multi-MB range
      (e.g. intraday/tick data instead of daily).
