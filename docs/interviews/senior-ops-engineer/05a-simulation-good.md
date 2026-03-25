# Simulation: Good Candidate

**Format:** Live call, screenshare. Haroun + Omer interviewing. ~60 min.

---

## Phase 1: Build the Pipeline (18 min)

**Haroun:** "Deals close in HubSpot. Right now, onboarding is kicked off manually — someone creates tasks, sends emails, tracks things in spreadsheets. How would you automate the start of this?"

**Candidate:** "Before I get into a solution — what happens today after a deal closes? Like, who does what?"

**Haroun:** "Waqar on our OPS team sees the deal close. He creates a bunch of tasks manually, pings people on Slack, tracks everything in a spreadsheet. He's the one making sure nothing falls through the cracks."

**Candidate:** "Got it. So Waqar is the system right now. How many deals are closing per month?"

**Haroun:** "30-40."

**Candidate:** "Yeah, that's not gonna scale with one person tracking spreadsheets. Okay, so the first thing I'd want is a trigger — HubSpot deal moves to Closed Won, that fires a webhook. The question is what does that webhook create and where. What does your team use for project management?"

**Haroun:** "Linear for engineering. OPS is on the spreadsheets."

**Candidate:** "So the move is to get OPS onto Linear for onboarding. When a deal closes, we auto-create a Linear ticket for that dealership. The ticket represents the full onboarding — and each step in the onboarding process is a status the ticket moves through.

What's nice about that is you don't need a separate dashboard to track how onboarding is going. Linear already measures how long a ticket sits in each status. So if you set up the statuses right — intake, setup, testing, go-live, whatever the actual steps are — you get cycle time per stage just from the team doing their job and moving tickets."

**Haroun:** "What data would you pull from HubSpot into the ticket?"

**Candidate:** "Dealership name, primary contact info, deal owner — the basics. But honestly I'd want to know: is onboarding the same for every customer? Or are there different types of customers that go through different paths?"

**Haroun:** "Good question. Each dealership uses a different integration — think of it like different software providers. Some take 24 hours to set up, some take 2-3 weeks. That's on the HubSpot deal."

**Candidate:** "Okay, that's critical. So I'd pull the integration type and use it to template the ticket. A dealership on the fast integration gets a ticket with expected timelines that reflect that. A dealership on the slow one gets a different set of expectations baked in. Maybe even different statuses or subtasks depending on what the integration requires.

I'd also want that integration type as a label on the Linear ticket so we can filter and compare later — are all our slow onboardings on the same integration? That's useful data."

**Haroun:** "Would you do one ticket per dealership, or multiple tickets?"

**Candidate:** "I'd start with one ticket that moves through statuses. It's simpler and it gives you the cycle time view immediately — you can see exactly where each dealership is and how long they've been there. If we find later that different people own different steps and need their own tickets, we can add subtasks. But start simple, get the data flowing, iterate."

**Haroun:** "Okay, so what are the statuses? Walk me through the pipeline — what does a dealership go through from deal close to live?"

**Candidate:** "That's exactly what I need to figure out. I don't know your onboarding process — can you walk me through it? Like, what are the actual steps that happen between 'they signed' and 'they're live'?"

**Haroun:** "Sure. First someone on OPS takes the intake — confirms the deal info, reaches out to the dealership, collects any missing details. Then we set up their dashboard. Then there's the integration piece — connecting to their existing systems. Then we enable some feature flags in our system. Then we test everything. Then we give them their number and they're live."

**Candidate:** "Okay, so that's roughly six steps. Let me map those to statuses...

The first one is the intake — I'd call that something like 'Intake Requested.' The ticket gets auto-created when the deal closes, and it lands in this status. OPS picks it up, reaches out to the dealer, gets whatever they need. When they have everything, they move it forward.

Next is dashboard setup. That sounds like it's on us — internal work. So 'Dashboard Setup.' Someone on the team does the config, moves the ticket when it's done.

