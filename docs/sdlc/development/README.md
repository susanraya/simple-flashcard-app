# Development

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
### DEV-PLAN-V1 · approved · source: plan:v1

Development plan version 1 is approved and organizes the flashcard app build into 3 sprints of 20-point capacity each, covering auth/schema, deck+card CRUD with responsiveness, and the study-session loop with reliability work.

Plan status: approved, version 1. Sprints: (1) 'Auth, Schema & Deck List' — learners can sign up, sign in, sign out, and see/create decks on a backed PostgreSQL database with full data isolation; (2) 'Deck & Card CRUD, Responsive' — complete deck lifecycle (rename, delete) and full card management (add, view, edit, delete) with responsive layout verified across all screens; (3) 'Study Session, Results & Reliability' — full study session loop (shuffle, flip, mark right/wrong, wrong-card repeat, end-of-session score), per-deck progress history, and cross-cutting error handling for failed saves. Backlog spans 6 epics (EPIC-001 Learner Accounts and Private Access, EPIC-002 Deck Management, EPIC-003 Card Management, EPIC-004 Study Session, EPIC-005 Session Results and Deck Progress, EPIC-006 Responsive Web Experience and Platform Foundations) and 22 stories (US-001–US-022), each broken into implementation tasks assigned to backend-agent, frontend-agent, devops-agent, qa-agent, or integration-agent roles.

**Related:** US-001, US-002, US-003, US-004, US-005, US-006, US-007, US-008, US-009, US-010, US-011, US-012, US-013, US-014, US-015, US-016, US-017, US-018, US-019, US-020, US-021, US-022

- ⚠ No ticket-level completion/status (done, in review, blocked, etc.) was provided for any story or task — only planned scope is known, not what has been built.
- ⚠ No code artifacts, pull requests, commit references, or build logs were included in this input.
- ⚠ All 6 epics have role '(unassigned)' in the plan — no owning role recorded at the epic level.
- ⚠ US-022 (free, English-only app, no extra services) is not explicitly referenced by any sprint goal, unlike its sibling stories US-020 and US-021 — unclear which sprint is intended to deliver/verify it; flagging as an ambiguity for confirmation.

### DEV-SPRINT-1 · approved · source: plan:SPRINT-1

Sprint 1 targets authentication, the core database schema, and private per-account access, capacity 20 points.

Goal: Learners can sign up, sign in, sign out, and see/create their decks on a backed PostgreSQL database with full data isolation. Items:
- EPIC-001 Learner Accounts and Private Access (unassigned role).
- US-001 Sign up for an account (5 pts, integration-agent). Tasks: provision Cognito User Pool and app client (devops-agent); build SPA sign-up form with Cognito SDK (frontend-agent); implement FastAPI JWT validation middleware (backend-agent); create POST /auth/learners endpoint (backend-agent); create database schema for learners, decks, cards, study_sessions (backend-agent).
- US-002 Sign in to an existing account (3 pts, frontend-agent). Tasks: build SPA sign-in form; implement token storage and refresh logic (both frontend-agent); verify only email-password auth is offered (qa-agent).
- US-003 Sign out (2 pts, frontend-agent). Tasks: implement sign-out action (frontend-agent); enforce post-sign-out redirect on protected routes (qa-agent).
- US-004 Keep every learner's data private to their account (3 pts, backend-agent). Tasks: add ownership scoping to all deck/card/session queries; return 404 for cross-learner resource access by ID (both backend-agent); implement SPA route guards for all authenticated screens (frontend-agent).

**Related:** EPIC-001, US-001, US-002, US-003, US-004

- ⚠ No completion status reported for any story or task in this sprint — cannot confirm sign-up, sign-in, sign-out, or data-isolation work is actually done.

### DEV-SPRINT-2 · approved · source: plan:SPRINT-2

Sprint 2 targets full deck and card CRUD plus a responsive layout verified across all screens, capacity 20 points.

