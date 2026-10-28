<!-- sdlc:auto:start adr -->
# ADR-0004: Use AWS for Cloud

Status: Accepted  
Date: 2026-10-28

## Context and Problem Statement

Which Cloud technology does the project use? Decided in architecture v1.

## Considered Options

- AWS
- Google Cloud
- Azure

## Decision Outcome

Chosen option: AWS, because Approved stack. One account hosts the app (ECS Fargate), database (RDS PostgreSQL), cache/queue (Redis) and durable file storage (S3) at a low-cost footprint for a few hundred users.

## Consequences

Some AWS-specific configuration (IAM, VPC, Fargate) is required; widely supported so help is easy to find.
<!-- sdlc:auto:end adr -->