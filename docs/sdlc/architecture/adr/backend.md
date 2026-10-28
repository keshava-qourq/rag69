<!-- sdlc:auto:start adr -->
# ADR-0002: Use FastAPI 0.115 for Backend

Status: Accepted  
Date: 2026-10-28

## Context and Problem Statement

Which Backend technology does the project use? Decided in architecture v1.

## Considered Options

- FastAPI 0.115
- Django REST Framework
- Flask

## Decision Outcome

Chosen option: FastAPI 0.115, because Approved stack. Python gives first-class spreadsheet parsing and tabular aggregation for imports and dashboard queries; FastAPI is light and fast at this scale.

## Consequences

Background work and workers must be wired explicitly (via Redis/RQ) rather than coming bundled.
<!-- sdlc:auto:end adr -->