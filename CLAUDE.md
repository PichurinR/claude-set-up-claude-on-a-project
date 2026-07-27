# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

A minimal Express API (in-memory data, no database) used as a course starter project.

## Commands

- `npm install` — install dependencies
- `npm run dev` — start the API with auto-reload on http://localhost:3000
- `npm start` — start the API without auto-reload
- `npm test` — run all tests (Node's built-in test runner)
- `node --test tests/users.test.js` — run a single test file
- `npm run lint` — run ESLint

CI (`.github/workflows/ci.yml`) runs `npm install`, `npm run lint`, then `npm test` on every push/PR — keep both green.

## Architecture

- `server.js` — Express app entry point; mounts route modules and starts the server. Exports `app` (without listening) so tests can import it directly via `supertest`.
- `routes/` — one file per resource (`users.js`, `health.js`), mounted under its resource path in `server.js`.
- `db/store.js` — in-memory data access layer; routes call into this instead of holding data themselves. Data resets on every restart.
- `tests/` — integration tests that hit the Express app through `supertest` rather than calling route handlers directly.

## Conventions

- Routes validate input and return JSON error bodies (`{ error: "..." }`) with the appropriate status code (400/404) rather than throwing.
- Data access always goes through `db/store.js`; route handlers do not touch the `users` array directly.
