# Simulation: Bad Candidate

**Format:** Live call, screenshare. Haroun + Omer interviewing. ~60 min.

---

## Phase 1: Build the Pipeline (15 min)

**Haroun:** "Deals close in HubSpot. Right now, onboarding is kicked off manually — someone creates tasks, sends emails, tracks things in spreadsheets. How would you automate the start of this?"

**Candidate:** "So I'd set up a webhook from HubSpot — when the deal moves to Closed Won, it triggers an API call to our backend. The backend would create the customer record in our database and spin up the onboarding pipeline. I'd probably build this as a serverless function — Lambda or something — that orchestrates the whole flow."

**Haroun:** "What does 'spin up the onboarding pipeline' mean? Where does it live?"

**Candidate:** "I'd build a service that manages onboarding state. A database table with the dealership info, a status column for where they are in the process, and an API that the team can use to advance each step. We could build a React dashboard on top of it so the team can see all active onboardings."

**Haroun:** "We use Linear for engineering work. Could that play a role?"

**Candidate:** "We could sync to Linear — maybe create a ticket when onboarding starts so engineering has visibility. But I'd keep the source of truth in our custom system. Linear is more for bug tracking and sprints, not really for this kind of workflow."

**Haroun:** "What data would you pull from HubSpot?"

**Candidate:** "Company name, contact info, deal size, deal owner. Whatever fields are on the deal. We'd store it all in our database."

**Haroun:** "Is onboarding the same for every customer?"

**Candidate:** "I'd design it to be flexible. We could have different onboarding templates or flows. Maybe a config file that defines the steps for each type. But to start, I'd build the general case and add customization later."

**Haroun:** "What would help you decide what those different flows look like?"

**Candidate:** "I'd talk to the team and map out the current process. Document each step, figure out the dependencies, and then model that in the system."

---

### What went wrong in Phase 1

- **Built a custom system instead of using existing tools.** Proposed a database, API, Lambda, React dashboard — a full engineering project for a problem that Linear solves out of the box.
- **Dismissed Linear.** "Linear is for bug tracking" — doesn't see that a workflow tool IS an observability tool.
- **No clarifying questions about the current process.** Didn't ask who does what today, how many deals close, what the pain is. Jumped straight to architecture.
- **Generic data answer.** "Whatever fields are on the deal" — no instinct for what data actually matters for onboarding.
- **Didn't ask about different customer types.** When prompted, gave an abstract answer ("config file, templates") instead of asking what makes customers different. Never discovered that integration type is the critical variable.
- **"Build the general case and customize later."** Sounds pragmatic but means they'll build something generic that doesn't serve anyone well.

---

## Phase 2: Read the Bottlenecks (12 min)

**Haroun:** "Okay, so imagine we set up onboarding tracking and it's been running. You want to know if things are getting faster. How would you figure that out?"

**Candidate:** "I'd build a dashboard. Show the average time from deal close to go-live. Maybe a chart showing the trend over time — is it going down? And then a breakdown by step so we can see where time is being spent."

**Haroun:** *[Screenshares the Integration Setup pipeline screenshot]* "Here's what we're seeing."

**Candidate:** "Okay. So these are the different stages... and those are the times. P50, P75, P95 — so percentiles. Looks like some of these stages take a while. Integration Setup is 15 days, Enable Flags is 4 weeks."

**Haroun:** "What jumps out to you?"

**Candidate:** "Enable Flags is the longest at 4 weeks. That seems like a lot. And Integration Setup at 15 days is pretty long too."

**Haroun:** "Why do you think Integration Setup takes 15 days?"

**Candidate:** "Could be a lot of things. Maybe the integration is complex, maybe there are bugs, maybe the team is overloaded. I'd want to dig into the tickets and see what's actually happening — read the comments, look at the activity."

**Haroun:** "The delay is on the dealership side. They have to do stuff in their system and they drag their feet."

**Candidate:** "Oh, okay. So it's a customer problem. We could send them reminders — like an automated email every few days saying 'hey, you still need to complete this step.' That would probably help."

---

### What went wrong in Phase 2

- **"I'd build a dashboard."** First instinct is to build something, not to look at what exists. The data is right there.
- **Read the numbers back without insight.** "Some of these stages take a while" — no analysis beyond restating what's on screen.
- **No questions about what the statuses mean.** Didn't ask what Integration Setup involves, what Blocked means, what Enable Flags is. Just took the labels at face value.
- **Vague root cause thinking.** "Could be a lot of things" — didn't hypothesize, didn't distinguish between technical delay, customer delay, or capacity issue. Waited to be told.
- **Jump to a shallow solution.** Once told it's the dealership dragging their feet, immediately went to "send reminders." Didn't ask why the dealer is slow, didn't think about whether different integrations are different, didn't think about what would actually make the dealer move faster. A reminder email is the minimum-effort answer.
- **Didn't notice the small sample size (4 issues).** Didn't caveat the data or ask about it.

