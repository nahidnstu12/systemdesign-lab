# System Design Labs

Hands-on engineering labs to move from **knowing a concept** → **implementing it** → **handling failures** → **production trade-offs**.

Stack where appropriate: **TypeScript / Node.js**, **PostgreSQL**, **Redis**, **Docker Compose**. Load testing with **k6**, tests with **Vitest**. Optional: structured logs + Prometheus metrics.

**Rule:** Do not outsource the whole lab to an AI. Implement core logic yourself; use review for architecture, missing failure scenarios, and production critique.

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

## Image & article sources (by lab)

References for diagrams and deeper reading. Inline images are hosted URLs—prefer linking to the canonical articles for long-term stability.

| Lab | Topic | Article | Diagram / image |
|-----|--------|---------|-----------------|
| 01 | Stateless architecture | [ByteByteGo — Stateless Architecture](https://blog.bytebytego.com/p/stateless-architecture-benefits-and) | [inline diagram](https://images.openai.com/static-rsc-4/_ZbO4Xf9aYqyMtNvNy7jTSapOspyn4NL120dGV1sOeNBhh1lxUIDzjl9XLamxdBvRCqmu4-nN3V3zQyR7TqoiFIAKRIzUdYuLZTKLWlWTsxhctse2CB4gccl91QEKz7MtOVebO6_VW7UOU36s-EsmACrimbmRPZ-E_E1Vf-2qLk?purpose=inline) |
| 02 | Cache strategies | [Event Looped — Cache Strategies](https://www.eventlooped.com/backend-system-design/cache-strategies) | [inline diagram](https://images.openai.com/static-rsc-4/vGjXlAIt9MZZaXPPaQTZMQsZHbtpos2P9RXlOOqBrZO7FKQ7rYFIEgLNyLWAnR-rPqWkqEZjQ-HC4dZx4qEKZ34vfwZV3V_XKTzUUX9mNZhAC0BuoXrU2l05BQkO5Qeo4BbFsHOchHytIplxUrHAprp-d_H6x1srvNpWIpajJtw?purpose=inline) |
| 03 | Queues & events | [Prepflix — Message Queues & Pub/Sub](https://prepflix.co.in/blogs/class-7-in-class.html) | [inline diagram](https://images.openai.com/static-rsc-4/82-pwbAJzg0N00yWFypkal6D1Ay9_dL2TSXEPHG_u3yCnzv9FhgneuToXFo_lDM9ryo6l72q9s59WvphkWOiMWs4-pqIMBEYl8elc4hrgCwcAQAZi3UUaMRicCnEoJAjLJoIHsSRlyI4hMOS5yurJ6fliyvnnnzJsSo9VHNJlRw?purpose=inline) |
| 04 | Query tooling | [Crunchy Data — pgAdmin 4 Query Tool](https://access.crunchydata.com/documentation/pgadmin4/4.20/query_tool.html) | [inline diagram](https://images.openai.com/static-rsc-4/SHZ6ptqlzshjmy9AI0MwEhV3nhlhIbwg-Y6D63LJE7DD14Z2jTnkbO3-yxR8-LVYrLgirlwoDVaLBQSl7hA_RyJncF752DWue4vqKD-KmVqxTJTd7a6GBFcAj4yH-vQk-HL-fN2rujaAy0X9cdFm0VmyLzQEE9sYFP3dzZYhN9w?purpose=inline) |
| 05 | Rate limiting | [InterviewCrafted — Rate Limiter (Token Bucket)](https://interviewcrafted.com/system-design/rate-limiter) | [inline diagram](https://images.openai.com/static-rsc-4/WsaVNC4eYePjWHS4RDKpoEzHEK3OZV6ABbOCDE_Rybcrm_HyUg28fSMX8aYuaLTZNOnJT96j8U1dgJyBgKzr1-aSf-C6vkgqa7ll41ZRZmBcjrY51JH2y6SgJo9Z--JUPz0-ul0-ifm2iv1WAjFpx-2JzSGjRqrYq6XJd-k6xFE?purpose=inline) |