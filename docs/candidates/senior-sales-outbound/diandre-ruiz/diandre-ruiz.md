---
name: DiAndre Ruiz
role: senior-sales-outbound
stage: technical
source: inbound
email: DiandreRuiz77@gmail.com
phone: "(215) 915-1004"
linkedin:
location: Remote (all prior roles remote)
applied_date: 2026-04-07
current_role: AI Engineer (Forward Deployed) at Revin AI
years_experience: 4
stage_history:
  - stage: sourced
    date: 2026-04-07
    notes: Inbound applicant for Senior SWE — New Product 0→1
  - stage: culture_screen
    date: 2026-04-07
    notes: Culture / Resume Screen scheduled with Haroun, 2:00 PM ET
  - stage: technical
    date: 2026-04-07
    notes: Passed culture screen. Advanced to 60-min technical interview.
---

# Candidate: DiAndre Ruiz

**Position:** Senior Engineer — New Product (0→1) / Sales Outbound
**Current Role:** AI Engineer (Forward Deployed) at Revin AI
**Location:** Remote (Philadelphia area — Temple University)

---

## Background

YC-backed founder (Soundry AI, W24) turned forward-deployed AI engineer at Revin AI. 4+ years building AI-native products. Two-time founder — ran Bandlez Music LLC for 8 years ($200K revenue, 250K monthly Spotify listeners) before co-founding Soundry AI (music generation platform, 15K users, $50K ARR, $1M pre-seed). Currently at Revin AI building AI customer service agents for enterprise clients in the service industry.

Temple University CS + Coding Temple bootcamp. AWS Certified Cloud Practitioner and Solutions Architect Associate.

### Resume Highlights

- **Revin AI (Dec 2025–Present):** Forward-deployed AI engineer. Built audio eval pipeline categorizing 100K+ calls using LLM analysis. Designed multi-node prompting architecture for bi-modal AI agent that books appointments and integrates into ServiceTitan API. Led client meetings with C-level execs. Defined LLM-as-judge KPIs embedded in 20+ companies' core metrics.
- **Soundry AI / YC W24 (Jan 2023–Dec 2025):** Co-founder. Owned product + technical strategy. NLP pipeline processing 300K unstructured documents. Cloud-agnostic data pipelines with 60x throughput improvement. Worked directly with customers to ship features.
- **Bandlez Music LLC (Jan 2015–Aug 2023):** Co-founder. Built proprietary audio pipelines generating $200K+ in licensing revenue. Led teams for major artists including Shaquille O'Neal.
- **Aston Technology (Jul–Nov 2023):** Short stint — React, Flask, SQL, REST APIs.

### Tech Stack

Python, JavaScript, TypeScript, SQL | React, Redux, React Query | Flask, FastAPI, REST APIs, Auth0, Data Pipelines | PostgreSQL, MySQL, Firestore, Vector DBs | AWS (EC2, S3, Lambda), GCP, Azure, Docker, GitHub Actions | OpenAI API, Anthropic API, Agentic Systems, LLMs, Eval Pipelines, PyTorch, LangChain, LangGraph, LiveKit, Promptfoo, LangSmith

---

## Fit Assessment

### Strengths

- **Current role is almost identical to Pam Sales Outbound.** Revin AI: AI agent that books appointments, integrates into industry CRM (ServiceTitan), enterprise clients in service industry. Direct experience with the exact problem space.
- **Real 0-to-1 founder experience.** Co-founded two companies. Owned product and technical strategy at Soundry AI through YC. This isn't side-project entrepreneurship — it's years of building, shipping, and selling.
- **Customer-facing at every stop.** Led client meetings with C-level execs at Revin. Translated customer requirements into shipped features at Soundry. Has been in the room.
- **AI-native.** LLMs, eval pipelines, agentic systems, prompt architecture, LLM-as-judge. Not just API calls — designed evaluation frameworks used across 20+ companies.
- **Full-stack breadth.** React frontend, Flask/FastAPI backend, SQL, cloud infra, data pipelines. Can touch every layer.
- **Entrepreneurial DNA.** Built Bandlez from 2015-2023 into 250K monthly Spotify listeners. This person builds things and makes them work.

### Concerns

- **Why did he leave Soundry AI?** Co-founded a YC company, raised $1M, had 15K users — then left after ~3 years. Need to understand what happened. Failure? Pushed out? Deliberate exit?
- **Depth vs breadth risk.** Resume reads wide — audio pipelines, NLP, data processing, booking agents, eval KPIs. "Forward Deployed AI Engineer" could mean deep product ownership or client config work. Need to probe.
- **CS fundamentals.** Temple University + Coding Temple bootcamp. YC acceptance offsets this, but domain modeling and systems design depth is unproven. Technical interview will test this.
- **All remote roles.** Every position has been remote. Is he willing to relocate to DC area for in-person?
- **Aston Technology stint was 4 months.** Short and basic. Not concerning on its own but worth noting.
- **$50K ARR after ~3 years at Soundry.** Modest traction. Was this a market problem, execution problem, or both?

---

## Interview Status

| Stage | Interviewer | Date | Result | Notes |
|-------|-------------|------|--------|-------|
| Culture Fit | Haroun | 2026-04-07 | Pass | Resume probe + culture screen |
| Short Circuit | | | Skipped | |
| Technical | Haroun | 2026-04-10 | No (19/35) | First interview with this format — some gaps may be interviewer calibration. Pending comparison with other candidates. |
| Closing | | | | |

