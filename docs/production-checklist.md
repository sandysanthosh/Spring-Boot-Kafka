# Spring Boot + Kafka Production Checklist

Use this checklist before releasing a Kafka-based service.

## Delivery guarantees

- [ ] Choose the required guarantee: at-most-once, at-least-once, or exactly-once.
- [ ] Make consumers idempotent. A message can be delivered again after a retry or rebalance.
- [ ] Define a stable event key when ordering for an entity matters; ordering is guaranteed only within a partition.
- [ ] Document the event schema, ownership, compatibility rules, and retention expectations.

## Producer

- [ ] Enable idempotence for business-critical events.
- [ ] Set acknowledgements to match durability requirements.
- [ ] Add a timeout and explicit error handling for failed sends.
- [ ] Avoid logging full payloads if they can contain customer or account data.
- [ ] Use a correlation ID / trace ID in headers for end-to-end troubleshooting.

## Consumer

- [ ] Use a meaningful consumer group ID and keep it stable across deployments.
- [ ] Set concurrency based on the number of topic partitions.
- [ ] Configure bounded retries and a dead-letter topic (DLT) for non-recoverable failures.
- [ ] Commit offsets only after successful business processing.
- [ ] Monitor consumer lag and alert before it impacts the downstream SLA.

## Operations and security

- [ ] Keep broker URLs, credentials, and certificates outside source control.
- [ ] Use TLS and authenticated access in shared or production environments.
- [ ] Configure topic retention, replication, and partition count intentionally.
- [ ] Define runbooks for consumer lag, DLT growth, broker unavailability, and poison messages.
- [ ] Expose health, metrics, and tracing through Spring Boot Actuator and your observability platform.

## Testing

- [ ] Test producer failures, duplicate delivery, malformed payloads, and consumer restarts.
- [ ] Test partition rebalancing and DLT replay.
- [ ] Use integration tests with a disposable Kafka environment before release.

## Incident triage

When a message is missing or delayed, check:

1. Producer send result and application logs.
2. Topic partition and broker availability.
3. Consumer group lag and assigned partitions.
4. Consumer exceptions, retry attempts, and the DLT.
5. The event key, offset, correlation ID, and downstream transaction outcome.
