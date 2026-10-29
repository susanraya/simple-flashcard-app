<!-- sdlc:auto:start adr -->
# ADR-0005: Use AWS Cognito User Pools for Auth

Status: Accepted  
Date: 2026-09-12

## Context and Problem Statement

Which Auth technology does the project use? Decided in architecture v1.

## Considered Options

- AWS Cognito User Pools
- Auth0
- Firebase Auth

## Decision Outcome

Chosen option: AWS Cognito User Pools, because Email-and-password-only hosted auth with JWT issuance that integrates natively with the approved AWS stack; no social login or SSO configured.

## Consequences

Cognito's hosted UI and SDK quirks add a little frontend complexity, but remove all password-handling from the backend.
<!-- sdlc:auto:end adr -->