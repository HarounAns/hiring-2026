# Integration Support Engineer

## Problem This Role Solves

**Problem:** Shaheer is the only Tier 2 support for integration/scheduler issues. Integration setup is the main onboarding bottleneck.

**Root Cause:** No dedicated support engineering capacity for DMS integrations. When integrations fail or stall, there's a single point of failure.

**Current state:**
- Integration issues escalate from OPS → Shaheer → Omer
- Third-party delays (CDK: 2-3 weeks, XTime: 24hrs, MyKaarma: 24-48hrs) frustrate customers
- Customers say: "Signed contract 3 weeks ago, still not live"
- OPS can't debug API failures — they always escalate
- No systematic improvement of integration reliability

**Why now:**
- Integration delays are the #1 onboarding bottleneck
- We anticipate significant growth — Shaheer can't scale
- Need dedicated capacity to debug, fix, and prevent integration issues

---

## Role Summary

This is a **support engineering** role focused on DMS integrations and data sync. You'll debug why an integration failed, fix it (code or config), and build systems so OPS can handle more issues without escalating to you.

**Critical mindset:** Your time is valuable. Every issue that hits your queue should either (a) get fixed permanently, or (b) result in a runbook/tool so OPS handles it next time.

**Note:** This role does NOT involve prompt engineering or LLM work. That's PAM Core Support.

---

## Responsibilities

### 1. Tier 2 Support for Integration Issues
- Receive escalations from OPS for DMS/scheduler issues
- Debug API failures — read request/response logs, trace data flow
- Diagnose configuration issues — audit settings in DynamoDB, review S3 data, identify misconfigurations
- Distinguish custom work from integration limitations — know what's possible in Tekion vs CDK vs XTime, etc.
- Work with third-party provider docs (Tekion, CDK, XTime, MyKaarma)
- Fix the issue — ship PRs for code bugs, update configs, coordinate with providers

### 2. Integration Debugging & Data Sync
- Debug why data didn't sync between Pam and the DMS
- Trace webhook flows and API calls
- Use AWS tools (DynamoDB, S3) to investigate configuration and data issues
- Identify if it's our bug, provider bug, config issue, or limitation of the integration
- Document patterns: "When you see X error from Tekion, it means Y"
- Build knowledge of what each integration can and can't do

### 3. Protect Your Time — Enable OPS
- Build runbooks for common integration issues so OPS can fix them
- Create tools/scripts that let OPS diagnose and resolve issues themselves
- When OPS escalates something they should have handled, push back and train them
- Track what's being escalated and why — identify patterns to eliminate

### 4. Build Runbooks & Automation
- Create AI-enabled runbooks for your own workflow
- Document debugging steps for each integration partner
- Automate repetitive diagnostic steps
- Contribute to knowledge base used by OPS and Tier 0 AI

### 5. Ship Fixes
- Open PRs for integration bugs you find
- Work with Omer's team on complex integration issues
- Own fixes end-to-end: identify, fix, test, deploy, verify
- Improve integration reliability over time

---

## Success Criteria

### Month 1
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Ramp | Understands top 5 integrations (Tekion, CDK, XTime, MyKaarma, Dealer-FX) | Assessment |
| Shadowing | Completed shadowing with Shaheer | Checklist |
| First fix | Shipped at least one PR for an integration issue | PR merged |
| Runbook | Created first runbook for OPS | Runbook exists, OPS using it |

### Month 3
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Escalation handling | Handling Tier 2 integration issues independently | Ticket review |
| PRs shipped | 10+ integration-related fixes | PR count |
| OPS enablement | 3+ runbooks in use by OPS | OPS feedback |
| Integration success rate | Improved from baseline | Onboarding metrics |

### Month 6
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Resolution rate | 80%+ of escalations resolved without Omer's team | Ticket metrics |
| OPS capability | OPS handling issues they used to escalate | Escalation patterns |
| Integration reliability | Fewer repeat failures per integration type | Support data |
| Time protected | Clear escalation criteria enforced with OPS | Qualitative |

