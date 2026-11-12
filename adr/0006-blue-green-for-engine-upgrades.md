# 0006. Use blue/green deployments for database engine upgrades

- **Status:** Accepted
- **Date:** 2026-11-09

## Context

Major engine versions leave standard support, after which extended-support fees apply. In-place
upgrades are quick but leave no clean way back if something breaks.

## Decision

Upgrade through a **blue/green deployment** (or a promoted, upgraded replica): an upgraded copy is
kept in sync, tested, then switched over in a short announced window. The old instance stays as the
rollback path until verification passes. The least critical instance goes first.

## Consequences

- Downtime is about a minute; rollback is a switch, not a restore.
- Two instances are billed while both run.
- The compatibility check (reserved words, auth plugin, character set, SQL modes) still has to be
  done before the switch.

See [note 03](../notes/03-database-engine-upgrade-playbook.md).
