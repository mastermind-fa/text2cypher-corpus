# Validation notes

- **Controlled fixtures.**
  - 36 of 121 fixtures received query-consistent query texts: 32 alias-inconsistent, 9 identical-text, 5 in both groups;
    in 16 fixtures a bound variable is renamed.
  - Result rows, labels and classes are unchanged.
  - The 85 unaffected fixtures reproduced every frozen verdict when re-scored.
  - Both versions are included (`controlled_cases/original/`, `controlled_cases/corrected/`), with the per-fixture
    correction manifest.
- **Verdicts.** Every verdict file is frozen. Re-scoring with the pinned scorers through the artifact's adapters
  reproduces them.
- **Hashes.** `hashes/SHA256SUMS` lists every file. `provenance/public_file_provenance.csv` gives each file's SHA-256 and,
  where internal identifiers were normalised for publication, the pre-normalisation SHA-256.
