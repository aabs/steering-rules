---
id: streaming-architectures
version: "1.0.0"
title: Streaming Architecture Rules
scope: project
status: active
---

:::rule id="STREAM-01" mandatory="true" category="streaming" tags="streaming, architecture, contracts"
Define every stream, topic, and event type with an explicit contract and clear business meaning.
:::

:::rule id="STREAM-02" mandatory="true" category="streaming" tags="streaming, ownership, producers"
Assign each event type a single owning producer.
:::

:::rule id="STREAM-03" mandatory="true" category="streaming" tags="streaming, semantics, events"
Use stream events to represent facts that have already happened.
:::

:::rule id="STREAM-04" mandatory="true" category="streaming" tags="streaming, boundaries, encapsulation"
Do not use streams to expose internal implementation details.
:::

:::rule id="STREAM-05" mandatory="true" category="streaming" tags="streaming, schema, versioning"
Evolve stream contracts in a backward-compatible way whenever feasible.
:::

:::rule id="STREAM-06" mandatory="true" category="streaming" tags="streaming, schema, validation"
Validate every inbound event before executing stream processing logic.
:::

:::rule id="STREAM-07" mandatory="true" category="streaming" tags="streaming, trust, security"
Treat every inbound event as untrusted until validation and authorization succeed.
:::

:::rule id="STREAM-08" mandatory="true" category="streaming" tags="streaming, delivery, reliability"
Assume events may be delayed, duplicated, reordered, or redelivered.
:::

:::rule id="STREAM-09" mandatory="true" category="streaming" tags="streaming, consumers, idempotency"
Make every stream consumer and processor idempotent or duplicate-safe.
:::

:::rule id="STREAM-10" mandatory="true" category="streaming" tags="streaming, producers, retries"
Make every stream producer safe to retry without creating duplicate business effects.
:::

:::rule id="STREAM-11" mandatory="true" category="streaming" tags="streaming, offsets, commit-order"
Do not commit offsets, checkpoints, or acknowledgements before the owned state change is committed.
:::

:::rule id="STREAM-12" mandatory="true" category="streaming" tags="streaming, consistency, publication"
Do not publish downstream events until the state change or durable intent that justifies them is secured.
:::

:::rule id="STREAM-13" mandatory="false" category="streaming" tags="streaming, outbox, consistency"
Use an outbox or equivalent durable intent pattern when state change and publication must not diverge.
:::

:::rule id="STREAM-14" mandatory="false" category="streaming" tags="streaming, deduplication, inbox"
Use a durable processed-event record when deduplication must survive restarts and failover.
:::

:::rule id="STREAM-15" mandatory="true" category="streaming" tags="streaming, ordering, partitions"
Do not assume global ordering across partitions, topics, or unrelated streams.
:::

:::rule id="STREAM-16" mandatory="true" category="streaming" tags="streaming, ordering, keys"
Rely only on ordering guarantees that are explicit for the relevant partition or key.
:::

:::rule id="STREAM-17" mandatory="true" category="streaming" tags="streaming, partitioning, keys"
Choose partition keys that preserve required ordering and distribute load predictably.
:::

:::rule id="STREAM-18" mandatory="true" category="streaming" tags="streaming, processors, responsibility"
Keep each stream processor responsible for one clear transformation, reaction, or aggregation.
:::

:::rule id="STREAM-19" mandatory="true" category="streaming" tags="streaming, topology, composition"
Build stream topologies from explicit processing stages with clear input and output contracts.
:::

:::rule id="STREAM-20" mandatory="true" category="streaming" tags="streaming, state, ownership"
Each stateful processor must exclusively own and manage its local processing state.
:::

:::rule id="STREAM-21" mandatory="true" category="streaming" tags="streaming, stateful-processing, consistency"
Keep each stateful processing step atomic within its own consistency boundary.
:::

:::rule id="STREAM-22" mandatory="true" category="streaming" tags="streaming, time, event-time"
Define whether each processing flow uses event time, processing time, or ingestion time.
:::

:::rule id="STREAM-23" mandatory="true" category="streaming" tags="streaming, timestamps, semantics"
Do not mix time semantics implicitly within the same processing flow.
:::

:::rule id="STREAM-24" mandatory="false" category="streaming" tags="streaming, watermarks, lateness"
Use explicit lateness and progress rules when correctness depends on event-time completeness.
:::

:::rule id="STREAM-25" mandatory="false" category="streaming" tags="streaming, windows"
Use windows only when the business calculation is explicitly window-bounded.
:::

