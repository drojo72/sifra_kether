# Sifra Kether — Architecture Overview

## Design Principles

1. **Editorial-first**: The database and API serve the editorial workflow, not the other way around
2. **Canonical root**: The biblical text is the immutable node zero
3. **Transversal integrity**: All cross-domain relations pass through the Entity Registry
4. **Traceable ingestion**: Every piece of data has a provenance chain: source -> batch -> job -> raw -> staging -> publish
5. **Semantic search**: Vector embeddings are first-class citizens, not an afterthought
6. **Privacy by design**: Editorial layer is isolated via Row-Level Security

## Repository Structure

```
sifra_kether/              (this repo — umbrella)
├── docs/                  Architecture decisions, cross-project docs
├── README.md
├── LICENSE
└── CONTRIBUTING.md

sifra_kether-api/          (backend)
├── database/
│   ├── schema/            Canonical SQL schema
│   ├── migrations/          Versioned migrations
│   ├── seeds/             Seed data
│   └── functions/         Stored procedures
├── src/
│   ├── api/               REST API endpoints
│   ├── ingest/            Pipeline: source -> batch -> job -> raw -> staging
│   ├── search/            Full-text + vector search
│   ├── auth/              Authentication & RLS context
│   └── models/            Domain models
├── tests/
└── docker/

sifra_kether-web/          (frontend)
├── src/
│   ├── reader/            Public text reader
│   ├── editor/            Editorial interface
│   ├── admin/             Admin dashboard
│   └── components/        Shared UI
├── public/
└── tests/

sifra_kether-mobile/       (mobile app)
├── src/
│   ├── reader/
│   ├── audio/             Text-to-speech, audio studies
│   └── offline/           Sync and cache
└── tests/

sifra_kether-branding/     (brand assets)
├── logo/
├── guidelines/            Brand manual
├── ui-kit/                Design system
└── editorial/             Publication templates
```

## Technology Stack

| Layer | Technology |
|-------|-----------|
| Database | Neon PostgreSQL (serverless) |
| Extensions | pgvector, pg_trgm |
| Backend API | FastAPI or similar |
| Search | pgvector HNSW + PostgreSQL full-text |
| Semantic layer | RDF triples in PostgreSQL |
| Frontend | SvelteKit or Astro |
| Mobile | React Native or Flutter |
| Hosting | Cloudflare Pages (static), Render/Vercel (API) |
| Assets | Cloudflare R2 / S3 |

## Database Architecture

See [database.md](database.md) for the complete schema documentation.

Key concepts:
- **Entity Registry**: Central registry of all domain entities
- **Schemas**: canon, tradition, parallel, symbol, editorial, ingest
- **Pipeline**: source -> batch -> job -> raw_data -> staging -> publish
- **Embeddings**: Linked to registry, searchable via HNSW
- **RDF**: Lightweight semantic triples for graph traversal

## API Design

- RESTful, resource-oriented
- Versioned: `/v1/`
- Content negotiation: JSON default, optional RDF/Turtle
- Authentication: JWT with RLS context
- Rate limiting per endpoint

## Deployment

- Neon PostgreSQL: production database with branching for dev/staging
- GitHub Actions: CI/CD for all sub-projects
- Branch protection on `main`
- Automated tests on PR

## Brand Alignment

All sub-projects must follow the Sifra Kether brand guidelines:
- Color palette: #16263F (midnight), #A97A42 (copper), #F7F5F0 (ivory), #404040 (graphite), #CFCFCB (stone)
- Typography: Editorial serif system (Times Modern lineage)
- Philosophy: Text is the protagonist. Copper is symbolic accent (5-10%). Blue is knowledge. Ivory is space to think.

See [Sifra_Kether-branding](https://github.com/keysign-labs/Sifra_Kether-branding) for full guidelines.
