# Third-party notices (dataset)

This package contains project-produced material and, when the corpus layer is present, BIRD-derived material adapted
under BIRD's licence (`DATA_LICENSE.md`). The third-party sources below were used to
produce it; none of their files are included. The terms were read from each source on 2026-11-02; BIRD was re-checked
on 2026-11-07.

| Source | Terms | What this package holds from it |
|---|---|---|
| BIRD (Li et al., NeurIPS 2023), `works_cycles` | CC BY-SA 4.0 (bird-bench.github.io, news of 27 April 2024; DAMO-ConvAI `bird/README.md`) | Without the corpus layer: record IDs and field hashes only. With it (`corpus/`): the questions and SQL of 464 records, adapted, under CC BY-SA 4.0. Never the database file |
| `works_cycles` database contents | Distributed by BIRD; appears to be based on Microsoft AdventureWorks (project observation; Microsoft's sample repository is MIT-licensed). Whether BIRD's licence covers the database files is not stated | Never the database file. With the corpus layer: the result rows of the 563 queries (query outputs over fictitious sample data) |
| CypherTurn (github.com/BarryQ/CypherTurn) | No licence file; README: "released for research purposes" | Case identifiers and scorer verdicts only |
| Mind the Query (github.com/endeavorXx/Mind-the-Query) | Apache-2.0 (repository); graph dumps from neo4j-graph-examples repositories without a licence file | Question `unique_id`s and scorer verdicts only; no dumps or result rows |
| Audited scorers (CypherTurn, CypherBench, GQLBench, Text2GraphQuery-Driver, PIPE-Cypher, CypherLens, CySpider) | Their own terms; several state no licence | Verdicts produced by running them; no code |

Where a source states no licence, all rights are reserved by its authors, so it is referenced by pinned commit and
fetched by the user (`FETCH_AND_RECONSTRUCT.md`), never redistributed. CC BY-SA 4.0 on this package does not relicense
any of these sources.
