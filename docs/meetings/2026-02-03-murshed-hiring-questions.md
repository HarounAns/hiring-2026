# Hiring Questionnaire for Murshed

**Manager:** Haroun  
**Recruiter:** Murshed  
**Date:** February 3, 2026

---

## 1. Can you walk me through the business goals driving these hires?

We're a ~$10M ARR AI company (Pam AI) serving 500+ car dealerships. We're signing 30-40 new dealerships per month, but our problems are on the **activation side, not demand side**.

The core business goals driving these hires:

1. **Improve customer activation** — Customers aren't onboarding fast enough. Delayed activation = delayed revenue and bad first impressions leading to churn.

2. **Fix the eval experience** — Product doesn't "feel good" during the trial period. LLM stability, latency, and reliability issues cause churn and lost deals.

3. **Build customer health visibility** — We're doing reactive firefighting instead of proactive monitoring. We need observability into customer health.

4. **Scale Outbound product** — Our second product ($1M ARR, 40 dealerships) will hit capacity issues in 3-6 months with only 2 engineers.

5. **De-risk fundraising** — We're raising Series A/B. Stability and scalability matter more than features for the investor story.

---

## 2. Of all the open roles, which are the top 1–2 priorities and why?

### Priority 1: PAM Core Support Engineers (x2)
**Why:** These directly unblock onboarding and address LLM quality issues. They handle Tier 2 escalations, ship fixes, and build runbooks so OPS can handle more without escalating. Every repeat escalation is a failure we want to eliminate.

### Priority 2: Senior Operations Engineer (AI-Powered Support Automation)
**Why:** This role builds the infrastructure we need — email-to-ticket pipelines, AI Tier 0 (auto-resolution), observability dashboards. Without this, we can't even measure if other hires are helping. Currently we have no visibility into support volume or escalation rates.

**Note:** Senior Pam Core (LLM Reliability) was our #1 priority, but **already filled** — Yousof Algburi starts February 2026.

---

## 3. For each role, what are the top 3 outcomes you expect in the first 90 days?

### Senior Operations Engineer
1. Email → ticket pipeline working with basic funnel dashboard
2. 90%+ of emails becoming trackable tickets
3. AI handling 10%+ of simple requests (Tier 0)

### PAM Core Support Engineer (x2)
1. Handling Tier 2 escalations independently (no supervision)
2. 10+ fixes shipped to production
3. 20% fewer escalations to Tier 3 (product engineers)

### Integration Support Engineer
1. Understands top 5 integrations (Tekion, CDK, XTime, MyKaarma, etc.)
2. 10+ integration fixes shipped
3. Measurable improvement in integration success rate

### Senior Dashboard Engineer
1. Code in production Day 1, multiple PRs merged Week 1
2. Shipping features independently
3. Agustin's load noticeably reduced, 3+ customer features shipped

### Senior Sales Outbound Engineer
1. Understands codebase, shipping fixes independently
2. Owns product day-to-day (Haroun not involved)
3. Can explain the sales ontology (leads, appointments, handoffs)

