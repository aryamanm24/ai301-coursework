# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

- Where it lives
  - Eval bundle: the plan's Diagnosis, Cause, or first paragraph that names the mechanism, read only against the `## Repro evidence` section (failing run, controls, earlier-step artifacts). Thread highlights are a different family.
  - Live: the diagnosis in `plan.md`, read against the reproduction quoted in the draft or the author's posted repro comment on the issue. A cause that is not supported by quoted repro lines is ungrounded.
- What good looks like: the cause matches what the controls show. A control that succeeds without the blamed component, or an artifact that shows the damage already happened before the step the plan will edit, means the cause does not follow. A thread theory the controls contradict is not a grounded cause. A one-line cause that names the site the repro isolates is enough.

## Scope

- Where it lives
  - Eval bundle: the plan's in-scope list, proposed changes, and approach steps. Sentences that say not in scope, deferred, separately, later, will not, or follow-up are the boundary, not extra work.
  - Live: the same lists in `plan.md` and the plan comment. The issue body is the one behavior the change has to fit.
- What good looks like: one change at the site the cause names, plus a regression test. A rewrite, a new option or setting, a dependency migration, a UI panel, a retry framework, a new abstraction, a CI matrix, or a test-harness migration bundled into this change is creep, even if the core fix is also present. Deferring that work in a sentence is a bounded plan.

## Executability

- Where it lives
  - Eval bundle: file, module, function, or repro-isolated site in the Candidate plan, plus the sentence that says what edit happens there.
  - Live: the files and approach sections of `plan.md`.
- What good looks like: a stranger can open that site and make the stated edit. "Somewhere", "whichever is easier", "not sure which layer", and "optimize whatever profiling finds" are not a startable edit. Naming the module and the edit, while leaving the exact function to confirm during the build, is still startable.

## Test plan

- Where it lives
  - Eval bundle: the plan's Test plan section only, compared with the symptom and commands in Repro evidence.
  - Live: the test plan in `plan.md`, which should be the unit-2 repro steps re-run and the output expected after the fix.
- What good looks like: a command or repro step plus a checkable outcome (exit code, printed text, assertion, symptom gone, comparison to a named reference). "Should feel fast" or "nothing else should feel broken" does not decide success.

## Honesty

- Where it lives
  - Eval bundle: a Risk, unknown, or Deviations paragraph in the Candidate plan.
  - Live: the risks section of `plan.md`, and `## Deviations` after the build.
- What good looks like: an unknown is labeled as an unknown and the edit site is still specified. A deviation from the posted plan is written under Deviations with the reason. This family does not change the verdict unless a rubric check names it.

## Comms

- Where it lives
  - Eval bundle: Thread highlights (role OWNER, MEMBER, or COLLABORATOR) and the Repo facts contribution-policy line, both read against the Candidate plan comment. The plan body is not the comment.
  - Live: the issue thread and the repo's CONTRIBUTING.md or AI policy, read against `comment.md`.
- What good looks like: if a maintainer named a culprit file, posted a patched build to test, or stated the fix, the comment mentions that direction and the change follows it or names the option it is taking. If the policy says AI usage must be disclosed, the comment names the tool or that assistance was used. Silence on AI is a pass when the policy does not require comment disclosure. "Same approach as above" is not a plan comment.
