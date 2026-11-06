# Corpus records

- `records_release_candidate.jsonl`: the 563 records (fields in `schema.json`; provenance per record in `provenance.csv`).
- `s3_pairs.jsonl`: the same records as scorer inputs (reference = gold Cypher result, candidate = gold SQL result).
- `ATTRIBUTION.md`: attribution for this layer (see also the top-level `ATTRIBUTION.md`).

Every field of every record can be checked against `../indexes/corpus_index.csv` (SHA-256 of the field value; non-string
values are hashed as `json.dumps(value, sort_keys=True, ensure_ascii=False)`). Read the top-level README, sections 8 and
9, before using the records: `cypher_okay` is a one-instance check, and some split combinations leak.
