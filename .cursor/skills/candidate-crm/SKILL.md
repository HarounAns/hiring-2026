---
name: candidate-crm
description: "Manage the candidate pipeline CRM — add candidates, update stages, record interview notes, query the pipeline. Use when the user mentions a candidate, pipeline, CRM, hiring, interview, culture screen, short circuit, stage, recruit, or asks about who's in the pipeline for a role."
---

# Candidate CRM

Lightweight git-native CRM for tracking hiring candidates. Candidates are markdown files with YAML frontmatter in `docs/candidates/`.

## File Structure

```
docs/candidates/
├── README.md                          # Pipeline rollup (auto-generated)
├── TEMPLATE.md                        # Template for new candidates
├── scripts/pipeline.ts                # Generates README from frontmatter
├── senior-sales-outbound/
│   └── candidate-name/candidate-name.md
├── senior-pam-core/
│   └── candidate-name/candidate-name.md
├── senior-ai-ops/
│   └── candidate-name/candidate-name.md
├── integration-support/
│   └── candidate-name/candidate-name.md
└── swe-llms/
    └── candidate-name/candidate-name.md
```

## Frontmatter Schema

Every candidate file must have this YAML frontmatter:

```yaml
---
name: Full Name
role: senior-sales-outbound  # see valid roles below
stage: culture_screen        # see valid stages below
source: inbound              # inbound | outbound | referral | recruiter
email:
phone:
linkedin:
location:
applied_date: 2026-03-24
current_role: Title at Company
years_experience: 7
stage_history:
  - stage: sourced
    date: 2026-03-24
    notes: How they entered the pipeline
---
```

**Valid roles:** `senior-pam-core`, `senior-ai-ops`, `senior-sales-outbound`, `integration-support`, `swe-llms`

**Valid stages (in order):** `sourced` → `culture_screen` → `short_circuit` → `technical` → `closing` → `offer` → `hired` | `rejected`

## Operations

### Add a New Candidate

1. Read `docs/candidates/TEMPLATE.md` for the file structure
2. Create `docs/candidates/{role}/{kebab-name}/{kebab-name}.md`
3. Fill in frontmatter (name, role, stage, source, contact info, applied_date)
4. Fill in Background and Fit Assessment sections from resume/context
5. Run `npx tsx docs/candidates/scripts/pipeline.ts` to regenerate the pipeline README

### Update a Candidate's Stage

1. Update the `stage` field in frontmatter to the new stage
2. Append a new entry to `stage_history` with the date, stage, and notes
3. Update the Interview Status table in the body
4. Run `npx tsx docs/candidates/scripts/pipeline.ts` to regenerate the pipeline README

### Record Interview Notes

Fill in the appropriate section in the candidate file:

- **Culture Fit Screen** → use the question/signal table format. Reference `docs/interviews/culture-fit-cheat-sheet.md` for the 6 questions + oath.
- **Short Circuit Screen** → use the Q1/Q2/Q3 pass/stop format. Reference `docs/interviews/{role}/06-short-circuit.md` for the role-specific short circuit questions.
- **Technical Interview** → free-form scoring + notes. Reference `docs/interviews/{role}/02-cheat-sheet.md` and `docs/interviews/{role}/04-scoring-debrief.md` for scoring rubrics.
- **Debrief** → final decision, strengths, concerns, offer details.

### Query the Pipeline

- **All candidates:** Read `docs/candidates/README.md`
- **Specific role:** Grep frontmatter: `rg "^role: senior-sales-outbound" docs/candidates/ -l`
- **Specific stage:** Grep frontmatter: `rg "^stage: culture_screen" docs/candidates/ -l`
- **Specific person:** Grep frontmatter: `rg "^name: Marwane" docs/candidates/ -l`

### Regenerate Pipeline README

```bash
npx tsx docs/candidates/scripts/pipeline.ts
```

Always run this after adding or updating candidates.

## Interview Process Reference

| Doc | Path |
|-----|------|
| Culture Fit Cheat Sheet | `docs/interviews/culture-fit-cheat-sheet.md` |
| Role Interview Pack | `docs/interviews/{role}/` |
| Short Circuit Screen | `docs/interviews/{role}/06-short-circuit.md` |
| Prep Guide | `docs/interviews/{role}/01-prep-guide.md` |
| Scoring Cheat Sheet | `docs/interviews/{role}/02-cheat-sheet.md` |
| Scoring & Debrief | `docs/interviews/{role}/04-scoring-debrief.md` |
