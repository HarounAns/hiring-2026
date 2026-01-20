# Senior Engineer – Sales Outbound

## Problem This Role Solves

**Problem:** Existing Service Outbound customers keep asking for Sales. We have demand but no product.

**Opportunity:** Dealerships receive hundreds to thousands of sales leads per month. A lead's likelihood to convert drops significantly within 30 minutes. Human sales teams can't respond fast enough, especially after-hours. This is a massive market opportunity.

**Current state:**
- Haroun is building the MVP to prove the concept
- Service Outbound is $1M ARR, 40 dealers — Sales could be bigger
- Existing customers want to buy it; we just need to build it

**Why now:**
- Customer demand is already there (upsell from Service Outbound)
- MVP will validate the approach
- Need dedicated engineering to productionize and scale

---

## Role Summary

You'll take over Pam Outbound Sales from Haroun and own it end-to-end. This is a **0→1 product engineering** role. You'll inherit a working MVP, then productionize it, scale it, and potentially rebuild parts of it as the product matures.

**What you're getting:**
- Working MVP with live customers
- Reasonable codebase that needs hardening
- Scrappy docs
- A PRD with clear vision

**What you'll do:**
- Fix bugs and ship features as they come in
- Take ownership of the product
- Productionize: reliability, observability, scalability, maintainability
- Potentially rebuild parts as you learn what's needed

---

## The Product: Pam Outbound Sales

AI-driven lead engagement that:
- Responds instantly to new CRM leads (SMS → Email → Phone)
- Sets appointments (test drives, showroom visits, trade-in appraisals)
- Handles objections, inventory questions, pricing questions
- Warm handoff to human sales reps when needed
- Full CRM integration (Tekion first)
- Closed-loop reporting (AI-assisted sales attribution)

**Key differentiator:** Phone calls. Most competitors do SMS/email only.

**Phases:**
1. SMS-first outbound (current MVP)
2. Add email
3. Outbound phone calling (the big differentiator)

---

## Responsibilities

### 1. Own the Product
- Take over from Haroun as primary engineer
- Understand the codebase, the data model, the integrations
- Be the person who knows how it works and can fix anything

### 2. Productionize the MVP
- **Reliability:** Handle edge cases gracefully (call drops, bad data, API errors)
- **Observability:** Know what's happening without SSH-ing into boxes
- **Scalability:** Doesn't fall over at 10x volume
- **Maintainability:** Code is readable, tested, documented
- **Configurability:** Different dealers can have different flows without code changes
- **Operability:** OPS/CS can troubleshoot without engineering

### 3. Understand and Extend the Ontology
- Learn the Outbound Orchestration data model (campaigns, contacts, messages, etc.)
- Build the Sales-specific entities (leads, vehicles of interest, appointments, handoffs)
- Fit Sales into the existing primitives while keeping it clean

### 4. Prompt Engineering
- Own the Sales conversation prompts
- Handle intents: availability, pricing, scheduling, trade-in, financing
- Build guardrails: never fabricate inventory, escalate when uncertain
- Tune for appointment conversion

### 5. Data Analysis & Reporting
- Build closed-loop reporting (lead → engaged → appointment → show → sold)
- Instrument for outcome-based pricing ($X per appointment)
- Analyze what's working, what's not, iterate

### 6. Ship Features
- Multi-channel journeys (SMS → email → phone)
- Human takeover and warm handoff
- Knowledge bank and AI configuration
- Dashboard and analytics

---

## Success Criteria

### Month 1
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Shipping | Code in production Day 1, multiple PRs merged Week 1 | PRs merged |
| Ownership | Handling bugs without Haroun by Week 2 | Issue resolution |
| Features | Shipped multiple customer-facing improvements | Release notes |
| Data model | Can explain the ontology and how Sales fits in | Whiteboard |

### Month 3
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Product ownership | Haroun not involved day-to-day | Time tracking |
| Reliability | Fewer customer-reported issues | Support tickets |
| Features | Phase 1 complete, Phase 2 in progress | Roadmap |
| Observability | Can debug issues without code diving | Dashboard/logs |

