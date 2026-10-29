<!-- sdlc:auto:start adr -->
# ADR-0001: Use React (TypeScript) for Frontend

Status: Accepted  
Date: 2026-09-12

## Context and Problem Statement

Which Frontend technology does the project use? Decided in architecture v1.

## Considered Options

- React (TypeScript)
- Vue
- Svelte

## Decision Outcome

Chosen option: React (TypeScript), because Approved stack. A single responsive SPA renders deck list, card management, study flow, and results; TypeScript keeps the session-shuffle and queue logic type-safe.

## Consequences

No SSR or PWA in scope, so SEO and offline use are not available — acceptable per requirements.
<!-- sdlc:auto:end adr -->