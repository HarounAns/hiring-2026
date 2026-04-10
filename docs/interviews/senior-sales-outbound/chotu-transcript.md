# Chotu Interview Transcript

**Call ID:** call_92d83b0cb7655c976a0e075e869
**Agent:** Sales Senior Engineer Interview Practice
**Duration:** 49 minutes
**Date:** 4/5/2026, 11:50:06 AM
**Candidate:** Chotu

---

**User:** Hello? 

**Agent:** Hey Chotu, thanks for taking the time. I'm going to walk you through a scenario based on a real product we're building. I want to see how you think through it — no tricks, just talk me through your reasoning. Sound good?

**User:** Yeah. 

**Agent:** Alright, here's the scenario.

**User:** Okay. So sorry. Let me let me ask some clarifying questions. We're building a dealership lead system So is when you say lead system, this is, like, similar to, like, like, HubSpot CRM. Is that am I is that the right way to think about it? 

**Agent:** Not quite — we're not building the CRM. The dealer already has a CRM. We're plugging into it. We pull leads from their CRM, the AI reaches out via SMS, has a conversation, books an appointment, and then we write everything back to their CRM.

**User:** Got it. Okay. But but we're also do you think it's important to actually build and model the CRM side of things least to understand, like, what it plugs into. Like, for example, like, you know, should do we need to model the lead Do we need to model the customer? Or that outside the scope of this interview? 

**Agent:** Yeah, model it. You need to understand what you're working with — what you're pulling in, what you're writing back. Think of it as your internal representation of the dealer's data.

**User:** Got it. Okay. So let's think about it this way. You know, a a lead hits the CRM with some sort of metadata about what the lead is. So you said things like Cars dot com, OEM manufacturing. Can you explain each lead type or lead source a little bit more in-depth so I can understand what the use cases are for? 

**Agent:** Sure. AutoTrader and Cars.com are third-party listing sites — someone browsed, saw a car they liked, submitted a form. OEM programs are manufacturer-driven — like a Ford incentive program that generates a lead. Walk-ins are people who just showed up at the dealership. Phone calls are inbound calls that get logged as leads. Website leads are from the dealer's own site.

**User:** Yeah. Got it. Okay. It's just helping me understand the problem space. Um, okay. So the idea is this. Right? If use the cars dot com example. So if someone is interested in a vehicle and they submit a form with their contact information, We basically send in a lead, and we say, hey. Um, I'm interested in this car. And then I'm assuming what, Pam calls them immediately or Pam texts them. Like, what exactly is happening? Like, what exactly are we designing? 

**Agent:** We text them. Instantly. The AI — Pam — sends an SMS, has a back and forth conversation, and tries to book an appointment. Test drive, showroom visit, whatever makes sense.

**User:** Got it. Okay. Okay. Got it. So so then I I think that for the entities um, you have think you have so you have a dealership, obviously. Right? That's an entity. You have a a customer who is, like, putting in their metadata. Right? So, like, you you must need my phone number. Maybe you said text. So I I don't know if you also fill in your email, but you said text. So let's just leave it text. You also have a a vehicle of interest in that case. Do all leads have vehicles of interest? Like, the cars dot com would make sense. But then you said also something like walk ins and phone calls. I don't think I don't think that's like a, you know, optional that might be an optional, uh, field, but, like, you could do a vehicle of interest. So you have the lead. You have a dealership. You have a vehicle of interest. You have, like, the actual person. Maybe you call that, like, a contact. 

**User:** I feel like those are probably the main entities Is that correct? 

**Agent:** What about the lead itself — is that the same as the contact, or is it a separate thing?

**User:** Is the lead the same thing as the contact? That's a good question. So a contact is essentially like, who the person is. Right? So if I click in a form, it's gonna take the name my name, Harun Ansari, that's the contact. And I think the idea is that a contact can have multiple leads. Right? Like, I as Harun, I'm sorry, with, like, a primary identifier, of, like, I don't know, phone number maybe is the key identifier. Maybe there's, like, some sort of UUID. I don't know. You might have to do some dedupping. I feel like that's outside the scope. Of our system. Maybe it's not. Right? Like, there's probably some sort of unique identifier for a contact And then the lead like, you can actually have one contact can have many, many leads. Right? So it's a one to many, uh, of leads. So I think they're separate entities. 

**Agent:** What if the same person submits a lead at two different dealerships — are those the same contact?

