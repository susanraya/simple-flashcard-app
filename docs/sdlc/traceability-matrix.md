# Traceability Matrix

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start legend -->
Built from recorded links, not written by a model: requirement key → plan item (`source_stable_key`) → development ticket (`stable_key`) → the ticket's test steps → the last live deployment that started after the work finished. **AC tests** counts the story's acceptance criteria that have a test case, and those whose test cases all passed in the latest finished E2E run.
<!-- sdlc:auto:end legend -->

<!-- sdlc:auto:start matrix -->
| Requirement | Epic | Title | Plan items | Sprint | Design | Code | Commits | Ticket | Tests | AC tests | Deployed |
|---|---|---|---|---|---|---|---|---|---|---|---|
| US-001 | EPIC-001 | Sign up for an account | US-001, US-001-T1, US-001-T2, US-001-T3, US-001-T4, US-001-T5 | 1 | POST /auth/learners, api, auth_provider, db, learners, spa | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-002 | EPIC-001 | Sign in to an existing account | US-002, US-002-T1, US-002-T2, US-002-T3 | 1 | auth_provider, learners, spa | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-003 | EPIC-001 | Sign out | US-003, US-003-T1, US-003-T2 | 1 | auth_provider, spa | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-004 | EPIC-001 | Keep every learner's data private to their account | US-004, US-004-T1, US-004-T2, US-004-T3 | 1 | api, cards, db, decks, learners, spa, study_sessions | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-005 | EPIC-002 | See my decks on the home screen | US-005, US-005-T1, US-005-T2, US-005-T3 | 1 | GET /decks, api, cards, db, decks, spa | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-006 | EPIC-002 | Create a deck | US-006, US-006-T1, US-006-T2 | 1 | POST /decks, api, db, decks, spa | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-007 | EPIC-002 | Rename a deck | US-007, US-007-T1, US-007-T2 | 2 | PATCH /decks/{id}, api, decks, spa | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-008 | EPIC-002 | Delete a deck with confirmation | US-008, US-008-T1, US-008-T2, US-008-T3 | 2 | DELETE /decks/{id}, api, cards, db, decks, spa, study_sessions | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-009 | EPIC-003 | Add a card to a deck | US-009, US-009-T1, US-009-T2 | 2 | POST /decks/{id}/cards, api, cards, db, decks, spa | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-010 | EPIC-003 | View all cards in a deck | US-010, US-010-T1, US-010-T2, US-010-T3 | 2 | GET /decks/{id}/cards, api, cards, db, spa | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-011 | EPIC-003 | Edit a card | US-011, US-011-T1, US-011-T2 | 2 | PATCH /cards/{id}, api, cards, spa | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-012 | EPIC-003 | Delete a card | US-012, US-012-T1, US-012-T2 | 2 | DELETE /cards/{id}, api, cards, spa | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-013 | EPIC-004 | Start a study session on a deck | US-013, US-013-T1, US-013-T2 | 3 | POST /decks/{id}/sessions, api, cards, db, spa, study_sessions | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-014 | EPIC-004 | See cards in shuffled order | US-014, US-014-T1, US-014-T2 | 3 | cards, spa | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-015 | EPIC-004 | Flip a card to reveal the back | US-015, US-015-T1, US-015-T2 | 3 | spa | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-016 | EPIC-004 | Mark a card right or wrong | US-016, US-016-T1, US-016-T2, US-016-T3 | 3 | spa, study_sessions | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-017 | EPIC-004 | Repeat wrong cards until answered correctly | US-017, US-017-T1, US-017-T2 | 3 | spa | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-018 | EPIC-005 | See my score at the end of a session | US-018, US-018-T1, US-018-T2 | 3 | POST /sessions/{id}/finish, api, db, spa, study_sessions | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-019 | EPIC-005 | See how a deck is going over time | US-019, US-019-T1, US-019-T2 | 3 | GET /decks/{id}/sessions, api, db, spa, study_sessions | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-020 | EPIC-006 | Use the app equally well on phone and desktop | US-020, US-020-T1, US-020-T2, US-020-T3 | 2 | spa | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-021 | EPIC-006 | Have my decks, cards and results stored reliably per account | US-021, US-021-T1, US-021-T2 | 3 | api, cards, decks, spa, study_sessions | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-022 | EPIC-006 | Use a free, English-only app with no extra services attached | US-022, US-022-T1, US-022-T2, US-022-T3 | 2 | spa | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
<!-- sdlc:auto:end matrix -->
