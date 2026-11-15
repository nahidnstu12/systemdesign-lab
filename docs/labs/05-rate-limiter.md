# Lab 05 — Build a production-ready rate limiter

**Advanced** · Redis + distributed systems · **Estimated: 5–6 hours**

## References

- Article: [Rate Limiter System Design (Token Bucket) — InterviewCrafted](https://interviewcrafted.com/system-design/rate-limiter)
- Diagram: ![Rate limiter](https://images.openai.com/static-rsc-4/WsaVNC4eYePjWHS4RDKpoEzHEK3OZV6ABbOCDE_Rybcrm_HyUg28fSMX8aYuaLTZNOnJT96j8U1dgJyBgKzr1-aSf-C6vkgqa7ll41ZRZmBcjrY51JH2y6SgJo9Z--JUPz0-ul0-ifm2iv1WAjFpx-2JzSGjRqrYq6XJd-k6xFE?purpose=inline)

## Scenario

Your API is becoming popular. Some clients generate too many requests, affecting other users. You need to protect the application while running multiple API instances.

## Your assignment

Implement a **distributed rate limiter**.

### Requirements

1. Limit requests per user or IP.
2. Support configurable limits.
3. Return HTTP 429 when limits are exceeded.
4. Include appropriate rate-limit response headers.
5. Ensure limits work across multiple application instances.
6. Handle Redis failures deliberately.

Choose one algorithm initially: fixed window, sliding window, or token bucket.

### Production experiments

- Send requests rapidly from one user.
- Send requests from multiple users.
- Send requests across two API instances.
- Test requests exactly at the rate-limit boundary.
- Disconnect Redis.
- Generate a sudden traffic spike.

### What you should demonstrate

- Rate-limiting algorithms
- Atomic Redis operations
- Distributed coordination
- Race conditions
- Traffic protection
- Graceful degradation

### Completion criteria

Two API instances must enforce the same user's rate limit consistently, including under concurrent requests.