**User:** Uh, no. I think I think I think that there's, like okay. So there's a a contact belongs to the dealership as well. Right? Like, if I exist at multiple dealerships, think based on the because you ultimately, you're building a CRM for the dealership. Right? Like, the dealership is kind of the main company. I would I believe Like, unless you wanted to do you know, external analysis or whatever like that, I think what makes the most sense is to have, uh, the contact tied to the dealership. And that you could potentially and, like, the world of analytics, go and, like, maybe do, like, a match on the phone number or whatever. 

**User:** For cross customer analytics. But I think what makes the most sense is, like, dealership is the primary entity, and then the contact can be an entity that exists on the dealership level. 

**Agent:** Got it. So what's the lead then — if contact belongs to a dealership, what is the lead on top of that?

**User:** If if contact belongs to a dealership, what is the lead on top of that? The lead is is is like, oh, like, I'm interested in this vehicle. Or, um, you know, I this you know, I have walked into this dealership. So the lead is like, the occurrence or the event you can have lots of those at different times for the, uh, for for our contact. 

**Agent:** Okay. And what's the lifecycle of a lead — what states can it be in?

**User:** Got it. Let's see. So the life cycle of a lead. That is like okay. So there's, like, fresh let me think about, like, at least the end of the spectrum, and then maybe we can think things within in the middle. At the beginning, at the start of a lead, it's like a fresh lead. Right? So a lead can kind of be like, you know, not not, I don't know, active or or some sort of start. And then at the end of it, it's, like, closed with, like I guess, let's think about the terminal states. So a lead can be, like, personally like, it it was successful and that we did what we needed to. And then, like, the person like, let let's take a step back and think about, like, the Cars dot com lead, I guess. In the Cars dot com lead, we basically have, like, closed the person. They have, like, shown up into the dealership and, like, maybe bought a car Honestly, this is more of a question for you because I don't know how to really think about this. Do we need to maintain states like they actually bought a vehicle on the lead Right? Is that, like, a state of like, the lead? Like, if we were to talk about, like, new car purchases, right, So it's like, you first start off in like, a active state. Right? Uh, or, like, you know, this is like a new fresh lead Maybe it's, like, uncontacted. And then the second state is, like, okay. We have, like, reached out to them. Like, sent a message. We sent a text to them, but then they haven't really responded. So that's, like, contacted. And then after that, if they respond, we essentially that's, like, almost like like an engaged state. Right? So, like, we've engaged them, and, uh, they're talking. Like, we continue to have that back and forth, and they're in this engaged state. I think our goal what's our goal? That's a good question. So there there might be this goal to, like, I don't know, maybe get them into the dealership. So maybe there's, like, a maybe it's, like, lead comes in, We send them a text. They respond. We try and either like, answer their questions or whatever. Um, and then they we try and book an appointment with them. Or maybe know, I question for you. Are we just kind of, like, trying to book an appointment? Like, what's the goal? Are we just warming them so that a human can take them? And, you know, do we escalate? Like, can you help me understand the goal of the system? 

**Agent:** The goal is to book an appointment — test drive, showroom visit, trade-in appraisal. Once it's booked, the dealer's sales team takes over. We write everything back to their CRM so they have context.

**User:** Okay. Well, if we're trying to book an appointment, then that's, like, the pause that's, like, the good end state. That's the terminal like, successful terminal state. So then, yeah, I think those are the different stages of of the lead. 

**User:** It's like uncontacted, contacted, Ideally, that's, like, very instantaneous. Uh, engaged, um, and then, you know, we'll stay in engaged. And then booked appointment. Right? So, like, actually, like, made the appointment and booked the appointment. Is is one of them. And then after booked appointment, I guess, then it's, like, did they show up? Right? And then you could start to, like, calculate things like show rate and and booking rate and and stuff like that. 

**Agent:** Do you track whether they showed up?

**User:** If we can, does the CRM do it? I think you kinda it kinda depends on on the system. I'm not really sure. Like, know, from from the AI texting perspective, the system we're building, we wouldn't know if they showed up, but that would needs to get pushed back into the CRM. 

**Agent:** Right. We don't track it today — that's actually one of the biggest gaps. Good instinct to call it out.

