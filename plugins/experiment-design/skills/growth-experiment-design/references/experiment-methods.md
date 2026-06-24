# Experiment Methods & Right-Sized Stats (the toolbox)

Use this when choosing *how* to test an intervention and *how rigorous* the stats should be.
Pick the method that fits the change and the traffic — don't default to a powered A/B test when the
team can't support one. The most important judgment call is **whether a stats-heavy approach even
fits** (Part 2); make that call first, then design accordingly.

---

## Part 1 — Methods catalog

For each method: what it is, when to use it, and what it's good/bad for.

### A/B test (controlled online experiment) & A/B/n
Randomly split users between control (A) and one or more variants (B, C…); compare a target metric.
Randomization is what makes it causal — seasonality and external events hit both arms equally and
cancel out.
- **Use when:** you have enough traffic to detect a meaningful effect and can randomize at the user
  level. The default for a clear yes/no hypothesis on a single change.
- **Good for:** clean causal reads isolating one change.
- **Bad for:** low traffic (can't reach significance), network-effect products (treatment leaks into
  control — use switchback), and many variants at once (A/B/n multiplies required traffic and
  false-positive risk unless you correct for multiple comparisons).

### Multivariate test (MVT)
Tests several element changes simultaneously in combination (full factorial) to measure each
element's effect *and* their interactions.
- **Use when:** high traffic, and you already know which elements matter.
- **Good for:** interaction effects; squeezing incremental gains on high-traffic pages.
- **Bad for:** anything under ~50K monthly visitors — traffic splits across all combinations, so a
  24-combination MVT needs ~12,000+ conversions. If projected duration exceeds ~4–6 weeks, skip it.

### Holdout / holdback group
A group deliberately kept on the old experience (a "global control") to measure the **cumulative**
impact of everything shipped over a quarter/year, not one experiment.
- **Use when:** you want true aggregate impact, want to catch slow-burn regressions, or to correct
  for summed individual wins overstating reality (novelty, interactions, artifacts inflate the sum).
- **Good for:** long-horizon measurement; de-duplicating overlapping experiment claims.
- **Bad for:** fast iteration (you withhold improvements). Typical size: ~5–10% of users.

### Painted-door / fake-door / smoke test
Expose a not-yet-built feature (button, menu item, landing page); measure how many try to use it; a
click reveals "coming soon" / a waitlist. A *smoke test* validates a whole product concept; a
*fake/painted door* validates a single feature inside an existing product.
- **Use when:** pre-build demand validation — deciding whether something is worth building, often the
  only option at low traffic.
- **Good for:** cheap, fast read on *interest/demand* before any engineering.
- **Bad for / risks:** tells you *how many* want it, not *why* or what they expected behind the door;
  doesn't measure willingness to pay or usability; curiosity clicks inflate it; overuse erodes trust
  (users who hit "coming soon" can feel deceived). Keep it out of critical/regulated flows.

### Concierge vs. Wizard of Oz vs. Painted door
All three "fake it before you make it," but differ on *what* is faked and whether the human is visible:

| Method | What the user sees | Human effort | Best for |
|---|---|---|---|
| **Painted/fake door** | Only an invitation — nothing behind it | None (a stub) | Measuring **demand** before building |
| **Concierge** | A human *openly* delivering the service | Visible, manual | **Generative** learning — *what* to build; rich qual insight |
| **Wizard of Oz** | A seemingly *automated* product; humans hidden | Hidden, manual | **Evaluative** — does a defined solution work; realistic behavior |

"Wizard of Oz hides the human; Concierge flaunts the human." Concierge gives richer but possibly
inflated signal (white-glove delight a self-serve product won't replicate); Wizard of Oz gives a more
realistic read. Classic examples: Zappos (Wizard of Oz), Wealthfront (concierge).

### Pre/post (before–after) & interrupted time series — *risky*
Measure a metric before vs. after a change, with no concurrent randomized control.
- **Why risky:** the periods differ in *time*, so the change is confounded with everything else that
  changed — seasonality, campaigns, external events. Kohavi's example: a new site always looked worse
  before/after, but the real cause was an Oprah traffic spike. Randomized tests avoid this because
  time-based confounds hit both arms equally.
- **Use (cautiously) when:** you genuinely can't randomize (e.g. a global pricing change everyone
  gets) — and only as a *double-check*, after ruling out other explanations.

### Switchback / diff-in-diff (marketplaces & geo)
- **Switchback:** flip the *whole* system between treatment and control over time within geo regions,
  for products where network effects make a normal A/B test invalid (treating riders changes driver
  supply for the "control").
- **Diff-in-diff:** compare the *change* in treated geos vs. the *change* in control geos, differencing
  out shared time trends.
- **Use when:** two-sided marketplaces, ride-share/delivery, social — interference between arms.
- **Bad for / caution:** statistically harder (time correlation between windows, geo clustering need
  cluster-robust standard errors); overkill for ordinary user-level features.

### Qualitative methods (interviews, usability tests, concierge, diary studies)
Not statistical tests — they generate *why* insight, and are especially valuable at low traffic. Best
practice: use *quant* to find **where** users drop off, then *qual* to learn **why**, and triangulate.
- **User interviews** — understand context, motivation, jobs-to-be-done. Small samples fine.
- **Usability / user testing** — watch users attempt a task; ~5 users surface ~80% of usability issues.
- **Diary studies** — users self-report over days/weeks; good for habit/longitudinal context, prone to
  self-report bias. (Standard UX practice.)

### Sequential testing / always-valid inference
Statistical methods built so you *can* peek repeatedly and stop early without inflating false
positives (they tighten the threshold for early looks, loosen it later).
- **Use when:** you want the option to stop early on a clear winner/loser. Most modern platforms
  (Statsig, Eppo, GrowthBook) offer this.
