# Decision Checklists

Use these during architecture review, production readiness, or incident diagnosis.

## Architecture Selection

- [ ] Business outcome and "done" definition are explicit and verifiable by evidence
- [ ] Task determinism and risk profile are understood
- [ ] Minimum sufficient application form chosen (Workflow / Single / Long-Horizon / Multi)
- [ ] Autonomy level matched to risk tolerance (not maximized by default)
- [ ] Model vs Harness responsibilities written down
- [ ] Platform-provided vs application-owned capabilities decided
- [ ] Success metrics and primary failure modes identified

## Harness Design

- [ ] Explicit Agent Loop with a verification stage
- [ ] Durable task state + interrupt / resume path
- [ ] Context assembly strategy defined (selection / compression / offload, not unbounded dump)
- [ ] Completion decided by environmental evidence, not model self-declaration
- [ ] Tool / action permission model exists (least privilege)
- [ ] Multi-dimensional budgets enforced (steps / tokens / time / cost)
- [ ] Failure and recovery behavior specified
- [ ] Reusable Skills treated as versioned, discoverable assets

## Production Readiness

- [ ] Sandbox / workspace isolation and lifecycle defined
- [ ] State externalized (task state + key artifacts at minimum)
- [ ] AI Gateway covers LLM + tool + agent traffic with identity and budget
- [ ] Observability present: Trace + metrics + cost attribution + audit
- [ ] High-risk actions require HITL or strong policy
- [ ] Asset registry for Prompt / Skill / MCP / Agent with versioning
- [ ] At least basic evaluation path (golden set or simulation)
- [ ] Cancellation, timeout, and compensation behavior defined

## Multi-Agent Readiness

- [ ] Single-agent path is already stable and observable
- [ ] Team topology and responsibility split are clear
- [ ] Task assignment and result aggregation are designed
- [ ] Communication surfaces and protocols chosen intentionally
- [ ] Shared identity, budget, and audit model across agents
- [ ] Failure isolation between agents considered

## Optimization Readiness

- [ ] Traces are captured in a form that can become Trajectories
- [ ] Attribution process exists (Model vs Harness vs Environment vs Spec)
- [ ] Golden dataset or equivalent evaluation asset has been started
- [ ] Badcase → fix → regression loop is operational
- [ ] Any self-evolution is gated by review, versioning, and rollback

## Failure Attribution Quick Guide

| Symptom | First Suspect | Second Suspect |
|---------|---------------|----------------|
| Bad reasoning with good context | Model | Prompt / Context Builder |
| Loops or never finishes | Task Contract (completion evidence, budgets) | Model |
| Loses progress after interrupt | State / Checkpoint / Runtime | — |
| Wrong tool effects / overreach | Action Contract + Permissions | Sandbox isolation |
| Cannot debug or measure | Observability (Trace) | Asset ownership |
| Works in demo, fails in prod | Runtime / Gateway / State durability | Governance |
| Multi-agent chaos | Single-agent stability first | Topology & aggregation |
