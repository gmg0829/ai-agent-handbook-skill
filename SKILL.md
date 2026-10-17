---
name: ai-agent-handbook
description: Enterprise AI agent engineering framework from Alibaba Cloud AI Agent Handbook. Use for production agent design, architecture review, Harness design, task systems, runtime and sandbox, governance, observability, security, evaluation, trajectories, golden datasets, controlled self-evolution, multi-agent systems. Triggers on enterprise agent, production agent, agent architecture, Harness, agent lifecycle, agent governance, agent optimization, 企业级Agent, Agent架构, 生产化, Harness设计, 多智能体.
metadata:
  version: "1.1"
  source: aliyun/ai-agent-handbook
---

# AI Agent Handbook Skill

Enterprise-grade agent engineering decision framework. Turn model capability into reliable, governable, evolvable systems.

## Core Principle

**Agent = Model + Harness**

- **Model**: understanding, planning, generation, tool selection
- **Harness**: everything outside the model that turns discrete judgments into a sustainable, interruptible, verifiable task process (context, state, tools, environment, recovery, verification, risk control)

**First diagnostic rule**: never attribute all failures to the model. Decide Model-side vs Harness-side before optimizing.

## Quick Diagnosis Flow

When a user brings an agent problem, run this sequence:

1. **Map the system** onto five layers: Model → Harness Orchestration → Runtime → Sandbox/Environment → Platform
2. **Locate the weak stage**: Architecture → Build → Run → Govern → Optimize
3. **Classify the failure**:
   - Model: reasoning, planning quality, tool choice under good context
   - Harness: context assembly, state/recovery, completion evidence, permissions, budgets, verification
   - Runtime/Sandbox: isolation, durability, long-running/async, traffic governance
   - Governance: observability, security, asset ownership, pre-release verification
4. **Apply the matching checklist** (see section 6 and `references/decision-checklists.md`)
5. **Prefer the lowest-complexity fix** that closes the gap. Most production issues are Harness or Runtime, not model capability.

## 1. Architecture Decision Framework

### Application Forms (not a strict upgrade ladder)

- **Workflow** — deterministic orchestration, low autonomy
- **Single-Agent** — one agent owns the task loop
- **Long-Horizon Agent** — extends time with durable state and recovery
- **Multi-Agent** — extends collaboration structure

Workflow and Agent coexist long-term. Choose **minimum sufficient** form based on task determinism, risk, and required autonomy. Do not default to maximum autonomy.

### Pre-build Questions

1. What business outcome constitutes "done" and how is it verified?
2. How much autonomy is justified by risk tolerance?
3. Which capabilities must be owned vs provided by a shared platform?
4. What is the lowest-cost architecture that still meets reliability and governance needs?

### Layered Responsibility

| Layer | Core Question | Owns |
|-------|---------------|------|
| Model | What can it understand and reason? | Semantics, planning, generation, tool choice |
| Harness Orchestration | How does the agent work? | Loop, Context, State, Plan, Tool, Skill, Permission, Verification |
| Runtime | How does it keep running? | Process, scheduling, concurrency, wait, recovery |
| Sandbox / Environment | Where does it act and with what blast radius? | Files, processes, network, secrets, isolation |
| Agent Platform | How to scale delivery and governance? | Multi-tenancy, asset registry, unified control plane |

## 2. Harness Design (Build)

Harness has three engineering contracts: **Task**, **Information**, **Action**.

### Task Contract — Sustainable Progress

Design for three properties:

- **Advanceable** — clear next-step semantics
- **Interruptible & recoverable** — durable state, checkpoint, resume
- **Verifiably complete** — completion decided by environmental evidence, **not** by the model saying "done"

Canonical loop: Prepare → Model → Act → Observe → Verify

Use explicit state machines, multi-dimensional budgets (time, tokens, steps, cost), stage gates, and completion evidence.

### Information Contract — Context, State, Assets

- Context Builder: assemble, compress, offload
- Session / Task State / Workspace
- Memory / Knowledge / **Skill**

Treat Skill as a first-class reusable capability asset (versioned, discoverable, governed). Longer prompts are not a substitute for Harness.

### Action Contract — Controlled Execution

- Action Plane with clear environment contracts
- Function Calling / MCP / A2A
- Least-privilege permission checks
- HITL for high-risk or irreversible actions
- Verification feedback before accepting results

## 3. Runtime Foundations

A working prototype is not a production agent. Production requires:

1. **Sandbox / Workspace** as first-class citizen (Agent-use-sandbox vs Agent-in-sandbox)
2. **Externalized state**: Event Log, Checkpoint, Workspace snapshot, Artifact
3. **AI Gateway** distinguishing three traffic types — LLM, MCP/tool, Agent task — with consistent identity, permission, budget, routing, audit, approval
4. Clear sync vs async boundaries; process end ≠ task complete
5. For Multi-Agent: explicit team topology, assignment, aggregation, and orchestration vs execution split

Stabilize a single agent before scaling to Multi-Agent.

## 4. Governance Essentials

- **Observability**: metrics, logs, Trace, events, cost attribution, audit
- **Security**: Prompt Injection defenses, identity, step-level validation, high-risk authorization, data exfiltration controls
- **Asset Management**: unified registry + versioning for Prompt, Skill, MCP, Agent
- **Pre-production verification**: user + environment simulation, scenario coverage, Agent Simulation before release

## 5. Optimization Flywheel

Two tracks:

- **Model track** (SFT, Agentic RL, distillation) — only after confirming the problem is model-side
- **Agent / Harness track** — primary lever for most production issues

Data path:

```
Runtime Trace → Trajectory → Golden Dataset → Evaluation / Badcase → Fix → Controlled Self-Evolution
```

- Trajectory = reusable behavioral and decision evidence
- Golden Dataset = input + trajectory + result + judgment criteria
- Controlled self-evolution converts validated experience into Memory / Skill / tools / mechanisms under versioning and risk bounds

## 6. Decision Checklists (summary)

**Architecture**
- Minimum sufficient form (not maximum autonomy)
- Clear "done" with verifiable evidence
- Model vs Harness boundaries explicit
- Platform vs application ownership decided
- Risk matched to autonomy

**Production Readiness**
- Durable task state + recovery path
- Sandbox / workspace isolation defined
- AI Gateway covers LLM + tool + agent traffic
- Observability (Trace + cost + audit) present
- Permission model + high-risk HITL defined
- Asset registry (Skill / Prompt / MCP) exists
- Evaluation path (golden set or simulation) exists

**Common Anti-Patterns**
- Longer prompts as substitute for Harness
- Model self-declares task completion
- Multi-Agent before single agent is stable
- Every failure blamed on the model
- Shipping without Trace → Trajectory capture
- Uncontrolled self-modification of tools or skills

Full printable checklists: `references/decision-checklists.md`

## 7. How to Respond

When activated:

1. Run the Quick Diagnosis Flow above
2. Speak in the handbook language (Model / Harness / Task Contract / Completion Evidence / Trajectory / etc.)
3. Point to the weakest layer and the lowest-complexity fix
4. Load the relevant reference only when deeper detail is required:
   - `references/architecture.md`
   - `references/harness-build.md`
   - `references/runtime.md`
   - `references/governance.md`
   - `references/optimization.md`
   - `references/decision-checklists.md`

Source: [aliyun/ai-agent-handbook](https://github.com/aliyun/ai-agent-handbook) (Apache-2.0)
