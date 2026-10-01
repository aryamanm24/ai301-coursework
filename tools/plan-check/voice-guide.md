# Voice guide: how I talk upstream

## Who I am in threads

I am a CS student making a first contribution to Path Review. My claim comment promised a repro, not a patch. My plan comment names the change I will make and how I will know it worked. Readers can expect short, specific comments in my own words, with the file I will touch and the command I will re-run.

## Rules I write by

### Rule: name the behavior, not "this bug"

Say the version (or commit) and the thing that is wrong, so the comment cannot be pasted onto another issue.

- Wrong: "I'd like to work on this bug, it looks like a good first issue."
- Right: "Picking this up: README tells you to set `OPENROUTER_API_KEY`, but `.env.example` only lists `mock`/`openai` and `OPENAI_API_KEY`."

### Rule: promise the next artifact, never a date

A claim comment names the repro I will post. A plan comment names the change and the check. Neither assigns a merge date or says the patch is guaranteed.

- Wrong: "Assign this to me, I will fix it by Sunday guaranteed."
- Right: "I will add `OPENROUTER_API_KEY` and an `openrouter` option to `.env.example`, then re-run the grep from my repro and post the output."

### Rule: say it like I would out loud

No "amazing project!!", no "kindly assign", no bot filler. One or two sentences I would actually say in a lab.

- Wrong: "Hello sir! Great project, I love Path Review and use it every day!! Looking forward to my first of many contributions here, thank you so much!"
- Right: "I am a first-time contributor. I reproduced the README / `.env.example` key mismatch on current main; report is in the next comment."

### Rule: my proof is my own words, even on a shared issue

Do not piggyback. If a classmate already reproduced it, I still write my environment and my commands.

- Wrong: "Same as above, can confirm."
- Right: "I ran the same check on macOS from commit `…`. After `cp .env.example .env`, grep shows `LLM_PROVIDER=mock` and `OPENAI_API_KEY` and no `OPENROUTER_API_KEY`."

### Rule: the plan is the change, not a redesign

The plan comment says the one file this issue needs. It does not bundle a rewrite, a new setting, or a migration the issue did not ask for.

- Wrong: "While I am in the env files I will also swap the HTTP client and add a settings panel for the timeout."
- Right: "The change is `.env.example` only. README, SETUP, and `core/config.py` already name the OpenRouter key, so I am leaving them as they are."

## Things I never post

- A deadline ("by tomorrow", "within 2 days").
- A request that the issue be reserved or assigned to me.
- A +1 or "any updates??" with no environment and no next step.
- A claim that I reproduced the bug when I only read someone else's comment.
- A root-cause story with no commands or output behind it.
