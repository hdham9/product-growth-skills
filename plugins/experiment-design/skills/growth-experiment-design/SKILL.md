---
name: growth-experiment-design
description: >-
  Brainstorm, shortlist, and design growth experiments for a chosen focus area. Use this once someone
  knows WHERE they want to grow (e.g. activation, retention, free→paid, referral) and needs to figure
  out WHAT to test and HOW. It picks up where a growth diagnosis leaves off. Triggers on: "what
  experiments should we run to improve [X]?", "help me design an A/B test / experiment", "brainstorm
  growth experiments for our onboarding/paywall/churn", "we want to improve activation — what should
  we try?", "turn this focus area into experiments", "design a test for [hypothesis]". Produces an
  ICE-scored shortlist, a top-3 experiment portfolio, and a full design for each (hypothesis, primary
  metric, intervention options, guardrails, risks, sample/duration, right-sized stats). Do NOT use it
  to diagnose WHERE to focus in the first place (that's a growth diagnosis), to read out / analyze a
  completed experiment's results, or to build analytics instrumentation.
---

# Growth Experiment Design

## What this skill does

It turns a **focus area** into a small set of well-designed experiments. Given where someone wants to
grow, it (1) brainstorms candidate experiments through five lenses, (2) scores them with ICE and
shortlists, (3) recommends a top-3 *portfolio*, and (4) designs each one to a "sufficient" standard —
hypothesis, primary metric, intervention, guardrails, risks, sample/duration, and right-sized stats.

The guiding belief: most teams either brainstorm narrowly (only product tweaks) or design sloppily
(no clear hypothesis, wrong metric, stats they can't support). A good process broadens the idea space,
then sharpens the few worth running.

This skill assumes the focus area is already chosen. Picking *where* to focus is a separate job (a
growth diagnosis). Analyzing results after an experiment runs is also separate. Hand off cleanly at
both ends.

## The method, end to end

1. **Get the focus area and context** (conversationally; accept a pasted diagnosis or a description).
2. **Brainstorm candidates** across the five lenses (mechanism, history, product, customer, market).
3. **Score with ICE and shortlist** (High/Medium/Low).
4. **Recommend a top-3 portfolio** optimizing impact, learning, and speed.
5. **Design each of the 3** — hypothesis → primary metric → intervention options → guardrails,
   implementation, risks, sample/duration → right-sized stats.
6. **Deliver the markdown report** and hand off to running + reading out.

Work through it conversationally. Don't fire a questionnaire — pull what you need as you go.

## Step 1 — Get the focus area and context

The user can **paste or reference the output of a growth diagnosis**, or just **describe the focus
area in their own words**. Either is fine — anchor on the driver they want to move.

Then gather the **five lenses** conversationally (these are also your brainstorming doorways in step 2):

- **Mechanism (levers):** which levers are available here — product, pricing, messaging, marketing,
  support, partnerships, sales?
- **History:** what's been tried in this area before, and what was learned (wins *and* dead ends)?
- **Product:** where's the friction, drop-off, or design/UX/UI weakness? Examine it through
  *discoverability* (can users find it?), *usability* (can they use it?), and *value* (do they want
  the outcome?).
- **Customer:** what do qual and quant insights say? And what open questions would we want an
  experiment to answer?
- **Market:** which similar or lateral companies offer inspiration? **Once the user has shared their
  own market view, offer to scan for 2–3 recent real-world examples** from comparable or adjacent
  products (use web search) to widen the brainstorm. Do this as an offer, not unprompted.

If the user is missing inputs, make reasonable, stated assumptions and proceed — momentum beats a
perfect intake.

## Step 2 — Brainstorm candidates across the five lenses

Generate a broad, non-redundant list of candidate experiments. Read `references/experiment-patterns.md`
and pull the proven patterns for this focus area as a starting menu — then push past them using the
five lenses so the list is specific to *this* product, not generic.

Aim for breadth: walk each lens deliberately and let it surface different ideas (e.g. the *history*
lens surfaces "re-run X but fix the flaw we found," the *market* lens surfaces "competitor Y does Z").
Capture each candidate as a one-liner with the lens it came from. Don't filter yet — quantity and
variety first.

## Step 3 — Score with ICE and shortlist

Score each candidate on **ICE**, each dimension **High / Medium / Low** (consistent with the diagnosis
skill's scale):

- **Impact** — if it works, how much would it move the focus-area metric?
- **Confidence** — how much evidence (from the five lenses) suggests it'll work?
- **Ease** — how cheap/fast is it to build and run?

Show the scores in a simple table with a one-line rationale each. Use the scores to cut the long list
down to a shortlist of the strongest candidates. Explain the reasoning, not just the letters.

## Step 4 — Recommend a top-3 portfolio

From the shortlist, choose **3** — but not simply the top-3 ICE scores. Choose a **portfolio that
optimizes across impact, learning, and speed**, unless the user directs otherwise. In practice that
usually means a balanced set such as:

- one **high-impact bet** (the big swing worth the effort),
- one **high-learning** experiment (resolves a key open question even if the direct metric impact is
  modest),
- one **fast/cheap win** (quick to ship, builds momentum).

State *why* each of the 3 earns its place on those three dimensions. If the user has a different
optimization (e.g. "we only care about speed this sprint"), follow their steer.

## Step 5 — Design each of the 3

For each of the three, build the design as a small funnel. Don't skip to a method before the
hypothesis and metric are clear.

**5a. Hypothesis + primary metric.**
- **Hypothesis:** *We believe [change] will cause [effect] for [audience] because [reasoning].*
- **Primary metric:** the single metric that decides success — as close to the focus-area driver as
  possible (use a leading indicator if the true metric is too slow/low-volume; note the tradeoff).

**5b. Generate 1–3 candidate interventions / methods.**
Offer up to three concrete ways to test the hypothesis — different interventions and/or different
methods (full build A/B, painted-door, concierge/Wizard-of-Oz, qual, etc.). Read
`references/experiment-methods.md` to pick methods that fit the change and the traffic. Briefly note
the tradeoff of each, then **let the user pick one**. Running autonomously (no user available), pick
the most promising and note the alternatives.

**5c. Flesh out the selected intervention.** Specify:
- **Guardrail / secondary metrics** — what must NOT get worse (e.g. don't lift signups by tanking
  retention; don't lift conversion by spiking refunds).
- **Practical implementation considerations** — what it takes to build/run, dependencies, where it
  lives in the product/funnel, tracking needed.
- **Risks** — what could invalidate it or cause harm (trust erosion, novelty effects, contamination).
- **Sample / duration** — who's in it and how long it runs (cover full business cycles).

**5d. Right-size the stats.** First decide whether a stats-heavy (powered A/B) approach even fits,
based on **traffic and stage** — can they reach a sensible MDE within a reasonable duration?
- If **yes**: note target MDE, confidence/power, rough sample/duration, and to fix the sample up
  front (or use sequential methods) to avoid the peeking trap.
- If **no**: **flag it explicitly** and give the **minimum-viable** guidance for that case — test
  bigger swings, loosen the confidence bar (e.g. 90%), use a leading indicator, or go
  painted-door/qualitative and triangulate. Be honest that the read will be directional, not
  definitive.
See `references/experiment-methods.md` for the thresholds, the four levers (baseline, MDE,
significance, power), and the low-traffic toolkit.

## Step 6 — Deliver the markdown report

Always produce a markdown file with this structure (clean prose + tables; no heavy visuals):

```
# Experiment Plan: [Focus area] — [Driver/objective]

## Context
[2–4 sentences: the focus area, why it matters, and a brief five-lens summary]

## Top 3 — recommended portfolio
[The 3, each with a sentence on why it earns its place across impact / learning / speed]

## Shortlist (ICE-scored)
[Table: candidate | Impact | Confidence | Ease | one-line rationale. The top 3 above are drawn from
this list; this section shows the full ranking and reasoning behind them.]

## Experiment designs
### 1. [Name]
- Hypothesis · Primary metric
- Intervention options (1–3) → Selected
- Guardrails · Implementation · Risks · Sample/Duration
- Stats approach (powered A/B or minimum-viable, with the flag)
### 2. [Name] …
### 3. [Name] …

## Next step
[Hand off: go run these, then read out the results]

## Appendix — full brainstorm
[All candidates, grouped by lens, so the breadth and reasoning are preserved]
```

Lead with the answer: the **top 3 portfolio comes before the full shortlist**, and the brainstorm
goes **last, as an appendix** — so the reader sees the recommendation first, with the full ranking
and raw idea space available below. (You still derive the shortlist first internally; this is just
the reading order.)

## Closing the design

End by naming the handoff: the plan says *what* to test and *how*; the next steps are to run it and
then read out the results (a separate job). Offer that as the natural follow-on rather than analyzing
hypothetical results here.

## Common pitfalls to steer the user away from

- **Narrow brainstorm** — only product tweaks; forgetting pricing, messaging, support, partnerships.
- **No clear hypothesis** — testing a change without stating the expected effect and why.
- **Wrong primary metric** — optimizing a metric that isn't close to the driver, or one too slow/low-
  volume to read.
- **Method-first thinking** — jumping to "let's A/B test it" before the hypothesis and traffic reality
  are clear.
- **Faking rigor** — running an underpowered A/B test and trusting a "no difference" or noisy "win."
- **No guardrails** — winning the primary metric while quietly breaking something else.
- **Three of the same** — a top-3 that's three variants of one idea instead of a balanced portfolio.
