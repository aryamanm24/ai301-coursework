# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s3/pull/185

**Branch**

docs/73-env-example-openrouter

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

No scored harness run was saved. `python3 run_eval.py` grades by calling the `claude` CLI, and that login returns `Failed to authenticate. API Error: 401 OAuth access token is invalid.` A run of errored packages is not an agreement score, and a partial or failed run cannot be the `--save-run` file. `beat-1-sandbox/unit-4/eval-run.txt` is still the starter placeholder, so there is no agreement line in it to match.

**Package analysis**

`pkg-17` (vuejs/core#14893, category `silent-drift`). Gold label: **reject**. Reading the package against `plan-match` as written, the verdict is **reject**. The plan names two deliverables: a dev-mode warning in `reactive.ts`, and an update to the reactivity-core docs. The description says the documentation now documents the limitation. The diff contains the warning and does not contain the docs page. The description does not say the docs were left out. That is the fail sentence in the check: the description claims a deliverable the diff does not contain. The other three checks would not save it. The verdict rule accepts only when every required check passes.

**Check rationale**

`plan-match` as it reads now in `tools/pr-precheck/rubric.md`:

> Evidence: The Diff, read against the Plan context scope (in scope, not in scope, deferred, deviation note) and against Description sentences that say what the diff contains or does not contain.
> Pass condition: Pass if every change in the diff is the change the plan names. A piece the plan marks deferred, not in scope, or a known limit is not a deliverable of this PR, and leaving it out passes when the description says so too. Fail if the plan names a deliverable and the diff does not contain it, unless the description states that omission. Fail if the diff adds behavior the plan did not ask for or marked out of scope (a new flag or config option, a rename pass, a rewrite of a function the plan did not name, unrelated help-text edits) while the description claims the PR matches the plan ("exactly", "exactly as planned", "implements the posted plan", "no other behavior changes", "no functional changes outside"). Fail if the description claims a deliverable the diff does not contain, such as a docs page the diff never edits.
> Weight: required

It reads that way because the activity's hold was a description sentence that was not true of the diff. A check that only asks whether the fix is present lets through both extras the description calls "exactly the plan" and a missing file the description says landed. The deferred-piece sentence is there so a plan that already names a limit, and a description that repeats it, still passes.

**Trade-offs**

The deferred-piece sentence is what lets an honestly disclosed shortfall through. `pkg-13` states in the plan and again in the description that `%VAR%` expansion is not handled, and the diff does not add it. That package stays a pass on this check. What the sentence gives up is a quiet omission: if the plan named a docs page and neither the diff nor the description mentioned it, a grader can still miss the gap when the plan's wording looks like a note rather than a deliverable. I am accepting that miss. The fail I wrote is for a description that claims the missing piece, which is the drift `pkg-17` actually shows.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
