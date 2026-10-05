# Archer feature specification

## Product

Archer is a freelance marketplace for thoughtful, independent work. Clients publish opportunities and hire freelancers; freelancers present their skills, find suitable work, and manage delivery. The same account may use both modes.

This is the evolving product brief. It describes what Archer should do, not how a repository must implement it. New feature decisions belong here; stable engineering boundaries belong in `AGENTS.md`; setup and operating instructions belong in `README.md`.

## MVP users

- **Guest:** view the public landing page, create an account or sign in, and then browse jobs in the web app.
- **Client:** create a profile, publish jobs, review proposals, hire, manage contracts, and review completed work.
- **Freelancer:** create a profile and portfolio, discover or save jobs, submit proposals, deliver work, and review clients.
- **Administrator:** moderate users and content, manage categories and skills, resolve reports, and inspect platform activity.

## Core journeys

### Find and hire

1. A client creates an account and sets up a short individual or company profile; setup can be completed later.
2. A client drafts and publishes a job with a clear brief, skills, budget, currency, and experience level.
3. Freelancers discover the open job and submit proposals.
4. The client compares proposals, shortlists candidates, and accepts one.
5. The freelancer accepts the contract offer.
6. Both parties manage milestones, messages, status, and completion in one workspace.
7. After completion, each party may leave one review.

### Find and deliver work

1. A freelancer creates an account and completes a public profile with skills, optional rate, availability, and portfolio; setup can be completed later.
2. They search, filter, and save relevant jobs.
3. They submit, edit, or withdraw a proposal while the job is open.
4. If hired, they accept the contract, submit milestone work, communicate with the client, and complete the engagement.

## MVP capabilities

### Accounts and profiles

- Email/password registration and sign-in.
- Account can enable client mode, freelancer mode, or both.
- Profile includes display name, avatar URL, location, timezone, languages, and account status.
- Client profile supports individual/company information, overview, industry, website, rating, and completed-contract count.
- Freelancer profile supports title, overview, skills, experience level, availability, languages, hourly rate, rating, and portfolio items.

### Jobs and discovery

- Job title, detailed description, category, required skills, work type, budget/rate range, currency, experience level, duration, deadline, and status.
- Fixed-price and hourly jobs are both supported.
- Signed-in job discovery supports keyword search, category, skill, work type, currency, budget/rate, experience level, pagination, and sorting.
- Freelancers can save and unsave open jobs.
- Freelancers can revisit and remove saved jobs from a Saved jobs view in Discover, including jobs that later close.
- Only the owning client edits a draft; publishing makes the job discoverable; accepting a proposal closes it to new proposals.

### Proposals

- One active proposal per freelancer per job.
- Proposal includes cover letter, proposed amount/rate, matching currency, estimated duration, optional milestone suggestions, and status.
- A freelancer can edit or withdraw a submitted proposal until it is accepted or rejected.
- Client proposal states include submitted, shortlisted, accepted, rejected, and withdrawn.

### Contracts and milestones

- A contract starts from an accepted proposal and preserves the accepted terms.
- Contract states include pending acceptance, active, completion requested, completed, cancelled, and disputed.
- Fixed-price contracts contain milestones. Milestones can be started, submitted, sent back for changes, approved, or cancelled.
- Milestone submissions include a message and optional external deliverable URLs.
- Status changes show a chronological activity history and require an audit reason where appropriate.
- Fixed-price completion requires every milestone to be approved. A freelancer may request completion; the client finalizes it. A client may also finalize directly after approvals.
- Either party may cancel an open offer or active contract with a reason; unfinished milestones and the job close. Either party may dispute active work, pausing actions until an administrator resumes or cancels the contract.

### Communication and trust

- Eligible clients and freelancers can have conversations tied to a job/proposal and continue them through a contract.
- Messages support text, optional attachment URLs, read state, and unread counts.
- In-app notifications cover proposals, contracts, milestones, messages, reviews, and moderation actions.
- Each completed contract participant may leave one 1–5 star review with optional feedback.
- Users can report users, jobs, messages, portfolio items, or reviews; administrators can resolve reports.

### Administration

- Administrators can view and moderate accounts and marketplace content.
- Administrators manage categories and skills and can inspect summary metrics.
- Administrative actions are visible in an audit trail.

## Product rules

- Supported currencies are exactly **USD** and **MMK**.
- Every amount is displayed with its currency; no exchange-rate conversion is performed.
- USD uses cents; MMK uses whole kyat. A proposal and its contract must use the job's currency.
- Archer records agreed terms only. The MVP has no payment, escrow, wallet, payout, fee, checkout, invoice, refund, or withdrawal flow.
- Public content must have loading, empty, error, and permission-denied states.
- The interface supports English and Burmese. A user can switch language from public and authenticated navigation, and the web preference persists on that device.
- The web interface supports light and dark appearance modes. The first visit follows the operating-system preference; an accessible navigation toggle lets the user override it, and that choice persists on the device.
- API clients request English or Burmese human-readable errors with `Accept-Language`; stable error codes remain language-neutral and unsupported locales fall back to English.
- User-entered marketplace content and taxonomy names remain in their authored language and are not automatically translated.
- Images are represented by URLs in the MVP; managed binary uploads may be added later.

## Surfaces

- **Web:** a public landing page without job listings or a sidebar; after sign-in, users enter a sidebar workspace for marketplace, client/freelancer work, and administrator tools. Signed-in users return to the landing page by signing out.
- **Mobile:** authentication, discovery, profiles, work, messaging, notifications, reviews, and role-aware navigation for both marketplace sides.
- **API:** the shared source of truth for account, marketplace, work, communication, trust, and moderation state.

## Out of scope for MVP

- Payment providers, escrow, balances, payouts, platform fees, invoices, refunds, withdrawals, and currency conversion.
- Social login, enterprise SSO, KYC/tax workflows, agencies/teams, subscriptions, promoted listings, advertising, video/audio calls, built-in file storage, time tracking, and AI matching/proposals.
- Additional interface languages beyond English and Burmese, and automatic translation of user-entered content.

## MVP acceptance

The MVP is feature-complete when:

1. A client can publish a USD or MMK job, receive proposals, accept one, manage a contract and milestones, complete it, and leave a review.
2. A freelancer can complete a profile, discover/save jobs, submit/manage a proposal, accept a contract, submit milestone work, message the client, and leave a review.
3. Both parties see consistent job, contract, currency, message, notification, and review state on web and mobile.
4. An administrator can moderate users/content, manage taxonomy, resolve reports, and inspect an audit trail.
5. No user-facing experience implies Archer processed or guarantees money.
6. A user can use the localized core web journeys in English or Burmese, with the selected locale retained across sessions and matching API error messages.
7. A user can switch the web interface between light and dark modes, with readable contrast and the selected mode retained across sessions.

## Decisions to revisit

- Whether to require a freelancer completion request before a client may finalize an approved fixed-price contract.
- Whether managed image uploads are needed for launch.
- Whether the mobile experience should add offline mutations or push notifications after the MVP.