---

## Phase 3: Automate the Bottleneck (15 min)

**Haroun:** "So the dealership drags their feet on Integration Setup. What would you do about it?"

**Candidate:** "Like I said, I'd set up automated reminder emails. We could trigger them from our system — if the ticket has been in Integration Setup for more than 3 days, send an email. Then another at 7 days. Maybe escalate to a phone call at 14 days."

**Haroun:** "What would the email say?"

**Candidate:** "Something like 'Hi, just checking in on your integration setup. Please complete the required steps so we can get you live. Let us know if you have any questions.'"

**Haroun:** "What if they have questions? What if they don't know what to do?"

**Candidate:** "We could include a link to a help doc or FAQ. Or they could reply to the email and our support team would help them."

**Haroun:** "How would you know if the reminders are working?"

**Candidate:** "We'd track the open rate on the emails. And we'd see if the average time in Integration Setup goes down."

**Haroun:** "Do all integrations take the same amount of time?"

**Candidate:** "Probably not. Some are probably more complex. But we'd have to look at the data to know."

**Haroun:** "Can you tell from this data which integrations are slower?"

**Candidate:** "Not from this view. We'd need to add some kind of label or tag for the integration type. Then we could filter and compare."

**Haroun:** "Would you do that?"

**Candidate:** "Yeah, we could add that as a field. Going forward we'd tag new tickets."

**Haroun:** "What about the existing tickets?"

**Candidate:** "We could try to backfill them, but it might not be worth the effort if there aren't that many. I'd focus on getting the new process right."

**Haroun:** "What would you ship in Week 1?"

**Candidate:** "Probably start building the webhook integration — get the HubSpot trigger working and create the basic pipeline. And start designing the reminder email flow."

---

### What went wrong in Phase 3

- **Reminder emails, not agent.** The solution is "send a generic reminder" — not a detailed walkthrough tailored to their integration type. It's what a PM would propose, not what an automation engineer would build.
- **Generic email content.** "Please complete the required steps" — the dealer already knows they need to complete the steps. The problem is they don't know HOW. The good candidate sends step-by-step instructions with screenshots.
- **No edge case thinking.** "Include a link to a help doc or they could reply and support would help them." Pushed the problem to support instead of designing the automation to handle replies.
- **Email open rate as the metric.** Measures activity (did they see the email) not outcome (did they complete setup faster). Vanity metric.
- **Didn't drive segmentation.** When asked about different integrations, acknowledged it but didn't have the instinct to go get that data. "We could add that as a field" — passive. Didn't propose backfilling existing tickets. Wouldn't "focus on getting the new process right" without historical data to compare against.
- **No conversation with OPS.** Never mentioned talking to the people who actually do onboarding today. Designing in isolation.
- **Week 1 answer is infrastructure with no quick wins.** "Start building the webhook" and "designing the reminder flow." No mention of talking to the team, looking at actual onboardings, or getting quick visibility into what's happening now.

---

## Comparison Summary

| Dimension | Good Candidate | Bad Candidate |
|-----------|---------------|---------------|
| **Phase 1: Tool choice** | Uses Linear — workflow = observability | Builds custom service + React dashboard |
| **Phase 1: Clarifying questions** | Who does what? How many deals? What tools? | None — jumped to architecture |
| **Phase 1: Customer types** | "Are there different paths?" → discovers integration type | Didn't ask until prompted, then gave abstract answer |
| **Phase 1: Key insight** | "Linear gives us cycle time for free" | "Linear is for bug tracking" |
| **Phase 2: Reading data** | Identifies bottlenecks, asks what statuses mean, distinguishes root causes | Reads numbers back, waits to be told why |
| **Phase 2: Root cause** | "Is it us, the customer, or a third party?" | "Could be a lot of things" |
| **Phase 3: Solution** | Agent with step-by-step instructions per integration type, handles replies, escalates when stuck | Generic reminder emails with a help doc link |
| **Phase 3: Edge cases** | Agent handles Q&A, schedules calls if stuck, escalates to human | "Support would help them" |
| **Phase 3: Measurement** | Cycle time before/after, completion rate per step, by integration type | Email open rate |
| **Phase 3: Segmentation** | "Can I filter by integration type? No? I'll backfill and add it to the process." | "We could add that as a field" (passive) |
| **Phase 3: Week 1** | Ship the HubSpot → Linear pipeline + tag existing tickets for visibility | Start building the webhook + designing reminder emails |
| **Meta-signal** | Thinks in loops: fix → measure → learn → fix better | Thinks in tasks: build the thing, move on |
