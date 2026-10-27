<!-- sdlc:auto:start adr -->
# ADR-0002: Use FastAPI 0.115 for Backend

Status: Accepted  
Date: 2026-10-27

## Context and Problem Statement

Which Backend technology does the project use? Decided in architecture v1.

## Considered Options

- FastAPI 0.115
- Express
- Django REST Framework

## Decision Outcome

Chosen option: FastAPI 0.115, because Exposes the small, clear set of auth and per-user note operations as a REST API with Pydantic validation and a lean footprint suited to individual scale.

## Consequences

Minimal batteries-included tooling means auth and email are assembled from libraries rather than a framework suite.
<!-- sdlc:auto:end adr -->