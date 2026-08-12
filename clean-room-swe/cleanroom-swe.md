---
id: cleanroom-testing
version: "1.0.0"
title: Cleanroom Software Engineering Rules
scope: project
status: active
---

:::rule id="CRS-001" mandatory="true" category="quality" tags="quality, testing, design"
Every implementation artifact must trace to a Spec-Kit specification artifact.
:::

:::rule id="CRS-002" mandatory="true" category="quality" tags="quality, testing, design"
Every accepted change must preserve the invariants declared by its specification.
:::

:::rule id="CRS-003" mandatory="true" category="quality" tags="quality, testing, design"
Correctness must be reasoned about before runtime validation is used as evidence.
:::

:::rule id="CRS-004" mandatory="true" category="quality" tags="quality, testing, design"
A review must verify behaviour against the specification, not merely inspect style.
:::

:::rule id="CRS-005" mandatory="true" category="quality" tags="quality, testing, design"
The author must not be the sole verifier of correctness.
:::

:::rule id="CRS-006" mandatory="true" category="quality" tags="quality, testing, design"
State-changing behaviour must be expressed as explicit transitions.
:::

:::rule id="CRS-007" mandatory="true" category="quality" tags="quality, testing, design"
Mutable state must be local, justified, and bounded.
:::

:::rule id="CRS-008" mandatory="true" category="quality" tags="quality, testing, design"
Side effects must be explicit at API boundaries.
:::

:::rule id="CRS-009" mandatory="true" category="quality" tags="quality, testing, design"
Business decisions must not be hidden inside incidental infrastructure code.
:::

:::rule id="CRS-010" mandatory="true" category="quality" tags="quality, testing, design"
High-risk logic must have machine-checkable correctness evidence.
:::

:::rule id="CRS-011" mandatory="true" category="quality" tags="quality, testing, design"
Production code must compile with zero compiler and analyzer warnings.
:::

:::rule id="CRS-012" mandatory="true" category="quality" tags="quality, testing, design"
Nullable reference types must remain enabled for production code.
:::

:::rule id="CRS-013" mandatory="true" category="quality" tags="quality, testing, design"
Warnings must be fixed or explicitly justified by a narrow suppression.
:::

:::rule id="CRS-014" mandatory="true" category="quality" tags="quality, testing, design"
Every build must be reproducible from source control alone.
:::

:::rule id="CRS-015" mandatory="true" category="quality" tags="quality, testing, design"
Dependency versions must be locked for repeatable restore.
:::

:::rule id="CRS-016" mandatory="true" category="quality" tags="quality, testing, design"
Generated artifacts must either be reproducible or excluded from source control.
:::

:::rule id="CRS-017" mandatory="true" category="quality" tags="quality, testing, design"
Tests must be derived from specified behaviour, not implementation structure.
:::

:::rule id="CRS-018" mandatory="true" category="quality" tags="quality, testing, design"
Regression tests must be added for every corrected defect.
:::

:::rule id="CRS-019" mandatory="true" category="quality" tags="quality, testing, design"
Property tests must cover behaviours with broad input domains.
:::

:::rule id="CRS-020" mandatory="true" category="quality" tags="quality, testing, design"
Critical edge cases must be named in the specification or the test.
:::

:::rule id="CRS-021" mandatory="true" category="quality" tags="quality, testing, design"
A passing test suite must not be treated as proof of correctness.
:::

:::rule id="CRS-022" mandatory="true" category="quality" tags="quality, testing, design"
Coverage must not be used as the primary measure of quality.
:::

:::rule id="CRS-023" mandatory="true" category="quality" tags="quality, testing, design"
Reliability claims must be supported by usage-oriented evidence.
:::

:::rule id="CRS-024" mandatory="true" category="quality" tags="quality, testing, design"
Performance-sensitive behaviour must have explicit budgets and validation.
:::

:::rule id="CRS-025" mandatory="true" category="quality" tags="quality, testing, design"
Concurrency behaviour must define ordering, isolation, and failure assumptions.
:::

:::rule id="CRS-026" mandatory="true" category="quality" tags="quality, testing, design"
External integration behaviour must define retry, timeout, and idempotency semantics.
:::

:::rule id="CRS-027" mandatory="true" category="quality" tags="quality, testing, design"
Failures must be modelled as expected outcomes, not exceptional surprises.
:::

:::rule id="CRS-028" mandatory="true" category="quality" tags="quality, testing, design"
Logs, metrics, and traces must not be the only evidence that behaviour is correct.
:::

:::rule id="CRS-029" mandatory="true" category="quality" tags="quality, testing, design"
Production assumptions must be observable.
:::

:::rule id="CRS-030" mandatory="true" category="quality" tags="quality, testing, design"
Each increment must be independently reviewable and releasable.
:::

:::rule id="CRS-031" mandatory="true" category="quality" tags="quality, testing, design"
A release must not proceed while mandatory CRS rules are violated.
:::

