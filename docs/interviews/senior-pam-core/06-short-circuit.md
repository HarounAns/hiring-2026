# Short-Circuit Screen — Senior Pam Core (LLM Reliability)

**15-20 min | Recruiter-led phone screen | Pass = 2/3 or 3/3**

Use this between the culture fit screen and the full technical interview. If they score 0/3 or 1/3, stop — don't advance to technical.

**For the recruiter:** Read each question exactly as written. You're listening for real stories with real details. No story = stop signal.

---

## Q1: Production LLM Experience

> "Tell me about an LLM-powered product you worked on that was live in production — real users depending on it. What was the hardest problem you had to solve?"

### Pass signals
- Describes a **specific product, company, and team**
- Tells a **real story** about something going wrong — tracing it, diagnosing it, fixing it
- Mentions **monitoring, reliability, or customer impact**
- You can tell they've **operated** an LLM system, not just built one

### Stop signals
- Only mentions personal projects, hackathons, or experimentation
- Can't describe who the end users were
- "I've used ChatGPT a lot" or similar
- Vague — no specific product, no specific problem

---

## Q2: LLM Change Management

> "How do you make sure an LLM system keeps working correctly when something changes — like a new model version or a prompt update?"

### Pass signals
- Mentions **testing, evals, or regression checks** — specific methods
- Talks about **not trusting the model blindly** after a change
- Describes **a process**, not just an intention ("we would run evals" vs "I'd test it")
- Mentions **rolling out gradually** or checking specific customer segments

### Stop signals
- "I'd just test it manually" or "try it out and see"
- No concept of systematic validation
- Treats model or prompt changes as low-risk by default
- Has never dealt with this problem before

---

## Q3: Production Incident Response

> "Tell me about a time a production system you were responsible for broke — an outage, a performance issue, customers getting a bad experience. Walk me through what happened and what you did."

### Pass signals
- Has a **real incident story** — specific system, specific failure, real stakes
- Describes a **structured response** — scoped the problem first, then contained it, then fixed it
- Mentions **communicating** to the team or stakeholders during the incident
- Talks about **what they changed afterward** to prevent it from happening again

### Stop signals
- Has never been responsible for a live system or been on-call
- "I looked at the logs and found the bug" — no structure, no triage
- Fixed it and moved on — no mention of prevention or follow-up
- Can't tell a real story

---

## How to Score

| Result | Decision |
|--------|----------|
| **3/3** | Strong advance to technical. Tell Haroun: "nailed all three." |
| **2/3** | Advance to technical. Note which question they were weak on. |
| **1/3** | Don't advance. Share notes with Haroun for a final call. |
| **0/3** | Hard no. Don't advance. |

**The most important question is Q1.** The role requires real production LLM experience — if they don't have it, nothing else matters.

---

## Tips for the Recruiter

- **Read the question exactly as written.** Don't paraphrase.
- **Let them talk.** Silence is okay — give them time to think of their story.
- **You're listening for real stories.** Specifics = pass. Generalities = stop.
- **Take notes on the details they give** — project names, what the system did, what went wrong. Haroun will read your notes.
- If they ask a clarifying question, say: "Whatever comes to mind — I'm interested in a specific example from your experience."