### Month 6
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Scale | 10+ customers live, system stable | Customer count, uptime |
| Team building | Hiring/building out eng + ops/cs for the product | Headcount, data-driven decisions |
| Phone calling | Phase 3 (outbound calls) launched | Feature shipped |
| Running the product | You're operating it, not just building it | Independence from Haroun |

### 1 Year
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Revenue | Sales Outbound is meaningful revenue line | ARR |
| Scale | 50+ customers, no engineering bottleneck | Growth rate |
| Product maturity | Dealers configure without engineering | Self-serve |
| Team | May have hired additional engineers for Sales | Headcount |

---

## Requirements

### Must Have
- 4+ years software engineering experience
- Strong TypeScript — our entire stack is TypeScript
- AWS experience (we run on AWS)
- Uses AI to code (Claude Code, Cursor, Copilot, etc.) — this is how we work
- Strong prompt engineering skills — you'll own the Sales AI behavior
- Can work with complex data models (ERDs, relational schemas)
- SQL proficiency — data analysis is part of the job
- Full-stack capable — backend, APIs, dashboards
- Can take ambiguity and turn it into working software

### Nice to Have
- Experience with CRM integrations (Tekion, Salesforce, etc.)
- Built multi-channel messaging systems (SMS, email, voice)
- Experience with outbound/marketing automation
- Worked on 0→1 products before
- Automotive or dealership domain experience

### Mindset
- **Ownership mentality** — this is your product, not Haroun's
- **Productionization instinct** — sees MVP and immediately thinks "what breaks at scale?"
- **Data-driven** — instruments everything, makes decisions based on metrics
- **Pragmatic** — ships working software, iterates based on feedback
- **Autonomous** — doesn't need hand-holding, figures things out

---

## What They'll Work On (First 30 Days)

**Week 1:**
- Day 1: Get access, ship first PR (bug fix or small improvement)
- Day 2-3: Deep dive on codebase while shipping more fixes
- Day 4-5: Understand Outbound Orchestration with Uzair/Mevlut, ship another fix
- End of week: Multiple PRs merged, can explain how a lead becomes an appointment

**Week 2:**
- Shipping fixes and small features daily
- Start productionization work (pick highest-risk area)
- Meet with Laith to understand Sales tooling context

**Week 3-4:**
- Shipping features independently
- Owns the backlog — prioritizing what to work on
- Written plan for months 2-3 that Haroun believes in

**If they can't ship code Day 1, wrong hire.**

---

## Reporting & Team

- **Reports to:** Haroun (CTO)
- **Works with:**
  - Uzair, Mevlut (Outbound Orchestration — to understand the data model)
  - Laith (Sales FDE — to understand dealer needs)
- **Stakeholders:** Samee (CEO) — Sales is a strategic priority

---

## The Ontology Challenge

The Outbound Orchestration system has a complex data model:
- Campaigns, Contacts, Messages, Channels, Cadences, etc.

For Sales, you need to:
- Understand these primitives deeply
- Build Sales-specific entities (Leads, Vehicles of Interest, Appointments, Handoffs)
- Fit them into the existing model without breaking Service Outbound
- Eventually may need to refactor/rebuild as Sales grows

**This is hard.** The right person finds this interesting, not intimidating.

---

## Red Flags (Don't Hire If...)

- Wants a fully spec'd out product — this is 0→1, ambiguity is the job
- Can't work with existing code — needs to start fresh
- No prompt engineering interest or experience
- Doesn't want to own a product — just wants to write code
- Needs a team around them — this is solo ownership initially
- Can't context-switch between feature work, bug fixes, and architecture

---

## Interview Process

See [interviews/senior-sales-outbound-engineer.md](../interviews/senior-sales-outbound-engineer.md)

---

## Compensation

*[To be filled based on market data]*

- Level: Senior (L5 equivalent)
- Location: [Remote / Hybrid / On-site]
