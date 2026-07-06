# Sources

One entry per trusted source pulled from. Add an entry the first time a source is used,
not per-document.

| Organization | Website | Resource Type | Typical Documents | Notes |
|---|---|---|---|---|
| Pakistan Stock Exchange (PSX) | psx.com.pk | Tier 1 — official exchange data & publications | Per-ticker price history, index constituents, sector lists, daily announcement sheets, company annual/quarterly filings, rule book, investor guides | Primary source for this repo |
| World Bank | data.worldbank.org | Tier 3 — international | Pakistan GDP, inflation, unemployment time series | **Interim only** for Pakistan-specific macro facts — see TODO.md, replace with PBS/Ministry of Finance |
| TwelveData | twelvedata.com | Market data API | PKR/USD daily FX rate | Cross-check source alongside Yahoo Finance |
| Yahoo Finance | finance.yahoo.com | Market data API | PKR/USD daily FX rate | Cross-check source alongside TwelveData |
| CapitalStake | capitalstake.com | Tier 2 — trusted Pakistani platform | (none collected yet — local staging folder was empty) | Listed in Section 5 Tier 2; revisit once actual data is sourced from them |
| Securities and Exchange Commission of Pakistan (SECP) | secp.gov.pk | Tier 1 — official regulator | Adjudication orders, circulars | Source folder on disk (secp/) was mislabeled/mixed quality — see TODO.md for excluded items |
| AHL Research (Arif Habib Limited) | arifhabibltd.com | Tier 2 — brokerage research | Market performance reviews, daily news highlights | |
| JS Research (JS Global) | js.com | Tier 2 — brokerage research | Daily technical analysis | |
| Central Depository Company (CDC) / National Clearing Company (NCCPL) | cdcpakistan.com / nccpl.com.pk | Tier 1 — official market infrastructure | Co-published with PSX (e.g. Investor Awareness Guide) | |

## Source tiers (CONTEXT.md Section 5)

**Tier 1 — Official (always try first):** PSX (psx.com.pk), SECP, SBP, Ministry of Finance
Pakistan, Pakistan Bureau of Statistics, Pakistan Economic Survey, listed companies' own
investor relations pages.

**Tier 2 — Trusted Pakistani platforms:** Sarmaaya, CapitalStake, publicly available
brokerage research.

**Tier 3 — International (universal concepts only, never PK market facts):** IFRS
Foundation, CFA Institute, OpenStax, Aswath Damodaran, Investopedia (concept pages only).
