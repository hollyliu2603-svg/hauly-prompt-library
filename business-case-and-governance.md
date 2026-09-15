# Business Case and Responsible Use

This section follows the why–what–how–impact model from Module 1, Topic 3 (La Trobe University, 2026) for a business case, then covers risks, safeguards and limitations.

## 1. Why change?

Hauly has one founder doing every operational job: answering support, sorting bugs, deciding what to build, moderating Circle, planning and writing content, and reviewing results. Each job is done by hand and from scratch. As the number of users grows, this workload grows with it, and there is no one else to share it with. Time spent on repetitive writing and sorting is time not spent improving the app.

## 2. What is the solution?

A library of ten tested prompts, one for each repeating job (see the [workflow table](README.md#2-the-workflow)). Module 1, Topic 3 describes prompt libraries as giving each automated workflow "a consistent, high-quality starting point". Each prompt:

- produces the same structure every time, so results can be compared and tracked
- has Hauly's real rules built in — no prices or shopping features, @usernames with an optional user-chosen first name, "lookalike" not "dupe", and Hauly's own ingredient pairing list
- says clearly what the AI must **not** do (guess causes, invent facts, remove posts, publish content)
- connects to the next step: structured outputs (for example Prompt 1's triage record) can be passed straight into another prompt (Prompt 2), which is where most of the automation potential comes from

The prompts **support** Holly rather than replace judgement. As Module 1, Topic 3 puts it, workflow automation "is not about replacing humans but about augmenting human performance".

## 3. How would it be put in place?

**Step 1 — Low-risk internal prompts first:** Prompts 1 (triage), 4 (bug summary), 5 (feature scoring) and 10 (weekly report). Nothing produced by these reaches users directly.

**Step 2 — User-facing drafts, always checked:** Prompts 2 (support replies), 8 (FAQ and articles) and 9 (notifications). Holly checks and approves everything before it is sent or published.

**Step 3 — Higher-risk judgement prompts, with extra checks:** Prompts 3 (ingredient report), 6 (trend analysis) and 7 (moderation). These deal with skincare information, possible misinformation, and other users' posts.

**Human-in-the-loop rules (Module 1, Topic 3 "escalation"):**

| Situation | What happens |
| --- | --- |
| Any reply, FAQ, article or notification | Holly approves before it goes out |
| Payment, safety, or data-loss messages | Flagged for Holly by Prompt 1 (`needs_human_review`) |
| A Circle post that may break the rules | AI only recommends; Holly decides |
| A trend with medical or exaggerated claims | Marked "not suitable" or "needs more evidence"; not published without fact-checking |
| Changes to the ingredient pairing list | Checked by Holly before use |

## 4. Impact — how success would be measured

**No time-saving or cost data has been collected yet.** The figures below are what a pilot would measure, not results.

| Area | What to measure in a pilot | Why it matters |
| --- | --- | --- |
| Efficiency | Minutes Holly spends per support reply, bug ticket and weekly report, before and after | Shows real time saved |
| Quality | Share of AI drafts sent with only minor edits | Shows whether drafts are usable |
| Accuracy | Number of invented facts or wrong labels found when checking outputs | Tracks the main risk found in testing |
| Consistency | Share of Prompt 1 results using only the allowed labels | Confirms data can be tracked |
| Moderation fairness | How often Holly overrules a Prompt 7 recommendation | Shows over- or under-flagging |
| Customer experience | Time from a support message arriving to a reply being sent | Shows the benefit to users |

**Evidence from testing so far:** in nine of the ten prompts, the final version followed its rules more closely than the first version (in Prompt 9 there was no visible difference) — for example, Prompt 2's reply fell from 231 words with an invented team to under 80 words with no invented details, and Prompt 5 correctly flagged a request that conflicts with Hauly's no-prices principle, which the first version had scored 4/5 for value. These are single test runs, not measured business results.

## 5. Risks and safeguards

Module 1, Topic 3 identifies three main risks of automating work with AI — hallucinations, bias and over-reliance — and three governance tools: audits, escalation and training. It also asks business cases to acknowledge data leakage.

| Risk | Where it showed up in testing | Safeguard in the prompts | Ongoing control |
| --- | --- | --- | --- |
| **Made-up information** ("hallucination") | Invented team (Prompt 2), invented bug cause (Prompt 4), invented app sections and outside facts (Prompt 6), guesses as facts (Prompt 10) | "Use only the facts given" rules; "(inferred)", "not provided" and "research questions" labels | Monthly check of a sample of outputs against the source messages |
| **Bias** | First version of Prompt 6 didn't check who a trend leaves out | Inclusive-language rule, testing against five types of users, and a self-check (Module 1, Topic 3 debiasing techniques); consistency self-check in Prompt 7 | Review how often moderation decisions are overruled, and for which types of posts |
| **Trusting the AI too much** ("over-reliance") | First version of Prompt 7 output "remove" | Nothing is sent, published or removed without Holly's approval | Keep the approval step even when outputs look reliable |
| **Privacy and data leakage** | Support messages and Circle posts contain personal information about users and others (e.g. a real name in the Prompt 7 test post) | Only the message text is used — no email addresses, payment details or account IDs | Only use AI tools whose data terms are suitable for user data |
| **Health-related misinformation** | First version of Prompt 3 reassured users that some pairings had "No concern here" | Hauly's own pairing list only, no "safe" claims, required disclaimer | Pairing list reviewed before any change |
| **Security** | Not tested | Prompts never ask for passwords, payment details or access to the app's systems | AI outputs are text only and never connected directly to app systems |

**Audits and training:** Holly keeps each prompt's known weak points (listed on each prompt page) and re-tests a prompt whenever it is changed or the AI model is updated.

## 6. Limitations

- **Testing was small.** Each version was run once on one sample input (plus one cross-check on GPT-4.1 mini for Prompts 1–7). AI outputs vary, so larger testing is needed before relying on any prompt.
- **Results differ between AI models.** In Prompt Lab, GPT-4.1 mini followed some rules less closely than Claude Sonnet 5 — for example, Prompt 6 marked the ice-rolling trend "suitable for founder review" and Prompt 2 hinted at data recovery. Any change of model should be followed by re-testing.
- **Prompt review scores are not proof.** Prompt Lab's review scored all tested prompts 72–91.5/100, including prompts whose outputs broke their own rules.
- **Sample inputs, not real data.** Test messages were written to match real Hauly features. Real user messages may be messier or more varied.
- **Rules reduce mistakes but don't remove them.** Prompt 6's final version still included a few outside statements, and Prompt 7's self-check was not proven to change decisions.
- **The AI only knows what is in the prompt.** It can't see the app's code, real user accounts, or live social media, so prompts must be kept up to date as Hauly changes. For example, Prompts 5 and 7 first said "@usernames only, never real names", but Hauly lets each user choose whether to add a first name. The wording was corrected and both prompts were re-tested.
- **Some prompts are only as good as their inputs.** Prompt 3 depends on Hauly's pairing list, and Prompt 10 depends on the other prompts' results being logged consistently.
