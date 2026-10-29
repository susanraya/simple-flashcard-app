# Development

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
### DEV-SPRINT-1 · draft · source: plan:Sprint 1

Sprint 1 — Auth, Schema & Deck List: goal is sign-up/sign-in/sign-out plus a backed deck list with full data isolation.

Goal: 'Learners can sign up, sign in, sign out, and see/create their decks on a backed PostgreSQL database with full data isolation.' Capacity: 20 points.

**Related:** EPIC-001, US-005, US-006

- ⚠ Plan does not explicitly list which backlog items belong to this sprint beyond what the goal text implies; exact item-to-sprint mapping is not given in the input.
- ⚠ No completion status, burndown, or actual outcome recorded for this sprint.

### DEV-SPRINT-2 · draft · source: plan:Sprint 2

Sprint 2 — Deck & Card CRUD, Responsive: goal is completing deck lifecycle and full card management with verified responsive layout.

Goal: 'Complete deck lifecycle (rename, delete) and full card management (add, view, edit, delete) with a responsive layout verified across all screens.' Capacity: 20 points.

**Related:** US-007, US-008, US-009, US-010, US-011, US-012, US-020

- ⚠ Plan does not explicitly list which backlog items belong to this sprint beyond what the goal text implies.
- ⚠ No completion status or actual outcome recorded for this sprint.

### DEV-SPRINT-3 · draft · source: plan:Sprint 3

Sprint 3 — Study Session, Results & Reliability: goal is the full study loop, progress history, and cross-cutting error handling.

Goal: 'Deliver the full study session loop with shuffled order, flip, mark right/wrong, wrong-card repeat, end-of-session score, per-deck progress history, and cross-cutting error handling for failed saves.' Capacity: 20 points.

**Related:** US-013, US-014, US-015, US-016, US-017, US-018, US-019, US-021, US-022

- ⚠ Plan does not explicitly list which backlog items belong to this sprint beyond what the goal text implies.
- ⚠ No completion status or actual outcome recorded for this sprint.

### DEV-EPIC-001 · draft · source: plan:EPIC-001

Backlog breakdown for Learner Accounts and Private Access.

US-001 Sign up (5 pts, integration-agent): tasks -- provision Cognito User Pool/app client (devops-agent), build SPA sign-up form with Cognito SDK (frontend-agent), implement FastAPI JWT validation middleware (backend-agent), create POST /auth/learners endpoint (backend-agent), create DB schema for learners/decks/cards/study_sessions (backend-agent). US-002 Sign in (3 pts, frontend-agent): build SPA sign-in form, implement token storage/refresh (frontend-agent), verify only email-password auth offered (qa-agent). US-003 Sign out (2 pts, frontend-agent): implement sign-out action, enforce post-sign-out redirect on protected routes (qa-agent). US-004 Private data (3 pts, backend-agent): add ownership scoping to all queries, return 404 for cross-learner access by ID, implement SPA route guards for authenticated screens (frontend-agent).

**Related:** US-001, US-002, US-003, US-004

- ⚠ No completion status, code artifacts, or review outcomes provided for any of these items; this reflects planned backlog only.

### DEV-EPIC-002 · draft · source: plan:EPIC-002

Backlog breakdown for Deck Management.

US-005 Deck list home screen (3 pts, backend-agent): GET /decks endpoint, SPA deck list home screen (frontend-agent), empty-state for zero decks (frontend-agent). US-006 Create deck (3 pts, backend-agent): POST /decks endpoint, SPA create-deck form (frontend-agent). US-007 Rename deck (2 pts, backend-agent): PATCH /decks/{id} endpoint, SPA rename-deck form (frontend-agent). US-008 Delete deck with confirmation (3 pts, backend-agent): DELETE /decks/{id} with cascade, SPA delete-deck confirmation modal (frontend-agent), verify history cleanup after deletion (qa-agent).

**Related:** US-005, US-006, US-007, US-008

- ⚠ No completion status, code artifacts, or review outcomes provided for any of these items; this reflects planned backlog only.

### DEV-EPIC-003 · draft · source: plan:EPIC-003

Backlog breakdown for Card Management.

US-009 Add card (3 pts, backend-agent): POST /decks/{id}/cards endpoint, SPA add-card form with clear-on-submit (frontend-agent). US-010 View cards (3 pts, backend-agent): GET /decks/{id}/cards endpoint, SPA card list view (frontend-agent), empty-state for zero cards (frontend-agent). US-011 Edit card (2 pts, backend-agent): PATCH /cards/{id} endpoint, SPA edit-card form (frontend-agent). US-012 Delete card (2 pts, backend-agent): DELETE /cards/{id} endpoint, SPA delete-card confirmation (frontend-agent).

**Related:** US-009, US-010, US-011, US-012

- ⚠ No completion status, code artifacts, or review outcomes provided for any of these items; this reflects planned backlog only.

### DEV-EPIC-004 · draft · source: plan:EPIC-004

Backlog breakdown for Study Session.

US-013 Start session (2 pts, backend-agent): POST /decks/{id}/sessions endpoint, SPA session start flow (frontend-agent). US-014 Shuffled order (2 pts, frontend-agent): client-side card shuffle, verify first-pass completeness (qa-agent). US-015 Flip card (2 pts, frontend-agent): flip-card component, keyboard support for reveal/marking. US-016 Mark right/wrong (3 pts, frontend-agent): mark-right logic, mark-wrong logic, track first-time-correct count. US-017 Repeat wrong cards (3 pts, frontend-agent): wrong-card repeat loop, detect session end and trigger result.

**Related:** US-013, US-014, US-015, US-016, US-017

- ⚠ No completion status, code artifacts, or review outcomes provided for any of these items; this reflects planned backlog only.

### DEV-EPIC-005 · draft · source: plan:EPIC-005

Backlog breakdown for Session Results and Deck Progress.

US-018 Score at session end (3 pts, backend-agent): POST /sessions/{id}/finish endpoint, SPA session result screen (frontend-agent). US-019 Deck progress over time (2 pts, backend-agent): GET /decks/{id}/sessions endpoint, SPA deck progress view (frontend-agent).

**Related:** US-018, US-019

- ⚠ No completion status, code artifacts, or review outcomes provided for any of these items; this reflects planned backlog only.

### DEV-EPIC-006 · draft · source: plan:EPIC-006

Backlog breakdown for Responsive Web Experience and Platform Foundations.

US-020 Phone/desktop responsive (3 pts, frontend-agent): apply responsive CSS across all screens, handle device rotation during study session, verify no offline/installable-app features (qa-agent). US-021 Reliable per-account storage (3 pts, backend-agent): consistent error responses across all API endpoints, SPA error messaging for failed saves (frontend-agent). US-022 Free, English-only, no extras (1 pt, qa-agent): audit all screens for no payment/upsell content, verify English-only interface and no notifications, verify no import/export/third-party integrations.

**Related:** US-020, US-021, US-022

- ⚠ No completion status, code artifacts, or review outcomes provided for any of these items; this reflects planned backlog only.
<!-- sdlc:auto:end narrative -->