:::rule id="CRS-032" mandatory="false" category="quality" tags="quality, testing, design"
Use Spec-Kit for specifications, clarification, analysis, implementation planning, and task derivation.
:::

:::rule id="CRS-033" mandatory="false" category="quality" tags="quality, testing, design"
Use Architecture Decision Records for decisions that affect correctness, reliability, or maintainability.
:::

:::rule id="CRS-034" mandatory="false" category="quality" tags="quality, testing, design"
Use PlantUML or Mermaid to describe state models, workflows, and integration flows.
:::

:::rule id="CRS-035" mandatory="false" category="quality" tags="quality, testing, design"
Use TLA+ or PlusCal for concurrent, distributed, or state-heavy correctness models.
:::

:::rule id="CRS-036" mandatory="false" category="quality" tags="quality, testing, design"
Use Dafny when executable code benefits from formal preconditions, postconditions, and proofs.
:::

:::rule id="CRS-037" mandatory="false" category="quality" tags="quality, testing, design"
Use FsCheck for property-based testing of C# and .NET behaviour.
:::

:::rule id="CRS-038" mandatory="false" category="quality" tags="quality, testing, design"
Use xUnit or NUnit for behaviour-and-regression test suites.
:::

:::rule id="CRS-039" mandatory="false" category="quality" tags="quality, testing, design"
Use Stryker.NET to assess whether tests detect meaningful behavioural changes.
:::

:::rule id="CRS-040" mandatory="false" category="quality" tags="quality, testing, design"
Use Microsoft.CodeAnalysis.NetAnalyzers as the baseline analyzer set for .NET code.
:::

:::rule id="CRS-041" mandatory="false" category="quality" tags="quality, testing, design"
Use StyleCop Analyzers when consistent public API and documentation style matter.
:::

:::rule id="CRS-042" mandatory="false" category="quality" tags="quality, testing, design"
Use SonarQube Community Edition for maintainability, reliability, and duplication analysis.
:::

:::rule id="CRS-043" mandatory="false" category="quality" tags="quality, testing, design"
Use dotnet format to make formatting enforcement repeatable.
:::

:::rule id="CRS-044" mandatory="false" category="quality" tags="quality, testing, design"
Use NuGet package lock files for deterministic dependency restore.
:::

:::rule id="CRS-045" mandatory="false" category="quality" tags="quality, testing, design"
Use GitHub Actions or an equivalent CI runner for repeatable verification gates.
:::

:::rule id="CRS-046" mandatory="false" category="quality" tags="quality, testing, design"
Use Dev Containers when local environment drift affects build or test repeatability.
:::

:::rule id="CRS-047" mandatory="false" category="quality" tags="quality, testing, design"
Use Dependabot or Renovate to make dependency updates explicit and reviewable.
:::

:::rule id="CRS-048" mandatory="false" category="quality" tags="quality, testing, design"
Use OWASP Dependency-Check or Trivy to detect known vulnerable dependencies and container layers.
:::

:::rule id="CRS-049" mandatory="false" category="quality" tags="quality, testing, design"
Use Semgrep for lightweight custom static checks that encode project-specific constraints.
:::

:::rule id="CRS-050" mandatory="false" category="quality" tags="quality, testing, design"
Use NBomber for .NET load, stress, and reliability testing.
:::

:::rule id="CRS-051" mandatory="false" category="quality" tags="quality, testing, design"
Use k6 for protocol-level load and reliability testing.
:::

:::rule id="CRS-052" mandatory="false" category="quality" tags="quality, testing, design"
Use BenchmarkDotNet for repeatable microbenchmark evidence.
:::

:::rule id="CRS-053" mandatory="false" category="quality" tags="quality, testing, design"
Use OpenTelemetry for portable traces, metrics, and logs.
:::

:::rule id="CRS-054" mandatory="false" category="quality" tags="quality, testing, design"
Use Prometheus and Grafana for reliability dashboards and operational signal review.
:::

:::rule id="CRS-055" mandatory="false" category="quality" tags="quality, testing, design"
Use Seq for structured log inspection in .NET systems.
:::

:::rule id="CRS-056" mandatory="false" category="quality" tags="quality, testing, design"
Use the .NET Aspire dashboard for local distributed-system inspection during development.
:::

:::rule id="CRS-057" mandatory="false" category="quality" tags="quality, testing, design"
Use CODEOWNERS to require independent review for high-risk areas.
:::

:::rule id="CRS-058" mandatory="false" category="quality" tags="quality, testing, design"
Use pull request checklists to require explicit evidence for CRS compliance.
:::

:::rule id="CRS-059" mandatory="false" category="quality" tags="quality, testing, design"
Use Git tags, release notes, or build provenance records to preserve certification evidence.
:::

:::rule id="CRS-060" mandatory="false" category="quality" tags="quality, testing, design"
Use containers only when their inputs, base images, and build steps are explicit.
:::