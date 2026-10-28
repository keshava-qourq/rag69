# Product Requirements

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
## Summary

### REQ-SCOPE · approved · source: requirements:scope

Lightweight MVP delivery scope for rag69, an internal single-organisation analytics dashboard, with product-owner-approved technology stack and services.

Delivery scope: lightweight. Requirements version: 1. Approved stack (do not substitute): Backend FastAPI 0.115 (Python for CSV/Excel parsing and aggregation); Cloud AWS (single account hosting, DB, file storage, scales to a few hundred users); Database PostgreSQL 16 (relational store for records, users/roles, filtering/aggregation); Frontend React 19 (interactive, responsive dashboards). Approved runtime services: Amazon S3 (saas; env AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, AWS_REGION, S3_BUCKET) for original file storage; Redis (container redis:7-alpine) used both as a background job Queue and as a Cache for dashboard aggregations. Required API keys/env vars: AWS_ACCESS_KEY_ID, AWS_REGION, AWS_SECRET_ACCESS_KEY, REDIS_URL, S3_BUCKET. Explicitly out of scope: native mobile app; any email-based flow (SendGrid was removed from the stack). Capabilities in scope: user login, manual data entry, CSV/Excel upload, dashboard with charts and tables, filtering by date and category, basic user documentation, email/password sign-in, S3 storage for uploads, bar/line/table chart types.

**Related:** EPIC-001, EPIC-002, EPIC-003, EPIC-004

### EPIC-001 · draft · source: requirements:EPIC-001

Authentication and Access Control: email/password sign-in for internal organisation members, with admin vs viewer role-based access, and admin-managed user accounts.

US-001 (critical): sign in with email/password reaches dashboard home on valid credentials (AC-001); invalid credentials show a generic, non-revealing error and keep the user on the sign-in page (AC-002); signing out ends the session, requiring re-authentication (AC-003). US-002 (high): viewers are denied user/data management functions (AC-004); admins can access user management, data management and all dashboards (AC-005); exactly two roles (admin, viewer) are assumed (AC-006, low-confidence). US-003 (high): admins create users with email/initial password/role (AC-007); role changes take effect on next sign-in (AC-008); deactivated users cannot sign in but their historical data is retained (AC-009); since email is out of scope, admins hand over initial passwords directly rather than via account-creation email (AC-010).

**Related:** US-001, US-002, US-003, AC-001, AC-002, AC-003, AC-004, AC-005, AC-006, AC-007, AC-008, AC-009, AC-010, NFR-001, NFR-002, NFR-003, NFR-011

- ⚠ ASSUMPTION (low confidence, unconfirmed): users are internal members of one organisation and only two roles (admin, viewer) exist — flagged for confirmation on the scope screen.
- ⚠ Email-based password reset/verification explicitly out of scope; no non-email recovery mechanism defined beyond an admin resetting/handing over a password directly (see NFR-011, accepted risk).

### EPIC-002 · draft · source: requirements:EPIC-002

Data Management: manual data entry and CSV/Excel upload, with uploaded originals stored durably in Amazon S3.

US-004 (high): admins enter records with date, category and metric via a form (AC-011); missing/invalid fields (e.g. non-numeric metric) are rejected with a validation message (AC-012); edits/deletes of saved manual records persist and flow through to dashboards (AC-013). US-005 (critical): admins upload a valid CSV/.xlsx file, rows import as records, and a success summary reports rows imported (AC-014); unsupported formats or uninterpretable columns are rejected with an explanation and no partial data (AC-015); upload history shows file name, uploader, time and import outcome (AC-016). US-006 (high): accepted uploads store the original file in S3, linked to the import record (AC-017); the import record can retrieve/reference the stored file (AC-018); if S3 storage fails, the user is told the upload did not complete and no partial import is recorded (AC-019).

**Related:** US-004, US-005, US-006, AC-011, AC-012, AC-013, AC-014, AC-015, AC-016, AC-017, AC-018, AC-019, NFR-004, NFR-006, NFR-009, NFR-010

- ⚠ ASSUMPTION (low confidence, unconfirmed): data enters only via manual entry and file upload (no live integrations), and the data domain is generic/unspecified — flagged for confirmation on the scope screen.

### EPIC-003 · draft · source: requirements:EPIC-003

Dashboards and Data Visualisation: configurable bar/line/table dashboards with date and category filtering, responsive for mobile browsers.

US-007 (critical): signed-in members see configured bar/line/table charts render current data (AC-020); charts/tables show a clear empty state instead of an error when no data matches (AC-021); dashboards reflect updated data on next load (AC-022). US-008 (high): admins add a chart choosing type (bar/line/table) and its data, saved and visible to all permitted users (AC-023); edits/removals persist and reflect on next view (AC-024); only bar, line and table types are offered (AC-025). US-009 (high): date-range filtering updates all charts/tables (AC-026); category filtering updates all charts/tables (AC-027); clearing filters restores the full dataset (AC-028). US-010 (medium): layout, charts and tables adapt to smaller screens without full-page horizontal scrolling (AC-029); access is via responsive web browser only, no native app (AC-030).

