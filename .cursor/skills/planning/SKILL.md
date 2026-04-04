---
name: planning
description: "Manage hiring tasks on Haroun's Linear board (HAR team). Use when the user asks to create hiring tickets, plan interviews, triage recruiting work, review what's pending, or manage hiring-related tasks. Also use when the user mentions Linear, tickets, issues, board, planning, or todos in a hiring context."
---

# Hiring Planning — Linear Board Management

Haroun tracks hiring tasks on his `HAR` team in Linear (`pam-ai` workspace). This skill covers creating, triaging, and reviewing those tasks.

All Linear operations use the `user-linear` MCP server — no custom scripts needed.

## Board Structure

### Labels

Use the **Hiring** label (green) for all tickets created from this repo. You can combine it with other HAR labels when relevant (e.g., `Hiring` + `People` for a hiring-manager alignment conversation).

### Priority Levels

| Priority | Meaning | Expectation |
|----------|---------|-------------|
| **Urgent (1)** | Candidate will churn or deadline is today | Act immediately |
| **High (2)** | Needs to happen this week (schedule interviews, send offers) | Schedule it |
| **Medium (3)** | This month (write JDs, source candidates, prep interview packs) | Track it |
| **Low (4)** | Backlog — nice-to-have improvements to the hiring process | Review monthly |

## MCP Tools

All Linear operations go through the `user-linear` MCP server. Key tools:

| Tool | Use For |
|------|---------|
| `list_issues` | Query open tickets (filter by team, label, assignee, state, priority) |
| `get_issue` | Get full details on a specific ticket |
| `save_issue` | Create or update a ticket |
| `list_issue_labels` | Look up available labels |
| `list_issue_statuses` | Look up available statuses for the HAR team |
| `save_comment` | Add a comment to a ticket (e.g., interview debrief notes) |

## Creating Tickets

When creating tickets on this board:

1. Always use `team: "HAR"` and `assignee: "me"`
2. Always apply the `Hiring` label — combine with others when appropriate
3. Write descriptions in markdown with context — these tickets are for Haroun's future self
4. Use checklists (`- [ ]`) for multi-step work (e.g., an interview day with multiple rounds)
5. Use sub-issues (`parentId`) to break large hiring initiatives into trackable steps
6. Link to candidate files in this repo when applicable: `docs/candidates/{role}/{name}/{name}.md`

### Ticket Title Conventions

- Include the candidate's name when the task is about a specific person: "Schedule culture screen — Youssef Ahmed"
- Include the role when relevant: "Source senior-pam-core candidates on LinkedIn"
- Be specific: "Send offer to Shabi Mustafa" not "Offer stuff"

## Weekly Board Review

When asked to review or triage the hiring board:

1. **List all open hiring tickets** — `list_issues` with `team: "HAR"`, `label: "Hiring"`, grouped by priority
2. **Flag stale tickets** — anything High priority sitting in Backlog for 7+ days
3. **Check for completed work** — anything done that should be moved to Done
4. **Surface blocked tickets** — anything waiting on a candidate response, scheduling, or another person
5. **Cross-reference the CRM** — read `docs/candidates/README.md` and flag candidates whose pipeline stage doesn't have a corresponding active ticket
6. **Propose priority changes** — if a candidate is about to churn or a role has become more/less urgent

### Review Query

```
CallMcpTool: user-linear / list_issues
  team: "HAR"
  label: "Hiring"
  assignee: "me"
```

Show: Status, Priority, Title, Age (days since created).

## Common Workflows

### "Create a ticket for this candidate"

1. Look up the candidate file in `docs/candidates/` (use the candidate-crm skill if needed)
2. Create a ticket with `save_issue`:
   - `team: "HAR"`, `assignee: "me"`, `labels: ["Hiring"]`
   - Title follows naming convention above
   - Description includes candidate context and link to their file
   - Priority based on urgency

### "Plan out interviews for X"

1. Look up where the candidate is in the pipeline (frontmatter `stage`)
2. Determine which interviews are next based on the stage sequence: `sourced → culture_screen → short_circuit → technical → closing → offer`
3. Create a parent ticket: "Interview pipeline — {Candidate Name} for {role}"
4. Create sub-issues for each remaining step (scheduling, prep, debrief)
5. Present the plan before creating tickets

### "What's on my plate for hiring?"

1. Pull all open HAR tickets with the Hiring label
2. Group by priority
3. Cross-reference with the CRM pipeline (`docs/candidates/README.md`)
4. Highlight what's overdue or stale
5. Suggest what to focus on this week

### "Triage after a batch of interviews"

1. Ask what happened (or let Haroun dump notes)
2. Update candidate files in `docs/candidates/` via the candidate-crm skill
3. Update or close corresponding Linear tickets
4. Create new tickets for follow-up actions (schedule next round, send rejection, draft offer)

### "We need to hire for a new role"

1. Understand the role scope
2. Create a parent ticket: "Hire {role title}"
3. Create sub-issues for each phase:
   - Write JD
   - Set up interview pack
   - Source candidates
   - First batch of screens
4. Apply appropriate priority based on urgency

## Integration with Candidate CRM

This skill and the `candidate-crm` skill work together:

- **CRM** = source of truth for candidate data, stages, and interview notes (markdown files)
- **Linear** = task tracker for what Haroun needs to *do* about those candidates (schedule, prep, follow up, decide)

When updating one, check if the other needs updating too. For example, after moving a candidate to `closing` in the CRM, check if there's a Linear ticket to draft the closing doc.
