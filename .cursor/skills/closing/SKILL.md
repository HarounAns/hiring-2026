---
name: closing
description: "Draft a 'Peer into my brain' closing document for a candidate who passed their final interview. Use when the user says 'close', 'closing doc', 'closing guide', 'write the offer doc', or mentions closing a candidate."
---

# Closing Doc — "Peer into my brain"

Inspired by HF0's data bomb approach: go so deep that the candidate feels you paid attention and cared. Reference specific things from interviews, informal conversations, and personal moments. The candidate should read this and think "I can't believe you remembered that."

## Workflow

### Step 1: Gather Data

Search every available source for the candidate's name:

```bash
SKILL_DIR="$HOME/.cursor/skills/google-workspace"
npx tsx $SKILL_DIR/scripts/gmail.ts notes --query "<candidate name>" --max 20 --user haroun@pamhq.com
npx tsx $SKILL_DIR/scripts/gmail.ts search "<candidate name>" --max 20 --user haroun@pamhq.com
node ~/.claude/skills/granola/scripts/fetch-notes.js | grep -i "<candidate name>" -B 5 -A 100
```

For each meeting note found, read the full doc:

```bash
npx tsx $SKILL_DIR/scripts/gmail.ts read-doc <fileId> --user haroun@pamhq.com
```

Also read:
- The candidate's CRM file: `docs/candidates/{role}/{name}/{name}.md`
- The role definition: `docs/roles/{role}.md`
- Interview materials: `docs/interviews/{interview-role}/`

### Step 2: Prompt the User for Personal Moments

Ask the user directly — these are the data bomb details no system captures:

- Informal conversations (meals, calls, texts) — what did the candidate say about why they want to join?
- What's their real motivation beyond career? (fear, ambition, frustration with current role)
- Personal details that show you care (family, relocation, life circumstances)
- Anything the candidate said that surprised you or stuck with you

### Step 3: Pick the 3 Gold Values

Ask the user which 3 of the 8 core values to highlight for this candidate. These get candidate-specific framing in the Core Values section. The other 5 are listed verbatim without framing.

### Step 4: Get Team Blurbs (if applicable)

Ask if any team members wrote blurbs about how Pam changed them. These go under the Embrace AI tab. Omer and Marcelo have standing blurbs that can be reused or updated.

### Step 5: Draft the Doc

Create `docs/candidates/{role}/{name}/closing-guide.md` using the template in [TEMPLATE.md](TEMPLATE.md).

**Tone:** This is Haroun talking directly to the candidate. First person. Honest. Not corporate. References specific moments to show you paid attention.

**Key principles:**
- The Aptitude section is the data bomb — specific interview moments, quotes, personal conversations
- Skills section is concise — bullet points, gaps framed as bridgeable
- Core Values section lists all 8 verbatim, 3 get candidate-specific framing underneath
- Embrace AI tab always links to the Hardworker's Paradox and includes team blurbs
- "My Worries" is honest and vulnerable, framed as wanting the environment to support them — never accusatory

### Step 6: Update Pipeline

After drafting, update the candidate's CRM file:
1. Set `stage: closing` in frontmatter
2. Add stage_history entries for any interview stages not yet recorded
3. Update the Interview Status table in the body
4. Run `npx tsx docs/candidates/scripts/pipeline.ts` to regenerate README

## Constants

### Hardworker's Paradox Doc
https://docs.google.com/document/d/16uI1o9NTiM-_ImNL1kK3oA1iV2rYhFohs1k2Jf2UJ64

### V4 Operations Vision
https://github.com/dream-lab-ai/eng-manager-external/blob/main/v4-operations-vision.md

### Key Accounts Self-Learning System
See `~/pam-key-accounts-investigation/docs/20X-KEY-ACCOUNT-SYSTEM.md`