Then integration — 'Integration Setup.' This is the one that probably takes a while, right? Because it involves the dealer's systems."

**Haroun:** "Yeah, that's the slow one. Third parties are involved too."

**Candidate:** "Makes sense. So the ticket could sit in Integration Setup for a while. That's fine — that's exactly the kind of thing we want to measure. If I can see that tickets spend 2 days in Dashboard Setup but 15 days in Integration Setup, that tells me where the problem is.

After integration... you said feature flags. 'Enable Flags' — that's probably someone on engineering or OPS flipping switches once the integration is confirmed working?"

**Haroun:** "Yeah, exactly."

**Candidate:** "Then testing — 'Testing.' Someone verifies end-to-end that everything works. And then the final status would be something like 'Number Communicated' or 'Live' — the dealer has their number and is taking calls.

So the pipeline is: **Intake Requested → Dashboard Setup → Integration Setup → Enable Flags → Testing → Number Communicated.**

One thing I'm wondering — do you need a 'Blocked' status? Like, if a ticket is in Integration Setup but we're waiting on a third party and there's nothing we can do, does it stay in Integration Setup or does it move to some kind of waiting state?"

**Haroun:** "Good question. What would you do?"

**Candidate:** "I'd be careful with that. If you add a 'Blocked' status, the cycle time for Integration Setup will look artificially fast because you pulled the waiting time out of it. You'd be hiding the bottleneck in the data.

I think the better approach is to keep the ticket in Integration Setup even when it's blocked, but add a label or tag — 'blocked: waiting on dealer' or 'blocked: waiting on third party.' That way the cycle time for Integration Setup reflects reality — it actually takes 15 days — but you can still filter to see how much of that is active work vs waiting.

If you split it into a separate status, someone looking at the data later might think Integration Setup is only 3 days and miss the real problem."

**Haroun:** "That's interesting. We actually do have a Blocked status right now."

**Candidate:** "Is it showing up as a big chunk of time?"

**Haroun:** "Yeah, 3 weeks."

**Candidate:** "That's what I was worried about. So the real Integration Setup time is probably 15 days plus some portion of that 3-week Blocked time. The Blocked status is absorbing time that should be attributed to the stage where the work is actually stuck. You're masking where the pain is.

I'd probably keep Blocked as an option for now since the team is used to it, but I'd want to track it carefully. Every time a ticket moves to Blocked, the reason should be captured — is it the dealer, a third party, waiting on internal work? Over time, that data tells you whether Blocked is mostly an integration problem, a testing problem, or something else."

**Haroun:** "What about In Review? Like, before we give the dealer their number, someone reviews everything."

**Candidate:** "I'd add that between Testing and Number Communicated. 'In Review' — final sign-off before go-live. Who does the review?"

**Haroun:** "Usually Waqar or someone senior on OPS."

**Candidate:** "Got it. So the full pipeline is:

**Intake Requested → Dashboard Setup → Integration Setup → Enable Flags → Testing → In Review → Number Communicated**

With Blocked as a status a ticket can enter from any stage, tagged with the reason. And every ticket gets a label for integration type so we can slice the data later.

The nice thing is, once this is running, you don't need me to build you a dashboard. Linear will show you: here's how long tickets sit in each status, here's where they pile up, here's your P50 and P95 for each stage. That's your onboarding health report — and the team generates it just by doing their job and moving tickets."

---

## Phase 2: Read the Bottlenecks (17 min)

**Haroun:** "Alright, so imagine we built what you described and it's been running for a few months. You said you'd want to know if onboarding is getting faster. How would you figure that out?"

**Candidate:** "I'd look at the cycle time data per status. Which stages are tickets sitting in the longest? Is there one stage that's consistently the bottleneck? And is it getting better or worse over time — like, are our last 10 onboardings faster than our first 10?"

**Haroun:** *[Screenshares the Integration Setup pipeline screenshot]* "Here's what we see."

