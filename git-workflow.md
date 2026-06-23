# Git Workflow

## Before any work

Create a feature branch named after the ticket before touching any files:
```bash
git checkout -b feature/<TICKET-KEY>-<short-description>
```

## During work

Commit planning artifacts (proposal, design, tasks, mockups) on the feature branch — not on main.

## After archive

After `/opsx:archive` completes: `git checkout main && git pull`
