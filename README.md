# Vendor CSV Processing Pipeline

Orchestrated CSV preparation for Concur expense imports — cleans, maps and normalizes distributor files across five clients, ready for upload.

## Situation

Five distributors delivered files in five different shapes into five different site paths. Turning each into a clean Concur expense-import CSV meant per-client manual cleanup — zero rows, property codes, inconsistent headers — every time files landed.

## Task

I designed and built a drop-folder orchestrator with per-client processing rules so new files turn into import-ready CSVs automatically, without touching the originals and without code changes when a site path moves.

## Action

- I wrote a single orchestrator that watches all five drop locations, detects new files, dynamically loads the matching client runner, and logs every run
- I implemented per-client cleanup and mapping rules — dropping zero-amount rows, mapping property codes, stamping the period, and normalizing headers before delivery
- I made every drop and output location fully environment-driven, so a site is configured, not reprogrammed
- I kept originals untouched by writing all processed output to a separate output tree

## Flow (high level)

```
Files land in drop folders -> detect new file
      |
Load matching client runner (one of five)
      |
Clean + map + normalize
      |
Write import-ready CSV (originals untouched) -> log run
```

## Result

Five clients now sit behind one entry point; import-ready CSVs are delivered with no manual cleanup step; originals are never modified; and onboarding a new site or moving a path is a configuration change, not a code change.

---

*High-level overview only — this project is a confidential client engagement; implementation details are not published.*
