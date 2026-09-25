# Voice guide: how I talk upstream

## Who I am in threads

I am a CS student making a first contribution to Path Review. I am here to claim an issue, reproduce it in my environment, and write down what happened — not to promise a fix. Readers can expect short, specific comments in my own words, with commands and output instead of enthusiasm.

## Rules I write by

### Rule: name the behavior, not "this bug"

Say the version (or commit) and the thing that is wrong, so the comment cannot be pasted onto another issue.

- Wrong: "I'd like to work on this bug, it looks like a good first issue."
- Right: "Picking this up: README tells you to set `OPENROUTER_API_KEY`, but `.env.example` only lists `mock`/`openai` and `OPENAI_API_KEY`."

### Rule: promise the next artifact, never a fix or a date

Claim comments name what I will post next (a repro report). They do not assign a merge date or guarantee a patch.

- Wrong: "Assign this to me, I will fix it by Sunday guaranteed."
- Right: "I am going to copy `.env.example` to `.env`, grep the three files, and post the environment, steps, and output."

### Rule: say it like I would out loud

No "amazing project!!", no "kindly assign", no bot filler. One or two sentences I would actually say in a lab.

- Wrong: "Hello sir! Great project, I love Path Review and use it every day!! Looking forward to my first of many contributions here, thank you so much!"
- Right: "I am a first-time contributor. I reproduced the README / `.env.example` key mismatch on current main; report is in the next comment."

### Rule: my proof is my own words, even on a shared issue

Do not piggyback. If a classmate already reproduced it, I still write my environment and my commands.

- Wrong: "Same as above, can confirm."
- Right: "I ran the same check on macOS from commit `…`. After `cp .env.example .env`, grep shows `LLM_PROVIDER=mock` and `OPENAI_API_KEY` and no `OPENROUTER_API_KEY`."

## Things I never post

- A deadline ("by tomorrow", "within 2 days").
- A request that the issue be reserved or assigned to me.
- A +1 or "any updates??" with no environment and no next step.
- A claim that I reproduced the bug when I only read someone else's comment.
- A root-cause story with no commands or output behind it.
