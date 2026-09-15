# 4. Bug Report Summarisation for Dev Handoff

**What it does:** Turns a raw, messy user bug report into a clean,
structured ticket ready to hand to a developer.

**Technique used:** RACE structure, plus breaking the task into fixed
sections (steps to reproduce, expected vs. actual behaviour, severity) so
nothing gets missed.

> **Role:** You are converting raw user bug reports into a structured ticket for a
> solo developer.
>
> **Action:** Extract the details needed to action the bug without re-reading the
> original message(s). Do not infer the technical cause of the bug unless the
> source message provides evidence for it.
>
> **Context:** Technology stack, if relevant and confirmed: {{tech_stack}}.
> Message(s): "{{messages}}"
>
> **Expected output:** Steps to reproduce (numbered, inferred if not explicit —
> mark inferred steps with "(inferred)"); expected vs actual behaviour; device/OS
> details if mentioned, else "not provided"; suspected affected tab/feature;
> severity guess (cosmetic / functional / blocking) with one-sentence reasoning.

**v1 → v2 note:** An earlier version let the AI guess at the technical cause
of the bug freely. That's risky — a confident-sounding but wrong diagnosis
could send a developer down the wrong path. The fix was a direct rule: only
infer a cause if the user's message actually gives evidence for it, and mark
any inferred reproduction steps as "(inferred)" rather than stating them as
fact.

**Why it matters:** Switching between the support inbox and the codebase is
expensive for a solo developer, and raw user language rarely maps neatly to
a workable ticket.

**How much can run on its own:** High — this is meant to save time on every
bug report, and gives a consistent ticket format for whatever backlog tool
is used.

**Watch out for:** Inferred steps could be wrong, and are labelled as such
rather than stated as fact; severity still needs a human sanity-check before
prioritising. The tech stack is only used if confirmed — naming an unconfirmed
stack risks a false-confidence diagnosis the AI can't actually verify.