**Related:** US-007, US-008, US-009, US-010, AC-020, AC-021, AC-022, AC-023, AC-024, AC-025, AC-026, AC-027, AC-028, AC-029, AC-030, NFR-005, NFR-008, NFR-010

- ⚠ ASSUMPTION (low confidence, unconfirmed): core features are limited to configurable dashboards, charts/tables and date/category filtering — flagged for confirmation on the scope screen.
- ⚠ Explicitly out of scope for this MVP: report export/sharing, chart types beyond bar/line/table, and a native mobile app.

### EPIC-004 · draft · source: requirements:EPIC-004

User Documentation: basic end-user guidance covering sign-in, data entry/upload, and dashboards/filters, appropriate for a lightweight MVP.

US-011 (medium): documentation covers signing in, entering data manually, uploading CSV/Excel files, and using dashboards and filters (AC-031); documentation describes only in-scope MVP features and omits out-of-scope items such as export, sharing or a native mobile app (AC-032).

**Related:** US-011, AC-031, AC-032

- ⚠ ASSUMPTION (low confidence, unconfirmed): documentation is generic end-user guidance since the specific data domain is unknown.

### REQ-NFR · draft · source: requirements:NFR-001..NFR-012

Twelve non-functional requirements spanning privacy, security, availability, performance, scalability, compatibility and usability, plus two explicitly accepted risks.

NFR-001 (privacy): dashboards/data require sign-in. NFR-002 (security): sign-in errors never reveal which field was wrong. NFR-003 (security): viewers blocked from management functions; role changes apply on next sign-in; deactivated accounts cannot sign in. NFR-004 (availability): imports are all-or-nothing, including S3 failures. NFR-005 (performance): repeated dashboard loads reuse cached aggregations. NFR-006 (performance): large uploads parse/validate in a background job. NFR-007 (scalability): sized for a single organisation, up to a few hundred users. NFR-008 (compatibility): responsive layout usable on phone/tablet browsers, no native app. NFR-009 (availability): original uploaded files retained durably in S3. NFR-010 (usability): clear validation messages and empty states. NFR-011 (security, accepted risk): no email-based password recovery; admins hand over initial passwords directly. NFR-012 (compliance, accepted risk): no specific regulatory/compliance constraints identified or designed for in this internal tool.

**Related:** NFR-001, NFR-002, NFR-003, NFR-004, NFR-005, NFR-006, NFR-007, NFR-008, NFR-009, NFR-010, NFR-011, NFR-012, US-001, US-002, US-003, US-004, US-005, US-006, US-007, US-009, US-010

- ⚠ NFR-012 assumes no regulatory/compliance constraints apply; no industry or compliance domain was specified in this project's input, so this has not been independently verified.
- ⚠ NFR-011 accepted risk: if an admin loses their own credentials, no recovery path is defined anywhere in the input.
<!-- sdlc:auto:end narrative -->

<!-- sdlc:auto:start summary -->
**Requirements version:** v1  
**Delivery scope:** lightweight  
**Approved:** 2026-10-28

**Capabilities in scope:** User login, Manual data entry, CSV/Excel data upload, Dashboard with charts and tables, Filtering by date and category, Basic user documentation, Email and password sign-in, Amazon S3 storage for uploaded files, Bar, line and table chart types

**Approved technology stack:**

| Layer | Choice | Rationale |
|---|---|---|
| backend | FastAPI | The heavy lifting here is receiving CSV/Excel uploads, validating and storing the rows, running the aggregations behind each chart, and producing exports. FastAPI is a Python framework, and Python has the strongest, best-known tools for reading spreadsheets and crunching tabular data, so the import and reporting features are natural to write. It is light and fast enough for your few-hundred-user, single-organisation scale. |
| cloud | AWS | A single-organisation internal dashboard needs somewhere dependable to run the app, store the database, and keep uploaded files and exported reports. AWS covers all of that in one account, scales down to a modest, low-cost footprint for a few hundred users, and its file storage (S3) is the natural home for your spreadsheet uploads and generated reports. It is the most widely supported option, so hosting help is easy to find. |
| database | PostgreSQL | Everything your users bring in -- manually entered records and uploaded spreadsheet rows -- is structured tabular data that you then filter, group and sum for charts. PostgreSQL is a relational database built precisely for that, and it does the date/category filtering and aggregation your dashboards depend on quickly and reliably at your data volumes. It also handles the user accounts and role permissions in the same place, so there is one system to run. |
| frontend | React | Your product is fundamentally a set of interactive, configurable dashboards -- charts, tables, filters by date and category -- that update as the user clicks. React is built for exactly this kind of screen, and because it is the most widely used option, the charting and data-grid building blocks you need (graphs, pivot tables, drag-to-arrange dashboards) already exist ready-made, which keeps the build shorter. It also handles a responsive layout that works in a mobile browser, which is what you asked for instead of a native app. |
<!-- sdlc:auto:end summary -->

