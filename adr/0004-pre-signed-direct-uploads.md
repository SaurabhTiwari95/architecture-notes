# 0004. Browsers upload files straight to S3 with pre-signed POST

- **Status:** Accepted
- **Date:** 2026-11-09

## Context

Uploading through the app server ties up workers and memory, and doubles bandwidth.

## Decision

The API checks the user and file, picks the object key, and returns a **pre-signed POST** with a
`content-length-range`, an exact `Content-Type` and a five-minute expiry. The browser uploads to the
private bucket directly. The API then confirms the object's size and type before saving the record.
The API role may only put and get objects under one prefix.

## Consequences

- Upload volume no longer affects app servers.
- Bucket CORS, lifecycle rules (abort incomplete multipart uploads) and a malware scan must be set
  up and maintained.
- Two round trips and a little more frontend code.

See [note 04](../notes/04-direct-to-s3-uploads.md).
