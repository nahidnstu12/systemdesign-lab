# Project spine — one Next.js app, all labs

**Not a monorepo.** One app repo (e.g. `bench-snippets`) that grows lab by lab. Same Postgres database; Redis joins in Lab 02+.

## Product: **Bench** (working name)

Tiny internal app to **save and look up dev snippets** (title, slug, body, owner). Boring domain on purpose — labs attach to real endpoints, not a new product each time.

| Lab | What you add on Bench |
|-----|------------------------|
| **01** | Login session + `whoami` + health; **2+ app containers** behind LB |
| **02** | `GET /api/snippets/:slug` with **cache-aside** (Redis) |
| **03** | `POST /api/snippets/:id/export` → **job + worker** (PDF/JSON file) |
| **04** | `GET /api/snippets` list/filter/sort on **100k rows** + indexes + pagination |
| **05** | **Rate limit** `POST /api/snippets` (and/or login) across instances |

### Core tables (grow over labs)

- `users` — Lab 01
- `sessions` — Lab 01 (shared store; not in-memory)
- `snippets` — Lab 01 minimal CRUD; Lab 02–05 stress this resource

### POC UI (optional)

One page: login, create snippet, open snippet, list (slow list comes Lab 04). Labs 01–05 can be proven with **curl + scripts**; UI is comfort, not the goal.

## Interview story (one arc)

“We built a small snippet API on Next.js. We made instances stateless and sessions shared, added Redis cache-aside, async exports via a queue, fixed list queries with indexes and cursor pagination, then distributed rate limiting — each step had explicit failure tests.”