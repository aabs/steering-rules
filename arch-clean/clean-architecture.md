---
id: clean-architecture
version: "2.0.0"
title: Clean Architecture Rules
scope: project
status: active
---

:::rule id="CA-01" mandatory="true" category="architecture" tags="architecture, clean-architecture, dependencies"
The domain layer shall not reference application, infrastructure, or presentation code; the application layer shall not reference infrastructure or presentation code; no inner layer shall import from outer-layer packages, namespaces, or assemblies.
:::

:::rule id="CA-02" mandatory="true" category="architecture" tags="architecture, clean-architecture, structure"
The system shall organize domain logic, application orchestration, infrastructure, and presentation as distinct named layers whose boundaries are visible in the package and project structure.
:::

:::rule id="CA-03" mandatory="true" category="architecture" tags="architecture, clean-architecture, domain, invariants"
Entities and value objects shall encode and enforce all business invariants; business rules and domain policies shall reside in domain-layer code that has no dependency on any delivery mechanism, framework, or infrastructure type.
:::

:::rule id="CA-04" mandatory="true" category="architecture" tags="architecture, clean-architecture, use-cases"
The system shall model each distinct application behavior as an explicit named use case or application service; use cases shall orchestrate domain operations and shall not implement infrastructure details such as SQL queries, HTTP calls, or file access.
:::

:::rule id="CA-05" mandatory="true" category="architecture" tags="architecture, clean-architecture, contracts"
Each use case shall define explicit named input and output data types; use case input and output types shall not contain or expose infrastructure-specific types such as ORM entities, HTTP request objects, or database row types.
:::

:::rule id="CA-06" mandatory="true" category="architecture" tags="architecture, clean-architecture, transactions"
The application service or use case shall define the transactional or consistency boundary for the operation it coordinates; transaction management shall not be performed inside domain entities or infrastructure adapters.
:::

:::rule id="CA-07" mandatory="true" category="architecture" tags="architecture, clean-architecture, ports-adapters"
Interfaces for capabilities required by inner layers shall be declared in the inner layer; infrastructure implementations shall depend on those interfaces, not the reverse; cross-layer interaction shall occur only through these declared interfaces.
:::

:::rule id="CA-08" mandatory="true" category="architecture" tags="architecture, clean-architecture, mapping"
WHEN data crosses a layer boundary, the system shall apply explicit mapping local to that boundary; adapters shall translate between external representations and internal domain models and shall not pass external types directly inward.
:::

:::rule id="CA-09" mandatory="true" category="architecture" tags="architecture, clean-architecture, persistence"
Persistence shall be implemented behind a domain-facing interface; repositories shall expose domain-meaningful named operations rather than generic data-table access such as raw query builders or table-scoped CRUD.
:::

:::rule id="CA-10" mandatory="true" category="architecture" tags="architecture, clean-architecture, errors"
WHEN an infrastructure or external system failure occurs, the system shall translate it to an application-layer result or typed error at the boundary; infrastructure exception types shall not propagate into application or domain layers.
:::

:::rule id="CA-11" mandatory="true" category="architecture" tags="architecture, clean-architecture, anti-corruption"
WHERE an external system uses a domain model incompatible with the application's domain model, the system shall implement an explicit anti-corruption or translation layer to prevent the external model from contaminating internal design.
:::

:::rule id="CA-12" mandatory="true" category="architecture" tags="architecture, clean-architecture, purity"
Core business logic shall be deterministic and free of direct I/O; time, randomness, and environment state shall not be read directly inside domain or use-case code and shall instead be injected through a defined abstraction.
:::

:::rule id="CA-13" mandatory="true" category="architecture" tags="architecture, clean-architecture, state"
The system shall not use global variables, static mutable state, or ambient context objects to share application state across components; all dependencies shall be passed explicitly.
:::

:::rule id="CA-14" mandatory="true" category="architecture" tags="architecture, clean-architecture, presentation"
Presentation code shall format, validate, and map requests and responses only; controllers, endpoints, and UI actions shall delegate all business behavior to use cases and shall not contain orchestration or business rule logic.
:::

:::rule id="CA-15" mandatory="true" category="architecture" tags="architecture, clean-architecture, validation, authorization"
The system shall validate all inputs at the application boundary before invoking domain behavior; authorization shall be enforced at the application or use-case boundary and shall not be performed inside infrastructure code.
:::

:::rule id="CA-16" mandatory="true" category="architecture" tags="architecture, clean-architecture, testability"
Domain and application logic shall be runnable and fully testable without a running web framework, database, message broker, or external service; the architecture shall isolate side-effect-free logic so it can be exercised without stubs or test doubles for those concerns.
:::

:::rule id="CA-17" mandatory="true" category="architecture" tags="architecture, clean-architecture, external-systems"
Databases, message brokers, file systems, third-party APIs, and frameworks shall be treated as replaceable external actors; domain and application layers shall contain no direct references to concrete external system types or vendor SDKs.
:::

:::rule id="CA-18" mandatory="true" category="architecture" tags="architecture, clean-architecture, composition-root"
Wiring of concrete implementations to abstractions shall occur exclusively at the composition root, which shall reside at the outermost architectural boundary.
:::

:::rule id="CA-19" mandatory="true" category="architecture" tags="architecture, clean-architecture, language"
The system shall use consistent business domain terminology for entities, value objects, use cases, ports, and repository methods; infrastructure or technical naming shall not appear in domain-layer identifiers.
:::

:::rule id="CA-20" mandatory="true" category="architecture" tags="architecture, clean-architecture, coupling"
Use cases shall not invoke other use cases directly; logic required by multiple use cases shall be extracted to a domain service or shared application service.
:::

:::rule id="CA-21" mandatory="true" category="architecture" tags="architecture, clean-architecture, change-isolation"
WHEN a framework, transport protocol, database technology, or external SDK is replaced, the domain and application layers shall require no modification.
:::

:::rule id="CA-22" mandatory="false" category="architecture" tags="architecture, clean-architecture, unit-of-work"
WHERE a use case coordinates multiple repository operations within a single consistency boundary, the system shall use an explicit unit-of-work abstraction to manage that boundary.
:::

:::rule id="CA-23" mandatory="false" category="architecture" tags="architecture, clean-architecture, cqrs"
WHERE separating read and write models materially improves clarity, performance, or independent evolution, the system shall use distinct command and query models.
:::

:::rule id="CA-24" mandatory="false" category="architecture" tags="architecture, clean-architecture, domain-events"
WHERE decoupling reactions from a domain action improves clarity without obscuring the overall flow, the system shall use domain events to communicate between bounded contexts or application components.
:::

:::rule id="CA-25" mandatory="false" category="architecture" tags="architecture, clean-architecture, modularity"
WHERE physical separation of layers into distinct projects or assemblies materially improves boundary enforcement, the system shall apply that separation.
:::
