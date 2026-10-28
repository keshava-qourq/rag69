# Traceability Matrix

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start legend -->
Built from recorded links, not written by a model: requirement key → plan item (`source_stable_key`) → development ticket (`stable_key`) → the ticket's test steps → the last live deployment that started after the work finished. **AC tests** counts the story's acceptance criteria that have a test case, and those whose test cases all passed in the latest finished E2E run.
<!-- sdlc:auto:end legend -->

<!-- sdlc:auto:start matrix -->
| Requirement | Epic | Title | Plan items | Sprint | Design | Code | Commits | Ticket | Tests | AC tests | Deployed |
|---|---|---|---|---|---|---|---|---|---|---|---|
| US-001 | EPIC-001 | Sign in with email and password | US-001 | 1 | POST /auth/login, POST /auth/logout, api_backend, postgres_db, users, web_frontend | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-002 | EPIC-001 | Role-based access for admin and viewer | US-002 | 1 | api_backend, postgres_db, users | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-003 | EPIC-001 | Manage user accounts (admin) | US-003 | 1 | GET /users, PATCH /users/{id}, POST /users, api_backend, postgres_db, users, web_frontend | — | — | not started | not run | 0/4 tested · 0/4 passing | — |
| US-004 | EPIC-002 | Enter data manually | US-004 | 1 | DELETE /records/{id}, PATCH /records/{id}, POST /records, api_backend, data_records, postgres_db, web_frontend | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-005 | EPIC-002 | Upload CSV or Excel files | US-005, US-005-T1, US-005-T2, US-005-T3, US-005-T4 | 2 | GET /uploads, POST /uploads, api_backend, data_records, import_worker, imports, postgres_db, redis_queue, web_frontend | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-006 | EPIC-002 | Store uploaded files in Amazon S3 | US-006 | 2 | POST /uploads, api_backend, imports, s3_store | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-007 | EPIC-003 | View data as charts and tables on a dashboard | US-007, US-007-T1, US-007-T2, US-007-T3 | 2 | GET /dashboards, GET /dashboards/{id}/data, api_backend, charts, dashboards, data_records, postgres_db, redis_cache, web_frontend | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-008 | EPIC-003 | Configure dashboards and their charts | US-008, US-008-T1, US-008-T2 | 3 | DELETE /charts/{id}, PATCH /charts/{id}, POST /dashboards, POST /dashboards/{id}/charts, api_backend, charts, dashboards, postgres_db, web_frontend | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-009 | EPIC-003 | Filter dashboard data by date and category | US-009 | 3 | GET /dashboards/{id}/data, api_backend, dashboards, data_records, redis_cache, web_frontend | — | — | not started | not run | 0/3 tested · 0/3 passing | — |
| US-010 | EPIC-003 | Use the application in a mobile browser | US-010 | 3 | web_frontend | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
| US-011 | EPIC-004 | Access basic user documentation | US-011 | 3 | web_frontend | — | — | not started | not run | 0/2 tested · 0/2 passing | — |
<!-- sdlc:auto:end matrix -->
