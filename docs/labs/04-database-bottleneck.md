# Lab 04 — Diagnose and optimize a database bottleneck

**Intermediate–Advanced** · PostgreSQL · **Estimated: 4–5 hours**

## References

- Article: [pgAdmin 4 — Query Tool](https://access.crunchydata.com/documentation/pgadmin4/4.20/query_tool.html)
- Diagram: ![Query tooling](https://images.openai.com/static-rsc-4/SHZ6ptqlzshjmy9AI0MwEhV3nhlhIbwg-Y6D63LJE7DD14Z2jTnkbO3-yxR8-LVYrLgirlwoDVaLBQSl7hA_RyJncF752DWue4vqKD-KmVqxTJTd7a6GBFcAj4yH-vQk-HL-fN2rujaAy0X9cdFm0VmyLzQEE9sYFP3dzZYhN9w?purpose=inline)

## Scenario

Your application has a growing database. Initially, queries were fast, but now some endpoints take several seconds. You are not allowed to solve every problem by upgrading the server.

## Your assignment

Create a database with realistic sample data and deliberately introduce slow queries.

### Requirements

1. Create a dataset with at least 100,000 records.
2. Build multiple filtering and sorting queries.
3. Measure query execution time.
4. Analyze execution plans.
5. Add appropriate indexes.
6. Implement pagination.
7. Measure the improvement.

### Production experiments

- Query without an index.
- Query with a suitable composite index.
- Compare offset pagination and cursor pagination.
- Test filtering and sorting together.
- Simulate concurrent database requests.
- Observe connection pool saturation.

### What you should demonstrate

- Database indexing
- `EXPLAIN ANALYZE`
- Query optimization
- Composite indexes
- Pagination strategies
- Connection pooling
- Database bottleneck identification

### Completion criteria

Produce before-and-after performance measurements and explain why your changes improved or failed to improve performance.