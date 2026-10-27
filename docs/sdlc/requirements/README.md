# Product Requirements

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
## Summary

### REQ-TECH-STACK · approved · source: requirements:tech-stack

Product owner approved the exact technology stack for this build: FastAPI backend, AWS cloud, PostgreSQL database, React frontend.

Decided stack (to be used exactly as specified, no substitutions):
- Backend: FastAPI 0.115 -- lean API for sign-in and per-user note save/fetch/search/delete; platform default; low infra cost at individual scale.
- Cloud: AWS -- hosts the web app, managed PostgreSQL, and backups; platform default; low running cost at individual scale.
- Database: PostgreSQL 16 -- durable, per-user-isolated storage; sorts notes by edit time; built-in text search covers search needs without a separate search system.
- Frontend: React 19 -- supports an instant-feeling, responsive single-screen app (typing, auto-save, live search filtering) on desktop and mobile browsers; no native app in scope.

### REQ-SERVICES · approved · source: requirements:services

Product owner approved SendGrid as the transactional email service, required because the app uses email/password sign-in.

Service: SendGrid (SaaS), env var SENDGRID_API_KEY. Rationale given: email/password sign-in requires reliably delivering password-reset (and likely account-verification) emails without running a mail server. API key required: SENDGRID_API_KEY.

**Related:** US-001, US-002

- ⚠ Rationale references password-reset and account-verification emails, but no user story or acceptance criterion in this requirements set covers a password-reset flow or an email-verification flow -- scope conflict to confirm with product owner.

### REQ-OUT-OF-SCOPE · approved · source: requirements:scope

Explicit exclusions from design/build for this delivery.

Out of scope: (1) Rich-text formatting, images and file attachments in notes. (2) Folders/notebooks and tags for organising notes. These are confirmed exclusions, not pending decisions.

**Related:** EPIC-003, EPIC-004

### US-001 · draft · source: requirements:US-001

Critical story: a new user can register with email and password to get a private notes space.

Priority: critical.
- AC-001: Valid, unused email + password submitted while on registration screen (not signed in) -> account created and user is signed in to their private notes area.
- AC-002: Email already has an account -> registration rejected, user told the email is already in use.
- AC-003: Invalid email format or blank password -> registration rejected, invalid field is indicated.

**Related:** EPIC-001, AC-001, AC-002, AC-003

- ⚠ Password strength/length requirements are not specified in the input.

### US-002 · draft · source: requirements:US-002

Critical story: a returning user signs in with email and password to reach their notes from any device.

Priority: critical.
- AC-004: Correct email + password on sign-in screen -> signed in and taken to notes list.
- AC-005: Incorrect email or password -> sign-in refused with a generic error that does not reveal which field was wrong.
- AC-006: No social login or SSO options are offered; email/password only.

**Related:** EPIC-001, AC-004, AC-005, AC-006, NFR-002

### US-003 · draft · source: requirements:US-003

High priority story: a signed-in user can sign out to protect their notes on shared browsers.

Priority: high.
- AC-007: Choosing sign-out ends the session and returns the user to the sign-in screen.
- AC-008: After signing out, attempting to open the notes list redirects to sign-in; no notes are visible.

**Related:** EPIC-001, AC-007, AC-008, NFR-002

### US-004 · draft · source: requirements:US-004

Critical story: a signed-in user sees exclusively their own notes; other users' notes are inaccessible.

Priority: critical.
- AC-009: Notes list shows only notes created under the signed-in user's own account, even when other users have notes in the system.
- AC-010: Attempting to access another user's note is denied and the note is not shown.

**Related:** EPIC-002, AC-009, AC-010, NFR-001

### US-005 · draft · source: requirements:US-005

Critical story: notes sync to the server so the same notes and latest edits appear on any device.

Priority: critical.
- AC-011: A note created/saved on one device appears with current content when signing in on another device.
- AC-012: A note edited on one device shows the most recent saved version when opened on another device.

**Related:** EPIC-002, AC-011, AC-012

### US-006 · draft · source: requirements:US-006

Critical story: a signed-in user creates a new note and types plain text into it.

Priority: critical.
- AC-013: Creating a new note and typing plain text stores a note under the user's account containing exactly the typed text.
- AC-014: No formatting, image, or attachment controls are available; plain typed text only.

**Related:** EPIC-003, AC-013, AC-014

### US-007 · draft · source: requirements:US-007

