# Sprint Plan

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start sprints -->
## Sprint 1: Sprint 1 — Auth, Schema & Deck List

Learners can sign up, sign in, sign out, and see/create their decks on a backed PostgreSQL database with full data isolation.

Capacity: 20 points · Committed: 19

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-001 | Story | Sign up for an account | 5 | integration-agent | — |
| ↳ US-001-T1 | Task | Provision Cognito User Pool and app client | — | devops-agent | — |
| ↳ US-001-T2 | Task | Build SPA sign-up form with Cognito SDK | — | frontend-agent | — |
| ↳ US-001-T3 | Task | Implement FastAPI JWT validation middleware | — | backend-agent | — |
| ↳ US-001-T4 | Task | Create POST /auth/learners endpoint | — | backend-agent | — |
| ↳ US-001-T5 | Task | Create database schema for learners, decks, cards, study_sessions | — | backend-agent | — |
| US-002 | Story | Sign in to an existing account | 3 | frontend-agent | US-001 |
| ↳ US-002-T1 | Task | Build SPA sign-in form | — | frontend-agent | — |
| ↳ US-002-T2 | Task | Implement token storage and refresh logic | — | frontend-agent | — |
| ↳ US-002-T3 | Task | Verify only email-password auth is offered | — | qa-agent | — |
| US-003 | Story | Sign out | 2 | frontend-agent | US-001 |
| ↳ US-003-T1 | Task | Implement sign-out action | — | frontend-agent | — |
| ↳ US-003-T2 | Task | Enforce post-sign-out redirect on protected routes | — | qa-agent | — |
| US-004 | Story | Keep every learner's data private to their account | 3 | backend-agent | US-001 |
| ↳ US-004-T1 | Task | Add ownership scoping to all deck/card/session queries | — | backend-agent | — |
| ↳ US-004-T2 | Task | Return 404 for cross-learner resource access by ID | — | backend-agent | — |
| ↳ US-004-T3 | Task | Implement SPA route guards for all authenticated screens | — | frontend-agent | — |
| US-005 | Story | See my decks on the home screen | 3 | backend-agent | US-002 |
| ↳ US-005-T1 | Task | Implement GET /decks endpoint | — | backend-agent | — |
| ↳ US-005-T2 | Task | Build SPA deck list home screen | — | frontend-agent | — |
| ↳ US-005-T3 | Task | Add empty-state for zero decks | — | frontend-agent | — |
| US-006 | Story | Create a deck | 3 | backend-agent | US-005 |
| ↳ US-006-T1 | Task | Implement POST /decks endpoint | — | backend-agent | — |
| ↳ US-006-T2 | Task | Build SPA create-deck form | — | frontend-agent | — |

## Sprint 2: Sprint 2 — Deck & Card CRUD, Responsive

Complete deck lifecycle (rename, delete) and full card management (add, view, edit, delete) with a responsive layout verified across all screens.

Capacity: 20 points · Committed: 19

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-007 | Story | Rename a deck | 2 | backend-agent | US-006 |
| ↳ US-007-T1 | Task | Implement PATCH /decks/{id} endpoint | — | backend-agent | — |
| ↳ US-007-T2 | Task | Build SPA rename-deck form | — | frontend-agent | — |
| US-008 | Story | Delete a deck with confirmation | 3 | backend-agent | US-006 |
| ↳ US-008-T1 | Task | Implement DELETE /decks/{id} with cascade | — | backend-agent | — |
| ↳ US-008-T2 | Task | Build SPA delete-deck confirmation modal | — | frontend-agent | — |
| ↳ US-008-T3 | Task | Verify history cleanup after deck deletion | — | qa-agent | — |
| US-009 | Story | Add a card to a deck | 3 | backend-agent | US-006 |
| ↳ US-009-T1 | Task | Implement POST /decks/{id}/cards endpoint | — | backend-agent | — |
| ↳ US-009-T2 | Task | Build SPA add-card form with clear-on-submit | — | frontend-agent | — |
| US-010 | Story | View all cards in a deck | 3 | backend-agent | US-006 |
| ↳ US-010-T1 | Task | Implement GET /decks/{id}/cards endpoint | — | backend-agent | — |
| ↳ US-010-T2 | Task | Build SPA card list view | — | frontend-agent | — |
| ↳ US-010-T3 | Task | Add empty-state for zero cards | — | frontend-agent | — |
| US-011 | Story | Edit a card | 2 | backend-agent | US-010 |
| ↳ US-011-T1 | Task | Implement PATCH /cards/{id} endpoint | — | backend-agent | — |
| ↳ US-011-T2 | Task | Build SPA edit-card form | — | frontend-agent | — |
| US-012 | Story | Delete a card | 2 | backend-agent | US-010 |
| ↳ US-012-T1 | Task | Implement DELETE /cards/{id} endpoint | — | backend-agent | — |
| ↳ US-012-T2 | Task | Build SPA delete-card confirmation | — | frontend-agent | — |
| US-020 | Story | Use the app equally well on phone and desktop | 3 | frontend-agent | US-005 |
| ↳ US-020-T1 | Task | Apply responsive CSS across all screens | — | frontend-agent | — |
| ↳ US-020-T2 | Task | Handle device rotation during study session | — | frontend-agent | — |
| ↳ US-020-T3 | Task | Verify no offline or installable app features | — | qa-agent | — |
| US-022 | Story | Use a free, English-only app with no extra services attached | 1 | qa-agent | — |
| ↳ US-022-T1 | Task | Audit all screens for no payment or upsell content | — | qa-agent | — |
| ↳ US-022-T2 | Task | Verify English-only interface and no notifications | — | qa-agent | — |
| ↳ US-022-T3 | Task | Verify no import, export, or third-party integrations | — | qa-agent | — |