<!-- sdlc:auto:start epics -->
## EPIC-001: Authentication and Access Control

Email/password sign-in for internal members of a single organisation, with role-based access distinguishing an admin (who manages users and data) from standard viewers. ASSUMPTION (low confidence): users are internal members of one organisation rather than external customers or the public, and the only roles are admin and viewer — correct on the scope screen if wrong. OUT OF SCOPE for this MVP: email-based flows such as emailed password resets or verification, because email (SendGrid) was removed from the stack; any such flow must be handled without email.

### US-001: Sign in with email and password

**Priority:** critical

> As a organisation member, I want to sign in using my email address and password, so that I can access the dashboards and data for my organisation securely.

| ID | Given | When | Then |
|---|---|---|---|
| AC-001 | I am a registered user with a valid email and password | I submit the correct credentials on the sign-in page | I am authenticated and taken to the dashboard home page |
| AC-002 | I am on the sign-in page | I submit an email or password that does not match an account | I remain on the sign-in page and see an error message that does not reveal which field was wrong |
| AC-003 | I am an authenticated user | I choose to sign out | my session is ended and I must sign in again to access any dashboard or data |

### US-002: Role-based access for admin and viewer

**Priority:** high

> As a system, I want to grant permissions based on whether a user is an admin or a viewer, so that only admins can manage users and data while viewers can only view.

| ID | Given | When | Then |
|---|---|---|---|
| AC-004 | I am signed in as a viewer | I attempt to access user management or data management functions | access is denied and the functions are not available to me |
| AC-005 | I am signed in as an admin | I open the application | I can access user management and data management functions in addition to all dashboards |
| AC-006 | the organisation needs to define roles | the system is configured | ASSUMPTION (low confidence): exactly two roles exist — admin and viewer — and this should be confirmed on the scope screen |

### US-003: Manage user accounts (admin)

**Priority:** high

> As a admin, I want to create, edit and deactivate user accounts and assign roles, so that I control who in the organisation can access the system and at what level.

| ID | Given | When | Then |
|---|---|---|---|
| AC-007 | I am signed in as an admin | I create a new user with an email, an initial password and a role | the user is saved and can sign in with those credentials |
| AC-008 | I am signed in as an admin viewing an existing user | I change their role between admin and viewer | the new role takes effect on their next sign-in |
| AC-009 | I am signed in as an admin | I deactivate a user account | that user can no longer sign in but their historical data remains intact |
| AC-010 | email is out of scope for this MVP | a new user needs their credentials | the admin provides the initial password directly (no account-creation email is sent) |

## EPIC-002: Data Management

Users bring data into the system through manual entry and CSV/Excel file upload. Uploaded files are stored in Amazon S3. ASSUMPTION (low confidence): data enters only via manual entry and file upload, not via live integrations with external systems, and the subject/domain of the data (sales, operations, finance, etc.) is unknown and treated generically — correct on the scope screen if wrong. OUT OF SCOPE for this MVP: live data integrations and connectors.

### US-004: Enter data manually

**Priority:** high

> As a admin, I want to add data records manually through a form, so that I can capture metrics that are not available as a file.

| ID | Given | When | Then |
|---|---|---|---|
| AC-011 | I am signed in as an admin on the manual data entry form | I enter values including a date and a category and submit | the record is saved and becomes available for display on dashboards |
| AC-012 | I am entering a record | I submit with a required field missing or an invalid value (e.g. a non-numeric metric) | the record is not saved and I see a validation message identifying the problem |
| AC-013 | I have previously saved a manual record | I edit or delete that record | the change is persisted and reflected in dashboards that use it |

### US-005: Upload CSV or Excel files

**Priority:** critical

> As a admin, I want to upload data from CSV or Excel files, so that I can bring existing datasets into the system without re-keying them.

| ID | Given | When | Then |
|---|---|---|---|
| AC-014 | I am signed in as an admin on the upload screen | I select a valid CSV or Excel (.xlsx) file and confirm the upload | the file is accepted, its rows are imported as data records, and a success summary shows the number of rows imported |
| AC-015 | I upload a file whose format is unsupported or whose columns cannot be interpreted | the system validates it | the upload is rejected and I see an error explaining what was wrong, with no partial data left in an inconsistent state |
| AC-016 | a file has been uploaded | I view the upload history | I can see the file name, who uploaded it, when, and the outcome of the import |

