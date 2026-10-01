# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

aryamanm24

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73#issuecomment-5922255538

Plan for #73, from the repro I posted above (main at `2f4e82f`).

After `cp .env.example .env`, grep showed `LLM_PROVIDER=mock` and `OPENAI_API_KEY` only, and `OPENROUTER_API_KEY` was not in the copy. README line 24 and `docs/SETUP.md` both tell you to set that key, and `core/config.py` already has `openrouter_api_key`. The example file is the one that is behind.

I will change `.env.example` only: add `openrouter` to the `LLM_PROVIDER` options comment, and add an `OPENROUTER_API_KEY` placeholder beside `OPENAI_API_KEY`. Default stays `mock`. I am not editing README, SETUP, or `core/config.py`, and I am not wiring a new client.

Check: re-run that same `cp` and grep. `OPENROUTER_API_KEY` should show up in the copied `.env`, the options comment should include `openrouter`, and the config grep should be unchanged.

---

## Your branch

**Branch**

docs/73-env-example-openrouter

**Evidence**

Before, on `main` at `2f4e82f`, the commands from the repro comment:

```bash
cp .env.example .env
grep -nE "OPENROUTER_API_KEY|OPENAI_API_KEY|LLM_PROVIDER" README.md .env.example .env
grep -nE "llm_provider|openai_api_key|openrouter" core/config.py
grep -n "OPENROUTER_API_KEY" .env || echo "OPENROUTER_API_KEY not found in .env"
```

`README.md`:

```
# Configure environment (add your OPENROUTER_API_KEY to .env)
cp .env.example .env
```

After `cp .env.example .env`, grep showed:

```
18:LLM_PROVIDER=mock
19:OPENAI_API_KEY=sk-your-key-here
```

and:

```
OPENROUTER_API_KEY not found in .env
```

`.env.example` options comment:

```
# Options: "mock" (default, no API key needed), "openai"
```

`core/config.py`:

```
llm_provider: str = Field(default="mock")
openai_api_key: str = Field(default="")
openrouter_api_key: str = Field(default="")
```

After, on `docs/73-env-example-openrouter`, same checkout, same commands plus the options line from the test plan:

```bash
cp .env.example .env
grep -nE "OPENROUTER_API_KEY|OPENAI_API_KEY|LLM_PROVIDER" README.md .env.example .env
grep -n "Options:" .env.example
grep -n "OPENROUTER_API_KEY" .env || echo "OPENROUTER_API_KEY not found in .env"
grep -nE "llm_provider|openai_api_key|openrouter" core/config.py
```

```
README.md:24:# Configure environment (add your OPENROUTER_API_KEY to .env)
.env.example:18:LLM_PROVIDER=mock
.env.example:19:OPENAI_API_KEY=sk-your-key-here
.env.example:20:# Required when LLM_PROVIDER=openrouter. README Quick Start tells you to set this after copying the example.
.env.example:21:OPENROUTER_API_KEY=sk-or-your-key-here
.env:18:LLM_PROVIDER=mock
.env:19:OPENAI_API_KEY=sk-your-key-here
.env:20:# Required when LLM_PROVIDER=openrouter. README Quick Start tells you to set this after copying the example.
.env:21:OPENROUTER_API_KEY=sk-or-your-key-here
```

```
17:# Options: "mock" (default, no API key needed), "openai", "openrouter"
```

```
21:OPENROUTER_API_KEY=sk-or-your-key-here
```

The "not found" line did not print. `core/config.py` was unchanged:

```
18:    llm_provider: str = Field(default="mock")
19:    openai_api_key: str = Field(default="")
20:    openrouter_api_key: str = Field(default="")
21:    openrouter_base_url: str = Field(default="https://openrouter.ai/api/v1")
22:    openrouter_model: str = Field(default="google/gemma-3-27b-it:free")
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Smoke from `ai301-unit3-starter/eval`: `python3 run_eval.py --rubric ~/.claude/skills/plan-check/rubric.md --evidence ~/.claude/skills/plan-check/references/evidence-guide.md --only pkg-01,pkg-02,pkg-04,pkg-20,calib-03 --include-calibration`. All five came back `ERROR` because the Claude CLI exited 1 with `Failed to authenticate. API Error: 401 OAuth access token is invalid.` No agreement line was printed. A partial run cannot write `eval-run.txt`, and this one did not grade any package, so it is not a scored run.

**Package analysis**

`pkg-02` (sharkdp/bat#3844, category `clear-accept`). Gold label: **accept**. Reading the package against the rubric as written, every required check passes, so the verdict is **accept**. The cause names the usize underflow at the two subtraction sites, and the repro controls fit that cause: no background means no subtraction, and width 2 means no overshoot. Scope is one saturating clamp in `src/printer.rs`, with the wide-char redesign marked not in scope. A stranger can start at those two sites. The test re-runs the repro and expects drawn output and exit 0. The thread has no comments, and the contribution policy states no AI policy, so thread-direction and ai-disclosure pass. The harness never returned a model verdict for this package; the reading above is the rubric applied to the bundle, not a line from `eval-run.txt`.

**Check rationale**

`cause-follows-repro` as it reads now in `tools/plan-check/rubric.md`:

> Evidence: The plan's stated cause (the Diagnosis, Cause, or opening paragraph that names what is wrong) read against the Repro evidence section only. Thread comments are not repro evidence.
> Pass condition: Pass if that cause is consistent with the repro's failing run and its controls: it explains the behavior the artifacts show, and no control, comparison, or earlier-step artifact in the Repro evidence contradicts it. Fail if any of these is true: (1) a control shows the blamed component already behaving correctly, or shows the symptom on a path that does not involve that component; (2) the symptom disappears when a subsystem the plan calls unrelated is turned off, or remains when the blamed component is not running; (3) an earlier artifact shows the data already damaged or discarded before the step the plan will change, so that later step cannot restore what the artifact shows is gone. A short cause that names the site the repro isolates passes. Quoting a thread comment whose theory the controls contradict is a fail. If the Repro evidence section is absent, grade unclear.
> Weight: required

It reads that way because the activity's hold on calib-03 was a cause taken from a thread comment while the repro controls showed the wait tracks highlighting, including a run with the pager out of the loop. A check that only asks whether a cause is named lets that through. The three fail rules are the control patterns in the wrong-cause packages: a blamed component the control already shows working, a subsystem the plan calls unrelated that the control turns off, and damage that is already gone before the step the plan will edit.

**Trade-offs**

The check holds a plan whose stated cause fights its own repro, and it lets a short cause through when that cause names the site the repro isolates. What it gives up is a wrong cause the repro never tests. If the bundle has no control and no earlier artifact, a confident mismatch can still pass. I am accepting that miss: the procedure says to write down what the controls rule out before reading the plan, and a package with no such control is not the failure this check is built to catch.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