### Mid-Level Mobile Engineer
1. Code in production Day 1, 3+ visible UX improvements
2. Assessment doc written (what to improve vs what's working)
3. CI/CD in place, junior engineer shipping better code

---

## 4. What skills are absolute must-haves versus nice-to-haves for each role?

### Senior Operations Engineer
**Must-haves:**
- Automation/pipeline experience
- AI/LLM integration experience
- TypeScript and AWS
- Data-driven mindset

**Nice-to-haves:**
- Support tooling experience (ticketing systems)
- Experience building observability dashboards

### PAM Core Support Engineer
**Must-haves:**
- Strong debugging skills
- TypeScript/AWS
- Customer communication skills
- Ability to push back (protect their time)

**Nice-to-haves:**
- Prompt engineering experience
- Prior support engineering experience

### Integration Support Engineer
**Must-haves:**
- API/webhook debugging experience
- TypeScript/AWS
- Customer communication skills

**Nice-to-haves:**
- DMS integration experience (automotive industry)
- Prior support engineering experience

### Senior Dashboard Engineer
**Must-haves:**
- TypeScript/React/Next.js
- Full-stack capability
- Fast shipping speed
- UX sensibility

**Nice-to-haves:**
- Experience with real-time data/analytics dashboards
- Previous startup experience

### Senior Sales Outbound Engineer
**Must-haves:**
- TypeScript/AWS
- Full-stack capability
- 0→1 product ownership experience
- Ownership mentality

**Nice-to-haves:**
- Prompt engineering experience
- CRM integration experience
- Data modeling/ERD experience

### Mid-Level Mobile Engineer
**Must-haves:**
- React Native
- "Uplevel vs rewrite" mindset (critical — must improve, not rewrite)
- Shipping speed

**Nice-to-haves:**
- Mentorship experience
- Mobile CI/CD experience

---

## 5. Where do you have flexibility on background, tools, or years of experience?

### Flexible on:
- **Industry background** — Automotive experience not required for any role
- **Specific tools** — We care about capability, not specific tool experience (e.g., any modern cloud vs. specifically AWS)
- **Years of experience** — For support roles especially, attitude and debugging ability matter more than years
- **Degree requirements** — None. Bootcamp grads, self-taught engineers welcome.

### Less flexible on:
- **TypeScript** — Our entire stack is TypeScript, so they need to be comfortable with it
- **AI/LLM experience** — For Senior Ops and Senior Sales Outbound roles, need real LLM integration experience (not just "interested in AI")
- **Seniority for senior roles** — Dashboard and Sales Outbound need to be genuinely senior (can own, not just execute)

---

## 6. Are there overlapping skill sets between roles that could allow one strong hire to cover multiple needs?

### Yes, some overlap:
- **PAM Core Support + Integration Support** — Both are support engineers shipping fixes. A strong generalist could potentially cover both, but the skill sets are different (prompt engineering vs. API debugging). We'd lose specialization.

- **Senior Dashboard + Senior Sales Outbound** — Both are full-stack TypeScript/React/AWS roles. A very strong hire could theoretically do both, but Sales Outbound requires 0→1 ownership that's hard to split.

### Recommendation:
Don't try to combine roles. The support roles especially need focus — every time they context-switch, escalation response time suffers. Better to have specialists who own their domain.

---

## 7. Who will these roles work most closely with, and how would you describe the team dynamic today?

| Role | Works Most Closely With |
|------|------------------------|
| Senior Ops Engineer | Waqar (OPS Manager), Maheen (Support Eng), Haroun (CTO) |
| PAM Core Support | Maheen (existing Support Eng), Anujan (Core), OPS team |
| Integration Support | Shaheer (Integrations), Omer (Head of Integrations), OPS team |
| Senior Dashboard | Agustin (Dashboard), Marcelo (Senior Eng), Kareem (PM) |
| Senior Sales Outbound | Laith (FDE), Haroun (CTO), Abdullah (COO/VP Sales) |
| Mid Mobile | Hassan (Junior who built current app), Omer (Head of Integrations) |

**Team dynamic today:**
- Fast-moving, async-heavy, low bureaucracy
- High ownership expected — people own problems, not tasks
- Direct communication with customers is common
- Some tension between features vs. stability priorities (CEO pushes features, CTO pushes stability)
- Support engineers getting pulled into feature work is a current problem

---

## 8. What is the size of the team today? How are they distributed?

**Total:** ~27 people (excluding sales)

| Department | Headcount | Notes |
|------------|-----------|-------|
| **Engineering** | 16 | Distributed across Core, Integrations, Dashboard, Mobile, Outbound, Platform, Sales |
| **Operations** | 7 | Waqar + 6 onshore OPS |
| **Customer Success** | 2 | Zach, Ashley |
| **Product** | 1 | Kareem |

**Engineering breakdown by team:**
- Core: 3 (Anujan, Zain, Raiyan) + Yousof joining Feb
- Integrations: 2 (Omer, Shaheer)
- Dashboard: 2 (Agustin, Marcelo)
- Mobile: 1 (Hassan - junior)
- Outbound: 3 (Uzair, Mevlut, Rehan)
- Platform: 2 (Juzer, Mohammad Meeran)
- Sales/FDE: 1 (Laith)
- Support: 1 (Maheen)

**Distribution:** Team is distributed (not co-located). Mix of US and international.

---

## 9. What traits or behaviors tend to make someone highly successful on your team?

1. **Ownership mentality** — They own problems end-to-end, not just tasks. If something breaks, they fix it; they don't wait to be assigned.

2. **Protect their time** — For support roles especially: every repeat escalation is a failure. They should build runbooks and tooling so issues don't come back.

3. **Ship fast, iterate** — Code in production Day 1 is expected for senior hires. We don't do long planning cycles.

4. **Customer empathy** — Many roles interact with customers directly. Need to balance customer urgency with sustainable solutions.

5. **Systems thinking** — Don't just fix the bug; ask why it happened and prevent the next 10.

6. **Written communication** — We're async-heavy. Need to document decisions, write clear PRs, communicate status in writing.

7. **Comfort with ambiguity** — Especially for 0→1 roles. We often don't have clear specs; need people who can define the problem.

---

## 10. What does the interview process look like for each role, and who are the key decision-makers?

### Standard Process (All Roles)
| Round | Duration | Interviewer | Focus |
|-------|----------|-------------|-------|
| 1. Recruiter Screen | 30 min | Murshed | Culture fit, logistics, salary expectations |
| 2. Hiring Manager Screen | 45 min | Haroun | Role fit, experience deep-dive |
| 3. Technical/Aptitude | 60 min | Yousof Algburi | Role-specific technical assessment |
| 4. Team Fit | 45 min | 1-2 future teammates | Working style, collaboration |
| 5. Final | 30 min | Samee or Haroun | Senior roles only, final alignment |

### Role-Specific Technical Focus
| Role | Technical Assessment Focus |
|------|---------------------------|
| Senior Ops Engineer | Automation design, AI/LLM integration, system architecture |
| Support Engineers | Debugging exercise, customer communication simulation |
| Senior Dashboard | Frontend architecture, code review, UI/UX sensibility |
| Senior Sales Outbound | Full-stack, data modeling, prompt engineering |
| Mid Mobile | React Native, "uplevel vs rewrite" scenario |

### Key Decision-Makers
- **Haroun (CTO):** Final say on all engineering hires
- **Samee (CEO):** Involved in senior role finals
- **Yousof Algburi:** Technical assessment for all roles

**Total rounds:** 4-5 (depending on seniority)  
**Format:** All virtual except final round for senior roles (can be in-person if candidate is local)

---

## 11. Have you made offers for similar roles and what are the most common reasons candidates get rejected later in the process?

### Recent Hire
We just hired Yousof Algburi for Senior Pam Core (LLM Reliability). This was our first senior engineering hire through a structured process.

### Common Rejection Reasons (Based on Similar Roles)

**Technical rejections:**
- Can't debug in real-time — when given a problem, they freeze or need too much hand-holding
- No production experience — great at theory, never operated systems at scale
- Missing systems thinking — fix the immediate bug but don't see the pattern

**Culture/fit rejections:**
- "Tell me what to do" mentality — waiting for specs instead of defining the problem
- Can't communicate clearly in writing — our interviews include written exercises for this reason
- Red flags on ownership — history of blaming others, not taking responsibility

**Process rejections:**
- Salary expectations misaligned (often 30-50% above our range)
- Timeline misaligned (need to start in 3+ months)
- Remote flexibility mismatch

---

## 12. How urgent are these hires, and are there any deadlines or milestones driving timing?

### Urgency Matrix

| Role | Urgency | Deadline/Driver |
|------|---------|-----------------|
| PAM Core Support (x2) | **HIGH** | Maheen is bottlenecked NOW. 3-4 day response times. |
| Senior Ops Engineer | **HIGH** | No observability = can't measure if other hires help |
| Integration Support | **MEDIUM-HIGH** | Shaheer is bottleneck, integrations block onboarding |
| Senior Dashboard | **MEDIUM** | Agustin overloaded but not blocking revenue |
| Senior Sales Outbound | **MEDIUM** | MVP exists, customer demand, but not urgent |
| Mid Mobile | **MEDIUM** | App works, needs polish, not blocking growth |

### Key Milestones
- **Fundraising:** Raising Series A/B. Stability and team scalability matter for investor story.
- **April checkpoint:** 3 months from now — are hires in pipeline? Ramping?
- **Outbound scale:** 3-6 months out, Outbound will hit capacity issues

### Ideal Timeline
- **Support roles:** Offers out within 4-6 weeks
- **Senior Ops:** Offers out within 6-8 weeks
- **Other roles:** Can be more flexible, 8-12 weeks

---

## 13. Are there any constraints I should be aware of upfront (budget, location, clearance, visa, remote policy)?

### Budget
- Competitive with market for the roles
- Specific ranges TBD per role — can discuss after calibrating with candidates
- Prefer not to share ranges upfront in job postings

### Location
- **Remote-friendly** — Team is distributed
- No geographic restrictions within US
- International candidates considered (we have international team members)
- No requirement for office presence

### Clearance/Visa
- No security clearance required
- **Visa sponsorship:** Case-by-case. Prefer candidates who don't require sponsorship, but open to discussing for exceptional candidates.

### Remote Policy
- Fully remote is fine
- Some roles may benefit from occasional in-person (senior roles, team offsites)
- No mandatory office days

### Other Constraints
- **Start date flexibility:** Prefer candidates who can start within 4 weeks of offer, but can accommodate up to 8 weeks for notice periods
- **Contractor vs FTE:** Prefer FTE for all roles. Contractor-to-hire possible for support roles if candidate prefers.

---

## Summary: Priority Order

1. **PAM Core Support Engineer (x2)** — Highest urgency, unblocks Maheen
2. **Senior Operations Engineer** — Enables measurement and automation
3. **Integration Support Engineer** — Unblocks onboarding bottleneck
4. **Senior Dashboard Engineer** — Capacity for customer-facing features
5. **Senior Sales Outbound Engineer** — New revenue line ownership
6. **Mid Mobile Engineer** — App polish (lowest urgency)

---

*Document prepared for recruiting kickoff meeting with Murshed.*