- **Trade-off:** generally less powerful than a fixed-horizon test of the same sample size — you pay
  for the right to peek.

---

## Part 2 — Right-sized stats

### First decision: is a powered A/B test even appropriate?
The deciding question is **not** stage per se but: *can you reach a small-enough MDE within a
reasonable duration with your traffic?*

- **Enough traffic** → run powered frequentist A/B tests by default.
- **Not enough traffic** → a powered A/B test is *inappropriate*; you'll run underpowered tests that
  falsely read "no difference," or draw false conclusions. Switch methods (below) rather than fake
  rigor. **Flag this explicitly to the user.**

Practical inputs (well-supported defaults, not laws): 95% confidence, 80% power, 2 variants, 2–3 week
duration (stretch to 4; reliability degrades beyond). Target MDE **2–5%** for mature/high-traffic
products; **10–15% is acceptable for startups** *if* testing big changes. Estimate daily
users/conversions from the last ~12 weeks (avoid seasonal spikes that give false hope).

### Sample size & MDE intuition (the four levers)
Power is a function of **baseline rate, MDE, significance (α≈0.05), and power (1−β≈0.80)**.
- **MDE is your test's resolution** — the smallest true effect it can reliably detect. Smaller MDE →
  proportionally more data. A bigger swing (20% vs 5% lift) dramatically cuts required sample/time.
- **Absolute vs relative:** at a 3% baseline, a 10% *relative* MDE = detecting 3.0% → 3.3%.
- **Higher baseline rate** → more conversions per user → more power for the same traffic.
- The practical chain: **bigger change → bigger MDE → less traffic & shorter test.** This is exactly
  why low-traffic teams should only test big swings.

### Duration
Run **at least one, ideally two, full business cycles** — almost always **2 weeks minimum (2–4
typical)** — regardless of when significance is hit, to cover every day-of-week. Monthly-cycle
businesses (SaaS renewals) → a full month. Volume alone doesn't substitute for a representative cycle.

### When you DON'T have the traffic — the toolkit
1. **Only test big changes.** Revamp whole flows, not button colors. Accept MDE 10–15%.
2. **Loosen the false-positive bar.** 90% confidence instead of 95% cuts required sample ~30% — a
   deliberate speed/rigor trade for startup decisions.
3. **Run longer / focus traffic** on your highest-volume surfaces; limit to 2 variants.
4. **Test leading indicators / micro-conversions** (a higher-volume step that correlates with the
   goal), or test messaging where volume is highest (ads, app-store, email).
5. **Painted-door demand tests** to validate interest before building.
6. **Qualitative + directional reads** (≈5-user tests, interviews, surveys, session recordings) — then
   triangulate.
7. **Bayesian / sequential approaches** converge faster on smaller samples and allow peeking; output
   is intuitive ("95% chance the lift is 3–13%"). Caveat: not free statistical power — a bad prior
   biases results.
8. **Ship & monitor** (cohort/version analysis) for un-randomizable changes — but only as a
   *double-check*, given confounds.

### The peeking problem
In a classical fixed-horizon test the false-positive guarantee holds only if you fix N up front and
look **once**, at the end. Repeated peeking and stopping at the first "significant" reading inflates
false positives from ~5% to ~20%. So either (a) fix N and don't stop early, (b) use sequential/
always-valid methods, or (c) use Bayesian approaches.

### Common pitfalls to watch for
- **Sample Ratio Mismatch (SRM):** observed split ≠ intended (e.g. 48/52) signals a bug that
  invalidates the test. A case of **Twyman's Law** — a surprising result is more likely a bug/leak
  than a breakthrough; check before celebrating.
- **Novelty effect:** new features spike early then fade — early results *overstate* impact.
- **Primacy effect:** users need time to adapt — early results *understate* impact. Detect both by
  plotting the effect over time.
- **Multiple comparisons:** testing many metrics/variants inflates spurious "winners"; correct (FDR/
  Bonferroni) or you ship noise.
- **Underpowered tests:** too little data → real effects missed → wrongly conclude "no difference."
- **Stopping early / peeking:** the most common way teams fool themselves.

---

## Sources
Kohavi, *Trustworthy Online Controlled Experiments* (summary): https://howtoes.blog/2025/06/11/trustworthy-online-controlled-experiments-complete-book-summary-all-key-ideas/ ·
RevenueCat, testing strategies for low-traffic apps: https://www.revenuecat.com/blog/growth/testing-strategies-for-low-traffic-apps/ ·
CXL, A/B testing alternatives: https://cxl.com/blog/ab-testing-alternatives/ ·
CXL, multivariate tests: https://cxl.com/blog/multivariate-tests/ ·
Statsig, holdouts: https://www.statsig.com/perspectives/holdout-groups-ab-testing ·
Learning Loop, concierge vs Wizard of Oz: https://learningloop.io/blog/concierge-vs-wizard-of-oz ·
Learning Loop, fake-door: https://learningloop.io/plays/fake-door-testing ·
DoorDash, switchback experiments: https://careersatdoordash.com/blog/switchback-tests-and-randomized-experimentation-under-network-effects-at-doordash/ ·
Eppo, sequential testing: https://www.geteppo.com/blog/sequential-testing ·
Atticus Li, MDE: https://atticusli.com/blog/posts/minimum-detectable-effect-ab-testing/ ·
Atticus Li, test duration: https://atticusli.com/blog/posts/how-long-should-you-run-ab-test-duration-guide/ ·
Statsig, sequential/peeking: https://www.statsig.com/perspectives/sequential-testing-ab-peek
