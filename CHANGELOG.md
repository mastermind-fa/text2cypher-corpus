# Changelog

## 1.0.1 — 2026-11-07
- Metadata-only release: `CITATION.cff` lists the five authors of the paper (with ORCID iDs where supplied) instead of
  a collective entry; `VERSION` and this changelog updated. No corpus record, result pair, verdict, split or index
  changed; every data file is byte-identical to 1.0.0 (compare `hashes/SHA256SUMS`).

## 1.0.0 — 2026-11-07
- First public release. Adds the 563-record corpus (`corpus/`), the S3 and S2 result pairs, and per-record split
  membership (`splits/`) to the controlled fixtures, frozen verdicts, corpus index and provenance of the private
  pre-release (1.0.0-rc.1).
- Licensed under CC BY-SA 4.0 (`LICENSE`, `DATA_LICENSE.md`).
