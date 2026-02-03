# Recruiter Kickoff: Murshed

**Manager:** Haroun  
**Recruiter:** Murshed  
**Date:** February 3, 2026

---

## 1. Can you walk me through the business goals driving these hires?

We're at ~$10M ARR with 500+ dealerships on our flagship product (Pam Inbound) and ~$1M ARR with 40 dealerships on Outbound. We're signing 30-40 new dealerships per month, but we have two major problems:

1. **Onboarding bottleneck** — Customers aren't getting activated fast enough. This delays revenue and creates bad first impressions.
2. **Product quality during evaluation** — The product doesn't "feel good" during eval due to LLM stability, latency, and reliability issues. This causes churn.

We're also raising a Series A/B, so stability is critical — one bad outage during investor diligence could tank the round.

**Additionally: Scaling the Outbound product**

Outbound is our second product line (~$1M ARR, 40 dealerships, growing fast). Within Outbound, we have an emerging **Sales Outbound** product — an MVP that I (Haroun) built and currently own. Existing Service Outbound customers are asking for Sales capabilities. There's real customer demand.

The problem: I can't run this product AND be CTO. Sales Outbound needs a dedicated engineer who can:
- Take full ownership of the product (not just execute tickets)
- Productionize the MVP (reliability, observability, scalability)
- Own the sales ontology (leads, appointments, handoffs)
- Ship multi-channel capabilities (SMS → email → phone)
- Interface with customers directly

This is a 0→1 product engineering role. Without a dedicated owner, Sales Outbound stalls — and we leave revenue on the table.

**Bottom line:** These hires are about unblocking growth by fixing onboarding, improving product quality, and scaling emerging products that have proven demand.

---

## 2. Of all the open roles, which are the top 1–2 priorities and why?

**Top 2 Priorities:**

1. **PAM Core Support Engineers (x2)** — Unblocks onboarding. These are Tier 2 support engineers who debug LLM behavior issues, ship PRs to fix them, and build runbooks so OPS can handle more without escalating. Our current support engineer (Maheen) is stretched thin and getting pulled into feature work.

2. **Senior Operations Engineer** — Builds AI-powered automation for the support process: email-to-ticket pipelines, AI Tier 0 (auto-resolution), smart triage and escalation. This creates observability and scalability in our support process.

**Why these two:** Every other problem stems from not being able to onboard and support customers at scale. These hires directly attack that bottleneck.

---

## 3. For each role, what are the top 3 outcomes you expect in the first 90 days?

### PAM Core Support Engineer (x2)
1. Handling Tier 2 escalations independently without supervision
2. 10+ fixes/PRs shipped to address recurring LLM behavior issues
3. 20% reduction in escalations to Tier 3 (product engineers)

### Senior Operations Engineer
1. Email-to-ticket pipeline working (Gmail → Linear)
2. Basic funnel dashboard showing support volume and escalation rates
3. 90%+ of emails becoming trackable tickets with categorization

### Integration Support Engineer
1. Understands top 5 integrations (Tekion, CDK, XTime, MyKaarma, DealerSocket)
2. First PR shipped addressing a recurring integration issue
3. First runbook created so OPS can handle common integration issues without escalating

### Senior Dashboard Engineer
1. Code in production Day 1, multiple PRs merged Week 1
2. Understands full dashboard architecture
3. Shipping features independently, reducing Agustin's load

### Senior Sales Outbound Engineer
1. **Haroun is out** — Fully owns product decisions. Doesn't ask permission, doesn't need oversight. Haroun learns about progress from demos, not standups.
2. **Customers live** — First paying customers on Sales Outbound (not just MVP pilots). Revenue attributable to their work.
3. **Phase 2 in progress** — Email channel scoped, designed, or in development. Roadmap owned, not inherited.

### Mid-Level Mobile Engineer
1. Code in production Day 1, 3+ visible UX improvements shipped
2. Assessment doc written identifying technical debt and improvement areas
3. Initial rapport and working relationship with junior engineer (Hassan)

