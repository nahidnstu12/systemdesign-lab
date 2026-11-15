# Lab 01 — Build a horizontally scalable API

**Intermediate** · Stateless architecture · **Estimated: 3–4 hours**

## References

- Article: [Stateless Architecture: Benefits and Tradeoffs](https://blog.bytebytego.com/p/stateless-architecture-benefits-and)
- Diagram: ![Stateless architecture](https://images.openai.com/static-rsc-4/_ZbO4Xf9aYqyMtNvNy7jTSapOspyn4NL120dGV1sOeNBhh1lxUIDzjl9XLamxdBvRCqmu4-nN3V3zQyR7TqoiFIAKRIzUdYuLZTKLWlWTsxhctse2CB4gccl91QEKz7MtOVebO6_VW7UOU36s-EsmACrimbmRPZ-E_E1Vf-2qLk?purpose=inline)
- Notes: [Scale from zero to millions](https://study-notes-gold.vercel.app/system-design-interview/03-scale-from-zero-to-millions-of-users/)

## Scenario

A web application initially runs on one server. Traffic increases, and you need to run multiple application instances without changing how clients interact with the application.

## Your assignment

Build a small API that supports multiple instances behind a load balancer.

### Requirements

1. Run at least two API instances.
2. Distribute incoming requests between instances.
3. Ensure application instances are stateless.
4. Handle shared user/session state correctly.
5. Ensure one instance can go down without taking down the entire application.

### Production experiments

- Stop one API instance while sending requests.
- Restart an instance and observe user sessions.
- Send concurrent requests to both instances.
- Check whether any important state exists only in local memory.

### What you should demonstrate

- Horizontal scaling
- Stateless application architecture
- Load balancing
- Shared session management
- Health checks and graceful shutdown

### Completion criteria

Your application should continue serving requests when one instance becomes unavailable.