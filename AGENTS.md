# Archer engineering boundaries

This file applies to the entire Archer workspace and to every nested project. It is stable guidance for agents and developers. Product behavior belongs in `SPEC.md`; setup and day-to-day commands belong in `README.md`.

## Repository boundaries

- Archer has three independent projects and three separate Git repositories: `archer-app`, `archer-api`, and `archer-mobile`.
- Do not import source files, unpublished packages, or database code across repositories.
- The API owns persistence, migrations, business rules, authorization, seed data, and the versioned OpenAPI contract.
- Web and mobile consume the API contract and may generate their own local types/clients.
- Root-level files are project governance and documentation only; implementation belongs inside the relevant repository.
- Keep each repository independently installable, testable, buildable, and deployable.

## Technology boundaries

- `archer-app`: React + TypeScript, React Router, TanStack React Query, React Hook Form/Zod where useful, and shadcn/ui conventions using preset `beEhfqy2`.
- `archer-api`: Node.js + TypeScript, Express, SQLite, Prisma 7, JWT access/refresh authentication, and request validation.
- `archer-mobile`: React Native + TypeScript with Expo managed workflow and Expo-compatible libraries.
- Pin dependencies in each repository's lockfile. Do not add a framework or service that changes the product boundary without documenting the decision.

## Non-negotiable domain rules

- Supported currencies are only USD and MMK. Store money as integer units with an explicit currency; never use floating-point money or implicit conversion.
- The MVP does not process, hold, settle, or promise money. Do not add payment, escrow, wallet, payout, fee, checkout, invoice, refund, or withdrawal behavior.
- API authorization is enforced server-side with role and ownership checks. Client-side guards are only presentation.
- Never expose password hashes, token hashes, refresh tokens, reset tokens, moderation notes, or private contact data.
- Preserve transactional history with status changes and audit events instead of destructive deletes.
- Do not commit secrets, database files, generated credentials, or environment files containing real values.

## API and integration rules

- Use `/api/v1`, JSON bodies, opaque IDs, and ISO 8601 UTC timestamps.
- Keep a consistent error envelope and bounded pagination/filter inputs.
- Contract-changing actions must be transactional and authorization-checked in the service layer.
- Breaking API changes require a new API version or a documented deprecation window.
- CORS must use an explicit per-environment allowlist.
- OpenAPI is the integration contract; update it with endpoint behavior changes.

## Quality gates

- Before committing, run the repository's typecheck, lint, tests, and production build when those scripts exist.
- Add or update tests for money handling, authorization, status transitions, validation, and every changed core journey.
- Keep loading, empty, error, and permission-denied states usable on all client surfaces.
- Prefer small, reversible changes. Do not delete or rewrite unrelated user work.
- Keep seed data deterministic and safe for local development only; document demo credentials in the owning repository README.

## Documentation ownership

- Update `SPEC.md` when product capabilities, user journeys, acceptance criteria, or out-of-scope decisions change.
- Update `AGENTS.md` only when a cross-project boundary, invariant, or quality rule changes.
- Update `README.md` when setup, commands, demo usage, repository navigation, or developer workflow changes.
- Project-specific READMEs may add implementation details but must not contradict these boundaries.

## Git and change scope

- Commit changes in the repository they belong to; do not create a synthetic root monorepo commit.
- Use focused commit messages that describe the change.
- Review `git status` before committing and leave unrelated modifications untouched.
