<!-- sdlc:auto:start adr -->
# ADR-0004: Use AWS for Cloud

Status: Accepted  
Date: 2026-09-12

## Context and Problem Statement

Which Cloud technology does the project use? Decided in architecture v1.

## Considered Options

- AWS
- GCP
- Azure

## Decision Outcome

Chosen option: AWS, because Approved stack. S3+CloudFront serves the SPA, App Runner/Fargate runs FastAPI, RDS runs PostgreSQL, Cognito handles email-and-password auth.

## Consequences

More moving parts than a monolithic host, but each is managed and free-tier-friendly at this scale.
<!-- sdlc:auto:end adr -->