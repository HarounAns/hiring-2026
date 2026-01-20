# PAM Core Support Engineer (x2)

## Problem This Role Solves

**Problem:** Maheen is the only Tier 2 support for PAM Core issues, and she's split between support and feature work. Support is losing.

**Root Cause:** No dedicated support engineering capacity for LLM/conversation issues. When customers report Pam behaving badly, there's a single point of failure.

**Current state:**
- PAM Core issues escalate from OPS → Maheen → Anujan (Tier 3)
- Maheen has 3-4 day response delays because she's doing feature work
- No one is systematically improving prompts based on support patterns
- OPS can't handle LLM issues — they always escalate

**Why now:**
- We anticipate significant growth — Maheen can't scale
- LLM reliability is Problem #2 (product doesn't feel good during eval)
- Need dedicated capacity that isn't pulled into feature work

---

## Role Summary

This is a **support engineering** role focused on LLM behavior and conversation quality. You'll debug why Pam said the wrong thing, fix it (prompts or code), and build systems so OPS can handle more issues without escalating to you.

**Critical mindset:** Your time is valuable. Every issue that hits your queue should either (a) get fixed permanently, or (b) result in a runbook/tool so OPS handles it next time.

---

## Responsibilities

### 1. Tier 2 Support for PAM Core Issues
- Receive escalations from OPS for LLM/conversation issues
- Analyze call transcripts to identify where Pam went wrong
- Determine root cause: model issue, context issue, prompt issue, or config issue
- Fix the issue — ship PRs for code bugs, update prompts for behavior issues

### 2. Prompt Engineering & LLM Debugging
- Debug why Pam said X when it should have said Y
- Improve prompts to reduce hallucinations, failed intents, bad responses
- Build understanding of prompt structure and how to tune behavior
- Document patterns: "When you see X, it's usually Y"

### 3. Protect Your Time — Enable OPS
- Build runbooks for common issues so OPS can fix them without escalating
- Create tools/scripts that let OPS diagnose and resolve issues themselves
- When OPS escalates something they should have handled, push back and train them
- Track what's being escalated and why — identify patterns to eliminate

### 4. Build Runbooks & Automation
- Create AI-enabled runbooks for your own workflow
- Document debugging steps so future you (or teammates) can move faster
- Automate repetitive diagnostic steps
- Contribute to knowledge base used by OPS and Tier 0 AI

### 5. Ship Fixes
- Open PRs for bugs you find — don't just escalate to Tier 3
- Work with Anujan and Senior Pam Core engineer on complex issues
- Own fixes end-to-end: identify, fix, test, deploy, verify

---

## Success Criteria

### Month 1
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Ramp | Handling escalations with supervision | Manager assessment |
| Shadowing | Completed shadowing with Maheen | Checklist |
| First fix | Shipped at least one PR for a support issue | PR merged |
| Runbook | Created first runbook for OPS | Runbook exists, OPS using it |

### Month 3
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Escalation handling | Handling Tier 2 independently | Ticket review |
| PRs shipped | 10+ support-related fixes | PR count |
| OPS enablement | 3+ runbooks in use by OPS | OPS feedback |
| Escalation reduction | 20% fewer escalations to Tier 3 | Ticket metrics |

### Month 6
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Resolution rate | 80%+ of escalations resolved without Tier 3 | Ticket metrics |
| OPS capability | OPS handling issues they used to escalate | Escalation patterns |
| Prompt improvements | Measurable reduction in repeat issue types | Support data |
| Time protected | Clear escalation criteria enforced with OPS | Qualitative |

### 1 Year
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Support scalability | 2x customers, same Tier 2 headcount | Volume vs resolution |
| Runbook coverage | All common issues documented | Audit |
| Tier 3 protection | Tier 3 only sees truly novel issues | Escalation analysis |

---

## Requirements

### Must Have
- 1-3 years software engineering experience
- Strong TypeScript — our entire stack is TypeScript
- AWS experience (we run on AWS)
- Uses AI to code (Claude Code, Cursor, Copilot, etc.) — this is how we work
- Strong debugging skills — can read logs, trace issues, find root cause
- Can ship PRs — not just diagnose, but fix
- Excellent written communication — customer-facing responses
- Customer empathy — genuinely wants to help, but also protects their time

### Nice to Have
- Experience with LLMs/prompt engineering
- Experience with voice/telephony systems
- SQL for querying customer data
- Built runbooks or internal tooling before

### Mindset
- **Protective of their time** — every repeat escalation is a failure
- **Fix it permanently** — hates seeing the same issue twice
- **Pushes back on OPS** — holds the line on escalation criteria
- **Documents everything** — future self and teammates will thank you
- **Ships fast** — working fix > perfect fix

---

## What They'll Work On (First 30 Days)

**Week 1:**
- Day 1-2: Get access, meet Maheen, understand product and support flow
- Day 3-5: Shadow Maheen on live escalations, understand common issues
- End of week: Can explain the escalation path and top 5 issue types

**Week 2:**
- Handle first escalations with supervision
- Ship first fix (even if small)
- Start documenting patterns you see

**Week 3-4:**
- Handle escalations independently
- Create first runbook for OPS (pick the most common issue)
- Push back on at least one bad escalation from OPS
- Written list of "things OPS should handle but don't"

---

## Reporting & Team

- **Reports to:** Haroun (CTO) initially, may move under Maheen or Senior Core hire
- **Works with:** Maheen (peer/mentor), OPS team (Waqar, Amina), Anujan (Tier 3)
- **Escalates to:** Anujan for truly complex issues, Senior Pam Core for reliability patterns

---

## The Funnel Mental Model

Your job is to **push resolutions earlier** in the funnel:

```
OPS (Tier 1) → YOU (Tier 2) → Anujan (Tier 3)
```

**Goal:** More issues resolved at Tier 1 (via your runbooks), fewer escalations to Tier 3.

**How you protect your time:**
1. Fix issues permanently (no repeats)
2. Build runbooks so OPS can handle it next time
3. Push back when OPS escalates something they should handle
4. Track patterns and eliminate root causes

---

## Red Flags (Don't Hire If...)

- Sees support as "beneath" engineering — this IS engineering
- Can't explain their debugging process
- No customer empathy (blames users)
- Won't push back — just accepts every escalation
- Wants to skip to "real engineering" — support is real engineering
- Can't ship PRs — only diagnoses, doesn't fix

---

## Interview Process

See [interviews/pam-core-support-engineer.md](../interviews/pam-core-support-engineer.md)

---

## Compensation

*[To be filled based on market data]*

- Level: Support Engineer (L3-L4 equivalent)
- Location: [Remote / Hybrid / On-site]
