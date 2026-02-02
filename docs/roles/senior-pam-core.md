# Senior Pam Core Engineer (LLM Reliability)

> **✅ FILLED** — Yousof Algburi hired (Feb 2026)

## Problem This Role Solves

**Problem:** Product doesn't "feel good" during customer evaluation → new customers are churning. Competition is catching up.

**Root Cause:** LLM reliability issues, poor response quality, lack of observability into LLM behavior and customer health.

**Current state:** Anujan and the junior engineers respond to fires but don't have the experience to proactively stabilize the system. They try, but they're reactive—fixing symptoms, not root causes.

**Why now:**
- Competition is catching up on voice/latency (our moat is eroding)
- New customer churn is a growth killer
- We can now afford to hire someone senior who can own this
- We need someone with opinions and a plan, not just another firefighter

---

## Role Summary

This is NOT a feature role. This is a "make it bulletproof" role.

You'll own the reliability and performance of our core AI voice platform, ensuring we can scale 10x without degradation.

---

## Responsibilities

- Own LLM reliability and response quality for the Pam voice system
- Reduce LLM-related incidents (hallucinations, bad responses, failed intents)
- Build observability into LLM behavior—know when it's performing well vs poorly
- Monitor customer health from an LLM perspective (is Pam saying the right things?)
- Improve prompt engineering, model selection, and fallback strategies
- Establish quality baselines and alerting for LLM performance
- Mentor junior engineers on LLM reliability practices

---

## Success Criteria

### Month 1 (This is when we need significant impact)
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Shipping | Code in production Week 1 | PRs merged |
| Top reliability issue | Identified AND fixed | Incident rate drops |
| Customer health visibility | Dashboard exists, team using it | Can see which customers are struggling |
| Ownership | Has a plan for next 90 days, we believe it | Written doc, team buy-in |

### Month 3
| Metric | Target | How to Measure |
|--------|--------|----------------|
| LLM-related incidents | -50% from baseline | Incident tracker |
| New customer churn (quality-related) | -30% | Churn analysis |
| Response quality | Measurable improvement in intent success rate | LLM metrics dashboard |
| Proactive alerts | Catching LLM issues before customers report | Alert → fix before ticket |

### Month 6
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Quality-related churn | Rare, not a pattern | Churn reasons |
| Eval experience | Customers say "Pam gets it right" | Feedback, conversion rate |
| LLM quality | Clearly better than competition | Win/loss analysis, customer feedback |
| Team | Junior engineers leveled up on LLM reliability | They can debug and improve prompts |

### 1 Year
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Reliability as moat | Sales uses it as differentiator | Sales feedback |
| Scale | 10x volume, no degradation | System handles growth |
| Incidents | Boring, rare, quickly resolved | Incident tracker |

---

## Requirements

### Must Have
- 5+ years software engineering experience
- At least 1 year working on production LLM systems
- Strong TypeScript — our entire stack is TypeScript
- AWS experience (we run on AWS)
- Uses AI to code (Claude Code, Cursor, Copilot, etc.) — this is how we work
- Knows how to improve a live system without breaking it
- Track record of improving system reliability incrementally
- Experience with observability tools (Datadog, Grafana, etc.)

### Nice to Have
- Voice/telephony experience
- Experience at high-scale consumer products
- Has been on-call for AI systems

### Mindset
- Gets energy from making things reliable, not just shipping features
- Thinks about blast radius and rollback before shipping
- Data-driven (measures before and after, not ship and hope)
- Proactive (finds problems before they find us)

---

## What They'll Work On (First 30 Days)

**Week 1:**
- Day 1-2: Get access, meet team, understand the codebase
- Day 3-5: Ship first fix (doesn't have to be big, but proves they can move)
- End of week: Knows where the fires are, has opinions

**Week 2:**
- Identify THE top reliability issue (not a list, THE one that matters most)
- Start fixing it
- Stand up basic customer health visibility (even if scrappy)

**Week 3-4:**
- Top issue fixed, in production, measurable improvement
- Customer health dashboard exists and team is using it
- Written plan for months 2-3 that we believe in

**If they can't do this in 30 days, wrong hire.**

---

## Reporting & Team

- **Reports to:** Haroun (CTO)
- **Works with:** Anujan (Core), Juzer (Platform), Maheen (Support)
- **Dotted line:** Core Support engineers (mentorship)

---

## Compensation

*[To be filled based on market data]*

- Level: Senior (L5 equivalent)
- Location: [Remote / Hybrid / On-site]

---

## Interview Process

See [interviews/senior-engineer.md](../interviews/senior-engineer.md)

---

## Red Flags (Don't Hire If...)

- Only wants to work on new features
- No experience with production incidents
- Can't explain how they'd measure reliability
- Dismissive of "boring" infrastructure work
- Ships big changes without a rollout strategy
- "Ship it and see" mentality