---

## Interview Notes

### Culture Fit Screen

**Vote:**

| Question | What they said | Signal |
|----------|---------------|--------|
| **Goals** | | |
| **Why Pam** | | |
| **10 years** | | |
| **5 years** | | |
| **AI** | | |
| **The Oath** | | |

### Short Circuit Screen

**Score: /3**

| Question | Pass/Stop | Notes |
|----------|-----------|-------|
| Q1: Prompt Engineering | | |
| Q2: SQL & Data | | |
| Q3: Building from Zero | | |

### Technical Interview

**Interviewer:** Haroun
**Date:** 2026-04-10
**Vote:** No (19/35)

**Caveat:** This was my first time running this interview format. Some gaps may reflect interviewer calibration — I could have nudged better in Phase 1 and given more room in Phase 2. Will recalibrate after running it with Adnan Zafar and the other candidates.

#### Scores

| Dimension | Score | Notes |
|-----------|-------|-------|
| Domain Modeling | 3/5 | Separated Contact from Lead, modeled agent config (Guardrail Config, System Prompt, Initial Message Config). But started in pipeline-brain (ingestion/transformation/presentation), needed nudge to entity-model. Listed DB columns with types before relationships. Missed VehicleOfInterest vs Vehicle, CrmNote write-back, co-buyers, routing/orchestration layer. |
| Ops Thinking | 2/5 | Strong on verification — LLM-as-judge, simulated conversations, mocked tool calls, composite scoring (real Revin experience). But no staged pipeline, no discovery from CRM data, no monitoring, no auto-disable/rollback, almost no failure modes. |
| Product Ownership | 3/5 | Good instinct to make inventory check global, not bespoke. Got to data-driven/AB testing and "never disappoint the customer but measure everything." But initial instinct leaned toward shipping, needed nudge about booking rate to reframe as hypothesis. |
| Quantitative Rigor | 3/5 | Mentioned booking rate and purchase rate. Got to experiments. But no statistical rigor, didn't close measurement loop unprompted. |
| Model Evolution | 2/5 | Didn't connect the three phases. Agent model from Phase 1 didn't evolve to support variants in Phase 3. Phases felt like separate answers. |
| Curiosity | 3/5 | Asked about account ownership and CSM structure. But didn't ask deep clarifying questions in Phase 1 — jumped to implementation. |
| Communication | 3/5 | Doc notes sparse and column-heavy. Verbal was stronger. |

**Total: 19/35** (No territory, high end)

**Red flags:** 1 of 10 (tables first). Not disqualifying.

#### Phase-by-Phase

**Phase 1 — Domain Modeling (⚠️ Mediocre):**
Got Contact, Lead (separated — good), Vehicle, Appointment, and agent-side config (Guardrail Config, System Prompt, Initial Message Config — good). State enum on Contact for lifecycle. Lead has Source for attribution. But: started with ETL pipeline thinking, needed nudge to focus on entities. Listed columns with types (FK, varchar, int). Missed VehicleOfInterest vs inventory, CrmNote write-back, co-buyers, routing/orchestration layer.

**Phase 2 — Ops Automation (⚠️ Mediocre):**
Verification was genuinely strong — LLM-as-judge scoring, simulated conversations, mocked tool calls, composite pass/fail score. Pulled directly from Revin experience. Got to "structured requirements → config" and "manual → asynchronous." But: no staged pipeline (connected → discovered → configured → verified → live), no discovery from historical CRM data, no monitoring, no auto-disable/rollback. Answer was thin outside his eval comfort zone.

**Phase 3 — Own It (⚠️ Mediocre, trending toward ✅):**
First instinct was to make inventory check a global improvement for all clients, not bespoke — good product thinking. After nudge about booking rate, got to data-driven/AB testing approach. "Never disappoint the customer but measure everything." Said this approach was "refreshing compared to previous roles." Genuine engagement. But needed nudges to get there, didn't connect back to Phase 1 model, no statistical rigor.

#### What He Did Well
- Agent-side modeling — Guardrail Config, System Prompt, Initial Message Config as first-class entities
- Verification/eval infrastructure — real depth from Revin (LLM-as-judge, simulations, composite scoring)
- Product instinct in Phase 3 — "make it global, not bespoke" + data-driven
- Genuine enthusiasm — "this is the best fit for me," called the AB testing approach "refreshing"

#### What He Missed
- No orchestration layer (LeadSource → RoutingRule → AgentConfig)
- No VehicleOfInterest vs Vehicle distinction
- No CrmNote write-back concept
- No staged onboarding pipeline
- No monitoring, auto-disable, or rollback
- Didn't connect the three phases into a coherent system
- Doc notes were sparse — schema dump, not domain thinking

---

## Debrief

| Question | Answer |
|----------|--------|
| **Final Decision** | Pending — need to complete interviews with Adnan Zafar, Mohamed Mahmoud, and remaining candidates before comparing. |
| **Strengths** | Real AI/eval depth from Revin. Agent-side modeling instincts. Product thinking in Phase 3. Domain overlap (booking agents + CRM integration). Genuine enthusiasm for the role. |
| **Concerns** | Systems thinking gaps — no ops pipeline, no monitoring, no failure modes. Domain modeling needed hand-holding. Phases didn't connect. All remote history — relocation unconfirmed. |
| **Offer Details** | |
