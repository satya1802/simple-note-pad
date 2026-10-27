<!-- sdlc:auto:start adr -->
# ADR-0001: Use React 19 for Frontend

Status: Accepted  
Date: 2026-10-27

## Context and Problem Statement

Which Frontend technology does the project use? Decided in architecture v1.

## Considered Options

- React 19
- Vue
- Svelte

## Decision Outcome

Chosen option: React 19, because Drives the single interactive notes screen with debounced auto-save, live search filtering and a save-status indicator, and renders a responsive layout for desktop and mobile browsers.

## Consequences

A SPA needs client-side route guarding and token handling; acceptable for this small single-screen app.
<!-- sdlc:auto:end adr -->