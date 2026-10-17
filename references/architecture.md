# Architecture Reference

## Application Form Selection

Not every problem needs maximum autonomy. Choose based on:

| Factor | Prefer Workflow | Prefer Agent |
|--------|-----------------|--------------|
| Task determinism | High | Low / open-ended |
| Risk of incorrect action | High | Controllable |
| Need for long-horizon recovery | Low | High |
| Collaboration complexity | Simple orchestration | Dynamic teaming |
| Observability & audit requirements | Strict | Still required, but different shape |

Long-Horizon and Multi-Agent are independent axes. You can have a long-running single agent or a short multi-agent collaboration.

## Maturity Levels (practical view)

1. **Prototype** — works in one session, state in memory, no formal recovery
2. **Reliable Single Agent** — durable state, sandbox, basic verification, restartable
3. **Governed Production** — gateway, permissions, observability, asset registry, evaluation
4. **Evolving System** — trajectory capture, golden datasets, controlled self-evolution, multi-agent platform

Jumping levels without the previous foundations usually fails.

## Reference Architecture Questions

When reviewing an architecture, force answers to:

- What is the unit of work and what constitutes completion evidence?
- Where does task state live and how is it recovered?
- What is the blast radius of tools and how is it constrained?
- Who owns the Harness vs who provides platform services?
- How are identity, budget, and audit applied uniformly?

## Platform vs Application Split

Good platforms provide:

- Runtime & sandbox lifecycle
- AI Gateway (LLM + MCP + Agent traffic)
- State and artifact storage contracts
- Observability and audit primitives
- Asset registry (Prompt / Skill / MCP / Agent)
- Evaluation and simulation infrastructure

Applications / product teams should own:

- Domain-specific task design and completion criteria
- Domain tools and knowledge
- Business risk policies and HITL thresholds
- Domain evaluation datasets
