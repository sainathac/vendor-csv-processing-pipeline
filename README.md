# Vendor CSV Processing Pipeline

Orchestrated CSV preparation for Concur expense imports — cleans, maps and normalizes distributor files across five clients, ready for upload.

## What it does

A drop-folder orchestrator watches five distributor locations, dynamically loads the matching client runner, processes new files and logs every run — delivering import-ready CSVs to the expense system.

## Flow (high level)

```
Files land in drop folders → detect new file
      ↓
Load matching client runner (one of five)
      ↓
Clean + map + normalize
      ↓
Write import-ready CSV (originals untouched) → log run
```

## Logic

- One orchestrator + five client runners, each with its own cleanup and mapping rules
- All drop/output locations configured through environment variables — no code changes per site
- Processed files are written to a separate output tree; originals are never touched

## Problems solved

- **Five distributors, five file shapes** → per-client runners behind a single entry point
- **Site-specific paths** → fully environment-driven configuration
- **Dirty input rows** → per-client cleaning rules (zero-amount rows, property-code mapping, period stamping, header normalization) applied before delivery

---

*High-level overview only — this project is a confidential client engagement; implementation details are not published.*
