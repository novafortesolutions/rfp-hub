# RFP Hub

Standard RFP object format and public aggregation API for web3 funding opportunities.

RFP Hub aggregates grants, RFPs, bounties, and retroactive funding opportunities from across the web3 ecosystem into a single, searchable, exportable dataset. The schema extends [DAOIP-5](https://daostar.org/daoip-5) (DAOstar Grants Metadata Standard) with RFP-specific fields.

**Live:** [rfp-hub-seven.vercel.app](https://rfp-hub-seven.vercel.app)

## Features

- **Standard RFP object format** — Versioned schema extending DAOIP-5 with fields for deadlines, budgets, requirements, evaluation criteria, and provenance tracking
- **Public REST API** — Unauthenticated, CORS-enabled API with filtering, search, pagination, and sorting
- **Multi-ecosystem** — Ethereum, Arbitrum, Optimism, Gitcoin, Starknet, and more
- **Export** — Full dataset export as JSON with schema version and timestamps
- **Provenance tracking** — Every entry tracks its source, verification status, and change history
- **Reference frontend** — Search, filter by ecosystem/status, and browse RFP details

## API

Base URL: `https://rfp-hub-seven.vercel.app/api/v1`

| Endpoint | Description |
|----------|-------------|
| `GET /rfps` | List RFPs with filtering, search, and pagination |
| `GET /rfps/:id` | Single RFP with requirements, criteria, deliverables |
| `GET /programs` | List funding programs |
| `GET /programs/:id/rfps` | RFPs under a specific program |
| `GET /ecosystems` | Ecosystems with RFP counts |
| `GET /stats` | Aggregate statistics |
| `GET /schema` | RFP object schema definition |
| `GET /export/json` | Full dataset export |

### Filtering

```
GET /api/v1/rfps?ecosystem=Ethereum&status=OPEN&search=zk&sortBy=deadline&sortDir=asc&limit=10
```

**Query parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| `ecosystem` | string | Filter by ecosystem name |
| `status` | enum | `OPEN`, `CLOSED`, `AWARDED`, `DRAFT`, `CANCELLED` |
| `type` | enum | `RFP`, `GRANT`, `BOUNTY`, `RETROACTIVE` |
| `search` | string | Full-text search on name and description |
| `budgetMin` | number | Minimum budget filter |
| `budgetMax` | number | Maximum budget filter |
| `deadlineFrom` | date | Deadline range start |
| `deadlineTo` | date | Deadline range end |
| `tags` | string | Comma-separated tag filter |
| `sortBy` | enum | `deadline`, `createdAt`, `budgetMax`, `name` |
| `sortDir` | enum | `asc`, `desc` |
| `page` | number | Page number (default: 1) |
| `limit` | number | Results per page (default: 20, max: 100) |

### Response format

```json
{
  "data": [...],
  "meta": {
    "page": 1,
    "limit": 20,
    "total": 13,
    "totalPages": 1
  }
}
```

## Tech Stack

- **Next.js 16** — App Router, API routes, server components
- **TypeScript** — Strict mode
- **Prisma** — PostgreSQL ORM with migrations
- **PostgreSQL** — Neon (production), local (development)
- **Tailwind CSS v4** — Styling
- **Zod** — Runtime validation for API inputs

## Schema

The RFP object extends DAOIP-5 `grantPool` with:

- Deadline, budget range, duration
- Structured requirements, evaluation criteria, deliverables
- Provenance metadata (source URL, verification status, change history)
- Multi-ecosystem tagging
- Duplicate detection via `sourceUrl` uniqueness

See `/api/v1/schema` for the full schema definition and DAOIP-5 field mapping.

## Getting Started

### Prerequisites

- Node.js 20+
- pnpm
- PostgreSQL

### Setup

```bash
# Clone
git clone https://github.com/novafortesolutions/rfp-hub.git
cd rfp-hub

# Install dependencies
pnpm install

# Configure database
cp .env.example .env
# Edit .env with your PostgreSQL connection string

# Run migrations and seed
pnpm prisma migrate dev
pnpm db:seed

# Start development server
pnpm dev
```

### Scripts

| Command | Description |
|---------|-------------|
| `pnpm dev` | Start development server (Turbopack) |
| `pnpm build` | Production build |
| `pnpm start` | Start production server |
| `pnpm db:migrate` | Run Prisma migrations |
| `pnpm db:seed` | Seed database with sample data |
| `pnpm db:studio` | Open Prisma Studio |
| `pnpm scrape` | Run EF ESP scraper |

## License

MIT
