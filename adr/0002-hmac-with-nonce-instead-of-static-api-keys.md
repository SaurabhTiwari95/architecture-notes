# 0002. Sign agent requests with HMAC and a single-use nonce

- **Status:** Accepted
- **Date:** 2026-11-09

## Context

A static API key sent in a header is enough to call the API forever if it is ever logged or
intercepted, and a captured request can be replayed as is.

## Decision

Each request carries a key id, a timestamp, a random nonce and an **HMAC-SHA256 signature** over
method, path, timestamp, nonce and a hash of the body. The server rejects requests older than five
minutes, nonces it has already seen (kept until they expire), and callers outside an IP allow-list.
Signatures are compared in constant time. The shared secret lives in a secrets manager, never in
code, and can be rotated by key id.

## Consequences

- A leaked log line or captured request can't be reused.
- Clients need a small signing helper, and clocks must be roughly in sync.
- The server needs a fast nonce store (Redis or a table with a TTL clean-up).
