# Simulation: Roleplay (Haroun as Candidate)

**Format:** Live call, screenshare, shared Google Doc. ~60 min.

**Note:** This simulation was generated via a roleplay exercise where Haroun acted as the candidate and Claude Opus 4.6 played the interviewer. It uses the updated problem-first opening prompt (no "how would you automate").

---

## Phase 1: Build the Pipeline (25 min)

**Interviewer:** "Thanks for making time for this. The way this works — it's not a quiz, there's no trick questions. We're going to talk through a real problem we have and I want to hear how you'd think about it. I'll jump in with context as we go. Sound good?"

*[Candidate nods]*

"Cool. So here's the situation. We're signing 30 to 40 new dealerships a month. Once a deal closes in HubSpot, onboarding starts — getting them set up, connected to our systems, and live on the platform. Right now, one person on our OPS team tracks the whole thing in spreadsheets and Slack. He's the system.

The problem is — we can't tell you how long onboarding actually takes. We can't tell you where things get stuck. We can't explain why some dealerships go live in a week and others take three months. We just don't have visibility.

How would you approach this?"

**Candidate:** "Yeah so this is interesting. Is the main issue just visibility or is it that there are customer-facing things that are problematic? Like do you actually want to do 30 to 40 a week instead of the month? Or are you saying you want to know if you can do more?

Immediately I'm thinking about observability and automation, but no sense automating things if there's actually no problem. Do you know if there's a problem?"

**Interviewer:** "Yeah — we know there's a problem. Dealers are churning, and when we look at the ones we lost, a lot of them had rough onboardings. Long waits, no communication, they felt like they signed up and then nothing happened for weeks. But honestly? That's anecdotal. Waqar — the guy running onboarding — he'll tell you 'yeah that one was rough' but we can't point to data that says why it was rough or where exactly it broke down.

So it's both. There are customer-facing problems, but we can't see the machine well enough to know what's actually causing it. And the volume is growing — we need to know if the process can handle more, but we can't answer that today because we don't even know how it performs at current volume."

**Candidate:** "Yeah I'd want to focus on observability. So help me understand the current process. What does an onboarding look like?"

**Interviewer:** "Sure. A deal closes in HubSpot — sales marks it Closed Won. Then Waqar on our OPS team picks it up. He reaches out to the dealership, confirms the deal info, collects anything that's missing. Then we set up their dashboard. After that there's an integration step — connecting their existing systems to ours. Then we change configuration based on the collected inputs. Then someone tests everything end-to-end. And then we give them their number and they're live.

That's the rough flow. But it's all tracked in Waqar's head and his spreadsheet."

**Candidate:** *[Writes in the shared Google Doc]*

```
1. HubSpot -> closed deal
2. Waqar sends an email - is this a welcome greeting email? How does he collect the info? Like a list of questions
3. Dashboard creation - what do we need for this? Emails, RBAC? Do we need any of this stuff from HubSpot, where is it collected?
4. Configuration - what is this? Configuration for the dashboard? The Pam instance? How do you know what to configure?
5. Testing e2e - what does this mean? Like phone calling Pam?
6. Handing them the number - are we done or is there more after this?
```

"I think these are my questions."

**Interviewer:** "Good questions. Number 2 — yeah, Waqar sends them an email. Not really a welcome greeting, more like 'hey, we need these things from you to get started.' Contact details, login credentials for their existing systems. It's not a structured form — it's just an email he writes each time.

Number 3 — dashboard creation. We need some info to set it up. Dealership name, their users, permissions. Some comes from HubSpot, some Waqar collects in that first email. It's not super clean.

Number 4 — configuration. Based on what we've collected — the dealership's setup, their integration type, what features they're using — we configure their instance. The inputs come from the earlier steps.

Number 5 — testing is basically calling the number, making sure the system works end-to-end. Someone on the team does that manually.

Number 6 — once we hand them the number, they're live. There's ongoing support, but from an onboarding perspective, that's the finish line.

Oh — and I skipped something. The integration step between dashboard setup and configuration — connecting to the dealership's existing systems. Different dealers use different providers. Some are quick, some take weeks."

**Candidate:** "Okay cool so your goal is observability on the system — do you guys track these different stages in a sheet or something? Waqar changes those?"

**Interviewer:** "Yeah, Waqar has a spreadsheet. Row per dealership, he updates the status manually. But it's his spreadsheet — it's not something the rest of the team is looking at. He updates it when he remembers to. Not really a source of truth — more like personal notes.

We use Linear for engineering work, but OPS isn't on it."

