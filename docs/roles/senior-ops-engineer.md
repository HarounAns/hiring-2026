# Senior Operations Engineer (AI-Powered Support Automation)

## Problem This Role Solves

**Problem:** No observability into support volume, manual triage is leaky, OPS and Support Engineers are overwhelmed with repetitive work.

**Root Cause:** Support process is email-based and manual, no proper ticketing system, no way to measure the funnel or identify automation opportunities.

**Current state:**
- Emails come in, but not all requests get logged as discrete work items
- Observability is at the thread level (open vs closed), which misses nuance
- One thread can contain many unrelated issues, questions, and requests
- No visibility into actual ticket volumes or escalation rates
- Manual end-of-day counts: "Was it 1-2 tickets or 10-12 to engineering?"
- OPS triages everything manually, including repeatable, known issues
- Support engineers (Maheen, Shaheer) get pulled in for work that could be automated or handled at Tier 1

**The deeper problem:**

We have no structured observability into onboarding/support pain, so we can't confidently link specific issues (integration delays, slow responses, repeated glitches) to churn.

As a result:
- **OPS and Support respond reactively** to loud anecdotes instead of data
- **We miss chances to proactively intervene** with at-risk accounts (reassurance emails, expectation setting, workarounds)
- **Product/Eng can't prioritize** the work that would actually reduce churn
- **We can't detect patterns** like "accounts with >X days in integration pending + >Y support touches churn at 3x baseline"

**Why now:**
- We anticipate significant growth — manual process won't scale
- Customers are churning and we only have anecdotes, not data, to explain why
- AI can now handle Tier 0 triage — we should use it
- Hiring more support engineers without automation = throwing bodies at the problem

---

## Role Summary

This is an **automation and observability** role, not a traditional support role.

You'll build AI-powered systems that:
1. Turn emails into tickets automatically
2. Create observability into the support funnel
3. Enable AI to handle Tier 0 (auto-resolution of simple issues)
4. Make OPS more effective with AI-assisted tooling

Your success metric: **push resolutions earlier in the funnel** (more Tier 0/Tier 1, less Tier 2/Tier 3).

---

## Responsibilities

### 1. Support Process Automation (Email → Tickets)
- Build AI pipeline to turn support emails into structured tickets
- Extract: customer, issue type, urgency, relevant context
- Auto-tag and route to appropriate queue
- Integrate with Linear for engineering visibility

### 2. Observability & Funnel Metrics
- Build dashboards showing:
  - Total requests per day/week/month
  - Resolution by tier (Tier 0 AI, Tier 1 OPS, Tier 2 Support Eng, Tier 3 Product Eng)
  - Time to resolution at each tier
  - Escalation rates and patterns
- Use data to identify automation opportunities

### 3. AI Knowledge Base & Auto-Response
- Build knowledge base system for common issues
- AI drafts responses, OPS does human-in-the-loop approval
- Continuously improve KB without breaking existing answers
- Goal: AI handles more Tier 0 resolutions over time

### 4. AI-Enabled Runbooks
- Create runbooks OPS can query via Claude Code
- "What do I check for this issue?" → AI suggests dials/switches
- Ability to test changes and verify fix worked
- Auto-generate customer response: "Issue resolved, here's what we did"

### 5. Smart Triage & Escalation
- Build system that suggests when to escalate and to whom
- Auto-route: PAM Core issues → Maheen, Integration issues → Shaheer
- Flag urgent issues that need immediate attention
- Reduce mis-routes and escalation delays

---

## Success Criteria

### Month 1
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Shipping | Code in production Week 1 | PRs merged |
| Email → Ticket pipeline | Working prototype | Emails automatically becoming Linear tickets |
| Funnel visibility | Basic dashboard exists | Can see volume by tier |
| Quick win | One automation that saves OPS time | OPS feedback |

### Month 3
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Ticket coverage | 90%+ of emails become tickets automatically | Audit sample |
| Tier 0 resolution | AI handling 10%+ of requests without human | Funnel metrics |
| Escalation accuracy | 80%+ of escalations go to right person first time | Mis-route tracking |
| OPS satisfaction | "This makes my job easier" | Qualitative feedback |

### Month 6
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Tier 0 resolution | AI handling 25%+ of requests | Funnel metrics |
| Time to resolution | 30% faster than baseline | Ticket metrics |
| Knowledge base | 50+ issues covered, actively used | KB metrics, OPS usage |
| Runbook usage | OPS using AI runbooks daily | Usage tracking |

