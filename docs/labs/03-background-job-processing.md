# Lab 03 — Build a reliable background job processing system

**Intermediate–Advanced** · Queue + Workers · **Estimated: 5–6 hours**

## References

- Article: [Message Queues, Pub/Sub & Event-Driven Architecture — Prepflix](https://prepflix.co.in/blogs/class-7-in-class.html)
- Diagram: ![Message queues](https://images.openai.com/static-rsc-4/82-pwbAJzg0N00yWFypkal6D1Ay9_dL2TSXEPHG_u3yCnzv9FhgneuToXFo_lDM9ryo6l72q9s59WvphkWOiMWs4-pqIMBEYl8elc4hrgCwcAQAZi3UUaMRicCnEoJAjLJoIHsSRlyI4hMOS5yurJ6fliyvnnnzJsSo9VHNJlRw?purpose=inline)

## Scenario

An application needs to process expensive tasks. Processing everything inside the HTTP request makes the API slow and unreliable. You introduce asynchronous processing.

## Your assignment

Build a job processing service. The job can be anything: generate a PDF, send an email, process an uploaded image, generate a report.

### Requirements

1. API accepts a job and responds quickly.
2. Job is persisted and queued.
3. Independent workers process jobs.
4. Failed jobs are retried.
5. Jobs cannot produce duplicate side effects when retried.
6. Permanently failed jobs can be inspected.

### Production experiments

- Kill a worker during processing.
- Make a job fail temporarily.
- Submit the same job twice.
- Run multiple workers simultaneously.
- Restart the worker process.
- Make a job take longer than expected.

### What you should demonstrate

- Asynchronous processing
- Queue and worker architecture
- At-least-once delivery
- Idempotency
- Retry with exponential backoff
- Dead-letter queue
- Graceful shutdown

### Completion criteria

A worker crash should not silently lose accepted jobs, and retries should not cause duplicate business operations.