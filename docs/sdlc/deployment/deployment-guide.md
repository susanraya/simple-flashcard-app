# Deployment Guide

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start how-it-deploys -->
Pushes to `main` run `.github/workflows/deploy.yml`, which builds the API image (if there is a backend) and deploys the SPA to AWS Amplify. Commits touching only `docs/sdlc/**` don't deploy. Deployments can also be started from the platform's Deployment tab.
<!-- sdlc:auto:end how-it-deploys -->

<!-- sdlc:auto:start environments -->
| Name | Service | Runtime | Scaling | Environment |
|---|---|---|---|---|
| CloudFront Distribution | AWS CloudFront | Managed CDN | Automatic edge | dev |
| S3 Static Bucket | AWS S3 | Object storage | Automatic | dev |
| App Server | AWS App Runner (or ECS Fargate single task) | FastAPI on Uvicorn | Single small instance | dev |
| PostgreSQL DB | Amazon RDS for PostgreSQL (db.t3.micro) | Managed PostgreSQL | Single AZ, small instance | dev |
| Cognito User Pool | AWS Cognito | Managed auth | Automatic | dev |
<!-- sdlc:auto:end environments -->

<!-- sdlc:auto:start live -->
_Not deployed yet._
<!-- sdlc:auto:end live -->

<!-- sdlc:auto:start topology -->
```mermaid
graph LR
  n_CloudFront_Distribution["CloudFront Distribution<br/>AWS CloudFront"]
  n_S3_Static_Bucket["S3 Static Bucket<br/>AWS S3"]
  n_App_Server["App Server<br/>AWS App Runner (or ECS Fargate single task)"]
  n_PostgreSQL_DB["PostgreSQL DB<br/>Amazon RDS for PostgreSQL (db.t3.micro)"]
  n_Cognito_User_Pool["Cognito User Pool<br/>AWS Cognito"]
  n_CloudFront_Distribution -->|"HTTPS"| n_S3_Static_Bucket
  n_App_Server -->|"TCP/TLS"| n_PostgreSQL_DB
  n_App_Server -->|"HTTPS (JWKS verification)"| n_Cognito_User_Pool
```
<!-- sdlc:auto:end topology -->