---

## 4. What skills are absolute must-haves versus nice-to-haves for each role?

### PAM Core Support Engineer
**Must-haves:**
- TypeScript proficiency
- Debugging skills (can read logs, trace issues, reproduce problems)
- Customer communication ability (clear, professional, empathetic)
- Ability to push back and protect their time

**Nice-to-haves:**
- Prompt engineering experience
- AWS experience
- Previous support engineering background

### Senior Operations Engineer
**Must-haves:**
- Automation/pipeline experience
- TypeScript proficiency
- Data-driven mindset
- AI/LLM integration experience

**Nice-to-haves:**
- AWS experience
- HubSpot/Linear integration experience
- Previous DevOps or platform engineering background

### Integration Support Engineer
**Must-haves:**
- API debugging skills (webhooks, REST APIs)
- TypeScript proficiency
- Customer communication ability
- Ability to push back

**Nice-to-haves:**
- DMS/automotive software experience
- Previous integration engineering background
- AWS experience

### Senior Dashboard Engineer
**Must-haves:**
- TypeScript + React/Next.js proficiency
- Full-stack capability (frontend + backend)
- Fast shipping speed (code in production Day 1)
- UX sensibility

**Nice-to-haves:**
- AWS experience
- Previous B2B SaaS dashboard experience

### Senior Sales Outbound Engineer
**Must-haves:**
- **Ownership mentality** — Has run a product or feature end-to-end. Made decisions, not just executed them. Can point to something and say "I built that, I owned it, here's what happened."
- **Talks to customers** — Comfortable getting on calls, understanding pain, translating to product. Not hiding behind a PM.
- **Ships fast** — Bias to action. Would rather ship something imperfect than wait for perfect requirements.
- **TypeScript + AWS proficiency** — Our stack. Non-negotiable.
- **Prompt engineering experience** — This is an LLM product. They need to understand how to make AI behave.

**Nice-to-haves:**
- Previous 0→1 experience (built something from scratch that became real)
- CRM integration experience
- Multi-channel messaging experience (SMS, email, phone)
- Sales domain knowledge

**Red flags for this role:**
- "I need a PM to tell me what to build"
- "I've never talked to customers directly"
- Wants to rewrite everything before shipping
- Can't articulate a product opinion

### Mid-Level Mobile Engineer
**Must-haves:**
- React Native proficiency
- "Uplevel vs. rewrite" mindset — must improve, not rebuild
- Mentorship ability (will work with junior engineer)
- Fast shipping speed

**Nice-to-haves:**
- Previous experience improving legacy mobile apps
- CI/CD experience for mobile
- iOS/Android native experience

---

## 5. Where do you have flexibility on background, tools, or years of experience?

**High flexibility:**
- **Industry background** — Don't need automotive/dealership experience. Any B2B SaaS or startup experience translates.
- **Specific tools** — AWS, HubSpot, Linear are all learnable. Strong fundamentals matter more.
- **Years of experience** — Title says "Senior" but what matters is production maturity and ownership mentality. A strong 3-year engineer who ships > 7-year engineer who talks.

**Low flexibility:**
- **TypeScript** — Non-negotiable. Our entire stack is TypeScript.
- **Debugging ability** — For support roles, this is the core job. Can't compromise.
- **Shipping speed** — Everyone ships code Week 1. Can't have slow ramp-up.
- **Prompt engineering** — For PAM Core and Sales Outbound roles, LLM experience is important.

---

## 6. Are there overlapping skill sets between roles that could allow one strong hire to cover multiple needs?

**Potential overlap:**
- **PAM Core Support + Integration Support** — Similar debugging skills, customer communication, TypeScript. A very strong hire could potentially flex across both, though the debugging domain is different (LLM behavior vs. API/webhooks).
- **Senior Dashboard + Senior Sales Outbound** — Both are full-stack TypeScript roles. Dashboard is more frontend-heavy, Sales Outbound is more 0→1 product. Less likely to combine.

