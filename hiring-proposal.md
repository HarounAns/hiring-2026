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
| Pam Core Support x2 | #1 (onboarding) partially, #3 (monitoring) | 🟡 Medium - juniors are slow to ramp |
| Integration Support | ? | ❓ Unclear - what problem? |
| Mid Dashboard | ? | ❓ Unclear - is dashboard blocking growth? |
| Mobile | ? | ❓ Unclear - is mobile a priority? |
| Senior Sales (New Product) | #5 | ❌ Low - product undefined |

### Gaps in Current Plan
- **No Outbound hire** - Problem #4 unaddressed
- **No Observability focus** - Problem #3 partially addressed by support hires
- **3 hires with unclear problem mapping** (Integration, Dashboard, Mobile)

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

---

#### 2. Pam Core Support x2 (Juniors)
**Problem Solved:** #1 - Onboarding bottleneck, #3 - Customer health visibility

| Timeframe | Success Criteria |
|-----------|------------------|
| **3 months** | Ramped on product. Handling tier-1 support independently. Onboarding time reduced 20%. |
| **6 months** | Built dashboards for key customer health metrics. Proactive alerting in place. |
| **1 year** | Onboarding is self-serve for 50% of customers. Support ticket volume down 30%. |

**Interview Focus:** Customer empathy, debugging skills, communication, ability to learn fast

**Risk:** Juniors take 3-6 months to ramp. Consider 1 mid-level instead of 2 juniors for faster impact.

---

#### 3. Integration Support (Junior)
**Problem Solved:** ❓ NEEDS CLARIFICATION

**Questions for Samee:**
- What problem does this solve?
- Are integrations blocking customer onboarding?
- Is this a support role or an engineering role?

| If integrations are blocking onboarding... | Success Criteria |
|-------------------------------------------|------------------|
| **3 months** | Top 5 integration issues documented and resolved. |
| **6 months** | Integration success rate > 95%. Self-serve integration docs. |
| **1 year** | Integrations are not a blocker for any deal. |

---

### BELOW THE FOLD (Unclear problem mapping)

#### 4. Mid-Level Dashboard Engineer
**Problem Solved:** ❓ NEEDS CLARIFICATION

**Questions for Samee:**
- Is the dashboard causing churn or blocking deals?
- What would this person build in Q1?
- Is this about the eval experience (Problem #2)?

| If dashboard is part of bad eval experience... | Success Criteria |
|-----------------------------------------------|------------------|
| **3 months** | Shipped 3 high-impact UX improvements based on customer feedback. |
| **6 months** | Dashboard NPS improved. Time-to-value metrics visible to customers. |
| **1 year** | Dashboard is a selling point, not a detractor. |

---

#### 5. Mid-Level Mobile Engineer
**Problem Solved:** ❓ NEEDS CLARIFICATION

**Questions for Samee:**
- Is mobile driving revenue or strategic priority?
- What's the Q1 mobile roadmap?
- Why now vs Q2?

---

#### 6. Senior Sales Engineer (New Product)
**Problem Solved:** #5 - New products undefined

**Recommendation:** HOLD until product is defined

**Questions for Samee:**
- What is the Sales product? Outbound for sales teams? CRM integration?
- Do we have a spec, even rough?
- Can we wait until Q2 when there's clarity?

**Risk:** Hiring senior talent for undefined product leads to churn or misalignment.

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

| Hire | Problem | Confidence | Action |
|------|---------|------------|--------|
| Senior Pam Core | Stability/LLM | ✅ High | Proceed |
| Core Support x2 | Onboarding/Monitoring | 🟡 Medium | Proceed (consider 1 mid vs 2 junior) |
| Integration Support | ❓ | ❓ Low | Clarify with Samee |
| Mid Dashboard | ❓ | ❓ Low | Clarify with Samee |
| Mid Mobile | ❓ | ❓ Low | Clarify with Samee |
| Senior Sales | New product | ❌ Low | Hold until product defined |
| **Outbound Engineer** | Scale | ✅ High | **ADD** |
| **Onboarding Specialist** | Throughput | ✅ High | **ADD (OPS)** |

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

1. **Integration hire** - What problem does this solve? Are integrations blocking onboarding?
2. **Dashboard hire** - Is dashboard part of the bad eval experience? What would they build Q1?
3. **Mobile hire** - What's the mobile priority? Why Q1 vs Q2?
4. **Sales product** - What is it? Can we hold this hire until it's defined?
5. **Outbound** - Why no hire when we expect scale issues in 3-6 months?
6. **OPS** - Should Waqar get an onboarding specialist to unblock the 30-40/month?

---

## Next Steps

- [ ] Align with Samee on problem → hire mapping
- [ ] Finalize which hires proceed vs hold vs add
- [ ] Write JDs by Wednesday
- [ ] Schedule Yousuf for technical interviews
- [ ] Define interview rubrics for each role
