<!-- sdlc:auto:start adr -->
# ADR-0001: Use React 19 for Frontend

Status: Accepted  
Date: 2026-10-28

## Context and Problem Statement

Which Frontend technology does the project use? Decided in architecture v1.

## Considered Options

- React 19
- Vue
- Angular

## Decision Outcome

Chosen option: React 19, because Approved stack. Delivers the interactive, configurable dashboards (charts, tables, date/category filters) as a responsive SPA that works in a mobile browser without a native app.

## Consequences

A SPA needs a separate static host (S3/CloudFront) and client-side auth handling; mature charting and grid libraries offset the build effort.
<!-- sdlc:auto:end adr -->