# Lab 01 — Practice guide (Next.js + Postgres)

Companion to [01-horizontally-scalable-api.md](./01-horizontally-scalable-api.md). Product context: [project spine](../project-spine.md).

## What you are proving

Clients hit **one URL** (load balancer). Traffic goes to **multiple Next.js processes** with **no sticky requirement**. **Session survives** restart/kill of one instance. **No auth or “who served me” state in process memory.**

```text
  Browser / curl
        │
        ▼
  ┌───────────┐     :8080 on Mac / :443 on VPS
  │  nginx    │  round-robin, health-aware upstream
  └───┬───┬───┘
      │   │
  ┌───▼───┐ ┌───▼───┐
  │ web-1 │ │ web-2 │   INSTANCE_ID=web-1 | web-2
  └───┬───┘ └───┬───┘
      └────┬────┘
           ▼
      PostgreSQL
      (users + sessions + snippets)
```

## Lab 01 stack (only what you need now)

| Piece | Lab 01? | Notes |
|-------|---------|--------|
| **Docker + Compose** | Yes | Same file you will extend in later labs |
| **PostgreSQL** | Yes | Sessions + minimal `snippets` |
| **Redis** | No | Lab 02 |
| **Load balancer** | Yes | **nginx** recommended (see below) |
| **2× Next.js containers** | Yes | Same image, different `INSTANCE_ID` |
| k6 | Optional | `curl` loops are enough for Lab 01 |

### nginx vs Caddy vs Traefik (pick one)

| | Use when |
|---|----------|
| **nginx (recommended)** | You want explicit `upstream`, round-robin, `max_fails` / passive health — matches most interviews |
| **Caddy** | You want minimal config locally; less “enterprise LB” vocabulary |
| **Traefik** | You already know Docker labels; skip for Lab 01 if labels feel like magic |

**Do not** run two separate public ports (`3001`, `3002`) as the “solution” — clients must use **one** entrypoint (LB).

## What to build (minimal)

Implement yourself (manual coding):

1. **Env:** `INSTANCE_ID`, `DATABASE_URL`
2. **Routes (Route Handlers):**
   - `GET /api/health` — 200 if DB reachable (readiness)
   - `GET /api/whoami` — `{ instanceId }` (proves LB rotation)
   - `POST /api/auth/login` — sets session (email/password OK as POC)
   - `GET /api/auth/me` — requires session; returns user
3. **Session store:** Postgres table (or signed cookie + session row). **Forbidden:** `Map` in module scope, default in-memory adapter without shared DB.
4. **Graceful shutdown:** On `SIGTERM`, stop accepting new work, drain short timeout, exit (custom server or documented container `stop_grace_period`).

Optional same lab: `POST /api/snippets` + `GET /api/snippets/:slug` so Lab 02 reuses them.

## Initial setup checklist (Mac)

1. Docker Desktop running.
2. New Next.js app (App Router), Prisma or Drizzle → Postgres.
3. `docker-compose.yml` with services: `db`, `web-1`, `web-2`, `nginx`.
4. nginx config: upstream `web-1:3000`, `web-2:3000`; `proxy_set_header Host/X-Forwarded-*`.
5. Migrate DB; seed one user.
6. `docker compose up --build`; open `http://localhost:8080`.

## Interactive tests (run by hand)

Keep scripts in `scripts/lab01/` and paste output into `labs/01-results.md`.

### 1 — Load balancing

```bash
for i in $(seq 1 20); do curl -s http://localhost:8080/api/whoami; echo; done
```

Expect **both** `instanceId` values over time.

### 2 — Session across instances

```bash
# login via LB, save cookie jar
curl -c /tmp/cj -b /tmp/cj -X POST http://localhost:8080/api/auth/login \
  -H 'Content-Type: application/json' -d '{"email":"demo@bench.dev","password":"demo"}'
curl -b /tmp/cj http://localhost:8080/api/whoami
curl -b /tmp/cj http://localhost:8080/api/auth/me
```

Repeat `whoami` + `me` — session must work regardless of which instance answers.

### 3 — Kill one instance

```bash
docker compose stop web-1
curl -b /tmp/cj http://localhost:8080/api/auth/me   # still 200
for i in $(seq 1 10); do curl -s http://localhost:8080/api/whoami; echo; done
docker compose start web-1
```

### 4 — Local memory audit (grep your code)

Search for: in-memory session, global `Map`, `let cache =`, module-level user store. If found, fix or document why it is safe (usually it is not for Lab 01).

### 5 — Graceful stop

```bash
docker compose stop web-2   # watch logs: shutdown hook ran
```

## Mac vs Hetzner

| Phase | Where |
|-------|--------|
| **Learn + debug** | **Mac** — Compose, logs, breakpoints on one container |
| **Confidence check** | **Hetzner (optional)** — same `docker compose`, firewall open only LB port, repeat experiments 2–3 |

VPS adds nothing to concepts until Compose works locally. Use VPS when you want “real single IP, real latency” or your Mac is RAM-limited running 2 Node containers.

## Done when

- [ ] One URL through nginx; two healthy backends
- [ ] `whoami` shows both instances
- [ ] Login cookie works after stopping either `web-*`
- [ ] Health fails when DB is down (optional: nginx marks backend bad)
- [ ] Short **trade-offs** note: sticky sessions vs shared store; why you picked nginx; what breaks at 10× traffic

## After Lab 01

Do **not**新建 another project. Tag `lab-01-complete`. Next in curriculum: **Lab 02** on `GET /api/snippets/:slug` — add Redis service to the **same** `docker-compose.yml`.