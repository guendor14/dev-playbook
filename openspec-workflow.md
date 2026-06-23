# OpenSpec Workflow

## Proposing new work

When the user describes a new user story, feature, or bug fix:
1. Create the Jira ticket first via MCP — do not create any OpenSpec artifacts yet.
2. Stop there. The user runs `work-on-ticket` to trigger the full artifact pipeline.

Never create proposal, design, tasks, or specs before the Jira ticket exists.

## Implementation lifecycle

Never implement directly. Always follow the full flow:

1. `/opsx:propose` — create the change folder, proposal, design, tasks. For any UI-touching change, spawn the designer subagent to produce mockups and place them in `assets/` **before** presenting artifacts for approval. Every new or modified page needs a mockup.
2. `/opsx:apply` — implement through tracked tasks only.
3. `/opsx:archive` — archive when all tasks are complete, then run post-archive steps (see below).

## Post-archive steps (run automatically, in order, without waiting for the user to ask)

1. **Transition the Jira ticket to "Done"** — derive the issue key from the branch name (e.g. `feature/SON-55-*` → `SON-55`). Call `getTransitionsForJiraIssue` first to find the correct transition ID, then call `transitionJiraIssue`.
2. **Build the app** — project-specific build command (see project CLAUDE.md).
3. **Checkout main and pull** — `git checkout main && git pull`

Never skip or defer these steps.

## After implementation: sync specs

After any implementation — even bug fixes and refactors — review the relevant capability specs and update them if the behavior changed. Use the `openspec-sync-specs` skill via subagent — do not manually write spec files with the Write tool.

## OpenSpec CLI safety

Never run `openspec archive` CLI. It moves folders to an `archive/` subfolder which may violate project conventions. Completion is tracked via `.openspec.yaml` only.

## Spec location

Specs live inside the SON folder that introduced or last updated them:
```
openspec/changes/son-49-pack-selection-screen/
  specs/
    pack-selection-screen/
      spec.md
```

There is no top-level `openspec/specs/` directory.

## Change folder naming

`son-{number}-{description}` — SON number always first.
- Fix qualifier goes after the number: `son-14-fix-agent-metadata-empty-response`
- No date prefix — the date is in git history
- All folders live flat under `openspec/changes/` — no `archive/` subfolder

## Assets and mockups

Mockups and design assets belong inside the SON folder under `assets/`. Never in a project-level `assets/` directory.
