# System Design Labs

Hands-on engineering labs to move from **knowing a concept** → **implementing it** → **handling failures** → **production trade-offs**.

Stack where appropriate: **TypeScript / Node.js**, **PostgreSQL**, **Redis**, **Docker Compose**. Load testing with **k6**, tests with **Vitest**. Optional: structured logs + Prometheus metrics.

**Rule:** Do not outsource the whole lab to an AI. Implement core logic yourself; use review for architecture, missing failure scenarios, and production critique.

**One app, many labs:** [project spine](./project-spine.md) — Next.js + Postgres (+ Redis later). Lab 01 hands-on: [01-practice-guide](./labs/01-practice-guide.md).

## Curriculum reference

- [30-day study plan](https://study-notes-gold.vercel.app/study-plan/02-30-day-curriculum/)
- [System design notes (scale)](https://study-notes-gold.vercel.app/system-design-interview/03-scale-from-zero-to-millions-of-users/)

## Labs (in repo order)

| # | Lab | Difficulty | Est. | Doc |
|---|-----|------------|------|-----|
| 01 | Horizontally scalable API | Intermediate | 3–4h | [01-horizontally-scalable-api.md](./labs/01-horizontally-scalable-api.md) |
| 02 | Production-style caching | Intermediate | 4–5h | [02-production-caching-layer.md](./labs/02-production-caching-layer.md) |
| 03 | Background job processing | Intermediate–Advanced | 5–6h | [03-background-job-processing.md](./labs/03-background-job-processing.md) |
| 04 | Database bottleneck | Intermediate–Advanced | 4–5h | [04-database-bottleneck.md](./labs/04-database-bottleneck.md) |
| 05 | Distributed rate limiter | Advanced | 5–6h | [05-rate-limiter.md](./labs/05-rate-limiter.md) |

## Recommended practice order

| Priority | Lab | Why |
|----------|-----|-----|
| 1 | Caching (02) | Cache invalidation and consistency |
| 2 | Horizontal scaling (01) | Distributed app fundamentals |
| 3 | Background jobs (03) | Reliability and async processing |
| 4 | Database optimization (04) | Performance diagnosis |
| 5 | Rate limiting (05) | Redis, concurrency, multi-instance coordination |

Each lab is an **independent** repository when you implement it—not one monolithic app.

## How to work each lab

1. **Understand** — bottleneck, constraints, expected behavior.
2. **Design** — simple architecture diagram; justify each component.
3. **Implement** — minimum working API/service; no full SaaS UI.
4. **Break things** — kill processes, disconnect deps, concurrency, partial failures.
5. **Measure** — latency, throughput, errors, resource use.
6. **Document** — what you built, what fails, what you’d change at scale.

## Deliverables (per lab)

- Working source code
- README with setup instructions
- Architecture diagram
- API examples or test cases
- At least 3 failure experiments
- Before/after measurements where applicable
- Short trade-off write-up

## Recommended stack

| Component | Technology |
|-----------|------------|
| Language | TypeScript |
| Runtime | Node.js |
| API | Express or Fastify |
| Database | PostgreSQL |
| Cache / coordination | Redis |
| Containers | Docker Compose |
| Load testing | k6 |
| Testing | Vitest |
| Monitoring | Structured logs + Prometheus (where useful) |

