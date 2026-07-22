# Sifra Kether

Sifra Kether is a digital library and editorial platform for sacred texts, Bible Studies, and comparative theological research. It is part of KeySign Labs and follows an editorial-first design philosophy.

## Purpose

Sifra Kether is built to organize, study, and publish sacred texts through a structured system that supports editorial workflows, manuscript and OCR ingestion, commentary, publication-ready outputs, and web, mobile, and API-based access.

## Scope

This project is designed as a cooperative knowledge platform. Contributions, editorial review, and structured data improvements are welcome when they align with the project's textual, editorial, and research standards.

## Architecture

Sifra Kether follows a multi-repository architecture within the KeySign Labs ecosystem:

| Repository | Purpose |
|------------|---------|
| [Sifra_Kether](https://github.com/keysign-labs/Sifra_Kether) | This repo. Umbrella documentation, architecture decisions, and cross-project coordination |
| [Sifra_Kether-api](https://github.com/keysign-labs/Sifra_Kether-api) | Backend API, database schema, ingest pipeline, search engine, authentication |
| [Sifra_Kether-web](https://github.com/keysign-labs/Sifra_Kether-web) | Web frontend, editorial interface, public reader, admin dashboard |
| [Sifra_Kether-mobile](https://github.com/keysign-labs/Sifra_Kether-mobile) | Mobile application (iOS/Android), offline reading, audio features |
| [Sifra_Kether-branding](https://github.com/keysign-labs/Sifra_Kether-branding) | Brand identity, logo assets, style guides, editorial design system |

## API

Sifra Kether exposes a public-facing REST API for structured access to texts, metadata, studies, and related editorial assets.

API documentation lives in the [Sifra_Kether-api](https://github.com/keysign-labs/Sifra_Kether-api) repository.

## Database

The canonical database schema is maintained in `Sifra_Kether-api/database/schema/`.

Current version: **v1.0 beta**

Engine: Neon PostgreSQL with pgvector, full-text search, and RDF triple store.

## Contributions

Contributions are welcome, especially in areas such as:

- Textual metadata and canonical references
- Editorial structures and study schemas
- Manuscript references and OCR pipelines
- API improvements and documentation
- Visual assets and publication workflows
- Comparative theology and parallel texts

Please read the [Contributing Guide](CONTRIBUTING.md) before submitting.

## License

This project is licensed under the Apache License, Version 2.0. See the [LICENSE](LICENSE) file for details.

## KeySign Labs

Sifra Kether is developed within the [KeySign Labs](https://github.com/keysign-labs) ecosystem.

KeySign Labs builds sustainable digital infrastructure for communities of knowledge, faith, and culture.

---

*Sifra Kether — Biblioteca Digital de Textos Sagrados*
