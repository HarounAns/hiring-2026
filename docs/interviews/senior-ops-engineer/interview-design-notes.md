# Senior Ops Engineer — Interview Design Notes

**Format:** Live call with screenshare. One flowing conversation, three phases.

**Interviewers:** Haroun + Omer

---

## The Problem This Interview Tests

Onboarding is slow and invisible. Deals close in HubSpot, then dealerships wait weeks to go live. The process is manual (email, spreadsheets, Slack pings), there's no ticketing, no cycle time data, no way to see where things get stuck. We're signing 30-40 new dealerships a month and this doesn't scale.

The person we hire builds the automation and observability layer. But the key insight is: **the workflow tool IS the observability tool.** If you put onboarding into Linear with the right statuses, you get cycle time per stage for free. You don't need a separate dashboard.

---

## Phase 1: Build the Pipeline (15-20 min)

### The Prompt

> "Deals close in HubSpot. Right now, onboarding is kicked off manually — someone creates tasks, sends emails, tracks things in spreadsheets. How would you automate the start of this?"

### What You're Testing

- Can they design the HubSpot → Linear trigger?
- Do they think about what data needs to flow?
- Do they think about ticket structure (parent + subtasks vs statuses)?
- Do they naturally arrive at "Linear gives us cycle time tracking for free"?
- Do they ask if different customers go through different onboarding paths?

### Key Insight the Candidate Should Reach

The workflow tool IS the observability tool. You don't need a separate dashboard if the tickets moving through statuses are the source of truth.

### What Great Looks Like

The candidate asks clarifying questions before designing anything. They discover the tool (Linear) through questions. They connect that statuses = cycle time for free. They ask the critical question: **"Is onboarding the same for every customer, or are there different paths?"**

They don't need domain knowledge (CDK, Tekion, DMS). They need the instinct that not all customers are the same and the automation should account for that. The domain knowledge comes from you when you answer.

**Example flow:**

**Candidate:** "What data is on the deal? And is onboarding the same for every customer, or are there different paths?"

**You:** "Good question. Each dealership uses a different integration — think of it like different software providers. Some take 24 hours to set up, some take 2-3 weeks. That's on the HubSpot deal."

**Candidate:** "Oh, so that's a big deal. I'd want to pull that into the ticket and template the onboarding differently based on which integration it is. A 24-hour integration and a 3-week integration shouldn't have the same workflow or the same expectations."

The signal isn't domain knowledge. The signal is **asking the right question** and then immediately connecting the answer to the system design.

### What Bad Looks Like

The candidate jumps straight to "build a custom service" — a Node.js app with a database and a custom dashboard. When you mention Linear, they dismiss it ("Linear isn't really designed for this"). They don't ask clarifying questions about the current process. Data flow is generic ("whatever's on the deal record"). They don't ask about different customer types. They see this as an engineering problem that requires custom code, not a process problem that existing tools solve.

### Red Flags

- Proposes building a custom app instead of using existing workflow tools
- Doesn't ask a single clarifying question
- "Whatever's on the deal" — no instinct for what data matters
- Doesn't think about different customer paths
- Treats observability as a separate problem from workflow
