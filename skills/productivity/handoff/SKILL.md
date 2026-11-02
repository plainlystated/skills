---
name: handoff
description: Compact the current conversation into a handoff document for another agent to pick up.
argument-hint: "What will the next session be used for?"
disable-model-invocation: true
---

Write a handoff document summarising the current conversation so a fresh agent can continue the work.

Save it to `~/Sync/handoffs/handoff-<project>-<YYYY-MM-DD>-<slug>.md` (create the directory if missing). `<project>` is the repo or workspace name the work belongs to (e.g. `homebase`, `cjp`, `personal-admin`); `<slug>` is a short kebab-case description of the task. Project first so handoffs group by project when listed; date before slug so they sort chronologically within a project. This directory is synced across machines, so the doc is available wherever the next session runs. Do not save to the workspace or a temp directory.

Structure:

- YAML frontmatter, first thing in the file:
  ```yaml
  ---
  created: <ISO 8601 UTC, e.g. 2026-10-12T20:12:00Z>
  updated: <same value as created, at write time>
  status: open
  ---
  ```
  `status` is one of `open`, `done`, `blocked`, `partial`. These fields exist so handoffs can be pruned later by age and state; keep them machine-parseable.
- Title, then a header block: **Date**, **Tool** (what the worker should use, e.g. Claude in Chrome signed in to X), **Scope** (exactly what is and is not in bounds), **Status** (starts as `OPEN`).
- **Why**: enough context to make the steps make sense. Keep it short.
- **Steps**: numbered, concrete, with stop conditions ("if X, STOP and report").
- **Suggested skills**: which skills the next agent should call the Skill tool for.
- **Report back**: what the worker must record.
- **Result**: a placeholder section at the bottom.

End the doc with this instruction, verbatim, so the worker knows the doc is the channel for results:

> **Worker:** when you finish (or stop), update this file in place. In the frontmatter set `updated` to now (ISO 8601 UTC) and `status` to `done`, `blocked` or `partial`. Set **Status** in the header to match, with the date. Replace the **Result** section with what you actually did, what you observed, and anything the next person needs to know. Do not create a separate file.

Do not duplicate content already captured in other artifacts (specs, plans, ADRs, issues, commits, diffs). Reference them by path or URL instead.

Redact any sensitive information, such as API keys, passwords, or personally identifiable information.

If the user passed arguments, treat them as a description of what the next session will focus on and tailor the doc accordingly.