## Sprint 3: Sprint 3 — Study Session, Results & Reliability

Deliver the full study session loop with shuffled order, flip, mark right/wrong, wrong-card repeat, end-of-session score, per-deck progress history, and cross-cutting error handling for failed saves.

Capacity: 20 points · Committed: 20

| Key | Type | Title | Points | Role | Depends on |
|---|---|---|---|---|---|
| US-013 | Story | Start a study session on a deck | 2 | backend-agent | US-010 |
| ↳ US-013-T1 | Task | Implement POST /decks/{id}/sessions endpoint | — | backend-agent | — |
| ↳ US-013-T2 | Task | Build SPA session start flow | — | frontend-agent | — |
| US-014 | Story | See cards in shuffled order | 2 | frontend-agent | US-013 |
| ↳ US-014-T1 | Task | Implement client-side card shuffle | — | frontend-agent | — |
| ↳ US-014-T2 | Task | Verify first-pass completeness | — | qa-agent | — |
| US-015 | Story | Flip a card to reveal the back | 2 | frontend-agent | US-013 |
| ↳ US-015-T1 | Task | Build SPA flip-card component | — | frontend-agent | — |
| ↳ US-015-T2 | Task | Add keyboard support for reveal and marking | — | frontend-agent | — |
| US-016 | Story | Mark a card right or wrong | 3 | frontend-agent | US-015 |
| ↳ US-016-T1 | Task | Implement mark-right logic | — | frontend-agent | — |
| ↳ US-016-T2 | Task | Implement mark-wrong logic | — | frontend-agent | — |
| ↳ US-016-T3 | Task | Track first-time-correct count | — | frontend-agent | — |
| US-017 | Story | Repeat wrong cards until answered correctly | 3 | frontend-agent | US-016 |
| ↳ US-017-T1 | Task | Implement wrong-card repeat loop | — | frontend-agent | — |
| ↳ US-017-T2 | Task | Detect session end and trigger result | — | frontend-agent | — |
| US-018 | Story | See my score at the end of a session | 3 | backend-agent | US-017 |
| ↳ US-018-T1 | Task | Implement POST /sessions/{id}/finish endpoint | — | backend-agent | — |
| ↳ US-018-T2 | Task | Build SPA session result screen | — | frontend-agent | — |
| US-019 | Story | See how a deck is going over time | 2 | backend-agent | US-018 |
| ↳ US-019-T1 | Task | Implement GET /decks/{id}/sessions endpoint | — | backend-agent | — |
| ↳ US-019-T2 | Task | Build SPA deck progress view | — | frontend-agent | — |
| US-021 | Story | Have my decks, cards and results stored reliably per account | 3 | backend-agent | US-006, US-009 |
| ↳ US-021-T1 | Task | Add consistent error responses across all API endpoints | — | backend-agent | — |
| ↳ US-021-T2 | Task | Implement SPA error messaging for failed saves | — | frontend-agent | — |

## Unscheduled

_Nothing unscheduled._
<!-- sdlc:auto:end sprints -->
