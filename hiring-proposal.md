# Q1 2026 Hiring Proposal

## The Core Question

**After we hire all of these people, will our problems be solved?**

Let's work backwards from problems → hires, not hires → hope.

---

## Current Problems (Ranked by Impact)

| # | Problem | Impact | Root Cause |
|---|---------|--------|------------|
| 1 | Customers don't onboard fast enough | Delayed revenue, bad first impression | OPS bottleneck + product complexity |
| 2 | Product doesn't "feel good" during eval | Churn, lost deals | LLM stability, latency, reliability |
| 3 | No visibility into customer health | Reactive firefighting | Missing monitoring/alerting |
| 4 | Outbound will hit scale issues in 3-6mo | Future fire | Only 2 engineers (Uzair, Mevlut) |
| 5 | New products undefined | Can't hire strategically | Need product clarity from Samee |

---

## Samee's Proposed Hires vs Problems

| Hire | Solves Which Problem? | Confidence |
|------|----------------------|------------|
| Senior Pam Core | #2 (stability/LLM) | ✅ High - if focused on stability |
| Senior Operations Engineer | #1 (onboarding), #3 (monitoring) | ✅ High - automation + observability |
| PAM Core Support x2 | #1, #2 (Tier 2 for LLM issues) | ✅ High - ships PRs, enables OPS |
| Integration Support | #1 (integrations are main onboarding blocker) | ✅ High - ships PRs, enables OPS |
| Senior Sales Outbound | New revenue line (customer demand exists) | ✅ High - 0→1 product ownership |
| Mid Dashboard | ? | ❓ Unclear - is dashboard blocking growth? |
| Mobile | ? | ❓ Unclear - is mobile a priority? |

### Gaps in Current Plan
- **No Outbound hire** - Problem #4 unaddressed
- **2 hires with unclear problem mapping** (Dashboard, Mobile)

---

## Proposed Hire Breakdown

### ABOVE THE FOLD (Clear problem → hire mapping)

#### 1. Senior Pam Core Engineer
**Problem Solved:** #2 - Product doesn't feel good during eval

| Timeframe | Success Criteria |
|-----------|------------------|
| **3 months** | Reduce P0/P1 incidents by 50%. Establish LLM reliability baseline metrics. |
| **6 months** | Latency p95 < 500ms. Customer-reported "quality" issues down 40%. |
| **1 year** | Zero unplanned outages. LLM reliability is a competitive moat. |

**Interview Focus:** LLM/AI systems experience, reliability engineering, incident response

**Status:** ✅ JD complete, interview guide complete, candidate (Yousof) identified

---

#### 2. Senior Operations Engineer (AI-Powered Support Automation)
**Problem Solved:** #1 - Onboarding bottleneck, #3 - Customer health visibility

This role builds AI-powered automation for the support process:
- Turn emails into tickets automatically (observability)
- Build AI Tier 0 (auto-resolution of simple issues)
- Create AI-enabled runbooks for OPS
- Smart triage and escalation routing
- Funnel metrics and optimization

| Timeframe | Success Criteria |
|-----------|------------------|
| **1 month** | Email → ticket pipeline working. Basic funnel dashboard exists. |
| **3 months** | 90%+ emails become tickets. AI handling 10%+ requests. |
| **6 months** | AI handling 25%+ requests (Tier 0). 30% faster resolution. |
| **1 year** | AI handling 40%+ requests. 2x customers, same support headcount. |

**Interview Focus:** Automation/pipeline experience, AI/LLM integration, data-driven mindset, TypeScript/AWS

**Status:** ✅ JD complete (internal + external)

---

#### 3. PAM Core Support Engineer (x2)
**Problem Solved:** #1 - Onboarding bottleneck, #2 - LLM quality issues (Tier 2 support)

Support engineers focused on LLM behavior and conversation quality. They debug why Pam said the wrong thing, ship PRs to fix it, improve prompts, and build runbooks so OPS can handle more without escalating.

**Key mindset:** Protect their time — every repeat escalation is a failure.

| Timeframe | Success Criteria |
|-----------|------------------|
| **1 month** | Handling escalations with supervision. First PR shipped. First runbook created. |
| **3 months** | Handling Tier 2 independently. 10+ fixes shipped. 20% fewer escalations to Tier 3. |
| **6 months** | 80%+ resolved without Tier 3. OPS handling issues they used to escalate. |
| **1 year** | 2x customers, same Tier 2 headcount. All common issues have runbooks. |

