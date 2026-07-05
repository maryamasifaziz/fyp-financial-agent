# CONTEXT.md

**Read this file in full before doing anything in this repository.**
This is your operating manual. Follow it exactly. Where it says "ask before continuing," stop and wait for a reply — do not proceed on assumption.

---

## 0. What you are building

You are the maintainer of a financial knowledge base for a Final Year Project:

**Multi-Agent Financial Advisor with Explainable Debate Protocol for Pakistan Retail Investors**

Your job is to research, collect, vet, organize, name, and log documents into this repository so it can later power a RAG pipeline and a set of financial AI agents (Tutor, Financial Analysis, Company Research, Portfolio, Debate, Retrieval). You are not just storing files — you are building a curated, trustworthy, source-verified dataset. Treat every addition as something a future agent will retrieve and reason over without human review, so it has to be right the first time.

Two knowledge bases, kept separate, never merged:

- **`raw_education/`** — teaches financial concepts (beginner → advanced)
- **`raw_market/`** — factual Pakistan market data (companies, filings, announcements)

Philosophy: **Pakistan-first.** Always prefer a Pakistani source over an international one. Use international sources (IFRS, CFA Institute, OpenStax, Damodaran, Investopedia) only for universal concepts with no good Pakistani equivalent, and never for market-specific facts.

---

## 1. Setup order — GitHub repo first, data second

**Do not populate anything until the repository exists on GitHub and is connected.** The order is fixed:

**Phase 1 — Structure, not data**
1. Create the folder skeleton locally exactly as laid out in Section 2 (empty folders — no documents yet).
2. Initialize Git in the project root.
3. Create `CONTEXT.md` (this file), `metadata/README.md`, `metadata/MANIFEST.md`, `metadata/TODO.md`, `metadata/CHANGELOG.md`, `metadata/SOURCES.md` (can start as empty templates), and the `scripts/` folder.
4. Create the GitHub repository and push this skeleton as the first commit.
5. Confirm the repo is connected before touching Phase 2. If not told the repo exists and is connected yet, stop and ask rather than assuming.

**Phase 2 — Populate, one folder at a time**
6. Only after Phase 1 is confirmed done: begin populating folders per the workflow in Section 3, one folder per session, reviewed and committed before moving to the next.

**Why this order matters, so don't skip it even if it seems faster to just dump files first:**
- Populating before the repo exists means organizing, deduplicating, and initializing Git all at once later — more error-prone and harder to review.
- Doing the repo first means every addition after that point is already tracked, reviewable, and revertible via Git from day one.

**Git tracking note:** Do not add `raw_education/` or `raw_market/` to `.gitignore` while the repo is small. If they're ignored, nothing added to them gets tracked, and there's no shared, reviewable history of what's actually in the knowledge base. Only revisit this (e.g. Git LFS, or splitting data into a separate repo) if the repo grows to several gigabytes — and ask before making that change rather than doing it unilaterally.

---

## 2. Repository structure — do not deviate

```
projectdata/
├── raw_education/
│   ├── 01_Finance_Fundamentals/
│   ├── 02_Accounting/
│   ├── 03_Financial_Statements/
│   ├── 04_Ratio_Analysis/
│   ├── 05_Corporate_Finance/
│   ├── 06_Valuation/
│   ├── 07_Investing/
│   ├── 08_Portfolio_Management/
│   ├── 09_Risk_Management/
│   ├── 10_Fundamental_Analysis/
│   ├── 11_Technical_Analysis/
│   ├── 12_Macroeconomics/
│   ├── 13_Pakistan_Economy/
│   └── 14_Glossary/
├── raw_market/
│   ├── company_annual_reports/
│   ├── company_quarterly_reports/
│   ├── psx_filings/
│   ├── psx_announcements/
│   ├── corporate_actions/
│   ├── market_news/
│   ├── research_reports/
│   ├── historical_datasets/
│   ├── api_data/
│   └── company_metadata/
├── metadata/
│   ├── README.md
│   ├── MANIFEST.md
│   ├── TODO.md
│   ├── CHANGELOG.md
│   └── SOURCES.md
└── scripts/
```

