# Architecture Decision Records

Short records of one decision each: the context, what was decided, and what it costs.
Format: [Michael Nygard's ADR template](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions).

| # | Decision | Status |
|---|---|---|
| [0001](0001-gateway-instead-of-direct-db-access.md) | AI agents reach data through a gateway, never directly | Accepted |
| [0002](0002-hmac-with-nonce-instead-of-static-api-keys.md) | Sign agent requests with HMAC and a single-use nonce | Accepted |
| [0003](0003-validate-then-commit-for-agent-writes.md) | Agent writes are validate-then-commit drafts, approved by a person | Accepted |
| [0004](0004-pre-signed-direct-uploads.md) | Browsers upload files straight to S3 with pre-signed POST | Accepted |
| [0005](0005-database-per-tenant.md) | One database per tenant, behind a tenant router | Accepted |
| [0006](0006-blue-green-for-engine-upgrades.md) | Use blue/green deployments for database engine upgrades | Accepted |

New record: copy [template.md](template.md) to the next number.