**User:** How does the AI know what to say to a lead? Okay. Let's take a step back. A lead essentially has some metadata. Right? Like, the lead itself has you know, what it's for, cars dot com, the vehicle of interest or whatever, I think, um, look. I think there's, like, potential ways to do this in different phases. Right? Like, the MVP is like, you know, everything is AI, so you can just kind of have, like, a very simple magic prompt, right, with just the tool call for booking an appointment. And then you can say, hey. You know, here's this, like, static greeting. That we generate based off of, like, the lead source type maybe. I guess, uh, that's interesting. Like, you you probably you know, the easiest, but probably the the not the not the most and probably not the best in in terms of, like, I guess, engagement rate, conversion rate, booking rate, whatever you wanna call it. Is to just have, like, a static message we send on every lead. Like, something like, hi. This is Pam from this dealership. How can I help you? Right? And it's like, well, you have all of this information about me, Like, you should leverage it. So then what I think we should do is, like, there's there's you know that's level one, and it's kind of, like, the most garbage. Uh, probably doesn't really convert super well. Level two, is, you know, static messages with, like, dynamic variables that you're able to essentially, use and and pull into for the different lead sources. Like, for example, in the cars dot com use case, you'd be like, hey. I saw that you're interested. Hey. Like, you'd say something, hi, John. Saw that you were interested in this, uh, you know, vehicle, like, whatever if they click the form for, like, a twenty twenty Honda Accord. For for the twenty twenty Honda Accord, when can I get you in or something like that? Right? And then level three, which may be overkill and and and and and and, uh, you know, essentially, like, maybe overengineering is if we, uh, like, dynamically use the AI, like an LLM, to generate a, uh, a static, uh, welcome greeting. Sorry. Not static. A dynamic, uh, welcome greeting based off of all of the content that we had. 

**User:** That means all of the metadata for the lead, for the contact, or whatever That's probably the most powerful, but maybe overkill. 

**Agent:** Okay. So you've got the greeting figured out. But what about the rest of the conversation — how does the AI know what tools it has access to, or how aggressively to push for an appointment?

**User:** So I think, um, look. You would probably in the like, you're gonna do some prompt engineering here. Right? Like, you'll have one tool call for the booking appointment, and then maybe some other sort of tool call for, like, escalations. I have a for that. Like, how do we escalate out of you know like, if we're doing something we're trying to do our job. Right? We're trying to do it well. And, uh, you know, there's just something that, like, requires a person in the loop Right? So, like, for example, we could build a very good AI system. Something with, like, you know, a really good greeting. Right? And then something also that has, like, a, uh, knowledge base for, like, you know, things like FAQs and just like, general knowledge about the dealership. And we could use, a vector rags or something like that. And then we also have, um, you know, the prompt. And, like, I think you could just kinda configure it so that it's all dynamic variables and then a tool call for you know, the the basically, what I was saying is, you know, if we do a really good job, you might need some sort of way to escalate. So for example, in the past, like, Pam for an inbound phone calling solution, we always have the ability to, like, transfer a phone call if we needed to. I think escalations, even in the case of texting, might be, like, you know, hey. Send a notification or send something to the CRM. Because we're writing everything to the CRM being like, hey. We need to get this guy, um, you know, some attention. So having an escalation for that, so maybe a tool call for that. And then tool call for the main case, is, like, booking via appointment. 

**Agent:** Got it. So you've got tool calls as part of the agent config. Does that config live somewhere in your model — is it an entity?

**User:** Yeah. That's a good question. Yeah. I mean, I think so. Right? So let's see. You would have this dealership with these leads and these contacts. And then you also have, like, an agent. I wonder how it's tied. Maybe you would have one agent per dealership Maybe an agent per lead type. But the thing is you also would wanna, like, kinda store contact variables when you're doing it. That's very interesting. 

**User:** I think spinning up an agent per contact sounds wrong and sounds overkill. It sounds like you're essentially wasting a ton of of of of yeah. I I I don't think that that's right. I think I think I think look. The agent config probably lives on the level of the dealership. 

**User:** And that maybe it dynamically takes the lead as a like, there might be, like, a agent table, and there might be, like, a agent x lead table. Agent x lead source, and then maybe, like, an agent x contact or maybe, like, a agent x lead x contact. I'm not sure. I could use some help on that. Like, how do you think about this? Like, maybe more of the business case. 

**Agent:** I want to see your instinct for how you'd model it. But let me ask you this — you said different lead sources might get different treatment. Does that mean one dealership could have multiple agent configs?

**User:** Yeah. Yeah. I'm saying that. I think so. Right? So, like, maybe okay. What's the way to think of this? You either have like, so agents themselves have dynamic variables. Right? It's like, I can have these dynamic variables that I'm injecting at runtime. And, that cool. That that makes sense. That's cool. But like, you know, how how composable do these things need to be? And I think it's like, well, the most brute force maybe potentially naive thing is, like, one agent on the entire dealership And, uh, if the agent exists on the entire dealership, that means that, uh, the the the everything is dynamic variables. Right? Like, the the lead source is dynamic variables. The welcome greeting is dynamic variables. And it's like, I don't know how useful that is. If we take the opposite extreme, and it's like you have an agent per contact, it's like, ugh, that's a lot of work. You're essentially, like, reusing You know, the entire prompt essentially gets reused. Right? Like, like, I I I I basically have to, like, spin up something in the middle. So I feel like the answer is that it's probably somewhere in the half like, a happy medium is probably agent on the level of the lead source. Right? So, like, I can have an agent per like, you know, when I say lead source, like, this is the Cars dot com agent, and this is how it behaves this way. Versus this is the phone walk in agent, and this is what behaves way. And then you're passing things like the contact variable as dynamic variables. That's what makes sense to me. 

