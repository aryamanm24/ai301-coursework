# Procedure: how this skill grades a plan package

## Read order

1. Read the Issue section first. Write down the one behavior the issue reports and nothing else.
2. Read the Repro evidence section next, before the plan. Write down what the failing run shows, and what each control, comparison, or earlier-step artifact rules in or out. This note is the only standard for the cause. Do not skip it because a thread comment already offers a cause.
3. Read Thread highlights. Write down only comments whose role is OWNER, MEMBER, or COLLABORATOR and that name a culprit file or function, post a patched binary or commit to test, or state the fix to make. Ignore questions and "contributors welcome".
4. Read the Repo facts contribution-policy line. Write down whether it requires disclosing AI usage in comments (the words "must be disclosed" or "all AI usage"). A rule about the pull request, human-written comments, or understanding the work is not that requirement.
5. Read the Candidate plan. Separate three lists: the cause sentence, the changes it will land in this change, and the changes it defers (not in scope, deferred, separately, later, will not, follow-up).
6. Read the Candidate plan comment last. It is the text that must mention a maintainer direction and any required AI disclosure. The plan body cannot substitute for it.

## Evidence gathering

1. Diagnosis: from step 2, the controls and the failing run. From step 5, the cause sentence. Do not gather the cause from Thread highlights.
2. Scope: from step 5, the will-land list only. Deferred lines are recorded so they are not counted as creep. Compare the will-land list to the one behavior from step 1.
3. Executability: from the plan, the named file, module, function, or repro-isolated site, and the verb of the edit (add, remove, clamp, refresh, set). "Investigate", "somewhere", and "whichever is easier" are the absence of an edit.
4. Test plan: from the plan's test plan only. Record the command or repro step and the outcome that decides success. Do not use the approach steps as the test.
5. Honesty: from the plan's risk or unknown lines. Record whether an unknown is labeled as unknown. This note is for the summary only; no required check reads it unless the rubric names one.
6. Comms: the direction note from step 3, the policy note from step 4, and the full plan comment from step 6.

## Check execution

1. Grade the checks in rubric order: cause-follows-repro, scope-bounded, stranger-can-start, test-observable, thread-direction, ai-disclosure.
2. For each check, apply that row's pass condition to the note gathered above. Grade pass or fail. Use unclear only when the section the check names is missing from the package, not when the plan is vague or confident. Vague is a fail when the pass condition says so.
3. Do not grade length, confidence, heading structure, or how polished the prose is. A short plan that meets the pass condition passes. A long plan that breaks it fails.
4. Quote one line from the package in the evidence field: the control that contradicts the cause, the extra change, the missing site, the subjective test sentence, the maintainer direction the comment skips, or the policy sentence.

## Verdict assembly

1. Apply the verdict rule in rubric.md. Accept only when every required check is pass.
2. A fail or an unclear on any required check makes the verdict reject. Preferred checks, if any, do not move the verdict.
3. In the summary, quote the evidence line of the first required check that is not pass. If all pass, say accept and quote the cause line.
4. End with the fenced JSON block the skill requires. The verdict field is accept or reject. Do not add text after the JSON.
