# Fetching third-party sources and reconstructing excluded layers

- **Third-party sources** (FETCH-ONLY): `third_party_sources/*.json` gives each source's URL, pinned commit, licence and use. The code artifact (https://github.com/mastermind-fa/text2cypher-scorer-audit-artifact) contains the fetch scripts (`third_party/fetch_scorers.sh`, `third_party/fetch_mind_the_query.sh`). They verify SHA-256 against `third_party_sources/EXTERNAL_PINS.json`.
- **CypherTurn and Mind the Query cases:** rebuilt by the artifact's `scripts/full_native.sh`. Mind the Query rebuilds are byte-identical; CypherTurn rebuilds match at verdict level.
- **Works-Cycles database:** download BIRD `train.zip` from https://bird-bench.github.io/ (CC BY-SA 4.0). It is needed only to re-execute stored corpus outputs.
- **Corpus:** in pre-consent mode only `indexes/corpus_index.csv` (IDs and SHA-256 of every field) is included. A reconstructed or later-released corpus can be checked against it.