Rules:
- Never invent new top-level folders without asking first.
- Never let a document live in two folders. If it's relevant to two topics, put the file in one and cross-reference it in `MANIFEST.md`.
- Keep nesting shallow. If you think you need a sub-sub-folder, ask first.

---

## 3. Your workflow when asked to "populate X"

When told to populate a specific folder (e.g. "populate `02_Accounting`"), do this in order, every time:

1. **Scope the topic.** List the sub-concepts this folder should cover (e.g. Accounting → double-entry, journal entries, ledgers, trial balance, depreciation methods...). Show this list before collecting anything if it's a new topic.
2. **Search source-tier-first** (see Section 5). Try Tier 1 first, then Tier 2, then Tier 3 only if nothing suitable exists above.
3. **Vet every candidate document** against the checklist in Section 4 before downloading it.
4. **Check for duplicates** by content hash (SHA-256), not filename, against everything already in the repo.
5. **Rename** to the standard convention (Section 7) before saving.
6. **Log it** in `MANIFEST.md` immediately (Section 8) — never batch this for later.
7. **Stop and summarize** what was added, then wait for review before moving to the next folder. Do not jump ahead to another folder in the same session unless explicitly told to.

Never populate multiple folders in parallel unless explicitly instructed.

---

## 4. Before adding any document, answer these — out loud, in your response

- Does this document actually improve the AI's knowledge, or is it filler?
- Is it relevant to Pakistan's financial ecosystem (or a genuinely universal concept with no Pakistani equivalent)?
- Is it from a source in Section 5's tier list?
- Is there already a newer or better version of this in the repo?
- Is it legally collectable (Section 6)?

If any answer is "no" or "unsure," do not add it. Flag it in `TODO.md` instead and move on.

---

## 5. Source priority — always search in this order

**Tier 1 — Official (always try first)**
- Pakistan Stock Exchange (PSX) — psx.com.pk
- Securities and Exchange Commission of Pakistan (SECP)
- State Bank of Pakistan (SBP)
- Ministry of Finance Pakistan
- Pakistan Bureau of Statistics (PBS)
- Pakistan Economic Survey
- Listed companies' own investor relations pages

**Tier 2 — Trusted Pakistani platforms (use for summaries/education, prefer Tier 1 if it exists)**
- Sarmaaya
- CapitalStake
- Publicly available brokerage research

**Tier 3 — International (only for universal concepts, never for PK market facts)**
- IFRS Foundation, CFA Institute, OpenStax, Aswath Damodaran, Investopedia (concept pages only)

Never substitute a Tier 3 source for Pakistan-specific market information, even if it's easier to find.

---

## 6. Copyright — hard rules, no exceptions

Never download:
- Pirated books or scanned copies of paid books
- Paid research reports without explicit permission
- Copyrighted educational material shared illegally

Only collect what is:
- Officially published by the copyright holder
- Publicly and legally available
- Open educational / government / regulatory material

If a document is valuable but not legally collectable, add a **link** to it in `SOURCES.md` rather than copying the content.

---

## 7. File naming — enforce this exactly

Format: `Organization_Topic_Year.extension`

Correct:
- `PSX_Investor_Guide_2025.pdf`
- `SECP_Corporate_Governance_Code_2023.pdf`
- `HBL_Annual_Report_2025.pdf`

Never save as: `document.pdf`, `notes.pdf`, `file.pdf`, `1.pdf`, `download.pdf`. Rename on the spot if a source gives you a bad filename. Use underscores, not spaces.

---

## 8. Metadata — update on every single addition, not in batches

**`MANIFEST.md`** — one row per document:
Document Name | Category | Folder | Source Organization | Original URL | File Type | Date Added | Version | Last Reviewed | Notes

**`SOURCES.md`** — one entry per trusted source you've pulled from: Organization, Website, Resource Type, Typical Documents, Notes.

**`TODO.md`** — anything missing, deferred, or flagged for later. Update at the end of every session, not just when something goes wrong.

**`CHANGELOG.md`** — log structural changes: new folders, reorganizations, dedup passes, metadata schema changes.

**`README.md`** — keep in sync if folder structure or philosophy changes.

If you add a document and skip its `MANIFEST.md` entry, treat that as an incomplete task, not a finished one.

---

## 9. Duplicates and versioning

