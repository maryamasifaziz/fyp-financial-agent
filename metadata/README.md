# Financial Knowledge Base — Multi-Agent Financial Advisor (Pakistan Retail Investors FYP)

This repository is the curated, source-verified document store powering a RAG pipeline
for a multi-agent financial advisor system (Tutor, Financial Analysis, Company Research,
Portfolio, Debate, Retrieval agents), built for a Final Year Project focused on Pakistan
retail investors.

Full operating rules for maintaining this repo live in `CONTEXT.md` at the repo root.
Read that file before adding, removing, or reorganizing anything here.

## Structure

- `raw_education/` — financial concepts, beginner to advanced (14 topic folders)
- `raw_market/` — factual Pakistan market data: companies, filings, announcements (10 topic folders)
- `metadata/` — this folder: manifest, sources, changelog, todo, and this README
- `scripts/` — helper scripts (dedup checks, ingestion tooling, etc.)

## Philosophy

Pakistan-first. Official sources (PSX, SECP, SBP, Ministry of Finance, PBS) are always
preferred over trusted Pakistani platforms (Sarmaaya, CapitalStake), which are preferred
over international sources (IFRS, CFA Institute, OpenStax, Damodaran, Investopedia).
International sources are only used for universal concepts with no Pakistani equivalent,
never for Pakistan-specific market facts.

## Status

Repository skeleton initialized. No documents have been added yet — population happens
folder-by-folder per the workflow in `CONTEXT.md` Section 3.
