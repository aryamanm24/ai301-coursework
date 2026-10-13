# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

- Where it lives
  - Eval bundle: Plan context (in scope, not in scope, deferred, deviation note) and the Diff, then Description sentences that say the PR matches the plan or that a named file or behavior landed.
  - Live: `plan.md` including `## Deviations`, `git diff main...HEAD`, and the Summary, Changes, and Notes sections of `pr_draft.md`.
- What good looks like: every hunk is the change the plan named, or both the plan and the description say what was left out. A new flag, a rename pass, or a function rewrite the plan did not name, under a sentence that says "exactly" or "no other changes", is drift. A description that says the docs were updated, when the diff has no docs file, is drift.

## Test evidence (harness category: not-tested)

- Where it lives
  - Eval bundle: the Test evidence section, and a fenced block in the Description when that section points there. The command to match is the failing path in the Plan context, not a control the repro already says succeeds.
  - Live: `test_evidence.md`, pasted into the Testing section of `pr_draft.md`. The before can be the unit-2 repro output. The after is the same commands on the branch.
- What good looks like: a fence shows the command and what it printed, before and after, on the path that used to fail. "Tests pass", "colors work now", and "verified for a full day" are not that output.

## Diff quality (harness category: unreviewable)

- Where it lives
  - Eval bundle: added lines in the Diff section.
  - Live: `git diff main...HEAD`. Committed files only.
- What good looks like: the added lines are the planned edit and its test. A commented-out print, a `DBG` or `DEBUG` line, a commented-out first attempt, an unused function, `dead_code`, an import regroup the plan did not ask for, or a hunk that repeats removed lines unchanged is debris. Rewrapping a line whose value actually changed is the edit.

## Standards and comms (harness category: standards-wall)

- Where it lives
  - Eval bundle: the Repo facts pull-requests line and contribution-policy line, read against the Description. A whatsnew file named in a required checklist is also checked in the Diff.
  - Live: `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`, read against `pr_draft.md`. The course disclosure goes in Notes for Reviewers.
- What good looks like: when the facts call the template a required checklist, the description links the issue and fills the checklist, and a named whatsnew entry is present. When the policy says all AI usage must be disclosed, the description says so. A template that only asks for a description, and a policy that does not require disclosure, are a pass when the description describes the change.