:::rule id="STREAM-26" mandatory="true" category="streaming" tags="streaming, windows, semantics"
Define window boundaries, triggers, and output semantics explicitly for every windowed computation.
:::

:::rule id="STREAM-27" mandatory="true" category="streaming" tags="streaming, late-events"
Define how late, missing, or out-of-order events must be handled.
:::

:::rule id="STREAM-28" mandatory="true" category="streaming" tags="streaming, replay, semantics"
Replay must not create new business meaning beyond reprocessing the original facts.
:::

:::rule id="STREAM-29" mandatory="true" category="streaming" tags="streaming, replay, determinism"
Reprocessing the same ordered input for a partition must produce the same derived state and outputs.
:::

:::rule id="STREAM-30" mandatory="true" category="streaming" tags="streaming, determinism, logic"
Keep stream processing logic deterministic and free of hidden side effects.
:::

:::rule id="STREAM-31" mandatory="true" category="streaming" tags="streaming, joins, correctness"
Do not join streams unless key alignment, time alignment, and late-event behavior are explicitly defined.
:::

:::rule id="STREAM-32" mandatory="true" category="streaming" tags="streaming, reference-data, enrichment"
Do not enrich a stream with external data unless consistency, freshness, and failure behavior are explicitly defined.
:::

:::rule id="STREAM-33" mandatory="true" category="streaming" tags="streaming, retries, classification"
Classify stream processing failures explicitly before deciding whether to retry.
:::

:::rule id="STREAM-34" mandatory="true" category="streaming" tags="streaming, retries, transient"
Retry only failures that are known to be transient and safe to retry.
:::

:::rule id="STREAM-35" mandatory="true" category="streaming" tags="streaming, retries, non-transient"
Do not retry validation, authorization, schema, or business rule failures indefinitely.
:::

:::rule id="STREAM-36" mandatory="true" category="streaming" tags="streaming, poison-events"
Do not retry the same failing event indefinitely without quarantine or escalation.
:::

:::rule id="STREAM-37" mandatory="false" category="streaming" tags="streaming, dead-letter, quarantine"
Move repeatedly failing events to explicit dead-letter or quarantine handling.
:::

:::rule id="STREAM-38" mandatory="true" category="streaming" tags="streaming, side-effects, safety"
Do not perform irreversible side effects from a stream processor unless duplicate execution is prevented or harmless.
:::

:::rule id="STREAM-39" mandatory="true" category="streaming" tags="streaming, side-effects, ordering"
Perform external side effects only after validation and commit preconditions succeed.
:::

:::rule id="STREAM-40" mandatory="true" category="streaming" tags="streaming, throughput, backpressure"
Apply back-pressure or throttling when downstream processing cannot keep up safely.
:::

:::rule id="STREAM-41" mandatory="true" category="streaming" tags="streaming, throughput, lag"
Do not allow unbounded consumer lag without explicit retention, expiry, or operator-visible consequences.
:::

:::rule id="STREAM-42" mandatory="false" category="streaming" tags="streaming, expiry, retention"
Use explicit retention or expiry rules when late processing can no longer produce a correct business outcome.
:::

:::rule id="STREAM-43" mandatory="true" category="streaming" tags="streaming, observability, identifiers"
Attach a stable event identifier to every event.
:::

:::rule id="STREAM-44" mandatory="true" category="streaming" tags="streaming, observability, correlation"
Attach causation or correlation identifiers to support tracing across stream topologies.
:::

:::rule id="STREAM-45" mandatory="true" category="streaming" tags="streaming, observability, telemetry"
Record throughput, lag, retries, dropped events, late events, and final disposition as structured telemetry.
:::

:::rule id="STREAM-46" mandatory="true" category="streaming" tags="streaming, security, provenance"
Preserve provenance and authorization-relevant context where downstream decisions depend on it.
:::

:::rule id="STREAM-47" mandatory="true" category="streaming" tags="streaming, security, data"
Do not place secrets or sensitive data in stream events unless explicitly required and protected.
:::

:::rule id="STREAM-48" mandatory="true" category="streaming" tags="streaming, schema, tolerance"
Consumers must ignore unknown forward-compatible fields unless the contract explicitly forbids them.
:::

:::rule id="STREAM-49" mandatory="true" category="streaming" tags="streaming, testing, reliability"
Test replay, redelivery, partition rebalancing, lag, out-of-order delivery, late events, joins, and failure recovery deliberately.
:::

:::rule id="STREAM-50" mandatory="true" category="streaming" tags="streaming, simplicity"
Prefer the simplest streaming topology and state model that satisfies the required correctness and latency needs.
:::