**Candidate:** "Okay so HubSpot automatically inserts into the sheet? And then they manually create tickets for engineering for their work... wait, when does engineering get involved?"

**Interviewer:** "No — nothing's automatic. Waqar sees the deal close in HubSpot, then manually adds a row to his spreadsheet. And engineering doesn't really get involved in the standard onboarding flow. They only get pulled in when something breaks — and when that happens, Waqar pings someone on Slack. No ticket, no formal handoff.

So there's no ticketing system in this process at all right now."

**Candidate:** "Ugh yeah I can see how that would get messy. So I think there are different ways to do this:

1. You can add tooling on top of the sheet — Google Sheets can send change events to an API and we could track them in a DB and get status of each state and see how long it's in each state.

2. You could also just use a project management tool like Linear to track these different dealerships throughout the funnel. I think you get built-in analytics for each stage out of the box. And then you could easily automate stuff like rules via their API to move things along the different stages.

I think either could make sense."

**Interviewer:** "Interesting — so you're saying both could work. Walk me through the tradeoffs. If you had to pick one, which would you lean toward and why?"

**Candidate:** "So I would do the DB because we would have maximum control. However Google Sheets is kinda wonky as a UI — too many things can go wrong. Cell mismatch, people deleting the whole thing on accident.

I'd probably start with Linear and see if we could get what we needed out of that. We could likely build tooling off of that if we needed to. We could likely ETL stuff into our DB for maximum control. Also HubSpot into Linear would probably be easy — either using existing integrations or just both services' APIs.

Oh but another important thing is that the sheet is minimally invasive and allows us to work in the current process. Moving the dealerships to Linear would have to be a process Waqar is cool with and could take some time."

**Interviewer:** "Waqar's actually pretty adaptable. The spreadsheet isn't something he loves, it's just what he has. So let's say we go with Linear. How would you set this up?"

**Candidate:** *[Updates the Google Doc]*

```
- TODO
- SENDING WELCOME EMAIL
- CREATING DASHBOARD
- CUSTOMIZING / CONFIGURING?
- TESTING
- DELIVERED
```

"But actually I think stages should be what they're currently in, so maybe Testing not Tested?"

**Interviewer:** "I like that you're thinking about the naming — active tense makes sense because it's where the ticket currently is. But you're missing a step. Remember the integration piece? That's a big chunk of the timeline. And on 'Sending Welcome Email' — does that need to be its own stage, or is that just part of kicking things off?"

**Candidate:** "Yeah maybe INTAKE or COLLECTING DETAILS makes more sense."

*[Updates the doc]*

```
- TODO
- INTAKE
- CREATING DASHBOARD
- INTEGRATION SETUP
- CUSTOMIZING / CONFIGURING
- TESTING
- DELIVERED
```

"You said Integration Setup takes a long time? Like you already know that? So you have an idea of what takes a long time, but it's more vibes and qualitative than quantitative I guess."

**Interviewer:** "Exactly. We know it's painful — Waqar will tell you that. But we can't say 'the median is 15 days' or 'it's worse for certain integrations than others.' It's all vibes.

So — you've got the statuses. Now let's say a deal closes in HubSpot. How does the ticket actually get into Linear?"

**Candidate:** "No, like I said we'd use an API or integration. I think what's important is adding details that we and the sales team collect and having some required fields in the CRM that we use to kick off. Maybe we'd add them as labels to the ticket if they change onboarding? Maybe add the integration to the ticket as a label?"

**Interviewer:** "Yeah, the integration type is probably the most important label you could put on the ticket. What other data from HubSpot would you want on the ticket?"

**Candidate:** "I don't know, I'm not sure. Maybe there's other stuff we'd configure Pam with. I don't fully get the whole process."

**Interviewer:** "No, that's totally fair — I wouldn't expect you to know our specific process. You'd sit down with Waqar, understand what info he needs at each stage, then figure out what can come from HubSpot automatically versus what needs to be collected. You said the right thing."

---

## Phase 2: Read the Bottlenecks (15 min)

**Interviewer:** "Okay — let's shift gears. Let's say we built what you've described. HubSpot deal closes, ticket gets created in Linear with the integration type as a label, statuses match the onboarding stages, and it's been running for a few months. How would you figure out if onboarding is actually getting faster or slower?"

**Candidate:** "So I guess an assumption I made is that Linear gives you visibility into time in each status out of the box. Is that a fair assumption?

If that's the case I can see how in each cycle we could look at:
1. How many dealerships did we onboard this week
2. Which statuses are dealerships getting stuck in — in the past month
3. Is there a specific integration (since we added the label) that's taking longer or quicker than others

