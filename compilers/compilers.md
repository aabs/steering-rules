---
id: compiler-development
version: "1.0.0"
title: Compiler Development Rules
scope: project
status: active
---

:::rule id="CMP-001" mandatory="false" category="compilers" tags="compiler, design"
Never implement lowerings in code generation systems. Instead create an independent transformation stage that performs the lowering.
:::

