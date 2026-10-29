<!-- sdlc:auto:start adr -->
# ADR-0003: Use PostgreSQL for Database

Status: Accepted  
Date: 2026-09-12

## Context and Problem Statement

Which Database technology does the project use? Decided in architecture v1.

## Considered Options

- PostgreSQL
- MySQL
- SQLite

## Decision Outcome

Chosen option: PostgreSQL, because Approved stack. PostgreSQL holds learners, decks, cards, and study_sessions with FK cascade deletes for deck removal.

## Consequences

Single-AZ small instance is fine for tens of users but not HA — acceptable per scope.
<!-- sdlc:auto:end adr -->