# Data provenance

| Component | Source | In this package | Condition |
|---|---|---|---|
| Controlled fixtures (S1) | Designed by the authors | Yes | — |
| Scorer verdicts (all studies) | Produced by running the pinned scorers | Yes | — |
| Corpus index (IDs and field hashes) | Derived from the corpus | Yes | — |
| Corpus records, 464 BIRD-derived | BIRD train (`works_cycles`), CC BY-SA 4.0; Cypher by the project | Yes (`corpus/`) | BIRD attribution; CC BY-SA 4.0 |
| Corpus records, 99 project-written | Five contributors (questions and SQL); Cypher by the project | Yes (`corpus/`) | Contributors' authorization (see below) |
| Model-output pairs (S2) | Pinned open-weight models; embed corpus rows | Yes (`model_outputs/`) | Model licences: Qwen3-4B Apache-2.0, Phi-3.5-mini-instruct MIT |
| CypherTurn, Mind the Query cases | Third-party benchmarks | No (rebuilt from source) | Fetched at pinned commits |
| Scorer code | Third-party repositories | No | Fetched at pinned commits |
| LLM reasoning traces, contributor identities, internal records | — | Never | Not released |

**Further provenance:**
- **Field-level provenance:** `provenance/corpus_field_provenance.csv`.
- **Mirror matching:** 383 BIRD-derived records match the official BIRD train release exactly. 81 match its full
  training file, checked against a public mirror.
- **Cypher authoring:** the authoring process of the Cypher translations could not be reconstructed from the available
  records. All 563 were validated by execution against the SQL results.

**Contributor authorization.** The 99 project-written records were created by a five-member annotation team. The
team leader has authorized the authors to use, publish, cite, adapt and redistribute the team's contributions for this
research, and the contributing annotators have agreed (authorization reported by the authors, 2026-11-07). This
authorization covers the contributors' own material only; it does not extend to BIRD or any other third-party source,
whose terms are listed in `ATTRIBUTION.md` and `THIRD_PARTY_NOTICES.md`.

**Subset note.** On the 464 BIRD-derived records alone, the post-hoc six-scorer result changes from 5/15 to 1/15
qualifying scorer pairs, with 21/464 non-unanimous. Any use of that subset must report this.
