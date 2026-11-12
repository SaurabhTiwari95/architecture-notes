# 0005. One database per tenant, behind a tenant router

- **Status:** Accepted
- **Date:** 2026-11-09

## Context

All tenants shared one database. One tenant's heavy workload took every tenant down, billing
included.

## Decision

Each tenant gets its own database. A tenant router (cached map of tenant to connection settings)
picks the connection per request. Each tenant has its own capped connection pool, with timeouts and
a circuit breaker. Billing runs as a separate service with its own servers.

## Consequences

- A failure or slow query affects one tenant only; billing survives a main-app outage.
- Migrations run per tenant and must tolerate mixed versions during a rollout.
- Cross-tenant reporting needs its own store.

See [note 02](../notes/02-multi-tenant-fault-isolation.md).