**Agent:** That makes sense. So how does a lead get matched to the right agent config — what does that routing look like in your model?

**User:** I think there's, like, a agent, uh, table or, like, I think agents just exist on the agents, likely, just exist on the lead source. Right? So, like, you can have, like, lead source agents table. And it takes the it has its own unique key, but it also takes in a foreign key for for um, what am I trying to say, for lead source. For yeah. So oh, shit. I just realized we we probably need a lead source table. Right? So lead source exists on the dealership. And there's, a dealer x lead source. Our our lead source just has dealer foreign key, and then agents also just have a lead source foreign key. 

**Agent:** Good. So lead source is the bridge — a lead comes in with a source, that maps to an agent config. Does every dealer have the same set of lead sources, or can they differ?

**User:** No. I think they differ. Right? Like, uh, well, that's super interesting, uh, because there might be some reusability also, like Cars dot com. Like, question for you. Do do do all of the do we see the same lead sources across dealerships, or do we actually see different ones? Like, we really, like, just create, like, crazy unique like, millions of different lead sources. 

**Agent:** Mostly the same — AutoTrader, Cars.com, OEM, walk-in, phone. But occasionally you'll see something you've never seen before.

**User:** I see. Yeah. Look. I think in this case, then, yeah, we can have, like, a lead sources table. And they're they're basically, like, you know, there's, like, a the you know, dynamic table sorry. Sorry. There's, a know, table that just has the same set of, like, lead sources, and then we can also match those to the dealer. And, like so we'll also have, like, a dealer x lead source. 

**User:** I like that idea because then we can start to maintain metadata that is, like, reusable and against across these lead sources. 

**Agent:** Good. So you've got a solid model taking shape — dealership, contact, lead, lead source, vehicle of interest, appointment, agent config, and the routing between them. 

**User:** Sorry. Can you say can you explain again? You're at forty dealerships today, it takes thirty to sixty minutes to, like, manually run scripts? Like, something hits head HubSpot. Like, can you explain more about how it works today? Do you guys get, like, notified when something hits HubSpot? Like, how are you guys doing it so that it takes thirty to sixty minutes? 

**Agent:** Yeah. A deal closes in HubSpot — that's our signal that a dealer has bought the product. Then an engineer manually sets up their CRM connection, configures the AI for their lead sources, and verifies everything is working. All by hand. Takes 30 to 60 minutes.

**User:** Okay. But how do you know that the thing has hit HubSpot? Like, you get a Slack notification? 

**Agent:** Yeah, basically. Someone sees it and kicks off the process manually.

**User:** Okay. So got it. So new new lead hits in HubSpot. It's it's in and then, basically, like, you're setting up the CRM connection. Sorry. Is HubSpot the CRM we're talking about, or HubSpot and the dealership CRM separate things? 

**Agent:** Separate things. HubSpot is our sales CRM — that's where we track our own deals with dealers. The dealer has their own CRM — that's where their leads live. Right now all dealers are on Tekion.

**User:** Tech Yeon. Oh, okay. Got it. Got it. Got it. Tech Yeon is, like, a dealership CRM. Got it. 

**User:** Okay. So and you're saying that, like, the CRM connection happens, the d like, the engineer sees this, goes and manually grabs the dealer techion ID or something and goes and puts in, like, a database. Is that what you're saying? 

**Agent:** Something like that, yeah. They set up the CRM credentials, configure the lead sources, set up the agent configs, verify it all works. All manual.

**User:** Okay. And when you're configuring lead sources, is that, like, you trying to trying to, like, check to see that, like, things are working? Like, what how do you test the credentials? Is, like, making, like, some sort of, like, crawl request with the credentials to see that they're working correctly? 

**User:** You, like, run a test script? Like, I I I I I think we could probably automate a lot of this stuff, but I before I suggest that, I kinda wanna make sure I understand it. 

**Agent:** Yeah, basically running a test script to validate credentials, pull some leads, make sure the connection works. Then manually setting up the configs. How would you automate that?

**User:** What what what is in a config? 

**Agent:** The agent config — the prompt, the greeting, which tools the agent has access to, which lead sources are active for that dealer.

