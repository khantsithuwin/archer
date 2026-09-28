# Archer MVP roadmap

Last reviewed: 2026-09-22

This file tracks delivery progress across Archer's three independent projects. Product behavior and acceptance criteria remain authoritative in `SPEC.md`; engineering boundaries remain authoritative in `AGENTS.md`.

## Status legend

- `[x]` Finished and available in the owning project.
- `[~]` Partially implemented; the remaining work is described below it.
- `[ ]` Not started or not yet available to users.

## MVP definition

Archer's MVP includes:

- Email/password accounts for clients, freelancers, administrators, and accounts using both marketplace roles.
- Client and freelancer profiles, freelancer portfolios, and public freelancer discovery.
- Signed-in job discovery with filtering, sorting, pagination, and saved jobs.
- Client job drafts, publishing, proposal review, hiring, and job status management.
- Freelancer proposals, contract offers, milestones, delivery, completion, cancellation, and disputes.
- Conversations, messages, notifications, reports, and post-contract reviews.
- Administrator metrics, user and content moderation, report/dispute resolution, taxonomy management, and an audit trail.
- Consistent USD and MMK handling without conversion or payment processing.
- Web and Expo mobile experiences consuming the same versioned API contract.
- Loading, empty, error, permission-denied, and responsive states for every user-facing journey.

## Completed

### Workspace and documentation

- [x] Define the product features and acceptance criteria in `SPEC.md`.
- [x] Define cross-project engineering boundaries in `AGENTS.md`.
- [x] Document setup, demo accounts, and developer workflow in the root and project READMEs.
- [x] Keep the web and API as independently installable and deployable Git repositories.
- [x] Create deterministic local seed data with connected jobs, proposals, contracts, and demo users.
- [x] Add client, freelancer, both-role, and administrator demo accounts.

### API (`archer-api`)

- [x] Build the Express + TypeScript API with Prisma 7 and SQLite.
- [x] Add JWT access/refresh authentication, logout, session revocation, email-verification tokens, and password-reset tokens.
- [x] Enforce server-side mode, ownership, validation, and status-transition rules.
- [x] Add client and freelancer profile APIs and portfolio CRUD endpoints.
- [x] Add category, skill, freelancer-discovery, and public freelancer-profile reads.
- [x] Add job discovery, drafts, editing, publishing, closing, and saved-job endpoints.
- [x] Add proposal submission, editing, withdrawal, shortlisting, rejection, and acceptance.
- [x] Add contract offers, milestone delivery/review, completion, cancellation, and disputes.
- [x] Add conversation, message, read-state, notification, review, and report endpoints.
- [x] Add administrator metrics, report updates, user suspension/restoration, and dispute resolution.
- [x] Record contract and administrator audit events for implemented status-changing actions.
- [x] Document implemented behavior in the versioned OpenAPI contract.
- [x] Cover money, authorization, job, proposal, contract, cancellation, and dispute journeys with automated tests.

### Web (`archer-app`)

- [x] Build a professional public landing page without authenticated navigation or public job listings.
- [x] Add registration and sign-in for client, freelancer, and both-role accounts.
- [x] Add the authenticated responsive sidebar workspace and sign-out behavior.
- [x] Add client and freelancer profile onboarding and editing for current core fields.
- [x] Add a both-role dashboard switcher for client and freelancer activity.
- [x] Add basic job search, currency filtering, job details, and loading/empty/error states.
- [x] Add client job draft creation, editing, publishing, proposal review, and closing.
- [x] Add freelancer proposal submission, editing, withdrawal, and status tracking.
- [x] Add client proposal shortlisting, rejection, and acceptance.
- [x] Add contract offer acceptance, milestone delivery links, feedback, completion, cancellation, disputes, and activity history.
- [x] Display USD as cents and MMK as whole kyat without floating-point storage or implicit conversion.
- [x] Add unit tests for onboarding, job budgets, proposals, and contract workflow validation.
- [x] Add persistent English/Burmese interface switching, locale-aware display, and translated core web journeys.
- [x] Send the selected web locale to the API and localize API error messages without changing stable error codes.
- [x] Add system-aware light/dark appearance modes with an accessible persistent toggle.

## Remaining MVP work

### Milestone 1 — Communication and trust on web

