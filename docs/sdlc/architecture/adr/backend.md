<!-- sdlc:auto:start adr -->
# ADR-0002: Use FastAPI (Python) for Backend

Status: Accepted  
Date: 2026-09-12

## Context and Problem Statement

Which Backend technology does the project use? Decided in architecture v1.

## Considered Options

- FastAPI (Python)
- Node/Express
- Django

## Decision Outcome

Chosen option: FastAPI (Python), because Approved stack. FastAPI provides Pydantic validation for deck/card/session payloads and JWT dependency injection for per-learner scoping with minimal boilerplate.

## Consequences

Stateless single instance; session shuffle is client-side so no server-side session store is needed.
<!-- sdlc:auto:end adr -->