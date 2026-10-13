---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer one question: is this pull request ready to submit? A PR package is a title, a description, the commits, the diff, and the test evidence, read against the plan the PR claims to implement and the issue that plan belongs to. Do not grade the plan by itself, and do not grade more than one package in a run.

## Inputs and modes

Live mode checks the student's own PR before it is opened. Read only these inputs:

- `plan.md` in the working copy, including any text under `## Deviations`.
- The branch diff from `git diff main...HEAD` (three dots), run in the working copy. That diff is every committed change on the branch. Uncommitted files are not part of the diff.
- The draft title and description in `pr_draft.md`.
- The captured command output in `test_evidence.md`.
- The issue URL named in the command. From that issue, read the thread. From the scoped repo, read `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`.

A house-chain student has no plan of their own. Read the house plan and the house repro pack wherever this frame says `plan.md` and the unit-2 repro.

Eval mode grades one package bundle. The bundle text is the whole world. Do not fetch anything and do not read `scope.md` or `voice-guide.md`. Grade every check and apply the full verdict rule.

## The scope seam (live mode only)

Before grading in live mode, read `scope.md`. Grade only a pull request against the repo on the `Repo:` line. If that line still has a placeholder, stop without grading and tell the student to replace it with their section's Path Review repo. Do not guess a repo. In eval mode, ignore `scope.md`.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` and hold the PR title and the description against those rules. In the summary, quote each rule the draft breaks. The voice guide does not change the verdict unless a rubric check names it. In eval mode, ignore `voice-guide.md`.

## Component reads

Read `rubric.md` for the checks and the verdict rule. Read `references/evidence-guide.md` for where each family of evidence lives. Execute `procedure.md` as written. If a procedure step does not say where to look or what to record, report that gap in the summary and do not invent a step. If `rubric.md` has no checks, or `procedure.md` has no steps, stop and say the tool cannot grade without them.

## Verdict and output

The verdict is `accept` (ready to submit) or `reject` (hold). There is no third verdict. End the reply with this fenced JSON block, valid and last, and write nothing after it:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

A short line per check may come before the block.

## Grading discipline

Name the quote or fact that decided each check. Grade the diff, the test output, and the description's claims, not the length or the polish of the prose. If a check passes by the rubric's stated condition, it passes even if it feels wrong. Follow `procedure.md` and report a gap instead of filling it. If the verdict rule does not say what `unclear` does, treat `unclear` on a required check as fail.
