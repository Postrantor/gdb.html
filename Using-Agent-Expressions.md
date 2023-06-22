---
description: Using Agent Expressions (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Using Agent Expressions (Debugging with GDB)
lang: en
resource-type: document
title: Using Agent Expressions (Debugging with GDB)
---
::: header
Next: [Varying Target Capabilities](Varying-Target-Capabilities.html#Varying-Target-Capabilities)]
:::

---

### F.3 Using Agent Expressions

Agent expressions can be used in several different ways by [GDB], and the debugger can generate different bytecode sequences as appropriate.

One possibility is to do expression evaluation on the target rather than the host, such as for the conditional of a conditional tracepoint. In such a case, [GDB] compiles the source expression into a bytecode sequence that simply gets values from registers or memory, does arithmetic, and returns a result.

Another way to use agent expressions is for tracepoint data collection. [GDB] adds `trace` bytecodes to save the pieces of memory that were used.

- The user selects trace points in the program's code at which GDB should collect data.
- The user specifies expressions to evaluate at each trace point. These expressions may denote objects in memory, in which case those objects' contents are recorded as the program runs, or computed values, in which case the values themselves are recorded.
- GDB transmits the tracepoints and their associated expressions to the GDB agent, running on the debugging target.
- The agent arranges to be notified when a trace point is hit.
- When execution on the target reaches a trace point, the agent evaluates the expressions associated with that trace point, and records the resulting values and memory ranges.
- Later, when the user selects a given trace event and inspects the objects and expression values recorded, GDB talks to the agent to retrieve recorded data as necessary to meet the user's requests. If the user asks to see an object whose contents have not been recorded, GDB reports an error.

---

::: header
Next: [Varying Target Capabilities](Varying-Target-Capabilities.html#Varying-Target-Capabilities)]
:::