### 1 Year
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Tier 0 resolution | AI handling 40%+ of requests | Funnel metrics |
| Support scalability | 2x customers, same support headcount | Headcount vs volume |
| Funnel optimization | Continuous experiments improving resolution rates | Experiment log |

---

## What They'll Work On (First 30 Days)

**Week 1:**
- Day 1-2: Get access, meet OPS team (Waqar, Amina), understand current process
- Day 3-5: Ship first automation (even if small — proves they can move)
- End of week: Has mapped current email → triage flow, identified quick wins

**Week 2:**
- Build Email → Linear ticket pipeline (MVP)
- Stand up basic funnel dashboard (even if scrappy)
- Start documenting common issue types

**Week 3-4:**
- Ticket pipeline in production, most emails becoming tickets
- Dashboard showing volume by tier
- First AI auto-response experiment (human-in-the-loop)
- Written plan for months 2-3 that we believe in

**If they can't do this in 30 days, wrong hire.**

---

## Requirements

### Must Have
- 3+ years software engineering experience
- Strong TypeScript — our entire stack is TypeScript
- AWS experience (we run on AWS)
- Uses AI to code (Claude Code, Cursor, Copilot, etc.) — this is how we work
- Experience building automation/pipeline systems
- Comfortable with AI/LLM integration (prompt engineering, API usage)
- Data-driven mindset — measures everything, experiments constantly
- Can ship fast in a startup environment

### Nice to Have
- Experience with support/ticketing systems
- Built knowledge base or FAQ automation before
- Experience with email parsing/processing
- Background in DevOps or internal tooling

### Mindset
- Gets energy from automation — "no human should do this repeatedly"
- Data-obsessed — builds dashboards, tracks metrics, runs experiments
- Pragmatic — ships MVP first, iterates based on data
- Collaborative — works closely with OPS, doesn't build in isolation

---

## Tech Stack (Expected)

- **Email processing:** Gmail API, parsing/extraction
- **Ticketing:** Linear API
- **AI/LLM:** Claude API for classification, response drafting, KB queries
- **Dashboards:** Whatever gets the job done (Retool, Metabase, custom)
- **Runbooks:** Claude Code integration, internal tooling

---

## Reporting & Team

- **Reports to:** Haroun (CTO)
- **Works closely with:** Waqar & Amina (OPS), Maheen (Support Eng), Shaheer (Integrations)
- **Stakeholders:** Samee (CEO) — cares about support scalability

---

## The Funnel Mental Model

This role owns pushing resolutions **earlier** in the funnel:

```
        ┌─────────────────────────────────────┐
        │   All Support Requests (100%)       │
        └─────────────────┬───────────────────┘
                          ▼
        ┌─────────────────────────────────────┐
        │   TIER 0: AI Auto-Resolution        │  ← BUILD THIS
        │   Target: 25-40% of requests        │
        └─────────────────┬───────────────────┘
                          ▼
        ┌─────────────────────────────────────┐
        │   TIER 1: OPS (Waqar/Amina)         │  ← MAKE MORE EFFECTIVE
        │   Target: 40-50% of requests        │
        └─────────────────┬───────────────────┘
                          ▼
              ┌───────────────────────────┐
              │  TIER 2: Support Eng      │  ← REDUCE LOAD
              │  (Maheen, Shaheer)        │
              │  Target: 10-20%           │
              └───────────┬───────────────┘
                          ▼
                  ┌───────────────────┐
                  │ TIER 3: Product   │  ← PROTECT
                  │ Eng               │
                  │ Target: <5%       │
                  └───────────────────┘
```

**Your job:** Make Tier 0 real, make Tier 1 more effective, reduce Tier 2/3 load.

---

## Red Flags (Don't Hire If...)

- Wants to build perfect system before shipping anything
- No experience with AI/LLM — this role requires it
- Doesn't care about metrics — "we'll know if it's working"
- Dismissive of OPS input — "I know what they need"
- Only wants greenfield — can't work with messy existing systems
- Can't ship fast — gets stuck in planning/design

---

## Interview Process

See [interviews/senior-ops-engineer.md](../interviews/senior-ops-engineer.md)

---

## Compensation

*[To be filled based on market data]*

- Level: Senior (L5 equivalent)
- Location: [Remote / Hybrid / On-site]
