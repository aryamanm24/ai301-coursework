# Evidence guide: where proof lives in a reproduction package

## Environment

- Where it lives
  - Eval bundle: the `Environment:` line (or a table of components) in the Candidate repro report; compare with the issue body's version/OS and with `bug reports:` under Repo facts.
  - Live: the draft repro comment, plus the issue's Environment section and the repo's bug template.
- What good looks like: the report names the tool version actually run and the OS/platform. If that version is not the issue's target, the report says so in one sentence. An empty report, or "it happens locally" with no version, is not an environment record.

## Steps

- Where it lives
  - Eval bundle: the numbered steps or fenced commands in the Candidate repro report.
  - Live: the draft repro comment; the issue body's steps are the trigger to match, not a substitute for the author's commands.
- What good looks like: a stranger could start from a stated state (fresh clone, playground link, `cp .env.example .env`) and type the same commands. Private repos, "our company monorepo (cannot share)", or `minikube start` with no driver on a Windows-driver issue are not followable.

## Behavior shown

- Where it lives
  - Eval bundle: fenced output, logs, CSS dumps, or traceback in the Candidate repro report, read against the Issue section's actual/expected behavior (panic vs validation error, missing `Content-Type`, blank pane, crash vs garbled text).
  - Live: the same artifacts in the draft, compared with the live issue body's symptom.
- What good looks like: the artifact is the issue's symptom, or it is clearly the author's actual result in a cannot-reproduce. A version banner, a session list, or a different error class is not the issue's behavior.

## Honesty

- Where it lives
  - Eval bundle: the report's first and last sentences (the claim about outcome) next to the artifacts in the same report. The Candidate claim comment is a second source for over-promising ("guaranteed reproducible", "I verified this race").
  - Live: draft claim + draft repro, same comparison.
- What good looks like: "reproduced" only when the artifact is the issue's behavior; "could not reproduce" when the shown run did not trigger it, with what differed named; no root-cause story without a transcript. Confident language does not replace the artifact.

## Comms

- Where it lives
  - Eval bundle: Candidate claim comment against the Issue title/body for specificity; Repo facts `contribution policy` for AI-disclosure and comment rules.
  - Live: the draft comment, the issue page, CONTRIBUTING.md / AI_POLICY.md / AGENTS.md on the repo.
- What good looks like: the claim names this issue's trigger or error and promises a report or investigation, not a merge or a date. If the policy says AI usage must be disclosed, the comments say so. Silence on AI is fine when the policy does not ask for disclosure.
