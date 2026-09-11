---
id: distributed-microservice-architecture
version: "1.0.0"
title: Distributed Microservice Application Architecture Rules
scope: project
status: active
---

:::rule id="MS-ARCH-01" mandatory="true" category="architecture" tags="architecture, microservices, bounded-context"
Define each microservice around a single bounded context and business capability.
:::

:::rule id="MS-ARCH-02" mandatory="true" category="architecture" tags="architecture, cohesion"
Keep each microservice highly cohesive and internally responsible for one clear purpose.
:::

:::rule id="MS-ARCH-03" mandatory="true" category="architecture" tags="architecture, coupling"
Minimize coupling between microservices and avoid shared internal implementation dependencies.
:::

:::rule id="MS-ARCH-04" mandatory="true" category="architecture" tags="architecture, ownership, data"
Each microservice must exclusively own and control its own data and domain logic.
:::

:::rule id="MS-ARCH-05" mandatory="true" category="architecture" tags="architecture, integration, contracts"
All inter-service interaction must occur through explicit published contracts.
:::

:::rule id="MS-ARCH-06" mandatory="true" category="architecture" tags="architecture, encapsulation, database"
Never allow one microservice to read or write another microservice's private persistence model directly.
:::

:::rule id="MS-ARCH-07" mandatory="true" category="architecture" tags="architecture, api, contracts"
Expose only stable service interfaces; never expose internal domain models as external contracts.
:::

:::rule id="MS-ARCH-08" mandatory="true" category="architecture" tags="architecture, compatibility, versioning"
Service contracts must evolve in a backward-compatible way whenever feasible.
:::

:::rule id="MS-ARCH-09" mandatory="true" category="architecture" tags="architecture, autonomy"
A microservice must be independently understandable and changeable without requiring coordinated changes to unrelated services.
:::

:::rule id="MS-ARCH-10" mandatory="true" category="architecture" tags="architecture, layering, separation"
Separate transport models, application workflows, domain logic, and persistence concerns within each microservice.
:::

:::rule id="MS-ARCH-11" mandatory="true" category="architecture" tags="architecture, domain"
Keep business rules in the domain layer, not in controllers, message handlers, or repositories.
:::

:::rule id="MS-ARCH-12" mandatory="true" category="architecture" tags="architecture, orchestration, workflow"
Model multi-step business workflows explicitly rather than spreading implicit process state across services.
:::

:::rule id="MS-ARCH-13" mandatory="true" category="architecture" tags="architecture, consistency"
Do not assume distributed transactions across microservices.
:::

:::rule id="MS-ARCH-14" mandatory="true" category="architecture" tags="architecture, consistency, eventual-consistency"
Design cross-service state changes to tolerate eventual consistency.
:::

:::rule id="MS-ARCH-15" mandatory="true" category="architecture" tags="architecture, idempotency, messaging"
Commands, events, and externally visible state transitions must be idempotent where repeat delivery is possible.
:::

:::rule id="MS-ARCH-16" mandatory="true" category="architecture" tags="architecture, failure, resilience"
Treat remote calls as fallible and define explicit failure-handling behavior at service boundaries.
:::

:::rule id="MS-ARCH-17" mandatory="true" category="architecture" tags="architecture, async, integration"
Prefer asynchronous integration for cross-service communication when immediate consistency is not required.
:::

:::rule id="MS-ARCH-18" mandatory="false" category="architecture" tags="architecture, sync, request-response"
Use synchronous request-response only when the caller requires an immediate business result.
:::

:::rule id="MS-ARCH-19" mandatory="true" category="architecture" tags="architecture, events, integration"
Publish domain-significant events only after the originating state change is committed.
:::

:::rule id="MS-ARCH-20" mandatory="true" category="architecture" tags="architecture, events, semantics"
Events must describe facts that have happened, not commands for another service to execute.
:::

:::rule id="MS-ARCH-21" mandatory="false" category="architecture" tags="architecture, choreography, events"
Use event choreography only when the resulting business flow remains understandable and governable.
:::

:::rule id="MS-ARCH-22" mandatory="false" category="architecture" tags="architecture, orchestration"
Use explicit orchestration when a business workflow requires centralized coordination or compensation.
:::

:::rule id="MS-ARCH-23" mandatory="true" category="architecture" tags="architecture, queries, composition"
Do not build cross-service queries by joining private data stores.
:::

:::rule id="MS-ARCH-24" mandatory="false" category="architecture" tags="architecture, read-models, cqrs"
Create dedicated read models or aggregation services when user-facing views require data from multiple services.
:::

:::rule id="MS-ARCH-25" mandatory="true" category="architecture" tags="architecture, api, responsibility"
A service interface must reflect business capabilities, not CRUD exposure of internal entities.
:::

:::rule id="MS-ARCH-26" mandatory="true" category="architecture" tags="architecture, invariants"
Enforce business invariants within the boundary of the service that owns them.
:::

:::rule id="MS-ARCH-27" mandatory="true" category="architecture" tags="architecture, validation"
Validate all inbound commands, events, and requests at the service boundary before processing.
:::

:::rule id="MS-ARCH-28" mandatory="true" category="architecture" tags="architecture, state, statelessness"
Keep service instances stateless between requests unless durable business state is intentionally modeled.
:::

:::rule id="MS-ARCH-29" mandatory="false" category="architecture" tags="architecture, sagas, compensation"
Use compensating actions for long-running distributed workflows that cannot be made atomic.
:::

:::rule id="MS-ARCH-30" mandatory="true" category="architecture" tags="architecture, contracts, semantics"
Service contracts must define both payload structure and behavioral semantics.
:::

:::rule id="MS-ARCH-31" mandatory="true" category="architecture" tags="architecture, naming, ubiquitous-language"
Use consistent ubiquitous language in service names, contracts, commands, events, and domain models.
:::

:::rule id="MS-ARCH-32" mandatory="true" category="architecture" tags="architecture, anti-corruption, integration"
Use anti-corruption translation at service boundaries when integrating different domain models.
:::

:::rule id="MS-ARCH-33" mandatory="false" category="architecture" tags="architecture, cqrs"
Separate command and query models when write concerns and read concerns materially differ.
:::

:::rule id="MS-ARCH-34" mandatory="false" category="architecture" tags="architecture, event-sourcing"
Use event sourcing only when it provides clear business or architectural value.
:::

:::rule id="MS-ARCH-35" mandatory="true" category="architecture" tags="architecture, dependencies"
Application-layer dependencies between microservices must flow only through published contracts, never through shared domain code.
:::