# Data licence

**Licence:** Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0). The full legal code is in
`LICENSE`; summary: https://creativecommons.org/licenses/by-sa/4.0/ ; legal code:
https://creativecommons.org/licenses/by-sa/4.0/legalcode (the legal code governs).

**What the licence covers.** Only material in this repository that the authors have the right to license:
- the controlled fixtures (original and corrected);
- the frozen scorer verdicts, statistics and corpus index (record IDs and field hashes);
- the provenance tables and the documentation.

**What it does not cover:**
- **BIRD:** material derived from BIRD remains under BIRD's own CC BY-SA 4.0 licence and must be attributed to BIRD
  (`ATTRIBUTION.md`). The BIRD database file is not included.
- **Third-party benchmarks and scorers:** CypherTurn, Mind the Query, the audited scorers, and any material fetched with
  `FETCH_AND_RECONSTRUCT.md` keep their own terms (`third_party_sources/`). Several of them state no licence; none is
  included here.
- **Corpus records:** the 563 corpus records (`corpus/`) and the model-output pairs (`model_outputs/`) are included and
  covered by this licence as follows. The 464 BIRD-derived questions and SQL queries are BIRD's material under BIRD's
  own CC BY-SA 4.0 licence; this release adapts them (Cypher translations, executed outputs, removed fields) and
  distributes the adaptation under CC BY-SA 4.0, as ShareAlike requires (`ATTRIBUTION.md`). The 99 project-written
  records are licensed with the authorization of their contributors (`DATA_PROVENANCE.md`). Model predictions in
  `model_outputs/` were generated with Qwen3-4B (Apache-2.0) and Phi-3.5-mini-instruct (MIT).
- **Code:** the analysis and reproduction code is released separately, in the artifact repository, under the Apache
  License 2.0. This data licence does not apply to it.

Attribution: see `ATTRIBUTION.md`; third-party sources: `THIRD_PARTY_NOTICES.md`. The licence grants only the rights the licensors hold; it does not grant rights in
material owned by others.
