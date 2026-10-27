# Sprint Plan

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start sprints -->
## Sprint 1: Sprint 1

Users can register, sign in/out, and create notes they alone can see, listed most-recent-first

Capacity: 20 points · Committed: 19

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-001 | Story | Register an account with email and password | 5 | backend-agent | — |
| US-002 | Story | Sign in with email and password | 3 | backend-agent | US-001 |
| US-003 | Story | Sign out of my account | 2 | backend-agent | US-002 |
| US-004 | Story | See only my own notes | 3 | backend-agent | US-002, US-006 |
| US-006 | Story | Create a plain-text note | 3 | backend-agent | US-002 |
| US-009 | Story | View all notes in a single most-recent-first list | 3 | backend-agent | US-006 |

## Sprint 2: Sprint 2

Notes auto-save with status feedback, can be deleted and searched, sync across devices, and the app is responsive and free of any billing surface

Capacity: 20 points · Committed: 18

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-005 | Story | Access my notes from any device | 2 | integration-agent | US-002, US-006 |
| US-007 | Story | Auto-save note edits | 5 | frontend-agent | US-006 |
| US-008 | Story | Delete a note | 2 | frontend-agent | US-006 |
| US-010 | Story | Search notes by their text | 3 | backend-agent | US-006 |
| US-011 | Story | Use the app across desktop and mobile browsers | 5 | frontend-agent | US-006, US-009, US-007, US-010 |
| US-012 | Story | Use the app free of charge | 1 | qa-agent | US-001 |

## Unscheduled

_Nothing unscheduled._
<!-- sdlc:auto:end sprints -->