**Roles that should stay separate:**
- **Senior Operations Engineer** — Very different skill set (automation, pipelines, observability). Don't combine with anything else.
- **Mid Mobile Engineer** — React Native specialist. Don't combine with web roles.

**Recommendation:** Start with dedicated hires for each. If we find a unicorn who can flex, great — but don't hire expecting flexibility.

---

## 7. Who will these roles work most closely with, and how would you describe the team dynamic today?

| Role | Works Most Closely With | Team Dynamic |
|------|------------------------|--------------|
| PAM Core Support (x2) | Maheen (current Support Eng), OPS team (Waqar, Amina), Anujan (Core) | Collaborative but stretched thin. Maheen is pulled between support and features. |
| Senior Ops Engineer | Waqar (OPS Manager), Amina (OPS), Maheen, Engineering | OPS team is capable but lacks tooling and observability. Need someone to build the automation layer. |
| Integration Support | Shaheer (Integration Eng), Omer (Head of Integrations), OPS team | Shaheer is sole integration support. Omer gets pulled in too often — that's a red flag. |
| Senior Dashboard | Agustin (Dashboard Eng), Marcelo (Senior Eng) | Agustin is overloaded. Solid engineer but needs capacity. |
| Senior Sales Outbound | Haroun (currently owns it), Laith (FDE), Outbound team (Uzair, Mevlut) | Haroun built the MVP but can't run it as CTO. This person takes full product ownership — not just engineering, but product direction. They'll work with Laith on customer-facing work and coordinate with the Outbound team on shared infrastructure. |
| Mid Mobile | Hassan (Junior Mobile Eng) | Hassan built the app with Rork (AI tool). App works but needs professionalization. Need mentor. |

**Overall team dynamic:** Fast-moving, scrappy, async-first. Everyone ships code. Low ego, high ownership. Engineering and OPS work closely together.

---

## 8. What is the size of the team today? How are they distributed?

**Total:** ~27 people (excluding sales)

| Department | Headcount | Notes |
|------------|-----------|-------|
| Engineering | 16 | CTO (Haroun), Head of Integrations (Omer), 14 engineers |
| Operations | 7 | Manager (Waqar) + 6 OPS specialists |
| Customer Success | 2 | Zach, Ashley |
| Product | 1 | Kareem |
| Executive | 1 | CEO (Samee) |

**Distribution by team:**
- Core/Platform: 5 engineers
- Dashboard: 2 engineers
- Integrations: 2 engineers
- Outbound: 3 engineers
- Mobile: 1 engineer
- Sales/FDE: 1 engineer
- Support: 1 engineer

**Proposed hires:** 7 engineering roles

---

## 9. What traits or behaviors tend to make someone highly successful on your team?

**We hire for culture first.** Skills are learnable. Grit is not.

**What we're looking for:**

1. **Wants the grind** — This is a startup. It's hard. The best people hear that and get excited, not scared.
2. **Ships fast** — Code in production Day 1. PRs merged Week 1. No long ramp-up periods.
3. **Owns outcomes, not tasks** — Doesn't wait to be told what to do. Sees the problem, proposes solutions, executes.
4. **Pushes back when needed** — Protects their time. Says "no" to scope creep. Prioritizes ruthlessly.
5. **Figures things out** — Doesn't need hand-holding. Gets stuck, unsticks themselves, asks for help when actually blocked.
6. **Customer empathy** — Especially for support roles. Understands that every ticket is a frustrated customer.
7. **Low ego** — Will debug a gnarly issue at 2am if needed. Will do unglamorous work.

**The Mevlut example:**
- Hired as a culture fit — showed grit, wanted the grind
- Worked his ass off, came to the office, leveled up fast
- Skills came after. Culture was the foundation.

**Red flags:**
- "I need to understand the full architecture before I can contribute"
- "That's not my job"
- Looking for work-life balance as priority #1 (we're not the right fit)
- Over-engineers solutions
- Can't explain things simply
- Needs constant direction

