---
id: modular-monolith-architecture
version: "1.0.0"
title: Modular Monolith Architecture Rules
scope: project
status: active
---

:::rule id="AMM-01" mandatory="true" category="design" tags="boundaries"
The system shall enforce module boundaries through compiler-level access controls — such as package-private visibility, internal access modifiers, or equivalent — rather than by naming convention or documentation alone.
:::

:::rule id="AMM-02" mandatory="true" category="design" tags="boundaries, contracts"
WHEN a module invokes behavior in another module, the invocation shall target only the receiving module's declared public interface; direct references to another module's internal types, repositories, or service implementations from outside that module are prohibited.
:::

:::rule id="AMM-03" mandatory="false" category="design" tags="data-ownership"
Each module shall own its own database tables, schemas, or collections; no module shall query or write to tables owned by another module; cross-module data needs shall be satisfied through the owning module's public query interface.
:::

:::rule id="AMM-04" mandatory="false" category="design" tags="contracts"
A module's public interface shall expose only stable data-transfer types and declared service contracts; internal domain entities, ORM models, and implementation-specific types shall not appear in a module's public API.
:::

:::rule id="AMM-05" mandatory="true" category="design" tags="dependencies"
The dependency graph across modules shall be acyclic; WHEN a cycle is detected between two modules, the system shall resolve it by extracting the shared concept to a dedicated shared kernel module or by replacing the direct dependency with an event.
:::

:::rule id="AMM-06" mandatory="false" category="design" tags="dependencies"
WHERE multiple modules depend on the same domain concept or cross-cutting concern, the system shall place it in an explicit shared kernel module with a minimal, stable API; modules shall not reach into each other to reuse shared logic.
:::

:::rule id="AMM-07" mandatory="false" category="design" tags="decoupling"
WHEN a module must react to a state change originating in another module, the system shall communicate that change through a domain event or in-process event bus rather than a direct synchronous call from the source module into the reacting module.
:::

:::rule id="AMM-08" mandatory="true" category="design" tags="cohesion"
Each module shall encapsulate a single identifiable business capability or bounded context; top-level module boundaries shall not be organized by technical role such as controllers, services, or repositories.
:::

:::rule id="AMM-09" mandatory="true" category="design" tags="deployment"
The system shall package and deploy all modules as a single executable artifact; module boundaries shall be logical code boundaries and shall not introduce inter-process communication, network calls, or separate deployment lifecycles between modules.
:::

:::rule id="AMM-10" mandatory="false" category="design" tags="testability"
Each module shall be fully testable in isolation using test doubles for any cross-module interface it depends on; no module's test suite shall require a concrete implementation of another module to be running.
:::
