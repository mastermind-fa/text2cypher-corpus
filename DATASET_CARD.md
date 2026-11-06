# Dataset card

## Summary
The dataset holds evaluation units and frozen verdicts of seven released Text-to-Cypher execution-accuracy scorers
(plus two secondary comparators).

| Code | Layer | Units | Content in this package |
|---|---|---:|---|
| S1 | Controlled fixtures | 121 | Fixtures (original and corrected) and verdicts. Labels: 57 equivalent, 49 not equivalent, 15 intent-dependent |
| S3 | Corpus pairs (Works-Cycles, from BIRD and project contributors) | 563 | Records, pairs, verdicts and index |
| S2 | Model-output pairs (Qwen3-4B, Phi-3.5-mini-instruct; zero-shot) | 158 | Pairs and verdicts |
| S18 | CypherTurn equivalence-preserving rewrites | 60 | IDs and verdicts; cases are rebuilt from CypherTurn |
| S20 | CypherTurn policy stress suite | 62 | IDs and verdicts; cases are rebuilt from CypherTurn |
| S23 | Mind the Query replication | 77 | IDs and verdicts; cases are rebuilt from Mind the Query |

## Intended uses
- Reproducing and auditing the paper's numbers.
- Testing a new result-equivalence scorer against the controlled fixtures.
- Applying the Reporting Card.

## Out-of-scope uses
- Training or fine-tuning Text-to-Cypher models.
- Ranking models.
- Treating an acceptance as proof of semantic equivalence.

## Known limitations
- **Intent-dependent fixtures:** 15 controlled fixtures have no single correct label.
- **Judgment type:** corpus and model-output judgments are one-instance result comparisons.
- **Provenance:** 81 BIRD-derived records were matched against a public mirror of BIRD train, not the official
  archive.
- **Cypher translations:** their authoring process could not be reconstructed from the available records. All were
  validated by execution against the SQL results.
- **CypherTurn rebuilds:** verdict-level, not byte-level.
- **Upstream licences:** several upstream repositories state no licence; their content is never included.

## Personal and sensitive information
- **Names:** contributors appear only as pseudonyms.
- **Excluded:** LLM reasoning traces and internal workflow fields.
- **Works-Cycles data:** the database is the AdventureWorks sample; its people and contact details are fictitious.

## Maintenance
Errata are released as new versions with a changelog entry. Released verdict files are never edited.
