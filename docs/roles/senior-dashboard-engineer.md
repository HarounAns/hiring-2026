# Senior Dashboard Engineer

## Problem This Role Solves

**Problem:** Agustin is overloaded. Customer demand for dashboard enhancements exceeds our capacity.

**Root Cause:** Dashboard is the primary interface for dealers to interact with Pam. Many Pam Core features are dashboard-related (takeover texting, conversation views, analytics). We need more capacity to ship features without burning out the team.

**Current state:**
- Agustin handling dashboard work solo
- Customer requests for dashboard enhancements piling up
- Dashboard features often touch Pam Core systems but don't change LLM behavior
- Features like takeover texting require full-stack work across the dashboard and backend

**Why now:**
- Customer demand is real and immediate
- Dashboard quality affects eval experience and retention
- Agustin at capacity — can't scale with current team

---

## Role Summary

This is a **full-stack engineering** role focused on Pam's customer-facing dashboard. You'll build features that help dealers see value, manage conversations, and interact with Pam — things like takeover texting, analytics, conversation views, and reporting.

**Key distinction:** This role touches Pam Core systems but does NOT involve LLM/prompt engineering. You're building the interface and plumbing, not the AI behavior.

**Tech stack:** TypeScript, Next.js, React, AWS

---

## Responsibilities

### 1. Ship Dashboard Features
- Build customer-facing features in the dealer dashboard
- Implement features like takeover texting, conversation management, analytics
- Work with backend systems to surface data and enable actions
- Ship fast — code in production Day 1

### 2. Full-Stack Development
- Frontend: React/Next.js components, pages, UX flows
- Backend: APIs, data fetching, integrations with Pam Core
- Database: Queries and data modeling for dashboard needs
- End-to-end ownership of features from design to deploy

### 3. Customer-Facing Quality
- Build interfaces that dealers actually want to use
- Improve UX based on customer feedback
- Make Pam's value visible through clear analytics and reporting
- Think about the eval experience — help prospects see ROI quickly

### 4. Work Across Teams
- Coordinate with Pam Core team when features require backend changes
- Work with OPS/CS to understand dealer pain points
- Collaborate on features that span dashboard and conversation systems

---

## Success Criteria

### Month 1
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Shipping | Code in production Day 1, multiple PRs merged Week 1 | PRs merged |
| Ramp | Understands dashboard architecture and data flow | Code review |
| Features | Shipped at least one customer-facing improvement | Release notes |
| Ownership | Handling bugs and small features without hand-holding | Issue resolution |

### Month 3
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Velocity | Shipping features independently, multiple per sprint | Sprint metrics |
| Capacity relief | Agustin's load noticeably reduced | Team feedback |
| Customer impact | 3+ customer-requested features shipped | Customer feedback |
| Code quality | PRs require minimal revision, good test coverage | Code review |

### Month 6
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Feature ownership | Owning major dashboard initiatives end-to-end | Project delivery |
| Dashboard quality | Fewer customer complaints about dashboard UX | Support tickets |
| Team contribution | Contributing to architecture decisions | Design docs |
| Eval experience | Dashboard helps close deals (mentioned in win analysis) | Sales feedback |

### 1 Year
| Metric | Target | How to Measure |
|--------|--------|----------------|
| Scale | 2x feature velocity vs today | Sprint metrics |
| Product impact | Dashboard is a competitive advantage | Customer feedback |
| Self-serve | Dealers can self-serve common tasks without support | Ticket reduction |
| Leadership | May be mentoring junior dashboard engineers | Team growth |

---

## Requirements

### Must Have
- 3+ years software engineering experience
- Strong TypeScript — our entire stack is TypeScript
- React/Next.js experience — you've built production React apps
- AWS experience (we run on AWS)
- Uses AI to code (Claude Code, Cursor, Copilot, etc.) — this is how we work
- Full-stack capable — comfortable with frontend, APIs, and databases
- Can ship fast — code in production Day 1

### Nice to Have
- Experience with dashboards, admin panels, or B2B SaaS interfaces
- Data visualization experience (charts, analytics)
- Experience with real-time features (WebSockets, live updates)
- Eye for UX (can identify and fix usability issues)
- SQL proficiency for analytics features

### Mindset
- **Ships fast** — gets features out the door, iterates based on feedback
- **Customer-focused** — thinks about what dealers need, not just what's technically interesting
- **Full-stack comfortable** — doesn't throw work over the wall to backend or frontend
- **Pragmatic** — builds what's needed, not over-engineered solutions
- **Collaborative** — works well across teams when features span systems

---

## What They'll Work On (First 30 Days)

**Week 1:**
- Day 1: Get access, ship first PR (bug fix or small improvement)
- Day 2-3: Deep dive on dashboard codebase, understand architecture
- Day 4-5: Ship more fixes, understand how dashboard talks to Pam Core
- End of week: Multiple PRs merged, can explain dashboard data flow

**Week 2:**
- Shipping small features daily
- Understand key dashboard areas: conversations, analytics, settings
- Meet with Agustin to understand backlog and pain points

**Week 3-4:**
- Shipping features independently
- Pick up a medium-sized feature from backlog
- Start contributing to architecture discussions

**If they can't ship code Day 1, wrong hire.**

---

## Reporting & Team

- **Reports to:** Haroun (CTO)
- **Works with:**
  - Agustin (Dashboard Engineer)
  - Pam Core team (for features touching backend systems)
  - Kareem (PM)
- **Stakeholders:** OPS/CS (dealer feedback), Sales (eval experience)

---

## Dashboard Landscape

| Area | What It Covers | Typical Features |
|------|----------------|------------------|
| **Conversations** | View and manage Pam conversations | Takeover texting, conversation history, filters |
| **Analytics** | Dealer performance metrics | Call volumes, appointment rates, ROI tracking |
| **Settings** | Dealer configuration | Business hours, routing rules, preferences |
| **Onboarding** | New dealer setup | Integration status, checklist, progress tracking |

---

## Red Flags (Don't Hire If...)

- Only wants to do frontend OR backend — this is full-stack
- Wants to work on LLM/AI stuff — this role is interface, not AI behavior
- Can't ship fast — needs long ramp before producing code
- Over-engineers solutions — builds for hypothetical future needs
- Poor UX instincts — builds things that work but are hard to use
- Needs detailed specs — can take requirements and figure out implementation

---

## Interview Process

See [interviews/senior-dashboard-engineer.md](../interviews/senior-dashboard-engineer.md)

---

## Compensation

*[To be filled based on market data]*

- Level: Senior (L5 equivalent)
- Location: [Remote / Hybrid / On-site]
