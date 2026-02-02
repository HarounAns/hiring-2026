# ADR-001: Q1 2026 Hiring Priorities

**Date:** January 19, 2026
**Status:** PROPOSED
**Deciders:** Haroun, Samee

## Context

We need to hire for Q1 2026. Samee proposed 6 engineering hires. We need to evaluate whether these hires solve our actual problems.

See: [jan-2026-state.md](../context/jan-2026-state.md)

## Decision

### Approved Hires (High Confidence)

| Role | Problem Solved | Rationale |
|------|---------------|-----------|
| Senior Pam Core (Stability) | Eval experience, LLM reliability | ✅ **HIRED** — Yousof Algburi (Feb 2026) |
| Core Support x2 | Onboarding, monitoring | Unblocks growth, customer health visibility |

### Needs Clarification

| Role | Question |
|------|----------|
| Integration Support | What problem does this solve? |
| Mid Dashboard | Is dashboard blocking growth? |
| Mid Mobile | Is mobile a Q1 priority? |
| Senior Sales (New Product) | Product undefined - hold? |

### Recommended Additions

| Role | Problem Solved | Rationale |
|------|---------------|-----------|
| Outbound Engineer | Scale in 3-6mo | Only 2 engineers, predictable pain |
| Onboarding Specialist (OPS) | Throughput | Real bottleneck is ops-side |

## Alternatives Considered

### Alternative A: Proceed with Samee's list as-is
- **Pros:** Faster, less friction
- **Cons:** 3 hires without clear problem mapping, no Outbound coverage

### Alternative B: Delay all hiring until product clarity
- **Pros:** More strategic
- **Cons:** Lose Q1, problems get worse

### Alternative C (Chosen): Proceed with clear hires, clarify others
- **Pros:** Progress on known problems, strategic on unclear ones
- **Cons:** Requires Samee alignment

## Consequences

### If we proceed:
- Senior Core hire focuses on stability (not features)
- Support hires focus on onboarding + monitoring
- Dashboard/Mobile/Integration hires depend on Samee answers
- Sales hire held until product defined

### If we don't:
- Eval experience stays bad → churn continues
- Onboarding stays slow → revenue delayed
- Outbound hits wall in 3-6 months

## Objection Handling

### "We need features to compete"
> We're signing 30-40/month - demand isn't the problem, activation is. Features on unstable base = more surface area to break.

### "Stability is boring / slows us down"
> Stability de-risks the raise. One bad outage during investor diligence could tank the round.

### "We can do both features and stability"
> With current team, no. Senior Core hire lets existing team focus on features while they harden the foundation.

### "Dashboard/Mobile are strategic"
> Maybe - but what problem do they solve THIS quarter? If the answer isn't clear, defer to Q2.

### "We need Sales product engineer now"
> For what product? Hiring senior talent for undefined work leads to churn. Define it first.

## Review Schedule

- [ ] **Feb 19** - 1 month: Are hires in pipeline? Any offers out?
- [ ] **Apr 19** - 3 month: Are hires ramped? Early signals?
- [ ] **Jul 19** - 6 month: Are problems solved? Metrics moved?
- [ ] **Jan 2027** - 1 year: Full retrospective