- [ ] Build the conversations list and message thread pages.
- [ ] Allow eligible clients and freelancers to start or continue a job/contract conversation.
- [ ] Support message attachment URLs, pagination, read state, and unread indicators.
- [ ] Build a notifications center with individual and mark-all-read actions.
- [ ] Add completed-contract review forms and display visible reviews.
- [ ] Add user-facing report actions for users, jobs, messages, portfolio items, and reviews.
- [ ] Add web tests for messaging permissions, reviews, notifications, and reporting.

### Milestone 2 — Discovery and profile completeness

- [ ] Expose category, skill, work type, experience level, budget, sorting, and pagination controls in job discovery.
- [ ] Add save/unsave controls and a saved-jobs page.
- [ ] Build freelancer search and public freelancer profile pages.
- [ ] Build portfolio create, edit, and remove forms with URL-based images.
- [ ] Add account editing for display name, avatar URL, country/city, timezone, and languages.
- [ ] Show ratings and completed-contract counts on relevant profiles.
- [ ] Add email-verification and forgot/reset-password screens.
- [ ] Connect production email delivery for verification and password resets.

### Milestone 3 — Administration

- [ ] Add paginated administrator user listing/search and safe user detail endpoints.
- [ ] Add administrator audit-log listing and filtering.
- [ ] Add category and skill create/edit/archive endpoints with audit events.
- [ ] Add job/content moderation endpoints rather than relying only on user suspension and reports.
- [ ] Build a role-protected admin web workspace.
- [ ] Show platform metrics, open reports, disputed contracts, moderated users/content, taxonomy, and audit history.
- [ ] Allow administrators to resolve reports and disputes and suspend/restore users from the web UI.
- [ ] Add authorization and audit tests for every administrator action.

### Milestone 4 — Mobile (`archer-mobile`)

- [x] Create the independent Expo managed-workflow repository.
- [x] Add secure session persistence and authentication/onboarding for client, freelancer, and both-role accounts.
- [x] Add initial role-aware navigation and profile setup for client and freelancer modes.
- [~] Add initial discovery, save action, proposals, contract actions, milestone submission/review, conversation list, messaging, and notifications. Reviews, client proposal review/hiring, and richer contract management remain.
- [x] Consume the OpenAPI behavior through a mobile-local API client; do not import web/API source files.
- [ ] Test the main client and freelancer journeys on supported iOS and Android targets.
- [x] Add the initial English/Burmese translation files and language switch with Burmese-specific type spacing and wrapping.

### Milestone 5 — Release readiness

- [ ] Add browser-level end-to-end tests for the complete client and freelancer journeys.
- [ ] Perform keyboard, screen-reader, contrast, responsive-device, and error-state reviews.
- [ ] Add CI for typecheck, lint, tests, builds, Prisma validation, and OpenAPI validation.
- [ ] Document deployment, environment variables, CORS origins, database backups, and recovery.
- [ ] Review rate limiting, security headers, session rotation/revocation, logs, and secret handling for production.
- [ ] Decide the production SQLite hosting/backup strategy or document a future database migration plan.
- [ ] Run a final seed/demo-data and documentation audit.

## MVP acceptance checklist

- [~] A client can publish a USD or MMK job, receive and manage proposals, hire, manage milestones, and complete a contract. Reviews still need a web interface.
- [~] A freelancer can complete a core profile, find work, manage a proposal, accept a contract, and submit milestone work. Saved jobs, messaging, public portfolios, and reviews still need web interfaces.
- [ ] Client and freelancer state is consistent across web and mobile; mobile has not been created.
- [~] Administrators can perform several moderation actions through the API, but the complete API surface and web workspace are unfinished.
- [x] Implemented user-facing money language records terms only and does not claim Archer processes or guarantees payments.

## Explicitly outside the MVP

- Payment processing, escrow, wallets, balances, payouts, platform fees, checkout, invoices, refunds, withdrawals, and currency conversion.
- Social login, enterprise SSO, KYC and tax workflows.
- Agencies, teams, subscriptions, advertising, and promoted listings.
- Built-in binary file storage, video/audio calls, and time tracking.
- AI matching or AI-written proposals.
- Additional interface languages beyond English and Burmese, and automatic translation of user-authored marketplace content.

## Working order

Complete milestones in order unless a production blocker requires otherwise:

1. Communication and trust on web.
2. Discovery and profile completeness.
3. Administration.
4. Mobile.
5. Release readiness.

For every completed item, update this file, the relevant section of `SPEC.md` when product behavior changes, the owning README when usage changes, and the owning repository's tests and OpenAPI contract where applicable.
