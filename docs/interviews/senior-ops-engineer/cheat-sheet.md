# Senior Ops Engineer — Interviewer Cheat Sheet

**60 min | Live call, screenshare | Haroun + Omer**

**You're filtering for:** Diagnoses before prescribing, uses existing tools over custom builds, connects workflow to observability, thinks in loops (fix → measure → learn → fix better)

---

## Before the Interview

- Have Linear open to the OPS team board ([Pam Onboardings project](https://linear.app/pam-ai/team/OPS/all)), filtered to Onboarding label
- Have the [cycle time screenshot](./integration-setup-pipeline.png) ready to screenshare in Phase 2
- Have a few Integration Setup tickets open for spot-checking in Phase 2
- Create a shared Google Doc with the candidate. Paste the following and nothing else:

```
We're signing 30-40 new dealerships a month. Once a deal closes in HubSpot,
onboarding starts — getting them set up, connected to our systems, and live
on the platform. Right now, one person on our OPS team tracks the whole thing
in spreadsheets and Slack. We can't tell you how long onboarding actually takes,
where things get stuck, or why some dealerships go live in a week and others
take three months.

---

Notes:
```

Don't add structure below "Notes:" — you want to see how the candidate organizes their own thinking. Say "How would you approach this?" out loud, don't put it in the doc.

---

## Phase 1: Build the Pipeline (15-20 min)

### Open with:

> "We're signing 30-40 new dealerships a month. Once a deal closes in HubSpot, onboarding starts — getting them set up, connected to our systems, and live on the platform. Right now, one person on our OPS team tracks the whole thing in spreadsheets and Slack. We can't tell you how long onboarding actually takes, where things get stuck, or why some dealerships go live in a week and others take three months. How would you approach this?"

### Context to give when asked (don't volunteer — let them pull it out of you):

| If they ask... | You say... |
|---|---|
| What happens today? Who does what? | Waqar on OPS sees deal close, manually adds a row to his spreadsheet, emails the dealer, tracks everything himself. He's the system. |
| What tools do you use? | Linear for engineering. OPS is on spreadsheets + Slack. |
| Walk me through the onboarding steps? | Intake → Dashboard Setup → Integration Setup → Configuration → Testing → Number Communicated |
| Is onboarding the same for every customer? | Each dealership uses a different integration provider. Some take a day, some take weeks. It's on the HubSpot deal. |
| What data is on the deal? | Dealership name, contacts, deal owner, integration type. |

### Follow-ups to have ready:

- *"You mentioned [X tool] — how does that compare to just using Linear?"* (if they propose a custom build)
- *"Would you do one ticket per dealership or multiple?"* (tests simplicity instinct)
- *"What are the statuses? Walk me through the pipeline."* (tests if they'll ask you for the process or guess)
- *"Do you need a Blocked status?"* (tests whether they understand how Blocked distorts cycle time data)

| Signal | Great | Concern |
|---|---|---|
| **First move** | Asks questions about current process before designing | Jumps to architecture / "I'd build a service" |
| **Tool choice** | Arrives at Linear (or similar workflow tool) | Proposes custom DB + React dashboard |
| **Key insight** | "Statuses give you cycle time for free" | "I'd build a dashboard" as a separate thing |
| **Customer types** | "Are there different onboarding paths?" | Doesn't ask, or gives abstract answer ("config file") |
| **Data instinct** | Asks what data matters for each stage | "Whatever's on the deal" |

---

## Phase 2: Read the Bottlenecks (15-20 min)

### Transition:

> "Let's say we built what you described and it's been running for a few months. You said you wanted observability — now you have the data. How would you figure out if onboarding is getting faster or slower?"

Then screenshare the [cycle time screenshot](./integration-setup-pipeline.png).

> "Here's what we're seeing. Take a look and tell me what jumps out."

### Follow-ups to have ready:

- *"Why do you think Integration Setup takes that long?"* (tests if they hypothesize or wait to be told)
- *"Is it us being slow or the dealer being slow?"* → Tell them it's the dealer dragging their feet
- *"What about Enable Flags at 4 weeks?"* (tests if they distinguish between dependency delay vs capacity issue)
- *"Do you trust this data?"* (if they don't question it themselves — open the actual tickets and let them spot-check)

### If they want to spot-check — let them:

Pull up Integration Setup tickets in Linear. Let them look at activity logs. Real things they might find:
- Tickets created directly in Integration Setup, skipping earlier statuses (data quality issue)
- Different BLKD labels (Pam Integration vs Vendor Integration — different root causes)
- Tickets with zero activity for weeks (abandoned? stuck? unclear)

| Signal | Great | Concern |
|---|---|---|
| **Reading data** | Identifies bottlenecks, asks what statuses mean | Reads numbers back: "some of these take a while" |
| **Root cause** | Distinguishes customer delay vs capacity vs dependency | "Could be a lot of things" — waits to be told |
| **Data quality** | Questions the data, wants to spot-check | Takes the numbers at face value |
| **Sample size** | Notes it (73 issues total) and factors it in | Doesn't mention it |
| **Blocked status** | Asks what it means, sees it as masking real stage time | Takes it at face value |

---

## Phase 3: Solve the Bottleneck (20-25 min)

### Transition:

> "So Integration Setup is the biggest bottleneck and the delay is the dealership dragging their feet. What would you do about it?"

### Follow-ups to have ready:

- *"What would the email/guide actually say?"* (tests specificity — generic "please complete setup" vs step-by-step per integration type)
- *"What happens when they reply and say 'I'm stuck on step 3'?"* (leads toward agent/automated handling of replies)
- *"How would you know if this is working?"* (tests measurement instinct — cycle time drop, not email open rate)
- *"Do all integrations take the same amount of time?"* → *"Can you tell from this data?"* (leads toward segmentation by integration type, backfilling labels)
- *"How would you roll this out? Do you turn it on for everyone?"* (tests pragmatism — should start with one integration type)
- *"What would you ship in Week 1?"* (THE closing question — always ask this)

| Signal | Great | Concern |
|---|---|---|
| **Solution depth** | Personalized guides per integration, handles replies, escalation path | Generic reminder emails with a help doc link |
| **Edge cases** | What if they reply? What if they're stuck? What if they want a human? | "Support would help them" |
| **Measurement** | Cycle time before/after, completion rate by step, by integration | Email open rate |
| **Segmentation** | "Can I filter by integration type? No? I'll backfill and add it." | "We could add that as a field" (passive) |
| **Rollout** | One integration first, talk to OPS, iterate | Turn it on for everyone |
| **Week 1** | Ship the foundation (HubSpot → Linear) + a quick win | "Start building the webhook" / infrastructure with no wins |

---

## The Meta-Signal

The best candidates **think in loops.** Every solution comes with "how would I know if this works" and every measurement comes with "what would I do differently based on what I learn." They don't just solve the problem — they build the system to keep solving it.

Bad candidates **think in tasks.** Build the thing, move on. No measurement, no iteration, no feedback loop.

---

## Quick Decision

| Dimension | Strong Yes | Lean Yes | Lean No | Strong No |
|---|---|---|---|---|
| **Diagnoses first** | Questions before design, pulls process out of you | Some questions, then designs | Few questions, mostly assumptions | Jumps straight to architecture |
| **Tool instinct** | Linear = observability for free | Open to Linear when suggested | Reluctant about Linear | "Linear is for bug tracking" |
| **Reads data** | Finds bottlenecks, questions data quality, spot-checks | Identifies bottlenecks correctly | Reads numbers back without insight | Misreads the data |
| **Solves the bottleneck** | Specific, per-integration, handles edge cases, measures outcomes | Good solution, some gaps in edge cases | Generic solution (reminders) | No real solution, hand-waves |
| **Week 1** | Foundation + quick win, talked to OPS | Reasonable plan, maybe too ambitious | Infrastructure-only, no quick wins | Vague / "I'd need to learn more" |
