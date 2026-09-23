# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73

**Verdict output**

I graded three open Path Review issues with the installed `issue-select` skill and the rubric in `~/.claude/skills/issue-select/rubric.md` (the same file the eval run used). Path Review house rule from `scope.md`: classmate claim comments do not block. Fit ranking uses the profile in `scope.md` and does not change verdicts.

Accepted (fit order):

1. https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73 — README / `.env.example` key mismatch; named files, 1–2 hours, empty thread, docs/config fit.
2. https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68 — empty-index `ZeroDivisionError` with an xfail already pointing at `KeywordSearcher.index()`; classmate claim ignored under the house rule.
3. https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72 — `verify_password` should fail closed on a malformed hash; also accepted, same house-rule treatment of the claim comment.

Rejected: none of the three.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73",
    "checks": [
      {"name": "repo-not-archived", "grade": "pass", "evidence": "codepath/pathreview-ai301-fa26-s3 has archived: false on the repo API (no archived banner)."},
      {"name": "recent-commits", "grade": "pass", "evidence": "default-branch commits on 2026-09-16 by Aburke225; within 90 days of 2026-09-22."},
      {"name": "bounded-scope", "grade": "pass", "evidence": "collaborator-filed docs/config bug: make README.md and .env.example agree on OPENROUTER_API_KEY / LLM_PROVIDER; two named files, 1–2 hours."},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees none; no open linked PR; comment thread is empty. Path Review house rule would also ignore classmate claims."},
      {"name": "ai-policy-allows", "grade": "pass", "evidence": "no CONTRIBUTING.md, AI_POLICY.md, or AI_USAGE_POLICY.md in the repo; silence passes."},
      {"name": "recent-release", "grade": "fail", "evidence": "no GitHub releases published (preferred only; does not change the verdict)."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/68",
    "checks": [
      {"name": "repo-not-archived", "grade": "pass", "evidence": "same Path Review repo; archived: false."},
      {"name": "recent-commits", "grade": "pass", "evidence": "same 2026-09-16 default-branch commits; within 90 days of today."},
      {"name": "bounded-scope", "grade": "pass", "evidence": "one named behavior: KeywordSearcher.index([]) must not raise ZeroDivisionError; files rag/retriever/keyword_search.py and tests/unit/test_keyword_search.py."},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees none; no open linked PR. acordero4852 commented 2026-09-19 'I'd like to take this one on'; Path Review house rule: classmate claims do not block."},
      {"name": "ai-policy-allows", "grade": "pass", "evidence": "repo is silent on AI (no CONTRIBUTING.md)."},
      {"name": "recent-release", "grade": "fail", "evidence": "no GitHub releases published (preferred only)."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72",
    "checks": [
      {"name": "repo-not-archived", "grade": "pass", "evidence": "same Path Review repo; archived: false."},
      {"name": "recent-commits", "grade": "pass", "evidence": "same 2026-09-16 default-branch commits; within 90 days of today."},
      {"name": "bounded-scope", "grade": "pass", "evidence": "one named behavior: core/security.py verify_password must return False on UnknownHashError instead of raising; covering xfail in tests/unit/test_security.py."},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees none; no open linked PR. sseid4 commented 2026-09-22 claiming it; Path Review house rule: classmate claims do not block."},
      {"name": "ai-policy-allows", "grade": "pass", "evidence": "repo is silent on AI (no CONTRIBUTING.md)."},
      {"name": "recent-release", "grade": "fail", "evidence": "no GitHub releases published (preferred only)."}
    ],
    "verdict": "accept"
  }
]
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1. Full confirming run from `ai301-unit1-starter/eval/`: `python3 run_eval.py --rubric ~/.claude/skills/issue-select/rubric.md --skill ~/.claude/skills/issue-select/SKILL.md --save-run …/beat-1-sandbox/unit-1/eval-run.txt`. Agreement **20/20** scored items `(bar: 18/20: PASS)`. Categories: `claimed 4/4  clear-accept 8/8  dead-repo 3/3  policy 1/1  scope 4/4`. That is the only full run, and it is the agreement line in the committed `eval-run.txt`.

**Issue analysis**

`issue-12` (bookwyrm-social/bookwyrm#1133, category `policy`). Gold label: **reject**. My rubric: **reject**. Repo facts on the 2026-08-12 snapshot show an active repo (default-branch commits through 2026-08-12), a bounded UI enhancement (“Include in-progress books in the reading-goal progress-bar”), assignees `none`, and linked PRs `none`. Those required checks pass. The contribution-policy line quotes BookWyrm’s contributing docs: `"We do not accept AI-generated code or documentation."` That is an outright ban, so `ai-policy-allows` is fail. The verdict rule accepts only if every required check is pass, so the issue is reject even though every other family looks like a first issue.

**Check rationale**

`ai-policy-allows` as currently written in `tools/issue-select/rubric.md`:

> Evidence: The `contribution policy` line under Repo facts (live: CONTRIBUTING.md, linked contributor docs, AI_POLICY.md / AI_USAGE_POLICY.md).
> Pass condition: Pass if the repo is silent on AI, has no CONTRIBUTING.md, or allows AI-assisted work with conditions (disclose, understand, test, human-review, "assistive AI allowed", "fully AI-generated PRs not accepted" while assistive use is allowed, "discouraged without human review"). Fail only on an outright ban of AI-generated code or documentation (for example "we do not accept AI-generated"). Conditions are not bans.
> Weight: required

I made this required after the policy category in the eval set: a first issue that is alive, bounded, and free is still the wrong first issue if the project will close an AI-assisted PR on sight. The pass condition is a ban-vs-conditions split, not a vibe check. Silence passes because most repos (including Path Review) state nothing. `issue-10`’s “strongly discourages generative AI … without human review” stays pass, because discouragement-with-review is a condition. `issue-12` is the fail.

**Trade-offs**

The quoted check rejects `issue-12` and nothing else in the 20 scored items: that is the only bundle whose policy line is an outright ban, and the full run’s `policy 1/1` line is how I know. What it gives up is that issue — a good-first-issue UI change in an active repo I would otherwise take. I am accepting that miss on purpose: walking into a stated “we do not accept AI-generated code or documentation” rule wastes a maintainer’s time and mine. Preferred `recent-release` is the other side of the same design: it fails `issue-06` (`latest release: none published`) but cannot flip that verdict, so a living repo with no tags still accepts.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. Fit and time: #73 is a docs/config mismatch with two named files (`README.md`, `.env.example`) and a 1–2 hour estimate. That matches what I said I wanted: a bounded first contribution I can finish in a few sessions, not a product feature. It is labeled `bug`, `docs`, `good first issue`, and `tier-1`. #68 and #72 are also accepted Python bugs with xfails, but #73 is the one I can reproduce just by reading two files and I want that for Unit 2.

2. What the verdict got right / what I weighed: the skill correctly accepted it — repo is not archived, commits landed 2026-09-16, the change is one named agreement between two files, nobody is assigned, and the repo is silent on AI. `recent-release` failed (no releases) and did not matter, which is the point of preferred. What I weighed that the rubric cannot: the thread is empty, so I will not be stacking a claim on top of a classmate who already posted a plan, and the opener is a collaborator, so the intended edit is already specified.

3. Anticipated difficulty in claiming it: Path Review says classmate comments do not block, and this issue has none yet, so the claim itself should be straightforward. The actual risk is a small one: I have to keep the README and `.env.example` in sync with `core/config.py` without inventing a third key or rewriting the setup docs. I have not posted a claim comment; that is Unit 2.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
