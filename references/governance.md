# Governance Reference

## Observability

Minimum viable observability for agents:

- Metrics (success rate, latency, cost, tool error rates)
- Structured logs
- Distributed Trace (especially across model → tool → sub-agent)
- Domain events (task started/completed/failed, high-risk actions)
- Cost attribution per task / user / agent
- Audit trail for permissions and sensitive actions

Trace is the foundation for later Trajectory construction.

## Security

Key threat surfaces:

- Prompt Injection (direct and indirect via tools/content)
- Over-privileged tools
- Data exfiltration
- Unauthorized high-impact actions
- Identity spoofing across agents or tools

Controls:

- Strong identity and authentication at gateway and tool boundaries
- Step-level permission checks
- High-risk action authorization (HITL or policy)
- Data boundary enforcement
- Content and tool output validation

## AI Asset Management

Treat the following as managed assets with registry, versioning, discovery, dependency tracking, and release process:

- Prompts / system instructions
- Skills
- MCP servers / tool definitions
- Agent definitions / configurations

Without asset management, production systems accumulate unowned, unversioned, undeployable knowledge.

## Pre-release Verification

Before production:

- User simulation
- Environment / tool simulation
- Scenario configuration covering happy path + edge cases + adversarial cases
- Agent Simulation runs that produce observable trajectories

Simulation is cheaper than production incidents.
