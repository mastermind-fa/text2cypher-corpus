# Text-to-Cypher Works-Cycles corpus and scorer-audit data

**Version:** 1.0.0 · **Repository:** https://github.com/mastermind-fa/text2cypher-corpus · **Data licence:** CC BY-SA 4.0
(https://creativecommons.org/licenses/by-sa/4.0/; `LICENSE`, scope in `DATA_LICENSE.md`) ·
**Companion paper:** *What Counts as Correct? A Cross-Implementation Audit of Execution Accuracy in Text-to-Cypher* (under review, ICDE 2027) · **Code:** https://github.com/mastermind-fa/text2cypher-scorer-audit-artifact (Apache-2.0)

## 1. What this is
The corpus underlying the paper's corpus-level and model-output analyses, together with the controlled fixtures and the
frozen verdicts of every audited scorer. The corpus is 563 natural-language questions over the `works_cycles` database,
each with a gold SQL query, a gold Cypher translation over a property-graph version of the same database, and the stored
result rows of both. **It is an evaluation resource.** It was built to study how execution-accuracy scorers judge
result pairs; it is not a training set (see section 9 before using it to train).

## 2. Origin
- **464 records (`R-A`, `R-B`):** questions and SQL from the BIRD training split, `works_cycles` database (Li et al.,
  NeurIPS 2023; CC BY-SA 4.0, https://bird-bench.github.io/). 383 match BIRD's official training release exactly
  (`R-A_bird_official_exact`); 81 match BIRD's full training file exactly, checked against a public mirror
  (`R-B_bird_mirror_exact`).
- **99 records (`R-C_project_written`):** questions and SQL written for this project by a five-member annotation team
  (pseudonyms A1–A5; 20/20/19/20/20 records).
- **All 563 Cypher translations:** produced by the project and its annotation team; see section 5.
- **Stored outputs:** produced by executing each SQL query on the SQLite database and each Cypher query on the graph.

## 3. Composition (verified counts)
| File | Records | Content |
|---|---:|---|
| `corpus/records_release_candidate.jsonl` | 563 | The corpus (562 distinct questions; one question occurs twice, WC-531 and WC-542) |
| `corpus/s3_pairs.jsonl` | 563 | The corpus as scorer inputs: gold Cypher result as reference, gold SQL result as candidate (study S3) |
| `model_outputs/s2_pairs.jsonl` | 158 | Zero-shot predictions of Qwen3-4B (82) and Phi-3.5-mini-instruct (76) on 111 distinct questions, executed and paired with the gold-Cypher result (study S2); 117 predictions return empty results |
| `model_outputs/s2_not_scored_units.json`, `PAIRS_MANIFEST.json` | — | Units not scored (non-executing predictions) and the pair-building manifest with source hashes |
| `splits/record_splits.csv` | 563 | Split membership per record (section 9) |
| `indexes/corpus_index.csv` | 563 | SHA-256 of every field of every record |
| `controlled_cases/` | 121 | Controlled fixtures (study S1), original and query-consistent corrected versions |
| `verdicts/` | — | Frozen verdicts of every scorer for S1, S2, S3, S18, S20, S23 (one row per unit, one column per scorer) |
| `third_party_sources/` | — | Pinned descriptions of the benchmarks and scorers that are fetched, not included |

Empty results: 9 records have an empty `sql_output` and 9 an empty `neo4j_output`.

## 4. The annotation team
The 99 `R-C` records (WC-464–WC-562) were written by a five-member annotation team led by a senior project member.
The team leader authorized the authors to use, modify, publish and redistribute the team's contributions, and the
annotators agreed (owner declaration, 2026-11-07). Annotators are identified only by pseudonym; their real names,
difficulty labels, paraphrases and notes are not released.

## 5. SQL-to-Cypher translation
Each SQL query was translated into Cypher over the graph described in section 7. A record
entered the corpus only when its Cypher result matched its SQL result under the corpus validation comparator
(`cypher_okay` is true for all 563). The internal records also hold LLM-generated SQL-to-Cypher derivation traces,
so the translation was at least partly LLM-assisted; the exact per-record process (manual, assisted or both) is not
documented. Those traces are not released.

## 6. Fields (`corpus/records_release_candidate.jsonl`)
`record_id` (WC-000…WC-562) · `s3_case_id` · `provenance_class` · `db_id` · `question` · `SQL` · `cypher` ·
`sql_output` (rows from SQLite) · `neo4j_output` (rows from Neo4j) · `cypher_okay` · `annotator` (pseudonym, `R-C` only).
Schema: `corpus/schema.json`; field provenance: `corpus/provenance.csv`, `provenance/corpus_field_provenance.csv`.

## 7. Database dependencies
- **SQL side:** the `works_cycles` SQLite database from BIRD's training archive (https://bird-bench.github.io/). It
  appears to be based on Microsoft's AdventureWorks sample (fictitious data). It is **not included**; obtain it from
  BIRD.
- **Cypher side:** a property graph converted mechanically from that database: every table row becomes a node labelled
  with its table name, every column a property, and every foreign key a relationship with a semantic type name
  (88 foreign keys, 71 relationship types; 64 populated labels and 70 instantiated types, because `Customer` is empty);
  BLOB columns are dropped. **The conversion script is not included in this release** (its authorship and licence
  are not documented), so re-executing the Cypher queries requires rebuilding the graph from this description.
- **Reproducing the paper does not require either database:** every scorer compares the stored result rows.

## 8. Execution verification and its limits
`cypher_okay = true` means the Cypher and SQL results matched on this one database instance under the corpus
validation comparator. **It is not proof that a translation is semantically equivalent to its SQL query, nor that
either query is a correct reading of the question.** Single-instance agreement can hide semantic defects (for example
queries that differ only on data absent from this instance), and the paper shows that released scorers disagree about
whether many of these pairs match at all (six-scorer non-unanimity on 41 of 563 pairs). Treat the gold queries as
execution-checked references, not as verified ground truth.

## 9. Splits and leakage
`splits/record_splits.csv` records, for every record, membership in the historical model-ready splits (exact question
match; 1 = member):
- `val_99`: the 99 `R-C` records (an expert-written evaluation set);
- `goldonly_train_371` / `goldonly_test_93`: an 80/20 split of the 464 BIRD-derived records (`random.Random(42)`);
- `mixed_train_gold` (395) / `mixed_test_gold` (69): where the same 464 records sit inside the mixed splits, which also
  contain about 40,000 Neo4j Labs public-corpus examples (**not included**).

**Leakage rule:** never train on the mixed training split and evaluate on `goldonly_test_93`. All 93 of those records
are in the mixed training split. Valid recipes: mixed train → mixed test and `val_99`; or gold-only train → gold-only
test and `val_99`. `val_99` is disjoint from all four. The paper's analyses use no split: they score fixed pairs.

## 10. Licence and attribution
- **Data:** CC BY-SA 4.0 (https://creativecommons.org/licenses/by-sa/4.0/). BIRD-derived questions and SQL remain
  BIRD's material under BIRD's CC BY-SA 4.0 licence; this release adapts them (Cypher translations, executed outputs,
  removed fields) and redistributes the adaptation under the same licence, as ShareAlike requires. See `ATTRIBUTION.md`
  and `DATA_LICENSE.md`.
- **Code:** the analysis and reproduction code is in the artifact repository under Apache-2.0; this data licence does not
  apply to it.
- **No claim** is made to BIRD's or any other third party's material.

## 11. Citation
Cite the paper and this dataset (`CITATION.cff`), giving the release tag. This repository is the canonical release of
the corpus and of the frozen verdicts. An earlier verdict-only snapshot on Kaggle (*Text-to-Cypher Execution-Accuracy
Scorer Audit*, version 1.0.0-rc.2) is not the corpus and is not needed for reproduction.

## 12. Not included
CypherTurn content; Mind the Query questions, result rows and graph dumps; scorer source code; the `works_cycles`
database files; the Neo4j Labs public-corpus examples; the graph-conversion script; LLM reasoning traces; BIRD evidence
hints; annotator names, paraphrases, difficulty labels and notes; raw model generations (only the executed pairs are
released). See `THIRD_PARTY_NOTICES.md` and `FETCH_AND_RECONSTRUCT.md`.
