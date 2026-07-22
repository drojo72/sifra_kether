# Sifra Kether — Database Documentation

## Overview

The Sifra Kether database is designed on Neon PostgreSQL with the following extensions:
- `vector` (pgvector) for semantic search
- `pg_trgm` for trigram text search

## Schema Organization

| Schema | Domain | Access |
|--------|--------|--------|
| `registry` | Entity registry central | Internal |
| `canon` | Biblical texts | Public read |
| `tradition` | Interpretive traditions | Public read |
| `parallel` | Comparative texts | Public read |
| `symbol` | Visual assets | Public read |
| `editorial` | Personal/editorial layer | Private (RLS) |
| `ingest` | Ingestion pipeline | Service only |

## Entity Registry

Every significant entity in the system has a mirror row in `registry.entity`.
This enables cross-domain relationships with real referential integrity.

Auto-registration is handled by triggers on domain tables.

## Ingestion Pipeline

```
source -> batch -> job -> raw_data
                          |
                          v
                       staging -> publish -> domain tables
```

Idempotency is guaranteed by content hashes at each stage.

## Search

Three search modalities:
1. **Full-text**: PostgreSQL tsvector on text content
2. **Semantic**: pgvector HNSW cosine similarity
3. **Hybrid**: Combined ranking with configurable weights

## RDF

Lightweight semantic triples stored in `public.rdf_triple`.
Named graphs per tradition: `rabbinic`, `comparative`, `kabbalistic`, etc.

## Version

Current schema version: **v1.0 beta**

Canonical file: `sifra_kether-api/database/schema/sifra_kether_db_v1_beta.sql`
