# Runtime Reference

## Why Runtime Matters

A demo that works in one interactive session is not a production agent. Production must answer:

- Where does the agent execute and with what isolation?
- Where does state live across process restarts and long waits?
- How does traffic (model, tools, tasks) enter and get governed?
- How do long-running and asynchronous tasks complete correctly?
- How do multiple agents coordinate without chaos?

## Sandbox & Workspace

Two deployment relationships:

- **Agent uses Sandbox**: orchestration outside, calls into isolated environment
- **Agent in Sandbox**: agent process + tools live together inside the isolation boundary

Treat Workspace as a first-class production resource: lifecycle, snapshots, cleanup, parallel exploration support.

## State Storage

Different objects have different consistency needs:

| Object | Typical Need |
|--------|--------------|
| Event Log / Trace | Append-only, durable |
| Checkpoint / Task State | Strong consistency for recovery |
| Workspace Snapshot | Point-in-time consistency |
| Artifact | Immutable after creation preferred |
| Long-term Memory / Knowledge | Eventual + search quality |
| Business Semantics | Domain-specific consistency |

Define a unified state contract even if physical storage differs.

## AI Gateway

Unify three traffic types under one control plane:

1. **LLM traffic** — model calls, routing, fallback, cost
2. **MCP / Tool traffic** — tool protocol proxying, auth, rate limits
3. **Agent traffic** — task entry, identity, budget, approval

Avoid collapsing them into a single undifferentiated proxy layer.

## Async & Long-running Tasks

- Distinguish process lifetime from task completion
- Define layered completion semantics
- Support timers, external events, and human waits
- Make cancellation and compensation explicit

## Multi-Agent Runtime Concerns

- Heterogeneous agent onboarding
- Team topology (hierarchical, peer, specialist pools)
- Task assignment and result aggregation
- Clear split between orchestration layer and execution systems
- Communication surfaces: capability, collaboration, internal, human-facing

Start with a stable single agent before scaling collaboration complexity.