---

## 10. What does the interview process look like for each role, and who are the key decision-makers?

### Hiring Philosophy

**We hire in this order: Culture → Aptitude → Skills.**

- **Culture** is hardest to change. Values are baked in.
- **Aptitude** (learning speed, problem-solving) is somewhat fixed but workable.
- **Skills** (TypeScript, React, AWS) are learnable. Don't over-index.

The process is designed to filter for culture first, then validate aptitude, then confirm skills.

### Process Overview

**All roles go through the same first step: Haroun's 15-min culture screen.**

This is intentionally short and intentionally brutal. Candidates hear the reality of the job — fast pace, high expectations, lots of ambiguity. This filters out people looking for a comfortable job. The people who stay after hearing the truth are the ones we want.

### Senior Roles (Ops Engineer, Dashboard, Sales Outbound) — 4 rounds

| Round | Format | Duration | Interviewer(s) | Focus |
|-------|--------|----------|----------------|-------|
| 1 | Recruiter Screen | 30 min | Murshed | Logistics, salary, basic red flags |
| 2 | Culture Screen | 15 min | Haroun | "Worst job ever" pitch — filter for grit |
| 3 | Technical + Aptitude | 60 min | Haroun + relevant senior | Role-specific assessment |
| 4 | Final | 30 min | Samee | Executive alignment |

### Support Roles (PAM Core Support x2, Integration Support) — 4 rounds

| Round | Format | Duration | Interviewer(s) | Focus |
|-------|--------|----------|----------------|-------|
| 1 | Recruiter Screen | 30 min | Murshed | Logistics, salary, basic red flags |
| 2 | Culture Screen | 15 min | Haroun | "Worst job ever" pitch — filter for grit |
| 3 | Technical + Aptitude | 60 min | Anujan + Omer | Debugging, pushback ability, systems thinking |
| 4 | Final | 30 min | Haroun | CTO alignment, final call |

### Mid Mobile — 4 rounds

| Round | Format | Duration | Interviewer(s) | Focus |
|-------|--------|----------|----------------|-------|
| 1 | Recruiter Screen | 30 min | Murshed | Logistics, salary, basic red flags |
| 2 | Culture Screen | 15 min | Haroun | "Worst job ever" pitch — filter for grit |
| 3 | Technical + Aptitude | 60 min | Hassan + Marcelo | React Native, uplevel-vs-rewrite mindset |
| 4 | Final | 30 min | Haroun | CTO alignment, final call |

### Technical Focus by Role

| Role | Technical Interviewer(s) | What They're Testing |
|------|-------------------------|----------------------|
| Senior Ops Engineer | Haroun + Juzer | System design, automation pipelines, AI integration |
| Senior Dashboard | Haroun + Marcelo | Frontend architecture, code review, UI/UX sensibility |
| Senior Sales Outbound | Haroun | Full-stack, data modeling, prompt engineering, ownership |
| PAM Core Support | Anujan + Omer | Debugging, customer communication, pushback ability, pattern-fixing |
| Integration Support | Anujan + Omer | API debugging, webhook troubleshooting, pushback ability |
| Mid Mobile | Hassan + Marcelo | React Native, uplevel-vs-rewrite mindset (critical) |

### Key Decision-Makers
- **All roles:** Haroun (CTO) has final say
- **Senior roles:** Samee (CEO) provides executive alignment
- **Support roles:** Anujan + Omer run technical, Haroun is final touch

### Decision Rule
**One No = No Hire.** If any interviewer isn't a Yes, we don't proceed.

### Note on Support Role Interviews
Anujan and Omer will be aligned on what to test for before interviewing. The goal of support hires is to **reduce escalations**, not just fix issues. They'll be testing for pushback ability, systems thinking, and whether candidates fix patterns vs. instances.

### Why the "Worst Job Ever" Pitch Works
Some recruiters worry this scares away good candidates. It doesn't — it scares away the wrong candidates. The people who self-select out after hearing the reality would have quit in 3 months anyway. The people who lean in are the ones who want the grind. This is intentional.

