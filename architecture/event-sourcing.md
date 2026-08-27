---
id: event-sourcing-architecture
version: "1.0.0"
title: Event Sourcing Architecture Rules
scope: project
status: active
---

:::rule id="ES-CORE-01" mandatory="true" category="architecture" tags="event-sourcing, source-of-truth, history"
For an event-sourced aggregate, its ordered event stream is the authoritative, immutable history of domain facts; current state is derived by replaying that history.
:::

:::rule id="ES-CORE-02" mandatory="true" category="architecture" tags="events, domain-language, semantics"
Events represent completed, domain-significant facts, expressed in ubiquitous language and independently of persistence or transport concerns.
:::

:::rule id="ES-CORE-03" mandatory="true" category="architecture" tags="events, granularity, contracts"
Record the meaningful business fact needed to explain a state transition; do not model events as database updates, implementation details, commands, or noise.
:::

:::rule id="ES-CORE-04" mandatory="true" category="architecture" tags="aggregate, consistency, invariants"
An aggregate is a single consistency boundary: it owns its state and events, evaluates commands against its rehydrated state, enforces its invariants, then emits resulting events.
:::

:::rule id="ES-CORE-05" mandatory="true" category="architecture" tags="aggregate, autonomy, dependencies"
Aggregate decision-making must use only command input, aggregate state, and domain rules within its boundary; it must not depend on synchronous external reads or ambient state.
:::

:::rule id="ES-CORE-06" mandatory="true" category="architecture" tags="replay, determinism, side-effects"
Event application and aggregate rehydration must be deterministic, side-effect free, and independent of wall-clock time.
:::

:::rule id="ES-CORE-07" mandatory="true" category="architecture" tags="ordering, concurrency, streams"
Preserve order within an aggregate stream and use optimistic concurrency, such as expected-version checks, to reject conflicting appends.
:::

:::rule id="ES-CORE-08" mandatory="true" category="architecture" tags="cqrs, projections, derivation"
Read models are derived views, not sources of truth; keep projections separate from aggregate decision logic and make them rebuildable from event history.
:::

:::rule id="ES-CORE-09" mandatory="true" category="architecture" tags="projections, idempotency, ordering"
Projection handlers must tolerate duplicate delivery and must not rely on a global order across independent streams.
:::

:::rule id="ES-CORE-10" mandatory="true" category="architecture" tags="evolution, compatibility, replay"
Treat event schemas as long-lived contracts; evolve them compatibly where possible, and use explicit version-aware transformation when required to preserve replayability.
:::

:::rule id="ES-CORE-11" mandatory="true" category="architecture" tags="metadata, observability, traceability"
Keep technical metadata separate from domain event data, while retaining enough metadata for causation, correlation, versioning, and replay diagnosis.
:::

:::rule id="ES-CORE-12" mandatory="true" category="architecture" tags="process, integration, boundaries"
Coordinate reactions that cross aggregate or service boundaries outside the originating aggregate, using durable asynchronous process logic where necessary.
:::

:::rule id="ES-ADVICE-01" mandatory="false" category="architecture" tags="snapshots, performance"
Use snapshots only when replay cost creates a material latency, availability, or operational problem; treat every snapshot as disposable derived state.
:::

:::rule id="ES-ADVICE-02" mandatory="false" category="architecture" tags="saga, process-manager, workflow"
Use a process manager or saga when a business workflow spans independent aggregate or service boundaries and requires durable coordination.
:::

:::rule id="ES-ADVICE-03" mandatory="false" category="architecture" tags="time, temporal-modelling"
Model effective business time separately from recording time when the domain must reason about when a fact was true, rather than merely when it was stored.
:::

:::rule id="ES-ADVICE-04" mandatory="false" category="architecture" tags="upcasting, migration"
Prefer additive, compatible event-contract evolution; introduce upcasting or translation only when compatibility cannot be maintained directly.
:::
