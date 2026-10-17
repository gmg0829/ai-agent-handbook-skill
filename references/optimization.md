# Optimization Reference

## Two Tracks

**Model optimization** (SFT, Agentic RL, distillation, etc.) only after confirming the failure is primarily model-side.

**Agent / Harness optimization** is usually the higher-leverage path for production issues: better context, better state, better tools, better verification, better budgets, better recovery.

## Data Flywheel

```
Runtime events / Trace
        ↓
Trajectory (structured behavioral + decision evidence)
        ↓
Golden Dataset (input + trajectory + result + judgment criteria)
        ↓
Evaluation / Badcase analysis
        ↓
Targeted fixes (Harness first, Model second)
        ↓
Controlled Self-Evolution (Memory / Skill / mechanism updates under governance)
```

## Trajectory

A Trajectory is more than a log. It should capture:

- Goal and constraints
- Key decisions and reasons (when available)
- Actions taken and observations
- Intermediate verification results
- Final outcome and evidence

Good trajectories become the raw material for both debugging and training/evaluation data.

## Golden Dataset

A high-quality evaluation asset contains:

- Input / scenario
- Expected or acceptable trajectories (or key properties)
- Final result criteria
- Explicit judgment rules (automatic or human)

Prefer quality and coverage of important failure modes over sheer volume.

## Badcase Loop

1. Detect (from production or evaluation)
2. Attribute (Model vs Harness vs Environment vs Spec)
3. Fix the highest-leverage layer
4. Add regression case to golden set
5. Re-evaluate

## Controlled Self-Evolution

Convert validated experience into:

- Memory updates
- New or improved Skills
- Tool improvements
- Mechanism / policy changes

Always under governance: versioning, review, rollback, risk bounds. Uncontrolled self-modification is a liability.
