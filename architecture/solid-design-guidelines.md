---
id: solid-design-guidelines
version: "1.0.0"
title: SOLID Design Guidelines
scope: project
status: active
---

:::rule id="SOLID-CORE-01" mandatory="true" category="design" tags="srp, cohesion"
Give each module one cohesive responsibility and one clear reason to change; split it when unrelated responsibilities evolve independently.
:::

:::rule id="SOLID-CORE-02" mandatory="true" category="design" tags="boundaries, domain, effects"
Keep domain decisions and invariants separate from orchestration, I/O, persistence, transport, frameworks, and other side effects.
:::

:::rule id="SOLID-CORE-03" mandatory="true" category="design" tags="ocp, variation, simplicity"
Introduce an extension seam only where behaviour is expected to vary independently; prefer adding behaviour over repeatedly changing stable policy code.
:::

:::rule id="SOLID-CORE-04" mandatory="true" category="design" tags="lsp, contracts, inheritance"
Use inheritance only for genuine substitutability: every subtype must preserve the parent’s observable contract, including valid inputs, guarantees, invariants, and failure behaviour.
:::

:::rule id="SOLID-CORE-05" mandatory="true" category="design" tags="composition, inheritance"
Prefer composition for reuse unless inheritance is required by a true subtype relationship.
:::

:::rule id="SOLID-CORE-06" mandatory="true" category="design" tags="isp, interfaces"
Expose small, cohesive, client-oriented interfaces; do not require clients to depend on operations they do not use.
:::

:::rule id="SOLID-CORE-07" mandatory="true" category="design" tags="dip, policy, abstractions"
High-level policy must depend on contracts it owns or defines, not on low-level implementation details.
:::

:::rule id="SOLID-CORE-08" mandatory="true" category="design" tags="dependencies, composition-root"
Make required dependencies explicit and compose concrete implementations at application boundaries; do not hide them in globals, service locators, or ambient mutable state.
:::

:::rule id="SOLID-CORE-09" mandatory="true" category="design" tags="boundaries, translation"
Translate external, framework, persistence, and transport models at their boundary; do not let them shape core domain abstractions.
:::

:::rule id="SOLID-CORE-10" mandatory="true" category="design" tags="simplicity, change-isolation"
Prefer the simplest design that isolates likely changes, maintains cohesive responsibilities, and keeps contracts clear.
:::

:::rule id="SOLID-ADVICE-01" mandatory="false" category="design" tags="cqrs, clarity"
Separate commands from queries when mixing mutation and observation obscures intent, invariants, or testability.
:::

:::rule id="SOLID-ADVICE-02" mandatory="false" category="design" tags="purity, testability"
Keep pure decision logic separate from side-effecting operations where doing so improves clarity or testability.
:::

:::rule id="SOLID-ADVICE-03" mandatory="false" category="design" tags="contracts, documentation"
Document or encode non-obvious behavioural contracts, including preconditions, guarantees, invariants, and error behaviour.
:::

:::rule id="SOLID-ADVICE-04" mandatory="false" category="design" tags="refactoring, smells"
Treat oversized types, repeated type-switching, feature envy, and broad interfaces as prompts to reassess cohesion and dependency direction.
:::
