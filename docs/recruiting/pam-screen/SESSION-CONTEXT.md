# Pam Recruiter Screen — Session Context

> Handoff doc for continuing development in a new session. Last updated: April 5, 2026.

---

## What This Is

An AI-first hiring pipeline where Pam (our voice AI product) cold-calls LinkedIn applicants, screens them with 6 questions, and produces scored transcripts. Haroun reviews the top candidates and decides who advances to a live interview.

**Role being hired for:** Senior Software Engineer — New Product (0→1)
**Linear ticket:** [HAR-30](https://linear.app/pam-ai/issue/HAR-30)

---

## Current State

### What's Built and Working

- **Retell agent** running and making real calls
  - Agent ID: `agent_b65af666c5814f0946aba94156`
  - LLM ID: `llm_6385d5481a76be4029ef5ce8dc1d`
  - Org ID: `org_9HBTA6QvBTHaEpw9` (Outbound account workspace)
  - Phone number: `+15717047278`
  - Agent prompt: `docs/recruiting/pam-screen/agent-prompt.md`

- **15 simulation evals** — all passing on latest draft
  - Eval JSON files: `docs/recruiting/pam-screen/evals/*.json`
  - Covers: happy path, never short-circuit, equity questions, busy/reschedule, wrong person, "is this AI?", comp deflection, rude candidate, already accepted offer, role questions, long answers, smooth transition, early remote volunteer, inbound unknown caller, partial unknown company

- **Post-call extraction** — 14 fields automatically extracted from every call
  - candidate_name, location, visa_status, comp_expectations, earliest_start_date, ownership_answer_summary, scaling_answer_summary, willing_to_relocate, noticed_ai, wants_reschedule, reschedule_time, call_summary, call_successful, user_sentiment

- **130+ real calls made** across 3 batches
  - Batch 1: 5 test candidates (archived/weak)
  - Batch 2: 30 DC-area candidates
  - Batch 3: 50 Top Fit candidates
  - Results: 21 successful full screens, 13 reschedule requests, 25 voicemails

### Candidates Screened and Graded

Transcripts saved at `docs/recruiting/pam-screen/transcripts/`. Each graded on a 30-point rubric (Ownership, Scaling, Comp Fit, Location, Availability, Communication).

| Rank | Candidate | Score | Recommendation | Comp | Location | Phone |
|------|-----------|-------|---------------|------|----------|-------|
| 1 | Rishwand | 27/30 | **Advance** | $170-180K | Will relocate | +12605151855 |
| 2 | Ian | 24/30 | **Advance** | ~$125K | Herndon, local | +19086449311 |
| 3 | Sindhuja Challa | 23/30 | Maybe | $180-200K | FL, will relocate, H-1B | +18133178461 |
| 4 | Haran (FINRA) | 23/30 | Maybe | ~$180K | Tysons, local, H-1B | +12016572788 |
| 5 | Kirankumar (Intuit) | 22/30 | Maybe | $110-150K | Will relocate | +16803568279 |
| 6 | Tayseer H. | 22/30 | Maybe | $140-160K | DC-Baltimore, local | +15714656420 |
| 7 | Tom | 22/30 | Maybe | $85-100K | Will relocate | +13466286501 |
| 8 | Buza | 21/30 | Maybe | ~$120K | Will relocate | +12143260099 |
| 9 | Sri Ramya | 20/30 | Maybe | $105-120K | NY, will relocate | +16075957445 |
| 10 | Rohan | 20/30 | Maybe | $100-120K | Will relocate | +18577460631 |
| 11 | Gabriel | 18/30 | Pass | $180-250K | Won't relocate | +18656078804 |

**Jotir Mahesh** also completed a full screen but hasn't been graded yet. Needs sponsorship.

### What's Not Done Yet

- **Resume screen (Stage 0.5)** — LinkedIn profile review to verify phone screen signals before advancing. Haroun wants this before moving candidates to Stage 1. LinkedIn profile URLs are in the applicant CSV.
- **Reschedule callbacks** — 13 candidates asked to reschedule (list in call logs). Need to call them back.
- **Retell skill reorganization** — Plan exists at `~/.cursor/plans/retell_skill_and_edd_docs_5ab277c1.plan.md` to rename `retell-edd` to `retell`, add multi-account profiles, write SKILL.md, RED-GREEN-EDD.md, and DEVELOPMENT.md. Not yet executed.
- **Stage 1 (async judgment call)** — Google Doc scenario for top candidates. Designed in README.md but not built.
- **Stage 2 (live session)** — Haroun's existing 3-phase interview. Prep guide exists at `docs/interviews/senior-sales-outbound/01-prep-guide.md`.

---

## Key Files

| What | Path |
|------|------|
| Agent prompt (source of truth) | `docs/recruiting/pam-screen/agent-prompt.md` |
| Eval test cases | `docs/recruiting/pam-screen/evals/*.json` |
| Tech spec + simulations | `docs/recruiting/pam-screen/tech-spec.md` |
| Pipeline design (4 stages) | `docs/recruiting/pam-screen/README.md` |
| Applicant CSV (500+ candidates) | `docs/recruiting/pam-screen/Pam_Sr Eng_0to1_Job_Applicant_Report_2026-03-29.xlsx - Job Applicants.csv` |
| Batch CSVs sent | `docs/recruiting/pam-screen/test-batch.csv`, `test-batch-2.csv`, `test-batch-3.csv` |
| Downloaded transcripts | `docs/recruiting/pam-screen/transcripts/*.md` |
| Headstarter onboarding (Yasin) | `docs/recruiting/headstarter-onboarding.md` |
| Culture fit cheat sheet | `docs/interviews/culture-fit-cheat-sheet.md` |
| Recruiter kickoff (Murshed) | `docs/recruiting/2026-02-03-murshed-hiring-kickoff.md` |
| Recruiting log | `docs/recruiting/log/2026-03-29.md` |
| Retell EDD skill | `~/.cursor/skills/retell-edd/` |
| Retell skill plan | `~/.cursor/plans/retell_skill_and_edd_docs_5ab277c1.plan.md` |

---

## Retell Setup

### Auth

- **API Key** stored in AWS Secrets Manager: `retell/outbound/api-key` (us-east-1)
- **JWT** cached locally at `~/.cursor/skills/retell-edd/.auth-cache.json` (for dashboard-only APIs like test cases)
- Config: `~/.cursor/skills/retell-edd/config.json`

### Scripts

```bash
SKILL_DIR="$HOME/.cursor/skills/retell-edd"
cd $SKILL_DIR

# List calls via SDK (uses Secrets Manager for API key)
npx tsx scripts/sdk-list-calls.ts --agent-id agent_b65af666c5814f0946aba94156 --hours 48 --exclude +17039463356

# List test cases
npx tsx scripts/list-test-cases.ts --llm-id llm_6385d5481a76be4029ef5ce8dc1d

# Run batch test
npx tsx scripts/create-batch-test.ts --llm-id llm_6385d5481a76be4029ef5ce8dc1d --test-cases <id1>,<id2>

# Check results
npx tsx scripts/list-test-runs.ts --batch-id <batch_id>

# Push prompt to Retell (inline JS)
node -e "..." # See agent-prompt.md push pattern in session history
```

### Version Gotcha

Test cases are tied to LLM versions. When you publish in the Retell dashboard, the draft resets. The `create-batch-test` script defaults to version 0 — for newer versions, create batches explicitly with `response_engine.version` set correctly, or run from the dashboard.

---

## Red-Green EDD Process

The development methodology we followed:

1. Write evals first (what "correct" looks like)
2. Write the prompt (make evals pass)
3. Run evals → Red (fail) → Fix prompt → Green (pass)
4. Test with real humans
5. Write evals from real failures (most valuable — e.g., Anna's early-remote short-circuit)
6. Publish → Monitor → Repeat

---

## What To Do Next

### Immediate: Resume Screen (Stage 0.5)

For the top 10-12 candidates who completed the phone screen:
1. Pull their LinkedIn profiles (URLs are in the applicant CSV)
2. Score their resume against the same rubric — does background support what they said?
3. Combine phone screen score + resume score for a final ranking
4. Advance top candidates to Stage 1 or directly to Haroun's live interview

### Then: Reschedule Callbacks

13 candidates asked to reschedule. Their numbers and preferred times are in the call logs. Need to call them back — either via Retell batch call or manually.

### Then: Execute Retell Skill Plan

Plan at `~/.cursor/plans/retell_skill_and_edd_docs_5ab277c1.plan.md`:
- Rename skill to `retell/`, add multi-account profiles
- Write SKILL.md, RED-GREEN-EDD.md, DEVELOPMENT.md
- Sync eval JSONs

### Ongoing: More Batches

~350 candidates in the CSV haven't been called yet. Can generate more batch CSVs and keep running.

---

## Haroun's Number (exclude from reports)

`+17039463356` — always filter this out when querying call logs.
