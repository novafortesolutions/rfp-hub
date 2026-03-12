# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.0] - 2026-03-12

### Added

- Prisma schema with models: Rfp, Program, Publisher, Requirement, EvaluationCriterion, Deliverable, ChangeRecord
- REST API endpoints:
  - `GET /api/v1/rfps` — List with filtering, search, pagination, sorting
  - `GET /api/v1/rfps/:id` — Single RFP with full relations
  - `GET /api/v1/programs` — List funding programs
  - `GET /api/v1/programs/:id/rfps` — RFPs by program
  - `GET /api/v1/ecosystems` — Ecosystem list with counts
  - `GET /api/v1/stats` — Aggregate statistics
  - `GET /api/v1/schema` — RFP object schema definition with DAOIP-5 mapping
  - `GET /api/v1/export/json` — Full dataset export
- Reference frontend with search, ecosystem/status filters, RFP cards, and detail pages
- Seed data: 13 RFPs across 5 ecosystems (Ethereum, Arbitrum, Gitcoin, Optimism, Starknet)
- CORS headers on all API routes
- Deployed to Vercel with Neon PostgreSQL

[0.1.0]: https://github.com/novafortesolutions/rfp-hub/releases/tag/v0.1.0
