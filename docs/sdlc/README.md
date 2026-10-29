# Simple flashcard app — SDLC Documentation

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start overview -->
create a simple flashcard app

**Documentation version:** v2
<!-- sdlc:auto:end overview -->

## Contents

<!-- sdlc:auto:start contents -->
| Document | State |
|---|---|
| [Requirements](requirements/README.md) | v1 approved |
| [Architecture](architecture/README.md) | 12 entries |
| [Development](development/README.md) | 4 entries |
| [Testing](testing/README.md) | 1 entry |
| [Deployment](deployment/README.md) | 1 entry |
| [Maintenance](maintenance/README.md) | 1 entry |
| [Data model](architecture/data-model.md) | generated |
| [API (OpenAPI)](architecture/api/openapi.yaml) | generated |
| [Decisions (ADRs)](architecture/adr/README.md) | 5 decisions |
| [Sprint plan](development/sprint-plan.md) | 3 sprints |
| [Developer guide](development/developer-guide.md) | generated |
| [API reference](development/api-reference.md) | 1 route |
| [Test report](testing/test-report.md) | not run yet |
| [Tests](testing/test-cases.md) | 0 tests |
| [Deployment guide](deployment/deployment-guide.md) | not deployed yet |
| [Runbook](deployment/runbook.md) | not deployed yet |
| [Release notes](deployment/release-notes.md) | 0 releases |
| [Traceability matrix](traceability-matrix.md) | 22 requirements |
| [Changelog](CHANGELOG.md) | 2 versions |
<!-- sdlc:auto:end contents -->

## Open gaps

<!-- sdlc:auto:start open-gaps -->
### Requirements

- AC-001 and AC-003 reference password rules ('meets the stated rules' / 'fails the stated rules') but no actual password policy (length, complexity) is defined anywhere in the provided input.

### Architecture

- study_sessions has a deck_id but no explicit learner_id column shown; per-learner scoping for session queries presumably relies on joining through decks.learner_id, but this join path is not explicitly confirmed in the input.

### Development

- No ticket-level completion/status (done, in review, blocked, etc.) was provided for any story or task — only planned scope is known, not what has been built.
- No code artifacts, pull requests, commit references, or build logs were included in this input.
- All 6 epics have role '(unassigned)' in the plan — no owning role recorded at the epic level.
- US-022 (free, English-only app, no extra services) is not explicitly referenced by any sprint goal, unlike its sibling stories US-020 and US-021 — unclear which sprint is intended to deliver/verify it; flagging as an ambiguity for confirmation.
- No completion status reported for any story or task in this sprint — cannot confirm sign-up, sign-in, sign-out, or data-isolation work is actually done.
- No completion status reported for any story or task in this sprint.
- US-020 belongs to EPIC-006 (Responsive Web Experience and Platform Foundations) in the backlog grouping but is addressed by this sprint's goal text — flagging the cross-epic placement for confirmation rather than silently resolving it.
- No completion status reported for any story or task in this sprint — study-session mechanics, scoring, progress history, and error handling cannot be confirmed as built.
- US-021 belongs to EPIC-006 (Responsive Web Experience and Platform Foundations) in the backlog grouping but is addressed by this sprint's goal text — flagging the cross-epic placement for confirmation.

### Testing

- Testing phase has not started; no test plans, cases, or results are available to document.
- The 22 QA-role tasks in the development backlog (e.g. verify data isolation, verify responsive/offline behavior, verify english-only/no-billing) have not been reported as executed.

### Deployment

- No deployment recorded yet; it is unknown whether the approved architecture has actually been provisioned in AWS.

### Maintenance

- No maintenance phase data available; there is nothing to document because the application has not been deployed.
<!-- sdlc:auto:end open-gaps -->