---

## 11. Have you made offers for similar roles, and what are the most common reasons candidates get rejected later in the process?

**Recent hire:** Yousof Algburi (Senior Pam Core) — hired February 2026.

**Common rejection reasons:**
1. **Slow to ship** — Talks about process, doesn't demonstrate velocity. "I'd want to understand X before..."
2. **Task-oriented, not outcome-oriented** — Waits for instructions. Doesn't show ownership.
3. **Over-engineers** — Proposes complex solutions to simple problems. Can't scope appropriately.
4. **Poor production judgment** — Doesn't think about safety, measurement, rollback. Would break things in prod.
5. **Weak debugging skills** — For support roles, can't trace issues systematically.
6. **Poor customer communication** — For support roles, can't explain technical issues to non-technical people.

**What we look for in the technical round:**
- How they structure problems
- Systems thinking (not just task completion)
- Production maturity
- Customer empathy
- Experience is a bonus, not required — right instincts matter more

---

## 12. How urgent are these hires, and are there any deadlines or milestones driving timing?

**Urgency: High**

| Role | Urgency | Why |
|------|---------|-----|
| PAM Core Support (x2) | 🔴 Critical | Onboarding is THE bottleneck. Every week we delay = revenue delayed. |
| Senior Ops Engineer | 🔴 Critical | Need observability before we can measure if anything else works. |
| Integration Support | 🟡 High | Integrations block onboarding, but Shaheer can hold the line short-term. |
| Senior Dashboard | 🟡 High | Agustin is overloaded but delivering. |
| Senior Sales Outbound | 🟡 High | CTO can't run a product. MVP works but needs dedicated owner to scale. Customer demand exists. |
| Mid Mobile | 🟢 Medium | App works. This is about professionalization, not fire-fighting. |

**Milestone context:**
- Raising Series A/B — stability and scalability are investor concerns
- Q1 2026 target: get high-confidence hires in pipeline
- Review checkpoint: February 19, 2026 — "Are hires in pipeline? Any offers out?"

---

## 13. Are there any constraints I should be aware of upfront (budget, location, clearance, visa, remote policy)?

**Location/Remote:**

| Role | Location Preference | Notes |
|------|---------------------|-------|
| Senior Dashboard | **Onshore (US) required** | Need someone dependable, same timezone, can be in the room when it matters |
| Senior Ops Engineer | Onshore preferred | High-touch role, benefits from proximity |
| Senior Sales Outbound | Onshore preferred | Customer-facing, US timezone alignment helps |
| PAM Core Support (x2) | Open to international | Async support can work across timezones |
| Integration Support | Open to international | Same as above |
| Mid Mobile | Open to international | UK timezone could work (potential expansion) |

**General:**
- Team is distributed (US, Canada, LATAM, Pakistan, Middle East)
- Async-first culture — strong written communication required
- For roles marked "onshore required," this is non-negotiable

**Visa/Clearance:**
- No clearance requirements
- Open to international candidates for roles that allow it
- Can sponsor if needed (case by case)

**Budget:**
- Competitive market rates
- More flexibility for Senior roles that directly unblock revenue (Core Support, Ops Engineer)
- Onshore roles will cost more — that's expected and acceptable for the right people
- Less flexibility for roles that are "nice to have" (Mobile)

**Other constraints:**
- **TypeScript is non-negotiable** — entire stack is TS
- **Shipping speed is cultural** — candidates who need long ramp-up won't fit
- **No agency fees preferred** — direct sourcing is ideal

---

## Summary: Priority Order

1. 🔴 PAM Core Support Engineer (x2)
2. 🔴 Senior Operations Engineer
3. 🟡 Integration Support Engineer
4. 🟡 Senior Dashboard Engineer
5. 🟡 Senior Sales Outbound Engineer
6. 🟢 Mid-Level Mobile Engineer

Let's focus sourcing energy on #1 and #2 first.
