# Archer

Archer is a freelance marketplace connecting clients and independent talent. The workspace contains three separate projects:

| Project | Path | Status |
| --- | --- | --- |
| Web app | [`archer-app`](./archer-app) | Implemented MVP shell and core marketplace flows |
| API | [`archer-api`](./archer-api) | Implemented Express/SQLite/Prisma API with seeded data |
| Mobile | [`archer-mobile`](./archer-mobile) | Initial Expo app with authentication, discovery, proposals, work, and messaging |

## Documentation map

- [`SPEC.md`](./SPEC.md) — evolving product features, journeys, rules, and acceptance criteria.
- [`TODO.md`](./TODO.md) — completed work, remaining MVP milestones, and delivery order.
- [`AGENTS.md`](./AGENTS.md) — stable engineering boundaries and quality rules for all projects.
- [`CLAUDE.md`](./CLAUDE.md) — short entry point for Claude-compatible coding agents.
- Project READMEs — implementation-specific setup and commands.

## Quick start

Start the API first:

```bash
cd archer-api
npm install
cp .env.example .env
npm run db:migrate -- --name init
npm run seed:demo
npm run dev
```

Then start the web app in another terminal:

```bash
cd archer-app
npm install
cp .env.example .env
npm run dev
```

Open `http://localhost:5173` for the public landing page. Create a client, freelancer, or both-role account and complete its profile, or sign in with a demo account. Jobs and the sidebar workspace appear after sign-in. Sign out to return to the landing page. The app uses `http://localhost:4000/api/v1` by default. See the [API README](./archer-api/README.md) and [app README](./archer-app/README.md) for full command/reference details.

## Demo accounts

All seeded demo accounts use the password `ArcherDemo123!`:

- Client: `client1@archer.local`
- Freelancer: `freelancer1@archer.local`
- Client + freelancer: `both@archer.local`
- Administrator: `admin@archer.local`

These credentials are for local development only.
The administrator account currently exercises API moderation endpoints; there is no admin web console yet.

## Developer workflow

1. Read `AGENTS.md` and the current `SPEC.md` section relevant to your change.
2. Work inside the owning repository; do not share source code through local imports.
3. Run typecheck, lint, tests, and build scripts available in that repository.
4. Update the owning README when setup or usage changes, and update `SPEC.md` when behavior changes.
5. Commit in the affected repository with a focused message.

The API is the source of truth for persisted behavior and exposes the versioned contract consumed by the web and mobile clients.

## GitHub repositories

The web app, API, and mobile app keep independent Git history in their own repositories:

- [Archer app](https://github.com/khantsithuwin/archer-app)
- [Archer API](https://github.com/khantsithuwin/archer-api)
- [Archer mobile](https://github.com/khantsithuwin/archer-mobile)

This root repository links them as Git submodules. Clone the complete workspace with:

```bash
git clone --recurse-submodules https://github.com/khantsithuwin/archer.git
```

If you cloned without submodules, initialize and update them with:

```bash
git submodule update --init --recursive
```
