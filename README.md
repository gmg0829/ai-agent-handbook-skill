# ai-agent-handbook-skill

Enterprise AI agent engineering skill distilled from [Alibaba Cloud AI Agent Handbook](https://github.com/aliyun/ai-agent-handbook).

## What it is

A decision framework skill for designing, reviewing, and improving **production** agents:

- Model vs Harness responsibility split
- Architecture form selection (Workflow / Single / Long-Horizon / Multi-Agent)
- Harness contracts: Task / Information / Action
- Runtime, sandbox, AI Gateway
- Governance, observability, security, asset management
- Optimization flywheel: Trace → Trajectory → Golden Dataset → Controlled Self-Evolution

## Install

Copy the `ai-agent-handbook/` directory into your agent skills folder (e.g. `.grok/skills/` or equivalent).

## Structure

```
ai-agent-handbook/
├── SKILL.md
└── references/
    ├── architecture.md
    ├── harness-build.md
    ├── runtime.md
    ├── governance.md
    ├── optimization.md
    └── decision-checklists.md
```

## Source

Distilled from [aliyun/ai-agent-handbook](https://github.com/aliyun/ai-agent-handbook) (Apache-2.0). This skill is a condensed engineering decision layer, not a full copy of the whitepaper.

## License

Apache-2.0 (aligned with upstream handbook).
