# Traceability Matrix

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start legend -->
Built from recorded links, not written by a model: requirement key → plan item (`source_stable_key`) → development ticket (`stable_key`) → the ticket's test steps → the last live deployment that started after the work finished. **AC tests** counts the story's acceptance criteria that have a test case, and those whose test cases all passed in the latest finished E2E run.
<!-- sdlc:auto:end legend -->

<!-- sdlc:auto:start matrix -->
| Requirement | Epic | Title | Plan items | Sprint | Design | Code | Commits | Ticket | Tests | AC tests | Deployed |
|---|---|---|---|---|---|---|---|---|---|---|---|
| US-001 | EPIC-001 | Register an account with email and password | US-001 | 1 | POST /auth/register, api, db, users, web_app | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-002 | EPIC-001 | Sign in with email and password | US-002 | 1 | POST /auth/login, api, db, users, web_app | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-003 | EPIC-001 | Sign out of my account | US-003 | 1 | POST /auth/logout, api, web_app | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-004 | EPIC-002 | See only my own notes | US-004 | 1 | GET /notes, GET /notes/{id}, api, db, notes, users | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-005 | EPIC-002 | Access my notes from any device | US-005 | 2 | GET /notes, api, db, notes, web_app | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-006 | EPIC-003 | Create a plain-text note | US-006 | 1 | POST /notes, api, db, notes, web_app | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-007 | EPIC-003 | Auto-save note edits | US-007 | 2 | PATCH /notes/{id}, api, db, notes, web_app | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-008 | EPIC-003 | Delete a note | US-008 | 2 | DELETE /notes/{id}, api, db, notes, web_app | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-009 | EPIC-004 | View all notes in a single most-recent-first list | US-009 | 1 | GET /notes, api, db, notes, web_app | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-010 | EPIC-004 | Search notes by their text | US-010 | 2 | GET /notes, api, db, notes, web_app | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-011 | EPIC-005 | Use the app across desktop and mobile browsers | US-011 | 2 | web_app | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-012 | EPIC-005 | Use the app free of charge | US-012 | 2 | web_app | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
<!-- sdlc:auto:end matrix -->