**User:** Oh oh, you're talking about, like, literally the schema that we built. You're saying that the like, my tables, the way that I've designed it is fine. And then a new techy on CRM leader, uh, techy on CRM ID shows up. And I basically need to say, hey. Given this ID, let's go spin up all the the records. We need to. So, like, go spin up all the lead sources and tie them to the dealership and things like that. Uh, that's what you're is is that correct? Am I on the right page right there? 

**Agent:** Yeah, that's right. So how would you automate that?

**User:** Okay. Got it. Okay. So what I think we can do potentially is, like, okay. From a HubSpot CRM perspective, we can set up webhooks that say when when this dealership with these properties fire. Go ahead and take that data and make an API call to, uh, you know, with the relevant metadata. And can we assume that the Techeon, uh, uh, metadata is stored in HubSpot? Do we have to go somewhere else? Like, how how are the current engineers getting getting it? 

**Agent:** Good question. Yeah, the Tekion credentials are captured during the sales process and stored in HubSpot. So when the deal closes, you have access to them.

**User:** Got it. So okay. Almost fair. It sounds like you're kinda leaning me towards everything that we need to set up these tables that's stored in HubSpot collected and gathered. So what I'd do is I'd set up this, like, you know, HubSpot webhook, go and actually get the data, from HubSpot, go and actually create some sort of API that goes and does a manual insertion. And create all the data and all the records. Is that is that you're looking for? 

**Agent:** That's a good start — you've got the trigger and the record creation. But you have CRM access now. What could you learn about this dealer before you configure anything?

**User:** Interesting. I think what we could do in theory is, like, we could start to actually pull all of the leads and the lead sources. Well, yeah, in theory, uh, you know, assuming that, like, rate limits and stuff allow for it because that's something that you have to kinda be mindful with with these systems is I could go and, like, just pull lead data from the CRM over the past, I don't know, whatever, a year and just be like, okay. Cool. Are my CRM sources. Are there any new CRM sources? That I've never seen before? Okay. How do I tie those to agents? Do you need special agents? Like, what are their use cases? Then what I could do outside of that is then be like, oh, cool. These are the different, uh, uh, lead sources set up so I can, like, auto create agent configs for each dealer x dealer x lead source. Right? 

**User:** I think, yeah, that's a good idea, and that could potentially speed up a whole lot of configuration. And you can almost get, like, an instantaneous pipeline, I think, if I'm not missing anything. 

**User:** To, like, HubSpot CRM lead, go in, check and test the credentials, and add them to whatever databases we need to. 

**User:** And then at the same time, off some sort of process. That goes and actually starts like, mining the CRMs to to to get an understanding of the dealerships. And then be like, okay. Cool. Now that I've seen all this data for the dealerships, I can like, auto auto sync agents to the lead source and then potentially flag ones that I'm not familiar with for a human interview. Or, honestly, I could even potentially use agents to look at these new lead sources and, like, not just flag for a human interview, but, like, actually create draft agent configs, um, uh, to to to speed up the process. 

**Agent:** Good. You mentioned flagging unknown sources — what happens to the dealer while that unknown source is being reviewed? Do they have to wait?

**User:** A good question. You're saying do they have to wait for us to the human in review? 

**Agent:** Yeah. Unknown source shows up — do you block the whole dealer from going live while you figure it out?

**User:** Oh, for no. I think you would go live with the sources that you do know. And, uh, and and and for the ones that you don't know. Yeah, you essentially bar like, you just don't configure those or you don't go live with those and and wait for the human to go and approve them and you know, I guess, run whatever testing they need to. 

**User:** To say, okay. This is, like, good for production. 

**Agent:** Good. So you've got the dealer live with known sources. How do you know the AI is actually going to say the right thing before real customers start getting messages?

**User:** The AI is gonna say the right thing before real customers start getting messages. 

**User:** Are you talking about for new lead sources or even for the existing ones? 

**Agent:** Even for the existing ones. You've auto-configured everything — how do you verify it actually works before you flip the switch?

**User:** Okay. Got it. So I think look. There's two things that you really wanna test. I think you wanna test the CRM integration. You also wanna test, like, the agent capabilities. Can it do its main core capabilities? Right? So for that, what you do is you you write something called evals. Right? So you you write evals for the AI. When you have evals for the AI, you're testing the core capabilities. And, essentially, what you're saying is, can I run these minimal sets of tests that represent what the agent needs to do? And I I think for us I mean, we haven't talked about evals in our data model, but I do think that evals probably exist on the level of the data model, maybe on the level of the agent or the lead source or the lead source x agent. Right? And these are the evals that need to run for these guys. And, essentially, it's like, okay. Should probably run that eval suite before and validate that everything's working and and flag any potential errors to a human in the loop. We should flag that all that stuff is working, uh, before before, uh, you actually go live in production. 

