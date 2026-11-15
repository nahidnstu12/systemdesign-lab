# Lab 02 — Build a production-style caching layer

**Intermediate** · Redis + PostgreSQL · **Estimated: 4–5 hours**

## References

- Article: [Cache Strategies — Event Looped](https://www.eventlooped.com/backend-system-design/cache-strategies)
- Diagram: ![Cache strategies](https://images.openai.com/static-rsc-4/vGjXlAIt9MZZaXPPaQTZMQsZHbtpos2P9RXlOOqBrZO7FKQ7rYFIEgLNyLWAnR-rPqWkqEZjQ-HC4dZx4qEKZ34vfwZV3V_XKTzUUX9mNZhAC0BuoXrU2l05BQkO5Qeo4BbFsHOchHytIplxUrHAprp-d_H6x1srvNpWIpajJtw?purpose=inline)

## Scenario

An application has frequently accessed records. Database queries are becoming expensive, so you decide to introduce Redis. Cached data must remain reasonably consistent with the database.

## Your assignment

Build a generic data retrieval service using the **cache-aside** pattern.

### Requirements

1. Read from Redis first.
2. On cache miss, fetch from PostgreSQL.
3. Store the result in Redis with TTL.
4. Invalidate or update cache when database records change.
5. Handle concurrent requests for the same uncached record.

### Production experiments

- Update a record while its previous version exists in Redis.
- Expire a cache entry.
- Send 100 concurrent requests for the same uncached record.
- Temporarily disconnect Redis.
- Simulate a failed database update.

### What you should demonstrate

- Cache-aside
- TTL and eviction
- Cache invalidation
- Cache stampede prevention
- Cache failure fallback
- Data consistency trade-offs

### Completion criteria

A database update must not leave your application serving outdated data indefinitely, and Redis failure must not unexpectedly break the entire API.