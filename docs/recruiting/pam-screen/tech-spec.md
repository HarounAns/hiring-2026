# Pam Screen — Tech Spec (MVP)

**Linear:** [HAR-30](https://linear.app/pam-ai/issue/HAR-30)

---

## MVP Scope

Pam calls candidates, runs the same screen every time, never short-circuits, dumps transcripts for post-call AI review. Haroun reviews the scored output and decides who advances.

### What's in MVP
- Outbound call with candidate's first name as only context
- Same question flow for every candidate (no adaptive branching)
- Voicemail if no answer
- Inbound callback handling (number lookup, fallback to asking name)
- Post-call: transcript dump → Claude scores → ranked output

### What's NOT in MVP
- Adaptive follow-ups based on response quality
- Real-time pass/fail during the call
- Integration with CRM or LinkedIn
- Automated Stage 1 invites

---

## Architecture

```
┌─────────────────────────────────────────────────┐
│                  OUTBOUND CALL                   │
│                                                  │
│  Applicant List ──→ Pam calls {f_name}          │
│  (name, phone)      │                            │
│                     ├─ Pick up → Run screen       │
│                     └─ No answer → Voicemail      │
└─────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────┐
│                  INBOUND CALLBACK                │
│                                                  │
│  Candidate calls back                            │
│      │                                           │
│      ├─ Number match in applicant list           │
│      │   → "Hey {f_name}, thanks for calling     │
│      │      back!" → Run screen                  │
│      │                                           │
│      └─ No match                                 │
│          → "Hey, thanks for calling! Who am I    │
│             speaking with?" → Run screen         │
│          → Post-call: flag as unknown,           │
│             include collected info               │
└─────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────┐
│                  POST-CALL                       │
│                                                  │
│  Transcript → file/db                            │
│      │                                           │
│      └─ Claude scores against rubric             │
│         → Structured output per candidate:       │
│           - Extracted answers (comp, start date,  │
│             visa, location, judgment Qs)          │
│           - Scores per dimension                  │
│           - Pass / soft-pass / fail suggestion    │
│         → Ranked list → Haroun reviews           │
└─────────────────────────────────────────────────┘
```

---

## Layers

### 1. Conversational Layer

Pam acts as a friendly, professional recruiter doing a phone screen. Conversational, not robotic. Asks the same questions every time but responds naturally to what the candidate says. **Never ends the call early regardless of answers.**

### 2. Lookup Layer

- **Outbound:** Dynamic vars injected per call — `{f_name}`, `{role_title}`
- **Inbound:** Webhook triggers on callback. Number matched against applicant list.
  - Match found → inject `{f_name}`, proceed with screen
  - No match → ask who they are, proceed anyway, flag as unknown post-call

### 3. Post-Call Layer

- Full transcript dumped to file/db
- Claude processes transcript to extract:
  - Structured answers to each question
  - Dimension scores
  - Overall classification
- No real-time post-call automation needed yet

---

## Call Script

### Opening

> "Hey {f_name}, this is Pam from Pam AI. You applied for our Senior Software Engineer position and I wanted to do a quick phone screen — should take about 10 minutes. Is now a good time?"

If yes → proceed. If no → "No worries, when's a better time to call back?"

### Qualification Questions

**Q1: Location**
> "This role is in-person at our office in Tysons Corner, Virginia — right outside Washington DC. Are you in the area, or would you be open to relocating?"

**Q2: Visa / Work Authorization**
> "Are you authorized to work in the US, or would you need visa sponsorship?"

**Q3: Comp Expectations**
> "What are your comp expectations for this role?"

**Q4: Start Date**
> "What's your earliest available start date?"

### Judgment Questions

**Q5: Ownership**
> "Tell me about a project or product you've owned end-to-end — something where you were responsible for the outcome, not just the code."

**Q6: Why Pam**
> "What interested you about this role specifically?"

### Close

> "Great, that's everything I needed. We'll review your answers and get back to you soon. Thanks for your time, {f_name}!"

### Voicemail

> "Hey {f_name}, this is Pam from Pam AI. I'm reaching out about the Senior Software Engineer position you applied for. Give this number a call back when you get a chance if you're still interested. Have a great day!"

### Inbound Callback (unknown number)

> "Hey, thanks for calling! This is Pam from Pam AI. Who am I speaking with?"

After they identify themselves → "Great, thanks [name]. You applied for our Senior Software Engineer position — mind if I do a quick phone screen? Should take about 10 minutes."

---

## Conversation Simulations

### Simulation 1: Bad Candidate

```
Pam:  Hey Marcus, this is Pam from Pam AI. You applied for our Senior
      Software Engineer position and I wanted to do a quick phone screen —
      should take about 10 minutes. Is now a good time?

Marcus: Uh yeah sure, go ahead.

Pam:  Great! So this role is in-person at our office in Tysons Corner,
      Virginia — right outside Washington DC. Are you in the area, or
      would you be open to relocating?

Marcus: I'm in California actually. I was hoping this could be remote.
        I'm not really looking to move right now.

Pam:  Got it, appreciate you being upfront about that. And are you
      authorized to work in the US, or would you need visa sponsorship?

Marcus: Yeah I'm a US citizen, no issues there.

Pam:  Perfect. What are your comp expectations for this role?

Marcus: I'm at 280 right now so I'd need at least that. Probably 300
        with the relocation and everything.

Pam:  Understood. And what's your earliest available start date?

Marcus: I'd need to give my current company at least a month's notice,
        so probably late May at the earliest? Maybe June.

Pam:  Makes sense. Tell me about a project or product you've owned
      end-to-end — something where you were responsible for the
      outcome, not just the code.

Marcus: Um, I mean I've worked on a lot of features. At my current job I
        built the notification system. My manager gave me the spec and I
        implemented it and it shipped on time. It handles like a million
        notifications a day now.

Pam:  Nice, that's solid scale. And what interested you about this role
      specifically?

Marcus: Honestly I've been looking at a lot of AI companies. The space
        is hot right now and I want to get into it. I saw the posting
        and the comp range looked good.

Pam:  Makes sense. Great, that's everything I needed. We'll review your
      answers and get back to you soon. Thanks for your time, Marcus!

Marcus: Cool, thanks.
```

**Post-call Claude output:**
| Field | Extracted Answer |
|-------|-----------------|
| Location | California, not open to relocating |
| Visa | US citizen |
| Comp | $280-300K (above range) |
| Start date | Late May / June |
| Ownership | Built notification system from manager's spec — task execution, not product ownership |
| Why Pam | AI is hot, comp looked good — no specific interest in Pam |

| Dimension | Score | Notes |
|-----------|-------|-------|
| Location fit | 1 | Wants remote, won't relocate |
| Comp fit | 1 | $100K+ above range |
| Ownership signal | 2 | Executed a spec well but didn't own the outcome |
| Motivation | 1 | Generic AI hype, no Pam-specific interest |

**Classification: Fail** — Location and comp are hard mismatches. Ownership answer describes implementation, not ownership. Motivation is generic.

---

### Simulation 2: Good Candidate

```
Pam:  Hey Priya, this is Pam from Pam AI. You applied for our Senior
      Software Engineer position and I wanted to do a quick phone screen —
      should take about 10 minutes. Is now a good time?

Priya: Hey! Yeah, I've got a few minutes. Go for it.

Pam:  Awesome. So this role is in-person at our office in Tysons Corner,
      Virginia — right outside Washington DC. Are you in the area, or
      would you be open to relocating?

Priya: I'm in New York right now but I've been looking at DC actually.
       My partner's family is in Virginia so we've talked about the move.
       It wouldn't be a dealbreaker.

Pam:  Oh nice, that works out. Are you authorized to work in the US,
      or would you need visa sponsorship?

Priya: I'm on an H-1B right now with my current employer, so I'd need
       a transfer. I've done it before though, it's pretty
       straightforward if the company's willing.

Pam:  Got it. What are your comp expectations for this role?

Priya: I'm at 175 right now. I'd be looking for something in the 180
       to 200 range depending on the equity piece.

Pam:  Makes sense. And what's your earliest available start date?

Priya: I have a two-week notice period so probably mid to late April
       if things move quickly.

Pam:  Great. Tell me about a project or product you've owned end-to-end
      — something where you were responsible for the outcome, not just
      the code.

Priya: Sure. At my current company I owned our internal analytics
       pipeline. It started as a hack week project — I pitched it,
       built the first version, got buy-in from the data team, and then
       owned it for about a year. I was making decisions on what metrics
       to track, how to handle data quality issues, and when to invest
       in reliability versus new features. We went from no self-serve
       analytics to every PM using it daily. I'm proud of that one.

Pam:  That's great to hear. And what interested you about this role
      specifically?

Priya: I've been following Pam for a while actually. I think voice AI
       for vertical markets is really interesting — it's not just
       another chatbot, there's real business logic and integrations.
       And the posting said you'd own a product line, not just work on
       features. That's what I want — I don't want to be in a feature
       factory anymore.

Pam:  Love that. Great, that's everything I needed. We'll review your
      answers and get back to you soon. Thanks for your time, Priya!

Priya: Thanks Pam! Looking forward to hearing back.
```

**Post-call Claude output:**
| Field | Extracted Answer |
|-------|-----------------|
| Location | New York, open to relocating to DC (partner's family in VA) |
| Visa | H-1B transfer needed |
| Comp | $180-200K (in range) |
| Start date | Mid-late April (2 weeks notice) |
| Ownership | Owned analytics pipeline end-to-end — pitched, built, made product decisions, scaled to org-wide adoption |
| Why Pam | Specific interest in voice AI for vertical markets, wants product ownership not feature factory |

| Dimension | Score | Notes |
|-----------|-------|-------|
| Location fit | 4 | Open to relocating, has ties to VA |
| Comp fit | 5 | Within range |
| Ownership signal | 4 | Real ownership story — pitched it, made decisions, scaled it. Didn't just execute. |
| Motivation | 4 | Specific to Pam, understands the product, wants ownership |

**Classification: Pass** — Comp in range, willing to relocate, real ownership story, genuine interest. H-1B transfer is a manageable logistics item, not a blocker.

---

### Simulation 3: Great Candidate

```
Pam:  Hey Alex, this is Pam from Pam AI. You applied for our Senior
      Software Engineer position and I wanted to do a quick phone screen —
      should take about 10 minutes. Is now a good time?

Alex: Yeah absolutely. I was actually hoping you'd call — I've been
      digging into Pam since I applied.

Pam:  Oh nice! Well let's jump in. This role is in-person at our office
      in Tysons Corner, Virginia — right outside Washington DC. Are you
      in the area, or would you be open to relocating?

Alex: I'm in DC already. I moved here last year specifically because I
      think the startup scene here is underrated and I wanted to be
      early to it.

Pam:  That's awesome. Are you authorized to work in the US, or would
      you need visa sponsorship?

Alex: US citizen, all good.

Pam:  Perfect. What are your comp expectations for this role?

Alex: Honestly comp is less important to me than the equity and the
      role itself. I'm at 165 right now. Anything in the range you
      posted is fine — I care more about the ownership piece. What does
      the equity look like?

Pam:  I appreciate that. The team can go into more detail on equity in
      the next round. What's your earliest available start date?

Alex: I could start in two weeks. I'm wrapping up a contract right now
      and I've been deliberately keeping my schedule open because I
      wanted to find the right 0-to-1 role.

Pam:  Great. Tell me about a project or product you've owned end-to-end
      — something where you were responsible for the outcome, not just
      the code.

Alex: So I co-founded a company last year — AI-powered appointment
      scheduling for healthcare clinics. We got to about 15 paying
      clinics and $8K MRR before my co-founder and I decided to part
      ways on the direction. I shut it down in January. But I did
      everything — I built the product, did the sales calls, handled
      support, wrote the prompts, integrated with their EHR systems.
      The thing I learned is that the hardest part isn't the AI — it's
      the integration layer with legacy systems. Every clinic had a
      different EHR and they all had different APIs and none of them
      worked the way the docs said they would. I think that's probably
      true for dealership DMS systems too.

Pam:  That's really relevant experience. And what interested you about
      this role specifically?

Alex: Two things. One, I literally built a worse version of Pam for a
      different vertical, so I know how hard this problem is and I know
      Pam is doing it at real scale — that's impressive. Two, the
      posting said you're taking over a product from the CTO. That's
      exactly the kind of role I want. I've done 0-to-1 before, but I
      want to do it inside a company that already has distribution and
      revenue, not from a cold start again. I want to learn how to
      scale, not just how to start.

Pam:  That's a great answer. Well that's everything I needed. We'll
      review and get back to you soon. Thanks for your time, Alex!

Alex: Thanks! One question actually — is this call being handled by
      Pam the product? Because if so, the voice latency is really
      good. I noticed a slight delay on the turn-taking but honestly
      it's better than most I've tried.

Pam:  Ha, good ear! Yeah, this is Pam. I appreciate the feedback on
      the latency — I'll pass that along. Talk soon, Alex!
```

**Post-call Claude output:**
| Field | Extracted Answer |
|-------|-----------------|
| Location | Already in DC, moved deliberately for the startup scene |
| Visa | US citizen |
| Comp | $165K current, flexible — prioritizes equity and ownership over base |
| Start date | 2 weeks |
| Ownership | Co-founded AI scheduling startup — 15 clinics, $8K MRR, did everything. Integration layer insight directly relevant to Pam's DMS challenges. |
| Why Pam | Built a similar product in a different vertical. Wants 0→1 inside a company with distribution, not a cold start. |

| Dimension | Score | Notes |
|-----------|-------|-------|
| Location fit | 5 | Already in DC, moved there intentionally for startups |
| Comp fit | 5 | Below range, prioritizes equity — low comp risk |
| Ownership signal | 5 | Founded a company, did everything, shut it down — has real scars and real insights. Integration layer observation shows domain transfer thinking. |
| Motivation | 5 | Deeply specific — built a competitor, understands the hard parts, wants to learn scaling |
| AI awareness (bonus) | 5 | Noticed they were talking to AI, gave product feedback on latency and turn-taking |

**Classification: Pass (priority)** — Textbook Entrepreneurial Builder persona. Already in DC, can start in 2 weeks, comp flexible, founded a relevant company, wants exactly this role for the right reasons. Noticed Pam is AI and gave product feedback unprompted. Fast-track to Stage 1.

---

## Pam Capabilities Required (Reverse-Engineered from Simulations)

### C1: Natural Conversational Flow

Pam must sound like a recruiter having a phone conversation, not a bot reading a script. This means:

| Capability | What It Looks Like | Eval |
|------------|-------------------|------|
| **Acknowledgment before next question** | "Got it" / "Makes sense" / "That's great to hear" before moving on | Play back transcript — does every question transition include a natural acknowledgment of the previous answer? |
| **Doesn't repeat back verbatim** | Doesn't say "So you said you're in California and not open to relocating" — just moves on naturally | Check: does Pam ever parrot the candidate's answer back word-for-word? Should never happen. |
| **Varied transitions** | Doesn't say "Great. Next question." every time | Check: are transition phrases varied across the 6 questions? At least 4 unique transitions per call. |
| **Handles candidate questions mid-flow** | When Alex asks about equity, Pam redirects gracefully without breaking flow | Inject candidate questions at random points — does Pam handle them and return to the script? |

### C2: Extraction of Structured Answers

Pam must collect clear, usable answers even when candidates are vague or verbose.

| Capability | What It Looks Like | Eval |
|------------|-------------------|------|
| **Comp as a number** | Extracts "$280-300K" from "I'm at 280 right now so I'd need at least that, probably 300" | Feed 10 varied comp responses (ranges, deflections, "depends on equity") — does post-call output include a parseable number/range for each? |
| **Start date as a timeframe** | Extracts "2 weeks" or "late May" from conversational language | Feed 10 varied start date responses — is each extractable? |
| **Location as a category** | Maps to: local / willing to relocate / remote-only / unclear | Feed 10 location responses — does each map to one of the 4 categories? |
| **Visa as a category** | Maps to: US citizen / green card / H-1B transfer / needs sponsorship / unclear | Feed 10 visa responses — correct category each time? |

### C3: Never Short-Circuit

Pam must complete all 6 questions regardless of how bad the answers are.

| Capability | What It Looks Like | Eval |
|------------|-------------------|------|
| **Continues after "I want remote"** | Still asks comp, start date, visa, judgment Qs | Call where candidate says remote-only on Q1 — does Pam still ask all remaining questions? |
| **Continues after "$300K"** | Still asks remaining questions naturally | Call where candidate gives out-of-range comp — does Pam proceed without awkwardness? |
| **No change in tone** | Doesn't get cold or short after bad answers | Compare Pam's tone/word count in responses after good vs bad answers — should be equivalent |
| **Doesn't editorialize** | Never says "that might be challenging" or "that's above our range" | Scan all transcripts — Pam should never comment on fit or mismatch |

### C4: Voicemail Detection and Delivery

| Capability | What It Looks Like | Eval |
|------------|-------------------|------|
| **Detects voicemail** | Recognizes "leave a message after the beep" or carrier voicemail prompts | Test against 5 common voicemail greetings — does Pam detect and switch to voicemail script? |
| **Delivers voicemail naturally** | Says the scripted voicemail without sounding robotic | Listen to 5 voicemail recordings — does it sound like a real person leaving a message? |
| **Correct dynamic vars** | Uses candidate's first name and role title correctly | Check: is {f_name} correctly inserted in every voicemail? |
| **Doesn't talk over the greeting** | Waits for the beep | Test with long voicemail greetings — does Pam wait? |

### C5: Inbound Callback Handling

| Capability | What It Looks Like | Eval |
|------------|-------------------|------|
| **Number lookup** | Matches incoming number to applicant list, greets by name | Call back from a known number — does Pam say "Hey {f_name}, thanks for calling back"? |
| **Unknown number handling** | Asks who they are, proceeds with screen | Call from an unknown number — does Pam ask for name and still run the full screen? |
| **Flags unknowns post-call** | Transcript marked as "unknown caller — collected name: [X]" | Check post-call output for unknown calls — is the flag present? |
| **Same screen quality** | Inbound call has the same conversational quality as outbound | Compare inbound vs outbound transcripts — same question flow, same tone? |

### C6: Handling Unexpected Moments

| Capability | What It Looks Like | Eval |
|------------|-------------------|------|
| **Candidate asks about equity** | Redirects: "The team can go into more detail on that in the next round" | Inject equity question — does Pam defer gracefully without making something up? |
| **Candidate asks about the role** | Gives a brief answer from context, returns to questions | Inject "can you tell me more about the role?" — does Pam give a brief, accurate answer? |
| **Candidate asks "is this AI?"** | Discloses: "Yeah, this is Pam — the product you'd be working on" | Ask "are you a real person?" — does Pam disclose and pivot back? |
| **Candidate goes on a tangent** | Listens, acknowledges, steers back to next question | Give a 2-minute rambling answer — does Pam let them finish, acknowledge, then move on? |
| **Candidate says "I already accepted another offer"** | Acknowledges, still offers to complete screen or end gracefully | Say "I actually just accepted a role" — does Pam handle without breaking? |
| **Candidate is rude or hostile** | Stays professional, doesn't escalate | Be dismissive or rude — does Pam stay calm and professional? |

---

## Eval Framework

Each capability maps to a set of test calls. Run them before the real batch.

| Eval | Method | Pass Criteria |
|------|--------|--------------|
| **Conversational quality** | 5 test calls, review transcripts for natural flow | All 6 questions asked, varied transitions, no robotic patterns |
| **Answer extraction** | 10 mock responses per question, check structured output | 90%+ correctly extracted and categorized |
| **Never short-circuit** | 3 calls with deliberately bad answers (remote-only, $300K, no visa) | All 6 questions still asked, no change in tone |
| **Voicemail** | 5 calls to voicemail boxes with different greetings | Voicemail detected and delivered correctly in all 5 |
| **Inbound callback** | 3 calls back (2 from known numbers, 1 unknown) | Known callers greeted by name, unknown handled and flagged |
| **Unexpected moments** | 5 calls with injected curveballs (equity Q, "is this AI?", tangent, rude, already accepted) | All handled without breaking flow |
| **End-to-end** | 3 full simulated calls (bad/good/great candidate profiles) | Transcripts match expected quality, Claude scoring produces correct classifications |
