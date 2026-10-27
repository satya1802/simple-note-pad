<!-- sdlc:auto:start adr -->
# ADR-0004: Use AWS for Cloud

Status: Accepted  
Date: 2026-10-27

## Context and Problem Statement

Which Cloud technology does the project use? Decided in architecture v1.

## Considered Options

- AWS
- Azure
- GCP

## Decision Outcome

Chosen option: AWS, because Hosts the static SPA, the container API and managed RDS PostgreSQL with backups at low cost, deploying without extra setup as the platform default.

## Consequences

Some AWS service familiarity required; costs stay small at individual scale.
<!-- sdlc:auto:end adr -->