**Interview Focus:** Debugging skills, TypeScript/AWS, customer communication, prompt engineering aptitude, pushback ability

**Status:** ✅ JD complete (internal + external)

---

#### 4. Integration Support Engineer
**Problem Solved:** #1 - Onboarding bottleneck (integrations are the main stopper)

Support engineer focused on DMS integrations (Tekion, CDK, XTime, MyKaarma). They debug API failures, fix data sync issues, ship PRs, and build runbooks so OPS can handle more without escalating.

**Key difference from PAM Core:** No prompt engineering. This is API/webhook debugging.

| Timeframe | Success Criteria |
|-----------|------------------|
| **1 month** | Understands top 5 integrations. First PR shipped. First runbook created. |
| **3 months** | Handling Tier 2 independently. 10+ fixes shipped. Integration success rate improved. |
| **6 months** | 80%+ resolved without Omer's team. Integration reliability measurably improved. |
| **1 year** | Integration success rate > 95%. Integrations not a blocker for deals. |

**Interview Focus:** API debugging, TypeScript/AWS, customer communication, integration experience, pushback ability

**Status:** ✅ JD complete (internal + external)

---

#### 5. Senior Dashboard Engineer
**Problem Solved:** Agustin is overloaded. Customer demand for dashboard enhancements exceeds capacity.

Full-stack engineer focused on Pam's customer-facing dashboard. Builds features like takeover texting, conversation management, analytics — touches Pam Core systems but doesn't change LLM behavior.

**What they do:**
- Ship dashboard features (conversations, analytics, settings)
- Full-stack: React/Next.js frontend, TypeScript APIs, AWS
- Work across teams when features touch backend systems
- Ship fast — code in production Day 1

| Timeframe | Success Criteria |
|-----------|------------------|
| **1 month** | Code in production Day 1, multiple PRs merged Week 1, understands architecture |
| **3 months** | Shipping features independently, Agustin's load reduced, 3+ customer features shipped |
| **6 months** | Owning major initiatives, dashboard quality improved, features helping close deals |
| **1 year** | 2x feature velocity, dashboard is competitive advantage, may be mentoring junior engineers |

**Interview Focus:** TypeScript/React/Next.js, full-stack capability, shipping speed, UX sensibility

**Status:** ✅ JD complete (internal + external)

---

#### 6. Senior Sales Outbound Engineer
**Problem Solved:** New revenue line — existing Service Outbound customers want Sales

Take over Pam Outbound Sales MVP from Haroun and own it end-to-end. 0→1 product engineering role.

**What they inherit:** Working MVP, reasonable codebase, scrappy docs, clear PRD

**What they do:**
- Productionize: reliability, observability, scalability, maintainability
- Own the Sales ontology (leads, appointments, handoffs) within Outbound Orchestration
- Prompt engineering for sales conversations
- Full-stack: dashboard, analytics, CRM integrations, multi-channel (SMS → email → phone)

| Timeframe | Success Criteria |
|-----------|------------------|
| **1 month** | Understands codebase, shipping fixes independently, can explain the ontology |
| **3 months** | Owns product day-to-day (Haroun not involved), Phase 2 (email) in progress |
| **6 months** | 10+ customers live, outbound phone calling launched, closed-loop reporting working |
| **1 year** | Sales Outbound is meaningful revenue line, 50+ customers |

**Interview Focus:** TypeScript/AWS, prompt engineering, data modeling (ERDs), full-stack, 0→1 experience, ownership mentality

**Status:** ✅ JD complete (internal + external)

---

#### 7. Mid-Level Mobile Engineer
**Problem Solved:** Uplevel existing mobile app built by junior engineer. App works but needs polish and professionalization.

Mobile engineer to improve existing app (built with Rork by junior), establish best practices, and mentor the junior engineer.

**Current state:** Working app in store, skinny layer on Pam Core backend, functional but needs UX polish

**What they do:**
- Uplevel app quality and UX
- Establish mobile best practices (CI/CD, testing)
- Mentor junior engineer who built it
- Ship improvements Day 1 — NOT rewrite

