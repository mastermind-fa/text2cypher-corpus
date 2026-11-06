# Release policy: Text-to-Cypher evaluation dataset (v0.1.0 candidate)

**Status: CANDIDATE.** Nothing in this directory has been published. No remote repository exists.
Publication requires the owner actions listed in `LICENSE_STATUS.md` §3.

## 1. Release classes

Every component in `manifests/master_dataset_inventory.csv` has exactly one class.

| Class | Meaning | Where it lives | Condition for publication |
|---|---|---|---|
| **PUBLIC-REDISTRIBUTABLE** | Project-authored material with no third-party content and no personal data: synthetic fixtures, case IDs, scorer verdicts, statistics, preregistrations, equivalence policies, the corpus ID/hash index, the Reporting Card | `public_repo_candidate/` | The owner assigns the project licence (CC BY-SA 4.0). No other permission is needed. |
| **PUBLIC-CONDITIONAL** | Material that may be published only after a named condition is met | `private_staging/` (gitignored) | Per component, see §2 |
| **FETCH-ONLY** | Third-party benchmarks, databases, graphs and scorer code | Not stored here. `third_party_sources/*.json` records URL, commit, licence and use. | Never redistributed. Users fetch from upstream at the pinned commit (the artifact repository's fetch scripts verify hashes). |
| **PRIVATE-ONLY** | Personal data, internal workflow fields, LLM reasoning traces, legacy training splits, pilot annotations | Stays in the research repository | Never released. |

## 2. Conditions for PUBLIC-CONDITIONAL components

| Component | Records | Conditions (all must hold) |
|---|---:|---|
| Works-Cycles corpus (`private_staging/corpus/records_release_candidate.jsonl`) and S3 pairs | 563 | (1) the owner adopts **CC BY-SA 4.0** for the corpus, which BIRD's ShareAlike terms require for R-A/R-B; (2) **written consent from all five R-C annotators** (A1–A5) for their 99 records, or those 99 records are dropped (see §4); (3) the owner confirms how the 563 Cypher translations were authored, for the AI disclosure |
| S2 prediction/reference pairs (`private_staging/model_outputs/s2_pairs.jsonl`) | 158 | Same as the corpus: the pairs embed corpus reference rows |
| Raw frozen predictions (`private_staging/model_outputs/raw_predictions/`) | 504 | Not released. Only the 158 executed predictions analysed in the paper are released, as pairs in `model_outputs/`; the other raw outputs are outside the paper's scope |

## 3. Rules that hold for every release
1. Frozen research files are copied **byte-for-byte**. `build_dataset_release.py` asserts that SHA-256 is unchanged, and `checks/verify_dataset_release.py` re-checks it against the research tree.
2. No third-party content enters `public_repo_candidate/`: no CypherTurn queries, answers or rows; no Mind the Query rows or dumps; no scorer code; no BIRD questions, SQL or database. The verifier scans for content markers.
3. No personal data: no annotator real names, e-mail addresses or chat transcripts. Annotators appear only as A1–A5 (corpus) and A/B (pilot).
4. No LLM reasoning traces (the `reasoning_trace` field and think-tag blocks), API error logs or internal review fields, in any class except PRIVATE-ONLY.
5. Reported paper numbers come from frozen verdicts. A release never re-scores or edits them.
6. `private_staging/` is gitignored. It must never be copied into `public_repo_candidate/` by hand. Promotion happens only by changing the class in the builder after the conditions in §2 are met, then re-running the builder and the verifier.

## 4. Fallback if consent is incomplete
If any R-C annotator does not consent, the corpus can be released as a **464-record BIRD-only subset** (R-A 383 + R-B 81) under CC BY-SA 4.0.

The paper's Table IV numbers are computed on all 563 records. A 464-record release therefore reproduces Table IV only at **R0**, from the frozen verdicts.

**This is not a neutral substitution.** On the 464 BIRD-derived records alone, the post-hoc six-scorer result changes from 5/15 to **1/15** qualifying scorer pairs, with 21/464 non-unanimous (the artifact build release gate). Any release or paper that uses the subset must report this. The subset is not yet built: it requires an owner decision.

## 5. Versioning
- **v0.1.0**: public layer only (controlled suite, verdicts, IDs, corpus hash index, external manifests). Possible as soon as the project licence is chosen.
- **v1.0.0**: adds the corpus, S3 pairs and S2 pairs once §2 conditions hold. It is the version cited by the camera-ready paper.
- Patch versions (`x.y.z`) fix documentation only. Any change to a released data file needs a minor or major bump and a CHANGELOG entry with old and new SHA-256.