Critical story: edits to a note save automatically to the server as the user types, with no manual save step.

Priority: critical.
- AC-015: Changes made while editing are saved to the server automatically on pause/continued typing, with no explicit save action.
- AC-016: Reopening a note after navigating away shows the most recently auto-saved changes.
- AC-017: While a save is in progress or has just completed, a clear save-status indication is given to the user.

**Related:** EPIC-003, AC-015, AC-016, AC-017, NFR-003

- ⚠ Exact UI form of the save-status indicator (text label, icon, timing) is not specified.

### US-008 · draft · source: requirements:US-008

High priority story: a signed-in user can delete a note after confirming, removing it everywhere.

Priority: high.
- AC-018: Choosing delete and confirming removes the note from the account and from the notes list on every device.
- AC-019: Cancelling the delete confirmation leaves the note unchanged.

**Related:** EPIC-003, AC-018, AC-019

### US-009 · draft · source: requirements:US-009

High priority story: all notes appear in one list ordered most-recently-updated first.

Priority: high.
- AC-020: All of a user's notes are shown in a single list ordered most-recently-updated first.
- AC-021: Editing a note moves it to the top of the list on return to the notes list.
- AC-022: No folders, notebooks, or tags are present; notes are a single list.

**Related:** EPIC-004, AC-020, AC-021, AC-022

### US-010 · draft · source: requirements:US-010

High priority story: a search box filters the notes list by matching note text.

Priority: high.
- AC-023: Typing a search term shows only notes whose text contains that term.
- AC-024: A search term matching no notes shows an empty result with a clear 'no matching notes' indication.
- AC-025: Clearing the search box restores the full most-recent-first list.

**Related:** EPIC-004, AC-023, AC-024, AC-025

### US-011 · draft · source: requirements:US-011

High priority story: the app's layout and core actions work on both desktop and mobile browsers.

Priority: high.
- AC-026: In a desktop browser, the layout is usable and all core actions (sign in, create, edit, delete, search) are accessible.
- AC-027: In a mobile browser, the layout adapts to the smaller screen and all core actions remain usable.

**Related:** EPIC-005, AC-026, AC-027, NFR-004

### US-012 · draft · source: requirements:US-012

Medium priority story: all app features are usable free of charge, with no billing anywhere.

Priority: medium.
- AC-028: No payment, subscription, or billing is ever requested while creating an account or managing notes.
- AC-029: No plans, pricing, or billing settings exist anywhere in the app.

**Related:** EPIC-005, AC-028, AC-029

### NFR-001 · draft · source: requirements:NFR-001

Privacy NFR: notes are strictly private to their owner, with no sharing or collaboration.

A signed-in user can see and open only notes created under their own account; any attempt to reach another user's note is denied. No sharing or collaboration between users is supported.

**Related:** US-004

### NFR-002 · draft · source: requirements:NFR-002

Security NFR: authentication gates all access to the notes area.

Only signed-in users can reach the notes area; signed-out or unauthenticated users are redirected to sign-in and see no notes. Failed sign-in attempts are refused with an error that does not reveal whether the email or password was wrong.

**Related:** US-002, US-003

### NFR-003 · draft · source: requirements:NFR-003

Usability NFR: users get a clear indication of auto-save status.

While edits are auto-saving, the user is given a clear indication of save status, so they can trust their work is not lost without pressing a save button.

**Related:** US-007

### NFR-004 · draft · source: requirements:NFR-004

Compatibility NFR: responsive layout keeps all core actions usable on desktop and mobile browsers.

The app is a responsive web application whose layout adapts to desktop and mobile browser screen sizes. All core actions (sign in, create, edit, delete, search) remain usable on both. No native mobile or desktop app is provided.

**Related:** US-011

### NFR-005 · draft · source: requirements:NFR-005

Scalability NFR: built lightweight for modest individual-user scale, not enterprise load.

The app is expected to serve individual users at modest scale, storing personal, non-regulated note data in a standard managed database. It should be built lightweight rather than for enterprise-grade load. Applies to the whole system.
<!-- sdlc:auto:end narrative -->

<!-- sdlc:auto:start summary -->
**Requirements version:** v1  
**Delivery scope:** lightweight  
**Approved:** 2026-10-27

**Capabilities in scope:** Email/password sign-in to a private account, Create a plain-text note, Auto-saving note edits, Delete a note, Single most-recent-first notes list, Search notes by their text, Server-synced notes available on any device, Each user sees only their own notes, Email/password login only (no social login or SSO), Responsive web app for desktop and mobile browsers

