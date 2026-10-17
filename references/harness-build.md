# Harness Build Reference

## Definition of Harness

Harness is the engineering system outside the model that organizes context, capabilities, state, environment, and control mechanisms around an Agent Loop, turning model judgments into executable, recoverable, and verifiable task processes.

It is **not**:
- A longer system prompt
- A synonym for any particular framework
- Purely the tool-calling layer

## Three Contracts

### 1. Task Contract

Goal: make progress deterministic enough to be reliable.

Key mechanisms:
- Explicit Agent Loop (Prepare → Model → Act → Observe → Verify)
- Task state machine with durable state
- Multi-dimensional budgets (steps, tokens, time, cost, tool calls)
- Stage gates / phase boundaries
- Delegation and asynchronous continuation
- Completion decided by **evidence from the environment**, not model self-declaration

Design questions:
- Can the task be interrupted and resumed without loss of progress?
- Is "done" checkable by an external observer or test?
- What happens when the model loops or gets stuck?

### 2. Information Contract

Goal: give the model the right information at the right time without unbounded growth.

Key objects:
- **Context Builder**: selection, compression, offloading
- **Session** vs **Task State** vs **Workspace**
- **Memory** (short/long), **Knowledge**, **Skill**

Skills should be treated as versioned, discoverable, governed assets — not just prompt snippets.

### 3. Action Contract

Goal: controlled, observable, reversible (where possible) effects on the world.

Key mechanisms:
- Clear environment contracts (what the tool/sandbox guarantees)
- Permission checks before high-impact actions
- HITL for irreversible or high-risk operations
- Verification after action (test, diff, assertion, human review)
- Support for Function Calling, MCP, A2A and similar protocols

## Harness Construction Patterns

Four common entry points:

1. **High-code frameworks** — maximum control, highest ownership cost
2. **Productized Harness** (Coding Agent CLI / SDK / workspace assistants) — reuse mature loops and tooling
3. **Managed Agents** — platform owns significant Harness + runtime surface
4. **Agent cloud products** — highest abstraction, lowest customization

Choose based on data boundary, customization depth, operational responsibility, and delivery speed.

## Minimal Viable Harness Checklist

- [ ] Explicit loop with Prepare / Act / Verify stages
- [ ] Durable task state + recovery path
- [ ] Context assembly strategy (not just "stuff everything in")
- [ ] Tool permission model
- [ ] Completion evidence definition
- [ ] Basic failure handling and budget limits