**Agent:** Good. So you run evals, everything passes — you're live. Now you've got 200 dealers running. How do you know if one of them is broken right now?

**User:** Yeah. It think we have to define what broken means. Like, I think, uh, there's things like errors in, like, the the the the you know, the conversation errors. Right? Like so, like, from from a monitoring and observability perspective, it's like, if any errors are occur in during the conversation, let's make sure we have good logging and alarms on any thresholds, like just to make sure that any single error is, like, populating a chat in, like, Slack or something. That's, like, one layer. The other thing is, like, you know, errors and integration tracking. In the tool calls themselves. I think that's very important. So, like, those are, like, deterministic errors. But then also outside of that, it's like, is the LLM kinda doing conversationally well? Right? I think, like, there's probably, like, an LLM as a judge element that we could run on every call or maybe, like, a sample of calls. And just be like, hey. Are we actually, you know, doing the job, or is is is is is is the AI kind of behaving as intended or expected? 

**User:** And then I also would probably tie a deter an a non sorry. A more deterministic measure. Right? So, like, you know, like, rates of, like, know, what is actually healthy for a for a dealership? It's probably, like, know, there's probably some sort of booking rate that we say is, like, the industry norm or some sort of conversion rate or some show rate something like that. So what we could do is we could start to, like, create, like, analytics on, like, you know, healthy accounts look like, and then also check, like, our bottom accounts. And then just be like, we could create some draw some threshold based off of data to say, like, this is healthy. These are not healthy metrics. And I think with all of that stuff in production, we have a pretty good observability and monitoring and metric layer for our system. 

**Agent:** Good. What happens at 2am when a dealer's AI starts sending bad messages and nobody's awake?

**User:** (inaudible speech)

**User:** That's a good question. I mean, like, we would do probably basic pager duty stuff. The idea is, like, okay. Like, you know, again, if so so so I see. So two AM. Even know if we should be texting people at two AM, but I think what we could do is, like, we could have, like, a off hours mechanism where I don't need okay. Forget off hours for a second. But let's say, yeah, we should do pager duty. Like, traditional, like, hey. You know, the error alerts or whatever have passed the mechanism like, passed to the past the threshold, and we should alert the you know, engineer on call and and and all that stuff. So I think that should exist. 

**Agent:** .

**User:** I also you know, part of me wants to wants to be like, there there should can maybe be, like, a AI auto shutoff thing or, like, you know, if you can if you can scope it to just one particular, like, agent that viewing an issue, maybe you can turn that off. I'm I'm not super sure exactly. But it's like, do you trust the LLM as a judge layer enough be like, hey. I'm gonna shut off this specific agent config from running, like, disable that. That's super interesting to me. I'm not super sure how to answer that, but, like, there's, traditional things that work, and then there's probably, like, auto shut off or something we could implement. 

**Agent:** Yeah, auto-disable is exactly the right instinct. If reliability drops below a threshold, pause that dealer's outreach automatically — don't wait for a human. 

**User:** Alright. 

**Agent:** shift to something different. 

**User:** Sorry. Sorry. 

**User:** You're saying pause the entire dealer's outreach? Isn't that kind of going against the principle we said before where it's, just turn off the one thing that's problematic or, like, you know, that we said with with with with, like, new agent configs. Don't you think we should if we can. Right? And if, you know, if we can, I'm and that's a big if. If we can, shouldn't we just shut off the one that's problematic and leave the rest running? 

**Agent:** Yeah, that's the right instinct — surgical is better than blunt. Disable the specific source or agent config that's broken, leave the rest running. Good catch.

**User:** That sounds pretty reasonable to me. I think I'd do it. 

**Agent:** How do you know it's actually better?

**User:** I see. I think we could Yeah. That is a good point. Good point. Right? Like, we could try it We could a b test it. We could say, like, hey. We we we we we see that this is yeah. This is actually, like, a booking rate experiment. Right? So what we could try is we could say, hey. Hey, dealership. Yeah. You know, you you oh, got it. So so so what we could do is, like, see the response. I will say, like, hey, guys. That makes a lot of sense. This may or may not be, like, a best practice, you know, and we'd, like, leverage precedent or whatever and say, we can try it. What we'll do is we will and again, I'm not exactly sure the most sophistic how sophisticated these dealership customers are, but, like, you could essentially be like, hey, guys. We're gonna try what you're saying, your your suggestion, and we'll roll out roll it out to, like, ten, twenty, thirty percent of traffic. And see if it's actually working well, and then get back to you with, uh, the decision. And if it's really good, then we'll roll it out to everybody. 