### 1 Year
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Integration success rate | > 95% | Onboarding funnel |
| Self-serve docs | Customers can troubleshoot common issues | Doc coverage |
| Support scalability | 2x customers, same Tier 2 headcount | Volume vs resolution |
| Integration not a blocker | Integrations rarely cited in deal losses | Win/loss analysis |

---

## Requirements

### Must Have
- 1-3 years software engineering experience
- Strong TypeScript — our entire stack is TypeScript
- AWS experience (we run on AWS)
- Uses AI to code (Claude Code, Cursor, Copilot, etc.) — this is how we work
- Experience with APIs and integrations — can read API docs, debug requests/responses
- Strong debugging skills — can trace data flow, read logs, find root cause
- Can ship PRs — not just diagnose, but fix
- Excellent written communication — customer-facing responses

### Nice to Have
- Experience with CRM/DMS systems
- Experience with webhook architectures
- SQL for querying customer data
- Built runbooks or internal tooling before
- Worked with third-party API providers

### Mindset
- **Protective of their time** — every repeat escalation is a failure
- **Fix it permanently** — hates seeing the same issue twice
- **Pushes back on OPS** — holds the line on escalation criteria
- **Documents everything** — future self and teammates will thank you
- **Patient with third parties** — can navigate provider delays professionally

---

## What They'll Work On (First 30 Days)

**Week 1:**
- Day 1-2: Get access, meet Shaheer, understand product and integration landscape
- Day 3-5: Shadow Shaheer on live escalations, learn the top 5 integrations
- End of week: Can explain each integration's data flow and common failure modes

**Week 2:**
- Handle first escalations with supervision
- Ship first fix (even if small)
- Start documenting patterns you see

**Week 3-4:**
- Handle escalations independently
- Create first runbook for OPS (pick the most common integration issue)
- Push back on at least one bad escalation from OPS
- Written list of "things OPS should handle but don't"

---

## Reporting & Team

- **Reports to:** Omer (Head of Integrations)
- **Works with:** Shaheer (peer/mentor), OPS team (Waqar, Amina), Omer's team (Tier 3)
- **Coordinates with:** Third-party providers (Tekion, CDK, XTime, MyKaarma)

---

## The Funnel Mental Model

Your job is to **push resolutions earlier** in the funnel:

```
OPS (Tier 1) → YOU (Tier 2) → Omer's Team (Tier 3)
```

**Goal:** More issues resolved at Tier 1 (via your runbooks), fewer escalations to Omer.

**How you protect your time:**
1. Fix issues permanently (no repeats)
2. Build runbooks so OPS can handle it next time
3. Push back when OPS escalates something they should handle
4. Track patterns and eliminate root causes

---

## Integration Landscape

| Provider | Common Issues | Your Role |
|----------|---------------|-----------|
| **Tekion** | API auth, data sync delays | Debug, fix, document |
| **CDK** | Long setup (2-3 weeks), config issues | Coordinate, troubleshoot |
| **XTime** | 24hr delays post-invite, webhook failures | Debug, build workarounds |
| **MyKaarma** | 24-48hr delays, data format issues | Debug, document patterns |
| **Dealer-FX** | Various integration issues | Debug, fix, escalate |

---

## Red Flags (Don't Hire If...)

- Sees support as "beneath" engineering — this IS engineering
- Can't explain their debugging process
- Gets frustrated with third-party delays — patience is required
- Won't push back — just accepts every escalation
- Wants to do LLM/prompt work — this role is integrations, not AI
- Can't ship PRs — only diagnoses, doesn't fix

---

## Interview Process

See [interviews/integration-support-engineer.md](../interviews/integration-support-engineer.md)

---

## Compensation

*[To be filled based on market data]*

- Level: Support Engineer (L3-L4 equivalent)
- Location: [Remote / Hybrid / On-site]
