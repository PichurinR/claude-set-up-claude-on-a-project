# NOTES.md

## CLAUDE.md

I kept `CLAUDE.md` to four short parts: a one-line description, the commands I run often (`dev`, `test`, running a single test file, `lint`), a short architecture note (entry point, one route file per resource, data access centralized in `db/store.js`), and two real conventions (JSON error shape, always going through the store instead of touching the in-memory array directly).

I deliberately left out a file-by-file structure listing, a "how to write tests" section, and generic advice like "add error handling" or "write unit tests" — all of that is either obvious from reading the code once, or generic enough that it doesn't need to live in a project-specific file. I also left out anything from `.env.example` beyond mentioning it exists, since it's sample config, not a real convention.

## Permission rules

- **Allow**: `Bash(npm test:*)` and `Bash(npm run lint:*)` — both are safe, read-only-effect commands I run constantly, so I don't want a prompt every time.
- **Ask**: `Bash(git push:*)` — pushing is visible to others, so I want a confirmation each time even though it's not destructive by itself.
- **Deny**: `Read(./.env)` and `Bash(git push --force:*)` — without the `.env` deny rule, Claude could read real secrets straight into context and potentially echo them back or into a commit. Without the force-push deny rule, Claude could overwrite remote history (mine or a teammate's) with no way to undo it from my side.

## Verification

- `/memory` shows `CLAUDE.md` loaded from the project root.
- `/permissions` shows the allow/ask/deny rules from `.claude/settings.json`.