**Candidate:** "Okay, let me read this... So these are statuses on the left, and then P50, P75, P95 — that's median, 75th percentile, 95th percentile for how long tickets spend in each status. Sample size is 4 issues, so small, but let's see what it says.

Todo is 19 hours median — that's fine, basically same day. Intake Requested is 11 days — that's already a while. Dashboard Setup is 10 days. Then... Integration Setup is 15 days median, 3 weeks at P75. Enable Flags is 4 weeks. Testing is 18 days. And Blocked is 3 weeks just sitting there.

The obvious ones are Enable Flags at 4 weeks and Integration Setup at 15 days. Those are the killers. But Blocked is interesting too — 3 weeks where nothing is happening. What does 'Blocked' mean? Is that waiting on someone?"

**Haroun:** "Yeah, Blocked is when we're waiting on a third party or the dealership to do something and we can't move forward."

**Candidate:** "So Blocked isn't really a step — it's a symptom. Tickets land there when something upstream got stuck. That probably overlaps with why Integration Setup is slow too. Is the delay on our side or the dealership's side?"

**Haroun:** "It's the dealership. They have to do stuff in their system — accept invites, configure settings, give us access. They drag their feet."

**Candidate:** "Classic. So the bottleneck isn't technical — it's the customer not doing their part. That changes what the solution looks like. This isn't a 'write better code' problem, it's a 'how do we get the customer to move faster' problem."

**Haroun:** "What about Enable Flags at 4 weeks?"

**Candidate:** "That one I'd want to understand better. Is that us being slow, or is it also waiting on something? Because 4 weeks at P50 for what sounds like flipping some switches... that feels like it's either blocked by a dependency from a previous step, or it's just sitting in a queue and nobody's getting to it. Which is it?"

**Haroun:** "Bit of both. Sometimes it's waiting on integration to fully complete, sometimes it's just that the team hasn't gotten to it."

**Candidate:** "So two different problems. One is a dependency issue — can't enable flags until integration is done, so the clock runs while it's waiting. The other is a capacity issue — it's ready but nobody's picked it up. Those have different solutions. The dependency one you solve by fixing the upstream bottleneck. The capacity one you might solve with automation or just better alerting — ticket's been ready for 48 hours, ping someone."

---

## Phase 3: Automate the Bottleneck (22 min)

**Haroun:** "So Integration Setup is 15 days because the dealership drags their feet. What would you do about it?"

**Candidate:** "Well, first instinct is a process fix. Do we have someone who calls the dealer and walks them through it? Holds their hand through the setup?"

**Haroun:** "We do that when we can. But at 30-40 new dealers a month, that's a lot of hand-holding."

**Candidate:** "Right, people scale linearly. So the question is — can I take what that person does on the phone and turn it into something automated?

Here's what I'd do. The moment a ticket enters Integration Setup, an agent sends the dealer a personalized email. Not a generic 'please complete your setup' — a step-by-step walkthrough specific to their integration type. 'You're on [X integration]. Here's exactly what you need to do: Step 1, go here, click this. Step 2, enter these credentials. Step 3, accept the invite we sent to this email.' Screenshots, links, the works.

The key is it has to feel like a person sent it, not a system notification they'll ignore."

**Haroun:** "What if they get stuck? What if they reply to the email with questions?"

**Candidate:** "That's the interesting part. If they reply, the agent should be able to handle it. Most of the questions are probably the same — 'I don't see the invite,' 'what credentials do I use,' 'I got an error on step 3.' If the agent has a knowledge base of common setup issues per integration type, it can respond to most of those.

But you need a fallback. If the agent can't answer the question — something it hasn't seen before, or the dealer is frustrated and wants a person — it escalates. Maybe it says 'let me loop in someone from our team' and creates a subtask or pings Slack. Or it offers to schedule a call: 'Would it help if one of our team walked you through this? Here are some times.'