**User:** And, you know, that's really cool because it also has the ability I didn't mean to cut you off. It also has the ability to, like, make our whole product offering better, we could start to AB test it across dealerships too. Right? So that's a very strong loop. 

**Agent:** Good. What metric are you optimizing for in that test?

**User:** I think booking rate. Right? 

**Agent:** Is booking rate enough?

**User:** Let me talk this through again. Sorry. Could you could you say the you say the hypothetical again, the the whole example? Because I feel like I was missing some stuff. 

**Agent:** Sure. Dealer says: instead of going straight to booking an appointment, have Pam first check if we have the car in stock and tell the customer about it. Right now she goes straight to asking when they can come in.

**User:** Um, I think booking rate is thing that matters the most. 

**User:** I could also see well, engagement rate doesn't matter. They're getting in like, you know, they're responding regardless, so that doesn't matter. Look. Downstream of it, we don't have this data. But show rate could get affected. Right? Let me think about this. We don't okay. So in in this hypothetical, we basically say, hey. I don't have I don't have the v hey. Ask Let's search to see if the car is in inventory first. So two things can happen. Pam can see that it's in inventory and tell the person to come in. Then they come in. And then it's like, oh, because we had the car in inventory, they actually show up. And then what could also happen is say, hey. I we don't have the car, and they don't show up. Okay. So so so what could happen is, like, booking rates can drop, but also potentially show rates could increase know. I think we'd probably wanna check both of those rates for the experiment and see what happens. Happens. 

**Agent:** .

**User:** Hey. Are you there? Hello? 

**Agent:** Yeah, still here. So you'd want to track both booking rate and show rate. But we don't track show rate today. What do you do?

**User:** I don't know. Are you saying engagement rate? We should be tracking engagement rate. I don't understand. 

**Agent:** No — show rate. Whether the customer actually showed up to the dealership. You said it yourself earlier — we don't track it. So if you want to run this experiment and measure whether inventory-first actually leads to more people showing up, what do you do?

**User:** Oh, I mean, look. I think we tried to get if if if it's possible, I think we now try and prioritize getting that data Maybe we do it in parallel. Right? It's like, can try and get that data, but, also, we realized the experiment is still valuable. Even without that data. So I think we could do a, like, like, a tortoise and hare type situation where we kick off the experiment and then hopefully hair can essentially get us the data back fast enough. It's acceptable if we don't. 

**User:** Think 

**Agent:** .

**User:** that's the way to do it. 

**Agent:** How would you get show rate data — where does it come from?

**User:** Oh, how would I get show rate data? Where does it come from? I'd imagine that the dealership is tracking it in the CRM. So maybe we could like, if we don't have it based off of the API, is that the assumption? Like, API because we have API access to Techeon, but we don't have show rate data. And if we don't have it, is it I mean, I guess what we would try and figure out is, can we get it from our existing API integration partners? Maybe we don't have it just because it's, a setting we have to turn on or maybe we to do some dev work. Um, and if it's truly not available through those means, it's like, could we, I don't know, ask the dealership to, like, provide it some way? Maybe we give them a tool. Maybe we give them a Chrome extension and we steal it. I I'm not sure. 

**Agent:** Good instinct — the CRM should have appointment completion status. That's the data you need. Build the tracking first, baseline it, then run the experiment properly.

**User:** How would you make the system figure out works and make the ad that are not one off prompt tweaks but assist? Got it. Look. I think that you can potentially build a self learning system if you give the AI a goal. So it's like, hey. Hey, guys. I want you to optimize for booking rate, for example. Right? This is to showcase the the the example and the idea, and then you can, like, push me on, like, com completeness if you'd like to. But the idea is, like, you can essentially build a self learning system by having an AI uh, you know, that basically changes the prompts uh, maybe on the level of the agent config, maybe on the level of the lead source, It sounds super clear to me right now. But if it's trying to optimize for booking rates, right, or something like that primarily, something that is reading the conversations. The LLM as a judge runs, basically tells you when things are problematic. Problematic and times, like, identifies places where you could have done something better and then have the uh, have another agent basically, um, recommend prompt changes And then, again, you've already done built the AB testing system. So it's like, hey. AB test. Go and run this at twenty percent. Do you see the main metrics going up? Honestly, it's not just booking rate. Right? Like, you're starting to build the system. If we build the monitoring and observability system for earlier across all of the different domains, across all of the different systems. Um, if you've built that, then you can essentially check all of those things and have the AI agent also wait the changes and be like, hey. This change that we made was actually really fire. We should roll it out at a higher percentage. And then you build, like, a self learning system that actually gets better with time. 