Once we're able to segment and identify bottlenecks we can start to solution and address them and maybe even automate parts of it. Like could we automate testing? Could we automate the integration setup? We would start with the larger buckets and try to do low-hanging fruit. Like are you familiar with the RICE prioritization method?"

**Interviewer:** "Yeah — Linear does give you cycle time analytics per status. P50, P75, P95 for how long tickets sit in each stage. And yeah, I know RICE. Let's make it concrete."

*[Screenshares the cycle time data]*

| Status | P50 | P75 | P95 |
|--------|-----|-----|-----|
| Across all statuses | 16d | 19d | 6w |
| Intake Requested | 12d | 16d | 19d |
| Dashboard Setup | 11d | 12d | 6w |
| Integration Setup | 22d | 29d | 29d |
| Enable Flags | 16d | 29d | 29d |
| Testing | 19d | 20d | 6w |
| Number Communicated | 16d | 23d | 29d |

*(73 issues, 3 status types, sliced by Status)*

"Here's what we're actually seeing. Take a look and tell me what jumps out."

**Candidate:** "These are some wild numbers. So basically if I understand this correctly this pretty closely maps to what we built. Enable Flags is customizations.

*[Screenshares the cycle time data]*
Why does it take on average 12 days? Like 30 days to enable flags — I think this is all very confusing. Either data quality sucks or you guys have some real issues.

What I would do is spot check this stuff."

**Interviewer:** "Yeah — you're right to question the data. What would spot checking look like?"

**Candidate:** "Go and look at some of these tickets. Like could I see how many tickets are in Integration Setup?"

**Interviewer:** *[Pulls up the Linear board, filters to Integration Setup]*

"Here — these are the real tickets sitting in Integration Setup right now. Four with the Onboarding label."

| Ticket | Dealership | Created | Integration | Assignee | Labels |
|--------|-----------|---------|-------------|----------|--------|
| OPS-1000 | Gullo Ford of Conroe | Mar 10 | CDK | Abdelrahman | Onboarding |
| OPS-646 | Sun State Ford | Mar 3 | Reynolds & Reynolds | Waqar | Onboarding, BLKD - Pam Integration |
| OPS-233 | Rehbein Ford | Feb 24 | Solera RedCap (NADA) | Abdelrahman | Onboarding, NADA |
| OPS-236 | Southern Chevrolet | Jan 20 | *(unclear)* | Amina | Onboarding, BLKD - Vendor Integration |

**Candidate:** "So like for Sun State Ford, it shows 6 days in the current state — what I'd want to see is dealers in states after integration and see that they were actually taking that long before getting into the next state.

Also check out Gullo Ford of Conroe — it was created and put directly into Integration Setup 16 days ago. Did this get abandoned? There's one line of activity — 'abdelrahman created the issue 16 days ago' — and nothing since.

Definitely some weird stuff going on."

**Interviewer:** "So what does that tell you about the data we were looking at?"

**Candidate:** "It's not super dependable. I would've imagined we'd see it in a sequence starting from TODO to go into INTAKE sequentially.

So I think we would need to work with operational leadership to make sure that we follow the rules so our observability actually tells the full picture."

**Interviewer:** "That's exactly right. The data is only as good as the process discipline. If someone creates a ticket and drops it straight into Integration Setup — skipping earlier statuses — then cycle time numbers for those stages are meaningless. How would you solve that?"

**Candidate:** "I'm not sure if Linear allows it, but with Jira they had rigid workflows or sequences we could define that tell us which state we could move things to and from. At least having that should add some structure. It's more of protecting people and guiding them so that it's a pit of success."

**Interviewer:** "Linear doesn't have that actually. It's more flexible — you can move a ticket from any status to any other. So if we can't enforce it at the tool level, what else could you do?"

**Candidate:** "Yeah I mean this would get solved by HubSpot creating the ticket in TODO and then we could come up with some ways to automatically move it across states.

For example if we auto sent the email for intake and the intake form was like a web app, we could check to see when all fields were filled and transition the ticket to the next state which is Dashboard Setup. We could auto-configure dashboard accounts for people using the contacts in HubSpot, we could also take emails if that's part of the intake process and automatically configure the dashboard and then move it to the Integration Setup state. And maybe we could automate that? Not sure which parts require humans in the loop."

---

## Phase 3: Solve the Bottleneck (20 min)

**Interviewer:** "You're basically saying: instead of relying on people to move tickets, make the system move tickets based on things actually happening. The ticket moves because the intake form was completed, not because Waqar remembered to drag it.

Let's zoom into Integration Setup since it's the biggest bottleneck. The delay is mostly on the dealership side — they have to do things in their existing systems. Accept invites, configure settings, give us access. And they drag their feet. What would you do about that?"

