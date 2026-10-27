<!-- sdlc:auto:start adr -->
# ADR-0003: Use PostgreSQL 16 for Database

Status: Accepted  
Date: 2026-10-27

## Context and Problem Statement

Which Database technology does the project use? Decided in architecture v1.

## Considered Options

- PostgreSQL 16
- MySQL
- SQLite

## Decision Outcome

Chosen option: PostgreSQL 16, because Stores users and notes durably, isolates each user's data, orders by updated_at, and performs built-in full-text search so no separate search service is needed.

## Consequences

Built-in text search is simpler than a dedicated engine but entirely sufficient at modest individual scale.
<!-- sdlc:auto:end adr -->