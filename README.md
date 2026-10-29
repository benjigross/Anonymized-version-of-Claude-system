# AI Job Search + Deal Sourcing System (Claude)

The Claude system I use to run my venture job search, and the deal sourcing that comes with it.
The same work that surfaces roles also surfaces startups I'd want to invest in.

> **Anonymized.** This is the real architecture and the real instructions, with every personal or
> specific detail replaced by a generic placeholder: firms are "VC Firm 1, 2…", companies are
> "Startup 1, 2…", people are "Connection 1, 2…", newsletters are "Newsletter 1, 2…", and file
> paths, doc IDs, emails, schedules and personal context are removed. My tracker, contacts,
> emails, drafts, deal ideas, theses and writing examples are not included.

## How it's organized

```
CONTEXT.md (single source of truth: background, priorities, theses, rules)
│
├── Main agent ── uses saved skills, triggered by what I say
│     ├── daily-brief          Gmail, Calendar, docs + tracker → ranked priorities; reconciles the tracker
│     ├── log-role             a job link → firm research, fit score, LinkedIn warm paths, tracker row
│     ├── draft-writing        applications, emails, pitches in my voice (voice guide + writing library)
│     ├── review-email-draft   reviews my latest Gmail draft; never sends
│     ├── intro-blurb          thank-you to a connector + a short forwardable blurb
│     ├── interview-prep       firm dossier, portfolio research, pitches, question bank
│     ├── investment-diligence pitch / screen / IC memo / case study / portfolio research playbook
│     └── weekly-review        full pipeline review + top 5 actions
│
├── Scout (scheduled, twice a week)
│     scans job + funding newsletters → new roles into the tracker, thesis-fit companies into a deal-ideas log
│
└── Reviewer (independent of whoever drafted)
      1. Recipient: cold read with only what the real reader would see
      2. Editor: knows my voice and principles, not the drafting history
```

Only two jobs get their own agent, because only two need separate context: the Scout runs
unattended on a schedule, and the Reviewer must not grade its own work. Everything else is a skill.

## Guardrails
- **Draft only.** Nothing is sent, submitted or published by an agent. I send everything.
- **Verify before asserting.** Facts need a source; uncertain items are flagged, not guessed.
- **Primary sources first.** Direct links and company sites over aggregators and feeds.
- **Learns from edits, with scope.** When I correct a draft, the correction is saved with its scope
  (this piece / this firm / always), so one-off edits don't become blanket rules.

## What it gets wrong (and the fix)
- Turned one-off edits into blanket rules → corrections are saved with their scope.
- Missed context → the daily brief checks sent mail, drafts and docs, not just the inbox.
- Mischaracterized revenue models, funding data and other startup details → I verify those myself.
- Overstated fit ("maps directly") → the voice guide flags overselling language.

## Repo layout
- `CONTEXT.template.md`: the structure of the single context file (contents removed)
- `skills/`: the eight skills
- `agents/`: Scout (scheduled prompt) and Reviewer (two lenses)
- `voice/voice-guide.md`: writing rules distilled from my edits (personal examples removed)
- `writing-library/README.md`: how finals and Claude-draft → my-final pairs are stored and weighted

## Tools
Claude (desktop app + scheduled tasks), with Gmail, Google Drive/Docs, Google Calendar, a browser
(LinkedIn, job boards, company sites), an Excel tracker, and Python for tracker edits and a dashboard.
