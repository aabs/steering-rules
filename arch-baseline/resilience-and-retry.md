---
id: resilience-and-retry
version: "2.0.0"
title: Resilience and Retry Rules
scope: project
status: active
---

:::rule id="RES-01" mandatory="true" category="resilience" tags="resilience, failure-classification"
The system shall classify every remote call, storage operation, and message delivery failure as exactly one of: transient, persistent, concurrency conflict, cancellation, timeout, or unknown — before deciding on any recovery action.
:::

:::rule id="RES-02" mandatory="true" category="resilience" tags="resilience, retry, safety"
WHEN a failure occurs, the system shall retry only if the failure is classified as transient AND the operation is idempotent or duplicate-safe. IF a failure is classified as validation, authorization, business rule, or deterministic application error, the system shall not retry.
:::

:::rule id="RES-03" mandatory="true" category="resilience" tags="resilience, idempotency"
WHEN an operation may be retried, the system shall ensure the operation is idempotent or duplicate-safe such that any number of repeated executions produces the same observable outcome as a single execution.
:::

:::rule id="RES-04" mandatory="true" category="resilience" tags="resilience, backoff, limits"
WHEN retrying an operation, the system shall apply increasing delay between attempts, enforce an explicit maximum retry count or total retry duration, and shall not exceed the operation's overall timeout or deadline; retry policy shall be defined at the boundary that owns the dependency interaction.
:::

:::rule id="RES-05" mandatory="false" category="resilience" tags="resilience, jitter"
WHERE multiple independent callers may retry the same dependency concurrently, the system shall add random jitter to retry delays to distribute load.
:::

:::rule id="RES-06" mandatory="true" category="resilience" tags="resilience, timeout"
The system shall set an explicit timeout on every remote call and every potentially blocking operation; the timeout value shall be defined at the boundary that owns the dependency interaction.
:::

:::rule id="RES-07" mandatory="true" category="resilience" tags="resilience, cancellation"
WHEN a cancellation is requested during a retrying or in-flight operation, the system shall stop retrying immediately, propagate the cancellation signal, and surface cancellation as a distinct non-retryable outcome rather than a fault.
:::

:::rule id="RES-08" mandatory="false" category="resilience" tags="resilience, circuit-breaker"
WHEN a dependency produces repeated failures, the system shall apply circuit breaking or equivalent isolation to stop forwarding traffic to that dependency until it recovers, rather than retrying indefinitely.
:::

:::rule id="RES-09" mandatory="true" category="resilience" tags="resilience, fallback, correctness"
WHEN fallback or default behavior is applied on dependency failure, the system shall make the degraded state observable to callers; the system shall not substitute default values unless those defaults are explicitly correct for the domain, and shall not use fallback to mask failed writes, lost messages, or inconsistent state.
:::

:::rule id="RES-10" mandatory="true" category="resilience" tags="resilience, degradation"
WHEN graceful degradation is applied, the system shall explicitly reduce the exposed capability rather than silently alter business semantics or return incorrect results.
:::

:::rule id="RES-11" mandatory="true" category="resilience" tags="resilience, commit-order"
The system shall not acknowledge success, publish externally visible events, or perform irreversible external effects until all required state changes are durably committed; durable intent shall be persisted before any external side effect is triggered.
:::

:::rule id="RES-12" mandatory="true" category="resilience" tags="resilience, messaging, deduplication"
WHEN consuming messages from a retryable or redeliverable source, the system shall treat delivery as at-least-once and shall ensure message processing is duplicate-tolerant.
:::

:::rule id="RES-13" mandatory="true" category="resilience" tags="resilience, ordering, messaging"
The system shall not assume global message ordering across unrelated streams or partitions unless the messaging infrastructure provides an explicit global ordering guarantee that the design relies on.
:::

:::rule id="RES-14" mandatory="true" category="resilience" tags="resilience, poison-messages, dead-letter"
WHEN a message fails processing on consecutive attempts up to the configured retry limit, the system shall route it to an explicit dead-letter or quarantine destination rather than retrying indefinitely.
:::

:::rule id="RES-15" mandatory="true" category="resilience" tags="resilience, concurrency"
WHEN a concurrency conflict is detected, the system shall handle it as a named failure class with an explicit resolution strategy and shall not treat it as a generic transient fault.
:::

:::rule id="RES-16" mandatory="true" category="resilience" tags="resilience, resource-protection, backpressure"
WHEN the system cannot safely process additional work, the system shall apply back-pressure or reject new requests with an explicit error; retry behavior shall not exhaust connection pools, threads, memory, or queues; the system shall not accept unbounded work when downstream capacity is degraded.
:::

:::rule id="RES-17" mandatory="false" category="resilience" tags="resilience, health"
The system shall provide health signals that distinguish readiness, liveness, and dependency degradation separately; health signals shall not infer dependency health from configuration presence or network reachability alone.
:::

:::rule id="RES-18" mandatory="true" category="resilience" tags="resilience, observability, tracing"
The system shall emit structured telemetry recording each retry attempt, final outcome, and failure classification; all retries and cross-service recovery flows shall carry a consistent correlation identifier; failures shall be reported once at the boundary that owns the recovery decision.
:::

:::rule id="RES-19" mandatory="true" category="resilience" tags="resilience, workflows, compensation"
WHEN implementing a long-running or multi-step distributed workflow, the system shall explicitly model timeout, retry, failure, and compensation transitions as named states in the workflow definition; WHERE a multi-step operation cannot be made atomic, the system shall implement compensating transactions to restore consistent state on failure.
:::

:::rule id="RES-20" mandatory="true" category="resilience" tags="resilience, testing"
The system shall include deliberate fault-injection tests covering retry exhaustion, timeout expiry, duplicate delivery, partial failure, and degraded dependency scenarios for every resilience-critical execution path.
:::

:::rule id="RES-21" mandatory="true" category="resilience" tags="resilience, ownership"
Every resilience mechanism shall have an identified owner, a defined recovery decision, and an explicit stopping condition that prevents unbounded retries or unconstrained resource consumption.
:::