| Timeframe | Success Criteria |
|-----------|------------------|
| **1 month** | Code in production Day 1, 3+ visible improvements, assessment doc written |
| **3 months** | Noticeably improved UX, CI/CD in place, junior shipping better code |
| **6 months** | Improved app store ratings, solid architecture, junior independent |
| **1 year** | Competitive quality app, foundation for future mobile initiatives |

**Interview Focus:** React Native, uplevel-vs-rewrite mindset (critical), mentorship, shipping speed

**Status:** ✅ JD complete (internal + external)

---

## Missing Hires (My Recommendations)

### Outbound Engineer (Mid or Senior)
**Problem Solved:** #4 - Outbound scale in 3-6 months

| Timeframe | Success Criteria |
|-----------|------------------|
| **3 months** | Ramped on Outbound codebase. Shipping features alongside Uzair/Mevlut. |
| **6 months** | Outbound handles 2x current volume with no degradation. |
| **1 year** | Outbound team is self-sufficient (3 engineers). |

**Why:** Outbound is $1M ARR, 40 dealers, growing fast. Only 2 engineers. This is predictable pain.

---

### Onboarding Specialist (OPS, not ENG)
**Problem Solved:** #1 - Onboarding bottleneck

| Timeframe | Success Criteria |
|-----------|------------------|
| **3 months** | Onboarding time reduced 30%. Defined playbook for all customer types. |
| **6 months** | Can onboard 50+ dealers/month without eng support. |
| **1 year** | Onboarding is a competitive advantage. |

**Why:** The onboarding problem is more OPS than ENG. Waqar's team may need reinforcement.

---

## Summary: Hire Confidence Matrix

| Hire | Problem | Confidence | Status |
|------|---------|------------|--------|
| Senior Pam Core | Stability/LLM | ✅ High | ✅ JD + Interview ready |
| Senior Operations Engineer | Observability/Automation | ✅ High | ✅ JD ready |
| PAM Core Support x2 | LLM issues (Tier 2) | ✅ High | ✅ JD ready |
| Integration Support | Integrations (Tier 2) | ✅ High | ✅ JD ready |
| Senior Sales Outbound | New revenue (0→1 product) | ✅ High | ✅ JD ready |
| Senior Dashboard | Capacity (Agustin overloaded) | ✅ High | ✅ JD ready |
| Mid Mobile | Uplevel existing app | ✅ High | ✅ JD ready |

---

## Interview Process (Draft)

### All Roles
1. **Recruiter Screen** (30 min) - Culture fit, logistics, salary expectations
2. **Hiring Manager Screen** (45 min) - Role fit, experience deep-dive
3. **Technical/Aptitude** (60 min) - Yousuf Algaburi for technical roles
4. **Team Fit** (45 min) - Work with 1-2 future teammates
5. **Final** (30 min) - Samee or Haroun for senior roles

### Role-Specific Technical
| Role | Technical Focus |
|------|-----------------|
| Senior Core | System design, LLM reliability, debugging production issues |
| Support Engineers | Debugging exercise, customer communication simulation |
| Dashboard/Mobile | Frontend architecture, code review, UI/UX sensibility |
| Outbound | Full-stack, scaling systems, async processing |

---

## Open Questions for Samee

1. ~~**Integration hire** - What problem does this solve? Are integrations blocking onboarding?~~ ✅ Resolved — Shaheer is bottleneck, integrations block onboarding
2. ~~**Dashboard hire** - Is dashboard part of the bad eval experience? What would they build Q1?~~ ✅ Resolved — Agustin overloaded, customer demand for enhancements
3. ~~**Mobile hire** - What's the mobile priority? Why Q1 vs Q2?~~ ✅ Resolved — Uplevel existing app built by junior with Rork
4. ~~**Sales product** - What is it? Can we hold this hire until it's defined?~~ ✅ Resolved — Pam Outbound Sales, MVP exists, customer demand
5. **Outbound** - Why no hire when we expect scale issues in 3-6 months?
6. **OPS** - Should Waqar get an onboarding specialist to unblock the 30-40/month?

---

## Next Steps

- [ ] Align with Samee on problem → hire mapping
- [ ] Finalize which hires proceed vs hold vs add
- [ ] Write JDs by Wednesday
- [ ] Schedule Yousuf for technical interviews
- [ ] Define interview rubrics for each role