### US-006: Store uploaded files in Amazon S3

**Priority:** high

> As a system, I want to persist each uploaded file in Amazon S3, so that original files are retained durably and can be referenced or re-processed.

| ID | Given | When | Then |
|---|---|---|---|
| AC-017 | an admin uploads a CSV or Excel file | the upload is accepted | the original file is stored as an object in Amazon S3 and the stored reference is linked to the import record |
| AC-018 | a file has been stored in S3 | the import record is viewed | the system can retrieve or reference the original stored file |
| AC-019 | storing a file in S3 fails | the upload is attempted | the user is informed the upload did not complete and no partial import is recorded |

## EPIC-003: Dashboards and Data Visualisation

Configurable dashboards that display imported and manually entered data as bar charts, line charts and tables, with filtering by date and category. Delivered as a responsive web app usable in a mobile browser. ASSUMPTION (low confidence): the core features are configurable dashboards, charts/tables and filtering — correct on the scope screen if wrong. OUT OF SCOPE for this MVP: report export and sharing (export/share was discussed for a larger scope but is not included in this Lightweight MVP), chart types other than bar, line and table, and a native mobile app (responsive web only).

### US-007: View data as charts and tables on a dashboard

**Priority:** critical

> As a organisation member, I want to see my organisation's data rendered as bar charts, line charts and tables on a dashboard, so that I can monitor the metrics relevant to my work at a glance.

| ID | Given | When | Then |
|---|---|---|---|
| AC-020 | data has been entered or uploaded and I am signed in | I open a dashboard | its configured bar charts, line charts and tables render using the current data |
| AC-021 | a dashboard includes a chart | the underlying data has no records for the selected scope | the chart or table shows a clear empty state rather than an error |
| AC-022 | I am viewing a dashboard | the underlying data changes (e.g. a new upload completes) | the dashboard reflects the updated data when next loaded |

### US-008: Configure dashboards and their charts

**Priority:** high

> As a admin, I want to add, remove and configure charts and tables on a dashboard, so that the dashboard shows the metrics and chart types that matter to the organisation.

| ID | Given | When | Then |
|---|---|---|---|
| AC-023 | I am signed in as an admin editing a dashboard | I add a chart and choose its type (bar, line or table) and the data it displays | the chart is saved and appears on the dashboard for all permitted users |
| AC-024 | I am editing a dashboard | I remove or reconfigure an existing chart | the change is persisted and reflected when the dashboard is next viewed |
| AC-025 | I choose a chart type | I select from the available options | only bar, line and table types are offered, consistent with this MVP scope |

### US-009: Filter dashboard data by date and category

**Priority:** high

> As a organisation member, I want to filter the data shown on a dashboard by date and by category, so that I can focus on the time period and segment I care about.

| ID | Given | When | Then |
|---|---|---|---|
| AC-026 | I am viewing a dashboard with date and category filters | I select a date range | all charts and tables on the dashboard update to show only data within that range |
| AC-027 | I am viewing a dashboard | I select one or more categories | all charts and tables update to show only data matching those categories |
| AC-028 | I have applied filters | I clear the filters | the dashboard returns to showing the full unfiltered dataset |

### US-010: Use the application in a mobile browser

**Priority:** medium

> As a organisation member, I want the web app to adapt to the size of my device's screen, so that I can view dashboards on a phone or tablet browser without a native app.

| ID | Given | When | Then |
|---|---|---|---|
| AC-029 | I open the application in a mobile browser | a dashboard loads | its layout, charts and tables adapt to the smaller screen and remain usable without horizontal scrolling of the whole page |
| AC-030 | no native mobile app is in scope | I access the product on any device | I do so through a responsive web browser only |

## EPIC-004: User Documentation

Basic user-facing documentation covering how to sign in, enter and upload data, and use dashboards and filters, appropriate for a Lightweight MVP. ASSUMPTION (low confidence): documentation is basic end-user guidance for the generic analytics features described, since the specific data domain is unknown.

### US-011: Access basic user documentation

**Priority:** medium

> As a organisation member, I want to read basic documentation on how to use the application, so that I can learn to sign in, manage data and use dashboards without external help.

| ID | Given | When | Then |
|---|---|---|---|
| AC-031 | I am a user of the application | I open the documentation | I find guidance covering signing in, entering data manually, uploading CSV/Excel files, and using dashboards and filters |
| AC-032 | I am reading the documentation | I look for a feature that is part of this MVP | the documentation describes only features that exist in this version and does not reference out-of-scope features such as export, sharing or a native mobile app |
<!-- sdlc:auto:end epics -->
