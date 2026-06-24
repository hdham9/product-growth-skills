# Common Experiment Patterns by Focus Area (the playbook)

Use this to jump-start the brainstorm. These are proven, recurring experiments people run for each
focus area — a starting menu, not a prescription. Adapt them to the product, and always pressure-test
against the five lenses (mechanism, history, product, customer, market) so you don't just copy a
pattern that doesn't fit. For each focus area: the metric it moves, then go-to experiments with the
typical method and the primary metric each targets.

A note on method: most of these *can* be A/B tested at sufficient traffic, but the listed method is
the one that usually fits best (and many work as painted-door or qual tests when traffic is thin —
see `experiment-methods.md`).

---

## Acquisition
**Moves:** new signups / new customers; CAC and channel efficiency upstream.

- **Landing-page value-prop / messaging test** — rewrite the hero around a sharper job-to-be-done.
  *Method:* A/B (or sequential at low traffic). *Primary metric:* visitor → signup rate.
- **Reduce signup friction** — fewer fields, SSO/social login, defer account creation until after
  first value. *Method:* A/B. *Metric:* signup-start → signup-complete.
- **New channel / audience test** — a small paid or content test in an untried channel or segment.
  *Method:* geo/holdout or simple before-after with spend caps. *Metric:* CAC and signups by channel.
- **Social proof on the landing page** — logos, counts, testimonials near the CTA. *Method:* A/B.
  *Metric:* visitor → signup.
- **Painted-door for a new use case** — a landing page for a use case you haven't built. *Method:*
  painted-door. *Metric:* click/waitlist rate (demand signal).

## Activation / onboarding
**Moves:** % of new users reaching first value ("aha"); time-to-value.

- **Define and instrument the aha moment, then shorten the path to it** — strip steps before first
  value. *Method:* A/B on the onboarding flow. *Metric:* signup → activated rate.
- **Setup/onboarding checklist or progress bar** — guide users to the activating action. *Method:*
  A/B. *Metric:* activation rate; step-completion.
- **Templates / starter content / sample data** — remove the blank-slate problem. *Method:* A/B.
  *Metric:* time-to-first-value; activation.
- **Contextual tooltips / interactive walkthrough vs. self-serve** — *Method:* A/B. *Metric:*
  activation; early retention (D7).
- **Reverse-trial / instant access** — give full value first, gate later. *Method:* A/B. *Metric:*
  activation and downstream conversion.
- **Onboarding usability test** — watch ~5 new users attempt setup. *Method:* qual usability test.
  *Output:* the friction points to then A/B.

## Engagement
**Moves:** frequency, depth, and breadth of use; power-user growth.

- **Lifecycle / triggered messaging** — nudge users back to a high-value action at the right moment.
  *Method:* A/B (holdout on the message). *Metric:* WAU/feature adoption; sessions per user.
- **Surface a high-retention feature earlier** — for features correlated with retention, drive
  adoption. *Method:* A/B. *Metric:* feature adoption → retention.
- **Habit loop / streaks / reminders** — *Method:* A/B. *Metric:* days-active (L7/L28); return rate.
- **Personalized home / recommendations** — *Method:* A/B. *Metric:* content consumed per session;
  return rate.
- **Notification opt-in & relevance** — *Method:* A/B. *Metric:* opt-in rate → return rate.

## Retention / churn
**Moves:** retained users / revenue; reduces churn; flattens the retention curve.

- **Onboarding-to-habit bridge** — connect activation to a repeatable habit in week 1. *Method:* A/B.
  *Metric:* D7/D30 retention.
- **Resurrection / win-back campaign** — targeted reactivation of dormant users. *Method:* A/B
  (holdout). *Metric:* resurrected users.
- **Churn-reason research + save flow** — interview churned users, then build a cancel/save flow
  (pause, downgrade, offer). *Method:* qual interviews → A/B on the save flow. *Metric:* voluntary
  churn rate.
- **Proactive health-score outreach (B2B)** — intervene on at-risk accounts. *Method:* holdout vs.
  outreach. *Metric:* renewal / logo retention.
- **Re-engagement of a key value moment** — bring lapsing users back to the action that retains.
  *Method:* A/B. *Metric:* retention curve shape.

## Monetization & pricing (incl. free→paid)
**Moves:** conversion to paid, ARPU, and (carefully) overall revenue.

- **Paywall placement & timing at a value moment** — trigger the upgrade prompt when value is felt.
  *Method:* A/B. *Metric:* free → paid conversion.
- **Pricing-page / plan-structure redesign** — repackage tiers, anchor, highlight a plan. *Method:*
  A/B. *Metric:* visitor → paid; ARPU. *Guardrail:* don't degrade total revenue.
- **Price-point / willingness-to-pay test** — *Method:* painted-door or cohorted price test (avoid
  showing different live prices to similar users simultaneously; use new-user cohorts or geo).
  *Metric:* conversion × price = revenue per visitor; *Guardrail:* refund/complaint rate.
- **Trial type & length** — free trial vs. freemium vs. reverse trial; trial length. *Method:* A/B on
  new users. *Metric:* trial → paid; *Guardrail:* long-run retention of converts.
- **Plan-gating / feature packaging** — move a feature across the paywall. *Method:* A/B. *Metric:*
  upgrade rate; *Guardrail:* activation/retention of free users.
- **Annual-plan nudge / discount** — *Method:* A/B. *Metric:* annual mix; *Guardrail:* total revenue,
  not just annual share.

## Referral / virality
**Moves:** invites, viral coefficient (k), organic share of new users.

- **In-product referral / invite flow** — surface invites at a moment of delight. *Method:* A/B.
  *Metric:* invites sent per user × invite → signup (k-factor).
- **Double-sided incentive test** — reward referrer and referee; vary the reward. *Method:* A/B.
  *Metric:* referral signups; *Guardrail:* incentive cost / fraud.
- **Shareable artifact / content** — make output worth sharing (report, design, score). *Method:*
  A/B. *Metric:* share rate → assisted signups.
- **Network/collaboration invites** — invite-a-teammate as part of setup. *Method:* A/B. *Metric:*
  multiplayer rate → retention.

## Expansion (esp. usage-based & B2B)
**Moves:** net revenue retention (NRR); seats/usage per account.

- **Seat-expansion prompts** — nudge admins to invite more users. *Method:* A/B (holdout). *Metric:*
  seats per account; NRR.
- **Usage-cap / upgrade prompts at the limit** — *Method:* A/B. *Metric:* upgrade rate; expansion ARR.
- **Cross-sell of an adjacent product/feature** — *Method:* A/B. *Metric:* attach rate.
- **Success-driven expansion (B2B)** — trigger expansion conversations on usage milestones. *Method:*
  holdout vs. CS outreach. *Metric:* expansion ARR; NRR.

---

## Using a pattern well
1. Start from the focus area's patterns, but only keep ones the five lenses support for *this*
   product (history, real friction points, customer evidence, market analogs).
2. Turn the chosen pattern into a specific hypothesis and primary metric (see SKILL.md).
3. Pick the method from `experiment-methods.md` that fits the change and the available traffic.
