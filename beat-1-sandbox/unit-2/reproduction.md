# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

aryamanm24

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73#issuecomment-5825875127

I'll work on the README / `.env.example` mismatch: README says to add `OPENROUTER_API_KEY` after `cp .env.example .env`, but `.env.example` only lists `mock`/`openai` and `OPENAI_API_KEY`. I'll copy the example env, grep those three names against `core/config.py`, and post a repro report with my environment, the commands, and what I actually see. Not promising a patch yet.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73#issuecomment-5825875222

## Reproduction report — README and `.env.example` disagree about which LLM API key to set

Reproduced the docs/config mismatch on current `main`.

**Environment**

- OS: macOS 26.6.2 (arm64)
- Python: 3.14.7
- Repo: `codepath/pathreview-ai301-fa26-s3`
- Commit: `2f4e82f` (2026-09-16, default branch `main`)

**Steps** (from a fresh clone of `main`)

```bash
git clone https://github.com/codepath/pathreview-ai301-fa26-s3.git
cd pathreview-ai301-fa26-s3
git rev-parse --short HEAD   # 2f4e82f

# README Quick Start, line 24-25
# Configure environment (add your OPENROUTER_API_KEY to .env)
cp .env.example .env

grep -nE "OPENROUTER_API_KEY|OPENAI_API_KEY|LLM_PROVIDER" README.md .env.example .env
grep -nE "llm_provider|openai_api_key|openrouter" core/config.py
grep -n "OPENROUTER_API_KEY" .env || echo "OPENROUTER_API_KEY not found in .env"
```

**Observed**

`README.md`:

```
# Configure environment (add your OPENROUTER_API_KEY to .env)
cp .env.example .env
```

`docs/SETUP.md` also says to set `OPENROUTER_API_KEY`.

After `cp .env.example .env`, grep shows:

```
18:LLM_PROVIDER=mock
19:OPENAI_API_KEY=sk-your-key-here
```

and:

```
OPENROUTER_API_KEY not found in .env
```

`.env.example` documents only:

```
# Options: "mock" (default, no API key needed), "openai"
```

`core/config.py` defines both keys:

```
llm_provider: str = Field(default="mock")
openai_api_key: str = Field(default="")
openrouter_api_key: str = Field(default="")
```

**Expected**

Copying `.env.example` should agree with the README: if setup tells you to add `OPENROUTER_API_KEY`, the example file should list that variable and mention OpenRouter as a `LLM_PROVIDER` option.

**Actual**

README (and SETUP) tell you to set `OPENROUTER_API_KEY`. The example env has `LLM_PROVIDER=mock` and `OPENAI_API_KEY` only. The code already has an OpenRouter field. This is the mismatch in #73.

I did not start the app or call an LLM provider. This report is only the file mismatch a new setup hits after `cp .env.example .env`.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Full confirming run from `ai301-unit2-starter/eval/`: `python3 run_eval.py --rubric ~/.claude/skills/repro-check/rubric.md --evidence ~/.claude/skills/repro-check/references/evidence-guide.md --skill ~/.claude/skills/repro-check/SKILL.md --save-run …/beat-1-sandbox/unit-2/eval-run.txt`. Agreement **20/20** scored items `(bar: 18/20: PASS)`. Categories: `clear-accept 8/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4`. That is the only full run, and it is the agreement line in the committed `eval-run.txt`.

**Package analysis**

`pkg-20` (ghostty-org/ghostty#13604, category `disclosure`). Gold label: **reject**. My rubric: **reject**. The repro is otherwise complete: Environment names ghostty 1.3.1 on Fedora 42, the steps launch with `--config-default-files=false` and query `CSI ? 996 n`, and the artifacts show `^[[?997;2n` vs the conditional-theme control `^[[?997;1n`, matching the issue. The claim names mode-2031 and a next investigation step. Repo facts say: “All AI usage in any form must be disclosed, stating the tool used and the extent of the assistance.” Neither comment names an AI tool or that assistance was used, so `ai-disclosure` fails. The verdict rule accepts only if every required check is pass, so the package is reject — that is the one-item disclosure floor.

**Check rationale**

`ai-disclosure` as currently written in `tools/repro-check/rubric.md`:

> Evidence: Repo-facts `contribution policy` plus the claim comment and repro report.
> Pass condition: Pass if the policy does not require disclosing AI usage, or if it does and at least one of the comments names the AI tool or that AI assistance was used. Fail only when the policy requires disclosure (for example "must be disclosed", "all AI usage … must be disclosed") and neither comment discloses. Course packages are AI-assisted work. Conditions such as "understand the work" or "assistive AI allowed" without a disclose-ask are not a fail.
> Weight: required

I made this required because the eval set has exactly one disclosure-wall package, and a rubric with no conventions check cannot buy that miss back on volume. The pass condition is a require-vs-silent split, not “AI mentioned somewhere.” `pkg-07` (p5.js) discloses and passes; `pkg-05` (conda, permissive-with-responsibility, no disclose-ask) passes by silence; `pkg-20` is the fail.

**Trade-offs**

The quoted check rejects `pkg-20` and nothing else in the 20 scored items: that is the only bundle whose policy *requires* disclosure and whose comments do not. The full run’s `disclosure 1/1` line is how I know. What it gives up is that package — an otherwise excellent mode-2031 repro I would post on a repo that did not ask for a disclosure line. I am accepting that miss: posting AI-assisted work against a stated “must be disclosed” rule is the thing the floor exists to catch. Path Review’s CONTRIBUTING.md does not ask for disclosure, so the same check is silent on my #73 comments.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