**Agent:** That's interesting. Does your data model from Phase 1 support running variants — like, two different agent configs simultaneously for the same lead source?

**User:** We're only watching no. We would have to go back and actually uh, so, look, we could potentially change the agent config to support a b testing variants. As part of the data model. Um, I've also used tools like Posthoc, which allows to run experiments. 

**User:** We 

**Agent:** .

**User:** could potentially try something like that, but then we'd yeah. We need to change the data model so that the prompts are not part of the config. 

**Agent:** .

**User:** Is there is there anything I'm missing? 

**Agent:** I think you've covered the main pieces. Let me ask you one more thing — if you could only track one metric to know whether this product is working, one number, what would it be and why?

**User:** I feel like booking rate. I feel like it's like, dude, if we're making appointment well, let me let me talk this to completion. Look. I think the key metrics that we can discuss are things like engagement rate, booking rate, 

**User:** show rate, maybe, like, time to first response, which should be near instantaneous. I think I think I'm I'm kinda torn between booking rate and show rate. Because it's like if a lot of people well, no. Show rate is stupid because um, I don't know. I think maybe show rate. Show rate makes a lot of sense. Because, like, if I can say that a lot of these people are actually show well, you know, there's even more data outside of show show rate. Well, in the case where But they get to go to the gate to I don't know. I'm I'm honestly torn. I feel like there's not a clear indicator 

**Agent:** What's the product actually trying to do for the dealer?

**User:** I I think you said earlier. Right? Unless I'm misunderstanding. I think you said the main thing is to book more appointments. 

**Agent:** Book appointments that actually show up. What's the point of booking an appointment if nobody comes in?

**User:** Maybe booking appointments where people don't actually show up is fine because you get that metadata in their system, and that's people that are, like, very highly qualified. I get what you're saying. So, yeah, I guess you're right. I mean, I guess you're saying that the right answer is show rate. 

**User:** (inaudible speech)

**Agent:** I'm not saying there's a right answer — I'm asking what you think. What does the dealer actually care about?

**User:** Look. The dealer wants to sell more cars. Right? At the end of the day I mean, it's either that they wanna sell more cars or, yeah. I mean, this is a sales product, sales outbound, so they're trying to sell more cars. So I think, um, look. The most brute force naive way to think about this is you actually don't care about show rate. You actually care about car selling rate. And, you know, how does this system affect car selling rate? And it's like, you can walk back of that stuff. It's like, okay. If the dealership gets a thousand leads or a hundred leads a day, well, you wanna at least you wanna message all of them, right, if you can. If you have the metadata, like, texting phone numbers or whatever, you wanna message all of them. And it'd be great if, like, don't know, something like seventy percent engaged. And of those seventy percent that engage, it'd be great if seventy percent of those seventy booked. Right? And of those people that booked, it'd be great if the seventy percent of that seventy percent of that seventy percent actually showed up It'd be great if seventy percent of those guys actually bought cars. Right? So I don't know. I don't know which rate metric to to track is. I feel like booking rate actually is really awesome because at the end of the day, even if you're not able to get them to come in, you have, you know, I guess, the ability I don't know, man. Honestly, this is, like, a tricky thing. I'm not sure I have a great answer for you. 

**Agent:** I think you're thinking about it the right way — it's a funnel, and the further downstream you measure, the more meaningful it is. Show rate is probably the best proxy we can reliably track right now, since close rate requires DMS integration we don't have. But you're right that the ultimate answer is revenue per lead.

**User:** Yeah. Well, yeah. But real quick, like, where is the product today? And, like, if I were to join, where would it be? 

**User:** What would I be, like, focused on, I guess, right now versus, like, a month from now versus, like, a year from now? 

**Agent:** Good question. Today the product works — 40 dealers live, AI is texting leads, booking appointments. But it's held together with a lot of manual work and my involvement. The first 90 days would be getting your hands dirty — understanding the codebase, the dealers, where things break. Then it's about making it scale — the onboarding automation we talked about, the monitoring, getting to 200 dealers without it being a nightmare. A year from now, ideally you've built the self-learning system you described — where the AI is actually getting better over time, not just being maintained.

**User:** Awesome. Yeah. That's really exciting, fun stuff. Thank you. I hope I get the the position. 

**User:** Have a good one. 

**Agent:** Thanks Chotu, really enjoyed the conversation. The team will follow up with next steps. Take care.

