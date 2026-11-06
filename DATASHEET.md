# Datasheet

## Motivation
To measure whether released Text-to-Cypher execution-accuracy scorers agree on the same result pairs, and to identify
the result-equivalence choices that cause disagreement.

## Composition
- **Instances:** result pairs, each with one verdict per scorer.
- **Labels:** S1 has designed labels. S18, S20 and S23 have rule-assigned equivalence classes. S2 and S3 have no gold
  label; the paper measures agreement on them.
- **Missing data:** in S3, 9 pairs have an empty reference result and 9 an empty candidate result. In S2, 117 of 158
  predictions return empty results.

## Collection
- **S1:** designed by the authors (deterministic builder).
- **S3:**
  - Questions and SQL come from BIRD train (`works_cycles`) for 464 records, and from five contributors for 99.
  - The Cypher queries target a graph converted from the same database. Their authoring process could not be
    reconstructed from the available records; every query was validated by execution against the SQL result.
- **S2:** one zero-shot generation per question with pinned open-weight models.
- **S18, S20, S23:** frozen rules applied to public benchmark queries, executed in a throwaway Neo4j 5.15.0 container,
  hashed before scoring.

## Preprocessing
Adapters convert each pair into each scorer's native input. They are frozen and hash-checked in the artifact
repository.

## Uses
See `DATASET_CARD.md`. Do not train on this data.

## Distribution
- **Channel:** a public GitHub repository (planned).
- **Licence:** CC BY-SA 4.0 (`LICENSE`, scope in `DATA_LICENSE.md`).
- **Third-party material:** fetched, never redistributed.

## Maintenance
Versioned releases with a changelog.
