# rag69 — SDLC Documentation

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start overview -->
kkk

**Documentation version:** v1
<!-- sdlc:auto:end overview -->

## Contents

<!-- sdlc:auto:start contents -->
| Document | State |
|---|---|
| [Requirements](requirements/README.md) | v1 approved |
| [Architecture](architecture/README.md) | 7 entries |
| [Development](development/README.md) | 4 entries |
| [Testing](testing/README.md) | 1 entry |
| [Deployment](deployment/README.md) | 1 entry |
| [Maintenance](maintenance/README.md) | 1 entry |
| [Data model](architecture/data-model.md) | generated |
| [API (OpenAPI)](architecture/api/openapi.yaml) | generated |
| [Decisions (ADRs)](architecture/adr/README.md) | 4 decisions |
| [Sprint plan](development/sprint-plan.md) | 3 sprints |
| [Developer guide](development/developer-guide.md) | not generated yet |
| [API reference](development/api-reference.md) | 0 routes |
| [Test report](testing/test-report.md) | not run yet |
| [Tests](testing/test-cases.md) | 0 tests |
| [Deployment guide](deployment/deployment-guide.md) | not deployed yet |
| [Runbook](deployment/runbook.md) | not deployed yet |
| [Release notes](deployment/release-notes.md) | 0 releases |
| [Traceability matrix](traceability-matrix.md) | 11 requirements |
| [Changelog](CHANGELOG.md) | 1 version |
<!-- sdlc:auto:end contents -->

## Open gaps

<!-- sdlc:auto:start open-gaps -->
### Requirements

- ASSUMPTION (low confidence, unconfirmed): users are internal members of one organisation and only two roles (admin, viewer) exist — flagged for confirmation on the scope screen.
- Email-based password reset/verification explicitly out of scope; no non-email recovery mechanism defined beyond an admin resetting/handing over a password directly (see NFR-011, accepted risk).
- ASSUMPTION (low confidence, unconfirmed): data enters only via manual entry and file upload (no live integrations), and the data domain is generic/unspecified — flagged for confirmation on the scope screen.
- ASSUMPTION (low confidence, unconfirmed): core features are limited to configurable dashboards, charts/tables and date/category filtering — flagged for confirmation on the scope screen.
- Explicitly out of scope for this MVP: report export/sharing, chart types beyond bar/line/table, and a native mobile app.
- ASSUMPTION (low confidence, unconfirmed): documentation is generic end-user guidance since the specific data domain is unknown.
- NFR-012 assumes no regulatory/compliance constraints apply; no industry or compliance domain was specified in this project's input, so this has not been independently verified.
- NFR-011 accepted risk: if an admin loses their own credentials, no recovery path is defined anywhere in the input.

### Architecture

- No architecture diagrams or explicit capacity/sizing beyond NFR-007's 'few hundred users' target were provided.
- This is the planned topology from the architecture phase; no deployment phase input exists yet confirming any of these nodes were actually provisioned.

### Development

- Input is labeled 'planning + implementation' but only planning data (sprints, backlog items, points, assigned roles) was supplied — no commits, build artifacts, or completion status were provided for any item.
- US-004's assignment to Sprint 1 is inferred from the sprint goal text, not an explicit per-item sprint tag in the input — recommend confirming.
- Sprint membership for these items is inferred from the sprint goal text matching their epics, not an explicit per-item sprint tag in the input — recommend confirming.

### Testing

- Testing phase has not started; no test plans, cases, or results are available to document.

### Deployment

- No deployment recorded yet; only a planned (not executed) deployment topology exists in the architecture phase.

### Maintenance

- Maintenance phase has no input because the project has not been deployed; nothing to document yet.
<!-- sdlc:auto:end open-gaps -->
