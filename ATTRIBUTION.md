# Attribution

- **BIRD** (Li et al., NeurIPS 2023), `works_cycles` database: questions and SQL of 464 corpus records. Data licence:
  CC BY-SA 4.0, stated on bird-bench.github.io (news entry of 27 April 2024), in the DAMO-ConvAI `bird/README.md`, and
  in the Hugging Face dataset metadata (checked 2026-11-02). The BIRD site adds that the benchmark was developed "for
  research and healthy application only". Changes: Cypher translations, executed outputs and verdicts were added.
  - The licence text says "our data" and does not state explicitly whether it covers the database files.
  - `works_cycles` appears to be based on Microsoft's AdventureWorks sample database (fictitious data). This is a
    project observation; BIRD does not state it. Microsoft's `sql-server-samples` repository is MIT-licensed, but it
    does not state that this licence covers the AdventureWorks data.
  - The database file itself is not included; users obtain it from BIRD.
- **Project contributors:** a five-member annotation team wrote the questions and SQL of 99 corpus records. The team
  leader authorized their use, publication, adaptation and redistribution for this research, and the annotators agreed
  (`DATA_PROVENANCE.md`). They are credited as a group; individual names are not published.
- **Cypher translations:** the project's translations of the SQL queries. How they were authored (manually, with AI
  assistance, or both) is not documented. As adaptations of CC BY-SA material, they would be released under the same
  licence.
- **CypherTurn** (github.com/BarryQ/CypherTurn; no licence file, README: "released for research purposes") and **Mind
  the Query** (github.com/endeavorXx/Mind-the-Query; Apache-2.0, graph-dump licences unverified): benchmark queries and
  graphs used to build native-Cypher cases. These are fetched from the original repositories, not included. Only case
  identifiers and verdicts are published here.
- **Audited scorers:** CypherTurn, CypherBench, GQLBench, Text2GraphQuery-Driver, PIPE-Cypher, CypherLens, CySpider;
  plus neo4j-labs text2cypher (context). Referenced by pinned commit, not included.

The licence of this dataset, CC BY-SA 4.0, applies only to material the authors can license. Third-party material keeps
its own terms.
