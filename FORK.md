# plainlystated fork

Fork of [mattpocock/skills](https://github.com/mattpocock/skills) carrying my
customizations as commits on `main`. To take upstream updates:

```bash
git fetch upstream && git merge upstream/main && git push
```

## Deltas vs upstream

### skills/engineering/to-spec

- Tracker hardcoded to GitHub Issues in the current repo (upstream defers to `/setup-matt-pocock-skills` config, which my repos don't have).
- Added process step: ask "Is there a ClickUp ticket for this?" and carry the number into the spec.
- Publishes with the `PRD` label (kept from my old write-a-prd flow) instead of `ready-for-agent`.
- Added step: create a GitHub milestone named after the feature and attach the spec issue — to-tickets attaches implementation issues to it later.
- Spec template gains a `## ClickUp` section (`Closes ClickUp #<number>`, omitted when none).

### skills/engineering/to-tickets

- Tracker hardcoded to GitHub Issues in the current repo; local-markdown publish path and its template removed.
- Dropped the `ready-for-agent` label.
- Added: look up the parent spec issue's milestone (created by to-spec) and attach each ticket to it; ask before creating one if missing.
- Issue template gains a `## Type` section (exactly `HITL` or `AFK`).
- HITL slices get a `HITL: ` title prefix — this is what `ralph-once` matches on to route the ticket to an interactive session instead of an AFK worker.
