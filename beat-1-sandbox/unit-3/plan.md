# Plan: make `.env.example` list the OpenRouter key README already tells you to set

Issue: https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73

## Diagnosis

The example env is behind the setup docs. The code already has the field.

From the repro I posted on #73 (macOS, `main` at `2f4e82f`):

README Quick Start says:

```
# Configure environment (add your OPENROUTER_API_KEY to .env)
cp .env.example .env
```

`docs/SETUP.md` says the same thing: edit `.env` and set `OPENROUTER_API_KEY`.

After `cp .env.example .env`, grep of the copy showed only:

```
18:LLM_PROVIDER=mock
19:OPENAI_API_KEY=sk-your-key-here
```

and `OPENROUTER_API_KEY not found in .env`. The options comment in `.env.example` is:

```
# Options: "mock" (default, no API key needed), "openai"
```

`core/config.py` already defines the field the docs name:

```
llm_provider: str = Field(default="mock")
openai_api_key: str = Field(default="")
openrouter_api_key: str = Field(default="")
```

So the mismatch is not a missing setting and not a README that should drop OpenRouter. Copying the example leaves out the variable the setup instructions tell you to fill in.

## Scope

In this change: `.env.example` only. Add `openrouter` to the `LLM_PROVIDER` options comment, and add an `OPENROUTER_API_KEY` placeholder next to `OPENAI_API_KEY`. Default stays `mock`, so a copied `.env` still runs with no key.

Not in this change:

- `README.md` and `docs/SETUP.md`. They already tell you to set `OPENROUTER_API_KEY`.
- `core/config.py`. `openrouter_api_key` is already defined. I am not adding a client, a new provider implementation, or the extra settings `openrouter_base_url` and `openrouter_model`. README does not mention those two, and this issue asks the example file and the README to agree on the key and the provider option.

## Files

- `.env.example`

## Approach

1. In the LLM section of `.env.example`, change the options comment so it lists `mock`, `openai`, and `openrouter`.
2. Add `OPENROUTER_API_KEY` with the same kind of placeholder `OPENAI_API_KEY` already uses, plus one comment that the line is for `LLM_PROVIDER=openrouter`.

## Test plan

Re-run the unit 2 commands from the repro comment, on this branch:

```bash
cp .env.example .env
grep -nE "OPENROUTER_API_KEY|OPENAI_API_KEY|LLM_PROVIDER" README.md .env.example .env
grep -n "Options:" .env.example
grep -n "OPENROUTER_API_KEY" .env || echo "OPENROUTER_API_KEY not found in .env"
grep -nE "llm_provider|openai_api_key|openrouter" core/config.py
```

After the fix I expect:

- `OPENROUTER_API_KEY` shows up in `.env.example` and in the copied `.env`. The "not found" line does not print.
- The options comment includes `openrouter`.
- README line 24 is unchanged (it still says to add `OPENROUTER_API_KEY`).
- The `core/config.py` grep is unchanged, including `openrouter_api_key`.

## Risks and unknowns

The placeholder matches the existing `sk-your-key-here` style. It is not a real key. `openrouter_base_url` and `openrouter_model` stay out of the example on purpose; if setup later needs them documented, that is a separate change. I have not started the app. This check is the file mismatch the repro already isolated.

## Deviations

Nothing changed between this plan and the branch. The diff is only `.env.example`: the options comment now lists `openrouter`, and `OPENROUTER_API_KEY` is the new line. README, SETUP, and `core/config.py` stayed as written above.
