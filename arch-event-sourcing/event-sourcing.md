---
id: event-sourcing-architecture
version: "1.0.0"
title: Event Sourcing Architecture Rules
scope: project
status: active
---

:::rule id="ES-00" mandatory="false" category="architecture" tags="aggregate, invariants"
## Event-sourcing model

- An aggregate’s event stream is its authoritative historical record.
- Aggregate state is rehydrated by applying its events in stream order.
- Events record completed domain facts, rather than commands or persistence mutations.
- Read models and snapshots are derived data and may be rebuilt.
- A stream normally corresponds to one aggregate consistency boundary.
- Technical metadata, such as correlation and causation identifiers, is separate from domain event payloads.
:::

:::rule id="ES-01" mandatory="true" category="architecture" tags="aggregate, invariants"
Evaluate a command and enforce its invariants within one aggregate boundary before appending its resulting events.
:::

:::rule id="ES-02" mandatory="true" category="architecture" tags="aggregate, dependencies"
Do not perform synchronous I/O, query other aggregates, call external services, or read ambient mutable state while an aggregate decides a command.
:::

:::rule id="ES-03" mandatory="true" category="architecture" tags="replay, determinism"
Keep event-application code deterministic and side-effect free; it must not depend on the current time, random values, network calls, or mutable global state.
:::

:::rule id="ES-04" mandatory="true" category="architecture" tags="concurrency, streams"
Append events with an expected stream version and handle concurrency conflicts explicitly; never silently overwrite or merge competing aggregate decisions.
:::

:::rule id="ES-05" mandatory="true" category="architecture" tags="projections, idempotency"
Keep projections outside aggregate decision logic, make them rebuildable from events, and ensure they tolerate at-least-once delivery.
:::

:::rule id="ES-06" mandatory="true" category="architecture" tags="integration, process-manager"
Place workflows and side effects spanning aggregates or external systems in durable process logic; do not coordinate them inside an aggregate.
:::

:::rule id="ES-07" mandatory="true" category="architecture" tags="evolution, compatibility"
Do not change the meaning of a published event. Add compatible event data or provide an explicit replay-time transformation for historical versions.
:::


:::rule id="ES-ADVICE-01" mandatory="false" category="modelling" tags="events, domain-language"
Name events as completed business facts and include enough stable domain context to explain why the transition mattered.
:::

:::rule id="ES-ADVICE-02" mandatory="false" category="modelling" tags="events, granularity"
Do not emit events for incidental implementation changes; emit facts that are meaningful to the domain and future consumers.
:::

:::rule id="ES-ADVICE-03" mandatory="false" category="operations" tags="snapshots"
Use snapshots only to address demonstrated replay cost; snapshots never replace the event stream as the recovery source.
:::

:::rule id="ES-ADVICE-04" mandatory="false" category="modelling" tags="time"
Represent effective business time separately from recorded time only when the domain requires temporal reasoning.
:::