Goal: Complete deck lifecycle (rename, delete) and full card management (add, view, edit, delete) with a responsive layout verified across all screens. Items:
- EPIC-002 Deck Management (unassigned role).
- US-005 See my decks on the home screen (3 pts, backend-agent). Tasks: GET /decks endpoint (backend-agent); SPA deck list home screen (frontend-agent); empty-state for zero decks (frontend-agent).
- US-006 Create a deck (3 pts, backend-agent). Tasks: POST /decks endpoint (backend-agent); SPA create-deck form (frontend-agent).
- US-007 Rename a deck (2 pts, backend-agent). Tasks: PATCH /decks/{id} endpoint (backend-agent); SPA rename-deck form (frontend-agent).
- US-008 Delete a deck with confirmation (3 pts, backend-agent). Tasks: DELETE /decks/{id} with cascade (backend-agent); SPA delete-deck confirmation modal (frontend-agent); verify history cleanup after deck deletion (qa-agent).
- EPIC-003 Card Management (unassigned role).
- US-009 Add a card to a deck (3 pts, backend-agent). Tasks: POST /decks/{id}/cards endpoint (backend-agent); SPA add-card form with clear-on-submit (frontend-agent).
- US-010 View all cards in a deck (3 pts, backend-agent). Tasks: GET /decks/{id}/cards endpoint (backend-agent); SPA card list view (frontend-agent); empty-state for zero cards (frontend-agent).
- US-011 Edit a card (2 pts, backend-agent). Tasks: PATCH /cards/{id} endpoint (backend-agent); SPA edit-card form (frontend-agent).
- US-012 Delete a card (2 pts, backend-agent). Tasks: DELETE /cards/{id} endpoint (backend-agent); SPA delete-card confirmation (frontend-agent).
- US-020 Use the app equally well on phone and desktop (3 pts, frontend-agent) — included here because the sprint goal explicitly calls out 'responsive layout verified across all screens,' though US-020 formally belongs to EPIC-006. Tasks: apply responsive CSS across all screens (frontend-agent); handle device rotation during study session (frontend-agent); verify no offline or installable app features (qa-agent).

**Related:** EPIC-002, EPIC-003, US-005, US-006, US-007, US-008, US-009, US-010, US-011, US-012, US-020

- ⚠ No completion status reported for any story or task in this sprint.
- ⚠ US-020 belongs to EPIC-006 (Responsive Web Experience and Platform Foundations) in the backlog grouping but is addressed by this sprint's goal text — flagging the cross-epic placement for confirmation rather than silently resolving it.

### DEV-SPRINT-3 · approved · source: plan:SPRINT-3

Sprint 3 targets the full study-session loop, end-of-session scoring, per-deck progress history, and cross-cutting save-error handling, capacity 20 points.

Goal: Deliver the full study session loop with shuffled order, flip, mark right/wrong, wrong-card repeat, end-of-session score, per-deck progress history, and cross-cutting error handling for failed saves. Items:
- EPIC-004 Study Session (unassigned role).
- US-013 Start a study session on a deck (2 pts, backend-agent). Tasks: POST /decks/{id}/sessions endpoint (backend-agent); SPA session start flow (frontend-agent).
- US-014 See cards in shuffled order (2 pts, frontend-agent). Tasks: client-side card shuffle (frontend-agent); verify first-pass completeness (qa-agent).
- US-015 Flip a card to reveal the back (2 pts, frontend-agent). Tasks: SPA flip-card component; keyboard support for reveal and marking (both frontend-agent).
- US-016 Mark a card right or wrong (3 pts, frontend-agent). Tasks: mark-right logic; mark-wrong logic; track first-time-correct count (all frontend-agent).
- US-017 Repeat wrong cards until answered correctly (3 pts, frontend-agent). Tasks: wrong-card repeat loop; detect session end and trigger result (both frontend-agent).
- EPIC-005 Session Results and Deck Progress (unassigned role).
- US-018 See my score at the end of a session (3 pts, backend-agent). Tasks: POST /sessions/{id}/finish endpoint (backend-agent); SPA session result screen (frontend-agent).
- US-019 See how a deck is going over time (2 pts, backend-agent). Tasks: GET /decks/{id}/sessions endpoint (backend-agent); SPA deck progress view (frontend-agent).
- US-021 Have my decks, cards and results stored reliably per account (3 pts, backend-agent) — included here because the sprint goal explicitly calls out 'cross-cutting error handling for failed saves,' though US-021 formally belongs to EPIC-006. Tasks: consistent error responses across all API endpoints (backend-agent); SPA error messaging for failed saves (frontend-agent).

**Related:** EPIC-004, EPIC-005, US-013, US-014, US-015, US-016, US-017, US-018, US-019, US-021

- ⚠ No completion status reported for any story or task in this sprint — study-session mechanics, scoring, progress history, and error handling cannot be confirmed as built.
- ⚠ US-021 belongs to EPIC-006 (Responsive Web Experience and Platform Foundations) in the backlog grouping but is addressed by this sprint's goal text — flagging the cross-epic placement for confirmation.
<!-- sdlc:auto:end narrative -->
