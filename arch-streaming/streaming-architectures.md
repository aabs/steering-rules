---
id: streaming-architectures
version: "2.0.0"
title: Streaming Architecture Rules
scope: project
status: active
---

:::rule id="STREAM-01" mandatory="true" category="streaming" tags="contracts"
Every stream event type shall have an explicit schema contract, a defined business meaning, and shall represent a fact that has already occurred; events shall not expose producer-internal implementation details.
:::

:::rule id="STREAM-02" mandatory="true" category="streaming" tags="contracts, ownership"
Each event type shall have a single designated owning producer responsible for its schema and publication; multiple uncoordinated producers of the same event type are prohibited.
:::

:::rule id="STREAM-03" mandatory="true" category="streaming" tags="contracts, schema"
Producers shall evolve event schemas in a backward-compatible manner; consumers shall tolerate unknown fields in forward-compatible schema versions and shall not reject events solely because they contain unrecognized fields.
:::

:::rule id="STREAM-04" mandatory="true" category="streaming" tags="validation, security"
WHEN an event is received, the system shall validate its schema and verify its authorization before executing any processing logic; events that fail validation or authorization shall not be processed.
:::

:::rule id="STREAM-05" mandatory="true" category="streaming" tags="delivery, idempotency"
The system shall treat all stream delivery as at-least-once; every producer shall be safe to retry without creating duplicate business effects; every consumer and processor shall be idempotent or duplicate-safe.
:::

:::rule id="STREAM-06" mandatory="true" category="streaming" tags="consistency, commit-order"
The system shall not commit offsets, advance checkpoints, or publish derived downstream events until the owned state change or durable intent is committed.
:::

:::rule id="STREAM-07" mandatory="false" category="streaming" tags="consistency, outbox"
WHERE state change and event publication must not diverge, the system shall use an outbox or equivalent durable intent pattern to guarantee both are committed atomically.
:::

:::rule id="STREAM-08" mandatory="false" category="streaming" tags="idempotency, deduplication"
WHERE deduplication must survive process restarts and failover, the system shall use a durable processed-event record rather than in-memory state.
:::

:::rule id="STREAM-09" mandatory="true" category="streaming" tags="ordering, partitions"
The system shall not assume global ordering across partitions, topics, or unrelated streams; processing logic shall rely only on ordering guarantees that are explicitly provided for the relevant partition or key.
:::

:::rule id="STREAM-10" mandatory="false" category="streaming" tags="ordering, partitions"
WHERE events must be processed in a defined relative order, the system shall choose partition keys that co-locate all related events onto the same partition and distribute load predictably.
:::

:::rule id="STREAM-11" mandatory="true" category="streaming" tags="topology"
Stream topologies shall be built from explicit named processing stages, each with declared input and output event types and a single defined responsibility.
:::

:::rule id="STREAM-12" mandatory="true" category="streaming" tags="state"
WHEN a processor maintains local state, the processor shall exclusively own that state; state reads, updates, and output emissions shall be atomic within the processor's consistency boundary.
:::

:::rule id="STREAM-13" mandatory="true" category="streaming" tags="time-semantics"
Each processing flow shall declare whether it operates on event time, processing time, or ingestion time; different time semantics shall not be mixed within the same processing flow without an explicit conversion step.
:::

:::rule id="STREAM-14" mandatory="false" category="streaming" tags="time-semantics, windows"
WHERE windowed computation is used, the system shall define the window type, boundaries, trigger conditions, allowed lateness, and output semantics explicitly.
:::

:::rule id="STREAM-15" mandatory="true" category="streaming" tags="time-semantics, late-events"
WHEN a processing flow performs time-dependent operations such as windowing, aggregation, or temporal joins, the system shall define the handling behavior for late, missing, and out-of-order events.
:::

:::rule id="STREAM-16" mandatory="true" category="streaming" tags="determinism, replay"
Stream processing logic shall be deterministic and free of hidden side effects; reprocessing the same ordered input for a given partition shall produce the same derived state and outputs; replay shall not generate new business effects beyond reprocessing original facts.
:::

:::rule id="STREAM-17" mandatory="true" category="streaming" tags="joins"
WHEN streams are joined, the system shall define key alignment, time alignment, and the handling of late or unmatched events before the join is implemented.
:::

:::rule id="STREAM-18" mandatory="true" category="streaming" tags="enrichment"
WHEN a stream is enriched with external data, the system shall define the data freshness requirement, consistency guarantee, and failure behavior explicitly.
:::

:::rule id="STREAM-19" mandatory="true" category="streaming" tags="failures, retries"
WHEN a stream processing failure occurs, the system shall classify it before retrying; the system shall retry only failures classified as transient and safe to retry; validation, schema, authorization, and business rule failures shall not be retried.
:::

:::rule id="STREAM-20" mandatory="true" category="streaming" tags="failures, dead-letter"
WHEN an event repeatedly fails processing up to the configured retry limit, the system shall route it to an explicit dead-letter or quarantine destination rather than retrying indefinitely.
:::

:::rule id="STREAM-21" mandatory="true" category="streaming" tags="side-effects"
WHEN a stream processor performs irreversible external side effects, the system shall ensure those effects are idempotent or protected against duplicate execution; side effects shall be triggered only after all validation and commit preconditions succeed.
:::

:::rule id="STREAM-22" mandatory="true" category="streaming" tags="throughput, backpressure"
WHEN downstream processing cannot safely keep up with inbound throughput, the system shall apply back-pressure or throttling; consumer lag shall not grow without explicit retention bounds and operator-visible alerting.
:::

:::rule id="STREAM-23" mandatory="true" category="streaming" tags="observability"
Each event shall carry a stable unique event identifier and a causation or correlation identifier to support deduplication, tracing, and lineage across stream topologies.
:::

:::rule id="STREAM-24" mandatory="true" category="streaming" tags="observability"
The system shall emit structured telemetry recording throughput, consumer lag, retry counts, dropped events, late event counts, and final event disposition for each processing stage.
:::

:::rule id="STREAM-25" mandatory="true" category="streaming" tags="security"
Events shall not contain secrets, credentials, or unencrypted sensitive personal data; WHEN sensitive data must be included in an event payload, the field shall be encrypted and access shall be explicitly authorized.
:::

:::rule id="STREAM-26" mandatory="false" category="streaming" tags="security, provenance"
WHERE downstream processing decisions depend on the authorization context or provenance of an event, the system shall preserve that context within the event payload or a linked audit record.
:::

:::rule id="STREAM-27" mandatory="true" category="streaming" tags="testing"
The system shall include deliberate tests covering replay, duplicate delivery, partition rebalancing, consumer lag, out-of-order events, late events, stream joins, and failure recovery for every critical stream processing path.
:::