The worst outcome is a dealer stuck for days with no response. The agent should either solve it or get a human involved within a few hours."

**Haroun:** "How would you know if this is actually working?"

**Candidate:** "The most direct measure is cycle time for Integration Setup. If it drops from 15 days to, say, 5 days after we turn on the agent, that's the signal. But I'd want to go deeper.

I'd look at it in stages. How many dealers complete setup after just the first email, no replies needed? That tells me how good the instructions are. How many need back-and-forth with the agent? That tells me where the instructions are unclear. How many escalate to a human? That tells me the limits of the automation.

If most dealers complete after the first email, the instructions are great. If most need 3-4 replies, the instructions need work. If most escalate to a human, the agent isn't ready and we should rethink."

**Haroun:** "Do all integrations take the same amount of time?"

**Candidate:** "Probably not, right? Some are probably way faster than others. Can I see that in the data — like, can I filter the cycle time by integration type?"

**Haroun:** "We don't have that label on the tickets."

**Candidate:** "Oh. So right now every onboarding ticket looks the same — we can't tell if a 3-week onboarding is slow because of the dealer, or normal because they're on an integration that just takes that long.

I'd want to fix that. First, I'd go back and tag the existing tickets with their integration type — that's a backfill, probably not that many tickets, and we'd get historical data to compare. Then going forward, every new ticket gets auto-tagged with the integration type from HubSpot. That should already be happening since we're pulling it in Phase 1 anyway.

Once we have that, we can set different expectations per integration. A CDK onboarding that takes 3 weeks might be normal. A fast-integration onboarding that takes 3 weeks is a problem. Right now we can't tell the difference."

**Haroun:** "How would you roll this out? Do you turn it on for everyone?"

**Candidate:** "No. I'd pick one integration type — probably the highest-volume one — and run it there first. See if the agent emails help, see if cycle time drops, work out the bugs. If it works, expand to the next integration type. Each one might need its own instructions, its own FAQ for the agent, so it's not just flipping a switch.

I'd also want to check with OPS before rolling it out. They know the actual pain points — which integration is the biggest headache, which dealers need the most hand-holding. They'll tell me if my instructions are wrong."

**Haroun:** "What would you ship in Week 1?"

**Candidate:** "Honestly? The HubSpot → Linear pipeline. That's the foundation — everything else depends on having tickets with the right data flowing through the right statuses. It's not glamorous, but it's the thing that unblocks everything else.

If I have time in Week 1, I'd also tag the existing onboardings with their integration type and pull the cycle time data. Even before any automation, just having visibility into 'CDK onboardings take 3x longer than Tekion' is valuable. It changes how the team sets expectations with dealers."

---

## Post-Interview Notes

### Best Thing They Said
"The workflow tool is the observability tool" — connected that Linear statuses give you cycle time for free without building dashboards.

### Biggest Concern
None significant. Would want to validate they can actually ship the HubSpot integration (hands-on technical), but their thinking is exactly right.

### Vote: Strong Yes

### Key Signals
- ✅ Asked clarifying questions before designing (what happens today, who does what, how many deals)
- ✅ Discovered Linear through questions, didn't assume tools
- ✅ Connected workflow = observability unprompted
- ✅ Asked about different customer paths without domain knowledge
- ✅ Read the pipeline data accurately, identified the right bottlenecks
- ✅ Distinguished between different root causes (customer delay vs capacity vs dependency)
- ✅ Climbed the full ladder: process → agent → edge cases → measurement → segmentation → data gaps
- ✅ Proposed backfilling integration labels and making it a new process
- ✅ Pragmatic rollout (one integration type first, talk to OPS)
- ✅ Week 1 answer was the foundation, not the flashy thing

### What Made Them Great
They think in loops. Every solution came with "how would I know if this works" and every measurement came with "what would I do differently based on what I learn." They didn't just solve the problem — they built the system to keep solving it.