**Approved technology stack:**

| Layer | Choice | Rationale |
|---|---|---|
| backend | FastAPI | The server's job is small and clear: sign users in, and save/fetch/search/delete each person's own notes. FastAPI is a lean, fast way to expose exactly those operations as an API the React app calls, and it's the default the platform builds with. Its light footprint suits a free app at modest individual scale where you don't want heavy infrastructure cost. |
| cloud | AWS | A free personal notepad needs reliable, low-cost hosting for a small web app and one database, with room to grow if usage picks up. AWS covers all of it (app hosting, a managed PostgreSQL, backups) and is the platform default, so it builds and deploys without extra setup. At individual scale your running cost stays small. |
| database | PostgreSQL | You need durable, private per-user storage for text notes, ordered most-recent-first, and searchable by their text. PostgreSQL does all of this in one managed database: it stores the notes, keeps each user's data isolated, sorts by edit time, and has built-in text search so you don't need a separate search system at this scale. That matches your 'standard managed database' assumption directly. |
| frontend | React | Your product is a responsive web app that has to feel instant on both desktop and phone browsers — typing into a note, auto-saving as you go, and filtering a list as you type a search term. React handles exactly this kind of live, interactive single screen well, and it's the platform default here so it builds cleanly. No native app is in scope, so a browser-first framework is the right fit. |
<!-- sdlc:auto:end summary -->

<!-- sdlc:auto:start epics -->
## EPIC-001: Account & Authentication

Users sign in to a private account using email and password so their notes are protected and personal. Assumption: authentication is email/password only — no social login or SSO is provided. No sharing or collaboration between users; each account's notes are strictly private.

### US-001: Register an account with email and password

**Priority:** critical

> As a new user, I want to create an account using my email address and a password, so that I have a private space to store my notes.

| ID | Given | When | Then |
|---|---|---|---|
| AC-001 | I am on the registration screen and am not signed in | I enter a valid, unused email address and a password and submit | an account is created for me and I am signed in to my private notes area |
| AC-002 | I am on the registration screen | I submit an email address that already has an account | registration is rejected and I am told the email is already in use |
| AC-003 | I am on the registration screen | I submit an invalid email format or leave the password blank | registration is rejected and I am shown which field is invalid |

### US-002: Sign in with email and password

**Priority:** critical

> As a returning user, I want to sign in with my email and password, so that I can access my own notes from any device.

| ID | Given | When | Then |
|---|---|---|---|
| AC-004 | I have a registered account and am on the sign-in screen | I enter my correct email and password and submit | I am signed in and taken to my notes list |
| AC-005 | I am on the sign-in screen | I enter an incorrect email or password | sign-in is refused and I see an error message that does not reveal which field was wrong |
| AC-006 | I am on the sign-in screen | I look for social login or SSO options | none are offered because only email/password login is supported |

### US-003: Sign out of my account

**Priority:** high

> As a signed-in user, I want to sign out, so that my notes are not accessible to anyone else using the same browser.

| ID | Given | When | Then |
|---|---|---|---|
| AC-007 | I am signed in | I choose to sign out | my session ends and I am returned to the sign-in screen |
| AC-008 | I have signed out | I try to open the notes list without signing in again | I am redirected to the sign-in screen and cannot see any notes |

## EPIC-002: Notes Privacy & Cross-Device Sync

Notes are stored on the server so they are available to the owner on any device via a browser, and each user can only ever see their own notes. Assumptions: notes sync to the server for cross-device access; data is personal but not regulated/special-category and is held in a standard managed database at modest individual-user scale; notes are strictly private with no sharing or collaboration.

### US-004: See only my own notes

**Priority:** critical

> As a signed-in user, I want to see exclusively the notes that belong to my account, so that my notes remain private to me.

| ID | Given | When | Then |
|---|---|---|---|
| AC-009 | other users also have notes in the system | I view my notes list | I see only notes created under my own account and none belonging to other users |
| AC-010 | I am signed in as myself | I attempt to access a note that belongs to another user | access is denied and the note is not shown |

### US-005: Access my notes from any device

**Priority:** critical

> As a user with notes saved on one device, I want my notes synced to the server, so that I can open the same notes on another device through the browser.

