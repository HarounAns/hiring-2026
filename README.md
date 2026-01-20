# Pam AI - Hiring & Org Planning 2026

## Quick Start

```bash
npm run dev  # View interactive org chart
```

## Structure

```
hiring-2026/
├── README.md                 # You are here
├── team-structure.html       # Interactive org chart
├── team-data.json           # Org data (edit this to update chart)
├── hiring-proposal.md       # Q1 hiring proposal for Samee
│
└── docs/
    ├── context/             # Background info, company state, market
    │   └── jan-2026-state.md
    │
    ├── decisions/           # Decision records with rationale
    │   └── 001-q1-hiring-priorities.md
    │
    └── reviews/             # Periodic reviews (1mo, 3mo, 6mo, 1yr)
        └── TEMPLATE.md
```

## How to Use This

### Making Decisions
1. Write context in `docs/context/`
2. Record decisions in `docs/decisions/` using the ADR format
3. Link decisions to context

### Reviewing Progress
1. Set calendar reminders for 1mo, 3mo, 6mo, 1yr
2. Copy `docs/reviews/TEMPLATE.md` and fill it out
3. Compare actual vs predicted outcomes

### Updating the Org Chart
1. Edit `team-data.json`
2. Run `npm run dev` to view changes

## Key Documents

| Doc | Purpose | When to Update |
|-----|---------|----------------|
| `team-data.json` | Current + proposed org | When team changes |
| `hiring-proposal.md` | Q1 hiring plan | Before Samee sync |
| `docs/context/*` | Snapshot of company state | Each planning cycle |
| `docs/decisions/*` | Why we made choices | When decisions are made |
| `docs/reviews/*` | Did our decisions work? | 1mo, 3mo, 6mo, 1yr |

## Review Schedule

- [ ] **Feb 19, 2026** - 1 month review
- [ ] **Apr 19, 2026** - 3 month review
- [ ] **Jul 19, 2026** - 6 month review
- [ ] **Jan 19, 2027** - 1 year review
