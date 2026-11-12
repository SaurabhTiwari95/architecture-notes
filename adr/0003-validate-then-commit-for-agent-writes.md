# 0003. Agent writes are validate-then-commit drafts, approved by a person

- **Status:** Accepted
- **Date:** 2026-11-09

## Context

Agents can draft records (invoices, requests) faster than people, but they can be wrong, they retry
on timeouts, and someone must remain accountable for what is posted.

## Decision

1. `POST /validate` checks the draft and returns a preview plus a short-lived token.
2. `POST /commit` with that token and an `Idempotency-Key` stores a **pending draft**. Repeating the
   same key returns the first result instead of creating a second draft.
3. A person approves the draft in the normal application; it then posts **under the approver's
   name**, within per-record limits and before its expiry.
4. Daily caps, an allowed-hours window and a circuit breaker apply per agent. Every step is written
   to an append-only audit log.

## Consequences

- No duplicate records from retries; no record without a responsible person.
- Writes are slower (human in the loop). That's the point.
- More moving parts: draft table, approval screen, expiry job.
