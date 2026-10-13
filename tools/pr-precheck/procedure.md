# Procedure: how this tool grades a PR package

## Read order

1. Read the Plan context first. Write down the files or functions it will change, anything it marks not in scope or deferred, and the command or scenario its test plan says to re-run.
2. Read the Diff next, before the description. List each file and the behavior each hunk adds. Mark any added line that is a comment, a debug print, an unused function, or a repeat of a removed line.
3. Read the Description. Copy out sentences that claim the diff matches the plan, that nothing else changed, or that a named deliverable (docs, a flag, a setting) is present. Copy any sentence that says a piece was left out on purpose.
4. Read the Test evidence. Copy each fenced command and the output under it. If the section says the output is in the description, copy that fence too.
5. Read the Repo facts pull-requests line and the contribution-policy line. Note whether the template is called a required checklist, and whether AI usage must be disclosed.

## Evidence gathering

1. Plan fidelity: the scope list from step 1, the hunk list from step 2, and the claim sentences from step 3. A deferred item counts only when both the plan and the description name it.
2. Test evidence: the failing path from step 1 next to the fences from step 4. Prose with no fence is recorded as no output.
3. Diff quality: only the added lines marked in step 2. Do not use the description to excuse a debug line.
4. Standards: the two repo-facts lines from step 5 next to the description. For a whatsnew file a required checklist names, look at the diff file list from step 2 as well.

## Check execution

1. Grade in rubric order: plan-match, repro-shown, no-debris, standards.
2. Apply that row's pass condition to the notes above. Grade pass or fail. Use unclear only when the section the check names is missing from the package. A vague sentence is a fail when the pass condition says so.
3. Do not grade length, confidence, or how many commits there are. A short description that matches the diff passes. A long one that claims a file the diff does not contain fails.
4. Put one quote in the evidence field: the extra hunk, the missing fence, the debris line, or the policy sentence.

## Verdict assembly

1. Apply the verdict rule in rubric.md. Accept only when every required check is pass.
2. A fail or an unclear on any required check makes the verdict reject.
3. In the summary, quote the evidence line of the first required check that is not pass. If all pass, say accept and quote the plan's scope line.
4. End with the fenced JSON block. Write nothing after it.