| ID | Given | When | Then |
|---|---|---|---|
| AC-011 | I created and saved a note on one device | I sign in on a different device and open my notes list | the same note appears with its current content |
| AC-012 | I edited a note on one device | I later open that note on another device | I see the most recent saved version of the note |

## EPIC-003: Note Creation, Editing & Deletion

Users can create plain-text notes, edit them with changes saved automatically, and delete notes they no longer want. Notes hold plain typed text only. Out of scope: rich-text formatting, images and file attachments.

### US-006: Create a plain-text note

**Priority:** critical

> As a signed-in user, I want to create a new note and type plain text into it, so that I can capture my thoughts.

| ID | Given | When | Then |
|---|---|---|---|
| AC-013 | I am signed in and viewing my notes list | I choose to create a new note and type plain text | a new note is created under my account containing exactly the text I typed |
| AC-014 | I am editing a note | I look for formatting, image or attachment controls | none are available because notes support plain typed text only |

### US-007: Auto-save note edits

**Priority:** critical

> As a user editing a note, I want my changes to save automatically as I type, so that I never lose my work and don't have to press a save button.

| ID | Given | When | Then |
|---|---|---|---|
| AC-015 | I am editing a note and have made changes | I pause or continue typing | the changes are saved to the server automatically without me taking any explicit save action |
| AC-016 | my edits have been auto-saved | I navigate away from the note and reopen it | the note shows my most recent changes |
| AC-017 | I am editing a note | a save is in progress or has just completed | I am given a clear indication of the save status |

### US-008: Delete a note

**Priority:** high

> As a signed-in user, I want to delete a note I no longer need, so that my notes list stays relevant.

| ID | Given | When | Then |
|---|---|---|---|
| AC-018 | I am viewing one of my notes | I choose to delete it and confirm | the note is removed from my account and no longer appears in my notes list on any device |
| AC-019 | I choose to delete a note | I am asked to confirm and I cancel | the note is kept unchanged |

## EPIC-004: Notes List & Search

All of a user's notes appear in a single list ordered most-recent-first, with a search box to find notes by their text. There are no folders, notebooks or tags, and search matches on note text only with no advanced filtering.

### US-009: View all notes in a single most-recent-first list

**Priority:** high

> As a signed-in user, I want to see all my notes in one list ordered with the most recent first, so that I can quickly find what I was last working on.

| ID | Given | When | Then |
|---|---|---|---|
| AC-020 | I have several notes | I open my notes list | all my notes are shown in a single list ordered most-recently-updated first |
| AC-021 | I edit a note so it becomes the most recently updated | I return to the notes list | that note appears at the top of the list |
| AC-022 | I view my notes list | I look for folders, notebooks or tags | none are present because notes are organised as one single list |

### US-010: Search notes by their text

**Priority:** high

> As a signed-in user, I want to search my notes by the text they contain, so that I can locate a specific note without scrolling.

| ID | Given | When | Then |
|---|---|---|---|
| AC-023 | I have notes containing various text | I type a search term into the search box | the list shows only my notes whose text contains that term |
| AC-024 | I have entered a search term that matches no notes | the search runs | I am shown an empty result with a clear 'no matching notes' indication |
| AC-025 | I clear the search box | the search term is removed | the full most-recent-first list of my notes is shown again |

## EPIC-005: Responsive Web Application

The product is delivered as a responsive web application usable in desktop and mobile browsers. Assumptions: free to use with no payments, plans or billing; no native mobile or desktop app is provided.

### US-011: Use the app across desktop and mobile browsers

**Priority:** high

> As a user, I want the app to work and adapt to desktop and mobile browser screen sizes, so that I can manage my notes on whatever device I have.

| ID | Given | When | Then |
|---|---|---|---|
| AC-026 | I open the app in a desktop browser | the notes interface loads | the layout is usable and all core actions (sign in, create, edit, delete, search) are accessible |
| AC-027 | I open the app in a mobile browser | the notes interface loads | the layout adapts to the smaller screen and all core actions remain usable |

### US-012: Use the app free of charge

**Priority:** medium

> As a user, I want to use all features without any payment, so that I can keep notes without cost or billing concerns.

| ID | Given | When | Then |
|---|---|---|---|
| AC-028 | I am using any feature of the app | I create an account and manage my notes | no payment, subscription or billing is ever requested |
| AC-029 | I explore the app | I look for plans, pricing or billing settings | none are present because the app is free to use |
<!-- sdlc:auto:end epics -->
