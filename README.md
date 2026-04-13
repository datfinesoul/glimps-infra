# Glimps Infrastructure

PostgreSQL 16 + Redis 7 for local development.

## Quick Start

```bash
# Copy and configure environment
cp .env.example .env

# Start services
docker compose up -d

# Verify services are healthy
docker compose ps
```

## Services

| Service | Port | Purpose |
|---------|------|---------|
| PostgreSQL | 5432 | Primary database |
| Redis | 6379 | Job queue + BullMQ |

## Testing "Works at All"

### Tool Requirements

- **docker** — run containers

### PostgreSQL

```bash
# Via docker exec (no psql needed)
docker exec glimps_postgres pg_isready -U glimps -d glimps
docker exec glimps_postgres psql -U glimps -d glimps -c "SELECT 1;"
```

### Redis

```bash
# Via docker exec
docker exec glimps_redis redis-cli ping
```

Expected output: `pg_isready` reports "accepting connections", `redis-cli` returns `PONG`.

## Stopping

```bash
docker compose down        # preserve data
docker compose down -v     # destroy data
```
