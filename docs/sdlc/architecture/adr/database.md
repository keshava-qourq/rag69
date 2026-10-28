<!-- sdlc:auto:start adr -->
# ADR-0003: Use PostgreSQL 16 for Database

Status: Accepted  
Date: 2026-10-28

## Context and Problem Statement

Which Database technology does the project use? Decided in architecture v1.

## Considered Options

- PostgreSQL 16
- MySQL
- SQLite

## Decision Outcome

Chosen option: PostgreSQL 16, because Approved stack. Relational store for users, roles, records, dashboards and imports; its indexed date/category grouping and aggregation drive the dashboards and keep everything in one system.

## Consequences

Aggregations are offloaded to Redis caching under repeated load (NFR-005); managing a relational schema requires migrations.
<!-- sdlc:auto:end adr -->