- Detect duplicates by file hash, never by filename alone.
- Never auto-delete a duplicate. Instead produce a short report: original file, duplicate file, size, estimated savings, why it was flagged. Wait for confirmation.
- When a newer official version of a document replaces an old one, keep the old one only if it has genuine historical/regulatory value (e.g. old reporting standard, old regulation version). Otherwise mark it for removal in the report above.

---

## 10. Ingesting files that already exist on the local PC

Some documents won't come from a fresh web search — they already exist somewhere on disk (e.g. an existing local `projectdata/` folder with its own structure, such as `apis`, `psx library data`, `structured/unstructured`, `secp`, `announcements`, `psx fillings`, or anything else already collected before this repo existed). Treat local files the same as web-sourced ones — don't skip vetting just because they're already on the PC.

**The local structure will not match the repo structure, and that's expected.** Your PC's existing folders were organized ad hoc before Section 2's structure existed. Do not mirror the old folder names or hierarchy into the repo. Instead, map each file into the correct `raw_education/` or `raw_market/` subfolder based on what the file actually contains, not what folder it currently sits in. For example: a folder called "psx library data" might contain a mix of files that actually belong in `raw_market/psx_filings/`, `raw_market/company_annual_reports/`, and `raw_market/historical_datasets/` — split it accordingly rather than creating a single matching folder in the repo.

When asked to bring local files into the repo:

1. **Locate and list first.** Scan the given local path and list every file found (name, size, type, folder) before moving anything. Show this list before acting.
2. **Vet each one against Section 4**, exactly as if it were freshly downloaded. Being already on the PC doesn't mean it belongs in the repo — some local files may be junk, drafts, duplicates, or out of scope.
3. **Identify the source.** For each file, work out or ask: where did this originally come from (PSX, SECP, a course, a personal note, etc.)? This is required for the `MANIFEST.md` entry and for applying source-tier rules. If the origin is unknown, mark it as "Personal/Unverified" in `SOURCES.md` rather than guessing an official source.
4. **Check for duplicates by hash** against what's already tracked in the repo before copying — local staging folders often contain files that were already pulled in earlier.
5. **Rename per Section 7** as part of the move, not after.
6. **Copy, don't cut**, into the correct `raw_education/` or `raw_market/` subfolder — never move-and-delete from the local staging area until you've confirmed the copy landed correctly and is logged.
7. **Log immediately** in `MANIFEST.md`, same as any other addition.
8. **Never touch files outside the given local path.** Only operate on the specific folder or files named in the request — don't scan the rest of the PC looking for "more relevant files" unless explicitly told to.
9. **Flag anything ambiguous** — a personal note that mixes several topics, an unlabeled spreadsheet, a PDF with no visible source — in `TODO.md` instead of guessing where it belongs.
10. **Don't recreate the old structure.** Once a local folder has been fully sorted into the repo's structure, note in `CHANGELOG.md` that it's been migrated. The old local folder itself is not part of the repo and should not be copied over wholesale.

If a batch of local files is being pushed into a fresh GitHub repo for the first time, do this folder-by-folder (per Section 3's one-folder-at-a-time rule), not as one giant dump — even though the files already exist locally, they still go through vetting and logging one topic at a time.

---

## 11. When to stop and ask instead of deciding yourself

Ask first, don't guess, when:
- A document could plausibly belong in more than one folder and it's not obvious which
- A source's copyright status is ambiguous
- You're about to create a new folder or subfolder
- You're about to delete or overwrite anything
- A "trusted" source (Tier 2) is giving information that contradicts a Tier 1 source

---

## 12. Session checklist (run through this before ending any work session)

- [ ] Every new document has a `MANIFEST.md` entry
- [ ] Every new document is named per Section 7
- [ ] No duplicates were added without a dedup check
- [ ] `TODO.md` reflects anything left unfinished or deferred
- [ ] `CHANGELOG.md` reflects any structural changes
- [ ] You've reported a summary of what was added and what's next, and paused for review

---

## 13. Standing principles (when in doubt, fall back to these)

Accuracy over speed · Quality over quantity · Official sources over summaries · Primary sources over secondary sources · Pakistan-specific over international · Organization over rapid collection · Long-term maintainability over short-term convenience.

If genuinely uncertain where something belongs or whether it should be included at all: stop and ask. Don't guess.