**Candidate:** "Do all integrations follow the same steps? Can you walk me through an example of what one has to do end to end?"

**Interviewer:** "Good question. No, they're different. Take CDK — the dealership has to log into their admin portal, accept an integration invite, configure some settings, give us an API key. Steps 1 through 4 are all on the dealer. Sometimes they do it in a day, sometimes they don't touch it for three weeks.

Tekion is simpler, fewer steps, goes faster. Reynolds & Reynolds involves a third-party vendor too — so now you're waiting on the dealer AND the vendor."

**Candidate:** "Yeah that's super interesting. So the way I'd probably tackle this is in slices. You can't and don't want to boil the ocean.

We'd use the observability layer and determine which of these are a problem and start with the ones that really take long and try to understand why.

I think in the most ideal version of this we see which APIs or ways we can do this stuff programmatically. Like can we send the integration invite to them programmatically? When they respond can we auto update the configs with the creds? And then the other part is making it stupid simple for them to do their jobs — so guides for each integration on 'what you need to do in order to enable Pam' with screenshots and whatever else to make their lives easy. That'll bring onboarding time down.

When people don't respond we should configure sequences to remind them. Similar to HubSpot sequences and workflows where people are reminded after inactivity."

**Interviewer:** "One thing I want to push on — you said 'start with the ones that really take long.' How would you decide which integration to tackle first? If CDK is slow but it's only 10% of our dealers, and Tekion is faster but it's 60% of our volume — does that change the priority?"

**Candidate:** "Yeah it does. I think we'd need to see average time, but then also total time that our OPS team is spending on those dealers."

**Interviewer:** "Right — because a fast integration that touches 60% of volume might still be eating more total OPS hours than the slow one at 10%.

Alright — last question. Let's say it's your first week. You walk in Monday. What do you actually do? What do you ship?"

**Candidate:** "I think it's important to ship quickly but also make sure it's toward your ideal direction.

So I'd take like maybe a day to fully understand the bottlenecks and problem and have an idea of directionally where I'd want to go. I'd check to see if our observability was good — based on what I saw in Linear it's a good start — and then I'd see which is a really big bottleneck, like the integrations issue. I would deep dive the tickets and see if there are any easy wins, something like send a Tekion guide to Tekion customers because the guide is simple and I'd get a win that way and build something I could easily iterate on for other integrations.

Also if in my deep dive I don't find any low-hanging fruit I can take a step back and probably do the HubSpot to Linear integration. That level of standardization I think would be valuable from the jump.

My goal would be to ship both of those things and maybe iterate on the integration piece a couple of times in my first week."

**Interviewer:** "That's a solid answer. You're not building infrastructure for the sake of it — you're picking something that delivers value immediately and is extensible. Thanks for walking through this with me."

---

## Post-Interview Notes

### Key Signals

- ✅ First instinct was to ask "is there actually a problem?" before solutioning
- ✅ Asked about the current process before designing anything
- ✅ Discovered Linear through the conversation naturally — not told to use it
- ✅ Connected that Linear statuses give cycle time for free (workflow = observability)
- ✅ Thought through tradeoffs between Google Sheets tooling vs Linear, acknowledged change management with Waqar
- ✅ Proposed integration type as a label for segmentation
- ✅ Instinct to spot-check the data — didn't take cycle time numbers at face value
- ✅ Caught data quality issues (Gullo Ford skipping statuses, zero activity for 16 days)
- ✅ Named the core tension: "observability only works if the process is followed"
- ✅ Proposed automation as the solution to process discipline (system moves tickets, not people)
- ✅ Asked for integration walkthrough before proposing a solution — didn't assume
- ✅ Thought about both sides: automate our end + make the dealer's part easier (guides, sequences)
- ✅ Week 1 answer was pragmatic: quick win (integration guide) + foundation (HubSpot → Linear)

### Areas That Could Go Deeper

- Mentioned RICE but didn't fully apply it when choosing which integration to tackle first — got there when pushed
- Guides + reminder sequences is solid but didn't explore what happens when a dealer replies with questions (agent concept)
- Didn't dig into the different BLKD labels on tickets (Pam Integration vs Vendor Integration = different root causes)

### Vote: Strong Yes

### What Made Them Strong

They start with diagnosis, not prescription. Every phase began with questions — "is there actually a problem?", "what does onboarding look like?", "do all integrations follow the same steps?" They didn't propose a solution until they understood the system. And when they saw data that didn't make sense, their instinct was to go look at the actual tickets rather than theorize.
