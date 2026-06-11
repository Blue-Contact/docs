# Blue Contact Docs

This repository is the central documentation hub for **Blue Contact** — a suite of data-ingestion and consumer-matching tools built on AWS.

## What is Blue Contact?

Blue Contact provides infrastructure and tooling for importing, normalizing, and fuzzy-matching consumer contact lists against existing databases. The platform is built primarily on **AWS Glue** and **Apache Spark**, storing results in **Amazon S3** and registering tables in the **AWS Glue Data Catalog** for querying via Amazon Athena.

Core capabilities include:

- **List import** — ingest delimited (CSV, pipe, tab) contact files from S3 with automatic header normalization
- **Fuzzy / phonetic matching** — match incoming records against a consumer database using [rapidfuzz](https://github.com/rapidfuzz/rapidfuzz-python) and [jellyfish](https://github.com/jamesturk/jellyfish) (Levenshtein, Jaro-Winkler, Soundex, Metaphone, etc.)
- **Key-based matching** — match on normalized email addresses, phone numbers, or mailing addresses
- **Parquet output** — write matched results back to S3 and register them as queryable Glue tables

## Repositories

| Repository | Description |
|---|---|
| [Blue-Contact/lscs](https://github.com/Blue-Contact/lscs) | AWS Glue jobs and helper scripts for list import and consumer matching |
| [Blue-Contact/docs](https://github.com/Blue-Contact/docs) | This repository — organization-level documentation |

## Projects

### LSCS (List & Consumer Services)

The [`lscs`](https://github.com/Blue-Contact/lscs) repository contains the Glue ETL jobs that power the matching pipeline:

| Job | Description |
|---|---|
| `glue/list_import_and_match.py` | Import a delimited list from S3 and fuzzy-match each row against a consumer table using name + ZIP blocking |
| `glue/list_import_and_match_keys.py` | Import a delimited list from S3 and match rows against a consumer key table (email, phone, or address keys) |

See the [LSCS README](https://github.com/Blue-Contact/lscs#readme) for full argument references, usage examples, and dependency information.

## Documentation

Additional documentation will be added here as the platform grows. Planned topics include:

- Architecture overview
- Data schema reference
- Deployment and infrastructure guides
- Contribution guidelines
