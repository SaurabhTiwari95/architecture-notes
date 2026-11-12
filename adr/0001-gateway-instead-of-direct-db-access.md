# 0001. AI agents reach data through a gateway, never directly

- **Status:** Accepted
- **Date:** 2026-11-09

## Context

AI agents running on another server need to read business data from an existing application whose
code we don't want to change. Giving them database credentials would be quickest but leaves no
allow-list, no audit trail and no limit on what a query can do.

## Decision

Agents call a separate **read gateway** that exposes named, allow-listed, read-only functions. The
gateway connects with a `SELECT`-only database user, preferably to a read replica.

## Consequences

- The existing application is untouched, so its users carry no regression risk.
- Every agent capability is explicit, reviewable and logged.
- New capabilities need a new function and a review: slower, deliberately.
- The gateway becomes a component to run, monitor and scale.

See [note 01](../notes/01-ai-agents-on-an-existing-system.md).
