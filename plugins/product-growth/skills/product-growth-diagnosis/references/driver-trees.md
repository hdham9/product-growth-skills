# Driver-Tree Templates by Business Model

This file is the starting library for building a product's "growth map." Don't apply a template
blindly — use it as a scaffold and adapt the branches to the specific product. A good tree is
**3–5 layers deep**, with branches that are **mutually exclusive and collectively exhaustive**
(MECE) — or at least exhaustive enough that nothing important is missing.

## The one principle that makes trees good: nest two shapes

There are two ways to break a metric down, and strong trees use both:

1. **Multiplicative (unit) decomposition** — for *value created in a period*.
   Example: `Revenue = Traffic × Conversion × AOV × Frequency`. This is the main shape of the tree.
2. **Additive growth-accounting (stock/flow) decomposition** — for *a stock of users or
   recurring revenue this period*. Example: `MAU(t) = New + Retained + Resurrected`. This is MECE
   by construction and is the right way to split any "active base" or "recurring revenue" node.

**Put the multiplicative tree at the top, then decompose the "users" / "recurring revenue" leaves
with the additive growth-accounting identity one layer down.** This nesting is the single most
useful structural move and is worth teaching the user explicitly.

---

## Universal spine: growth accounting (applies to every model)

For any active-user metric (Social Capital / Jonathan Hsu):

```
MAU(t)   = New(t) + Retained(t) + Resurrected(t)
MAU(t-1) = Retained(t) + Churned(t)
ΔMAU     = New + Resurrected − Churned
```

The four states — **New, Retained, Resurrected, Churned** — are the cleanest MECE branch set for
any active-base node.

For recurring revenue (MRR/ARR), add expansion and contraction:

```
MRR(t) = New + Retained + Resurrected + Expansion
ΔMRR   = New + Resurrected + Expansion − Churned − Contraction
```

**Quick Ratio** = `(New + Resurrected) / (Churned + Contraction)`. Above 1 = growing. Benchmarks
are model-specific: consumer apps ~1.5 is healthy; **enterprise SaaS should be >4** (because
subscription revenue is "default-retained" while consumer visitation is "default-not-retained").
A low quick ratio is a strong signal that churn — not acquisition — is the real problem.

**AARRR / Pirate Metrics** (Acquisition → Activation → Retention → Referral → Revenue): use this to
locate *which lifecycle stage* a weak driver lives in.

**Retention is the foundation under every model.** A flattening retention curve is the signal of
product-market fit. The Power User Curve (e.g. L7/L30 — how many of the last 7/30 days a user was
active) is a sharper engagement lens than DAU/MAU alone.

**Viral sub-loop:** `k-factor = invites per user × invite→signup conversion`.

---

## 1. B2B SaaS (sales-led and product-led variants)

**Top metric:** ARR (or MRR). PLG products often track an engagement/paid-teams NSM (e.g. Slack
"paid teams," Asana "weekly active paid users").

**Top decomposition — the ARR Bridge / Waterfall (industry standard):**
```
Ending ARR = Beginning ARR + New ARR + Expansion ARR − Contraction ARR − Churned ARR
Net New ARR = New + Expansion − Contraction − Churned
```

**Deeper layers:**
- New ARR (sales-led) = `Leads × Lead→SQL × SQL→Win × ACV`; `ACV = seats × price/seat`.
- New ARR (PLG) = `Signups × Activation rate × Free→Paid conversion × ACV`.
- Expansion ARR = `# expanding accounts × avg seat/usage uplift × price`.
- **NRR (net revenue retention)** = `(Start + Expansion − Contraction − Churn) / Start`; >110% means
  expansion outruns churn. This is the key health node.

**PLG funnel (the multiplicative tree PLG teams actually operate):**
Acquisition (visitors→signups) → Activation (% to "aha"; benchmark 20–40%, best-in-class >70%) →
Retention → Monetization (free→paid: freemium ~5%, free-trial ~17%, PQL 25–30%) → Expansion (NRR).
Lifting activation from 20%→30% ≈ a 50% increase in signups — activation is often the highest-leverage node.

**Frameworks:** ARR Bridge; growth accounting + Quick Ratio (>4); Reforge revenue-driver
decomposition; PLG funnel.
Sources: https://runway.com/resources/glossary/arr-bridge · https://mixpanel.com/blog/product-led-growth/ · https://www.reforge.com/blog/product-led-growth

---

## 2. B2C subscription apps

**Top metric:** subscription revenue / ARR; NSM often engagement (Duolingo DAU) or % paid.

**Top decomposition:**
```
Revenue ≈ New payers × LTV
LTV = ARPU × average subscriber lifetime,   lifetime ≈ 1 / monthly churn
```
Unit form: `Revenue ≈ Installs × Install→Trial × Trial→Paid × ARPU × lifetime`. Sustain the payer
base with the MRR growth-accounting identity.

**Deeper layers:**
- Trial→Paid: longer trials convert higher (~46% vs ~27%); paywall quality dominates and most
  conversions happen immediately.
- Churn: ~30% of annual subs cancel in month 1; annual plans retain far better than monthly.
- Pricing power: higher-priced apps realize multiples more revenue per payer.

**Frameworks:** RevenueCat subscription metrics; growth accounting; LTV/CAC + payback.
Source: https://www.revenuecat.com/state-of-subscription-apps/

---

## 3. Two-sided marketplace

**Top metric:** GMV; `Revenue = GMV × take rate`. NSM is usually *consumption* (nights booked,
rides, orders) rather than GMV, because GMV is confounded by AOV/FX.

**Top decomposition (a16z / Lenny):**
```
GMV = Active buyers × Orders per buyer × Average order value (AOV)
Revenue = GMV × Take rate
```

**Deeper layers — the marketplace-specific drivers:**
- **Liquidity / fill rate (match rate)** = transactions / intent (or sessions). This is the core
  operating job early on — "liquidity made measurable."
- "Zeros" = sessions with no successful match (demand the marketplace failed to clear).
- Supply side = `Active sellers × listings per seller × sell-through`; track *active* (transacting)
  supply, not registered.
- Time to match; market depth; concentration (% GMV from top sellers); cohort retention by geography
  (local network effects reset per market).
- The "hard side" (usually supply) must be seeded first.

**Frameworks:** a16z "13 Metrics for Marketplaces"; a16z "16 Ways to Measure Network Effects";
Andrew Chen *Cold Start Problem*.
Sources: https://a16z.com/13-metrics-for-marketplace-companies/ · https://www.lennysnewsletter.com/p/the-most-important-marketplace-metrics

---

## 4. E-commerce / DTC

**Top metric:** Revenue (and contribution margin).

**Top decomposition (the cleanest pure multiplicative tree):**
```
Revenue = Traffic × Conversion rate × AOV × Purchase frequency
Revenue per Visitor (RPV) = Conversion × AOV
```

**Deeper layers:**
- Traffic = `organic + paid + email/CRM + referral`; paid traffic = `spend / CPC`.
- Conversion = `product-view rate × add-to-cart × checkout-start × checkout-completion`.
- AOV = `items per order × price per item` (bundling/upsell).
- Frequency: split new vs returning; `LTV = AOV × frequency × gross margin × lifetime`. Gate on
  LTV/CAC and payback.

**Frameworks:** the T×CR×AOV×F growth equation (practitioner standard); LTV/CAC; AARRR for the
on-site funnel.
Sources: https://vwo.com/blog/important-ecommerce-metrics/ · https://revenuemap.app/blog/ecommerce-unit-economics

---

## 5. Transactional / fintech (revenue per transaction)

**Top metric:** TPV (total payment volume); `Revenue = TPV × net take rate`.

**Top decomposition:**
```
Revenue = Active accounts × Transactions per account × Avg transaction value × Take rate
TPV     = Active accounts × Transactions per account × Avg transaction value
```

**Deeper layers:**
- Active accounts via growth accounting (new + retained + resurrected − churned merchants/users).
- Take rate = `(gross fees − interchange/processing cost) / TPV` — *net* vs *gross* take rate is the
  key fintech nuance.
- Transactions per account = `activation × usage frequency × cross-product attach`.
- Take-rate benchmarks: payment processors 1–3%, marketplaces 5–15%, delivery 15–25%, ride-hail 20–30%.

Structurally identical to a marketplace (`GMV × take rate`); the difference is monetizing payment
flow rather than matching.
Sources: https://dojobusiness.com/blogs/news/fintech-transaction-revenue · https://portfolioiq.ai/databook/take-rate

---

## 6. Ad-supported media / content

**Top metric:** engagement (DAU/WAU/MAU) is the NSM — ad revenue follows attention.

**Top decomposition:**
```
Ad Revenue = Active users × Sessions per user × Ad impressions per session × (eCPM / 1000)
ARPU = Revenue / active users
```

**Deeper layers:**
- Users via growth accounting; engagement via Power User Curve (L7/L30).
- Impressions = `sessions × time/session × ad load` — ad load is the monetization-vs-experience lever.
- eCPM = `fill rate × CPM`, driven by targeting/data, format (video > display), advertiser demand.

**Frameworks:** the DAU × sessions × ad-load × eCPM equation; engagement NSM; Power User Curve.
Source: https://a16z.com/the-power-user-curve-the-best-way-to-understand-your-most-engaged-users/

---

## 7. Social / UGC / community / network-effect platform

**Top metric:** engagement (DAU/MAU) or consumption (e.g. "videos created that are viewed").

**Top decomposition (two-sided creator/consumer structure):**
```
Engagement (content consumed) = Active consumers × Sessions × Content consumed per session
Content created                = Active creators × Content per creator × Publish rate
```
The two sides feed a loop: content created → consumed → some consumers convert to creators / invite
others. The "hard side" is creators (the constrained side to seed).

**Deeper layers:**
- **Atomic network** density (smallest self-sustaining unit) — a seed metric, not a top line.
- Viral loop: `k-factor = invites × invite-conversion`; new users = `organic + viral + paid`.
- Creator funnel: consumer → contributor → creator → power creator (1-9-90 pyramid).
- Retention via Power User Curve.

**Note:** the clean multiplicative creator×content / consumer×consumption split is a synthesis — the
network-effect literature documents the *loop* well but rarely as a tidy formula. Adapt carefully.

**Frameworks:** Andrew Chen *Cold Start Problem* (atomic network, hard side); a16z "16 Ways to
Measure Network Effects"; viral loops.
Sources: https://a16z.com/16-ways-to-measure-network-effects/ · https://www.lennysnewsletter.com/p/atomic-network

---

## 8. Usage-based / developer infra / API (consumption pricing)

**Top metric:** Revenue, with NRR/NDR as the headline health metric (usage-driven NRR is commonly
115–130%+). NSM often consumption (Twilio "messages sent," Plaid "accounts linked").

**Top decomposition:**
```
Revenue = Active accounts × Units consumed per account × Price per unit
```
(units = API calls, GB, compute-hours, tokens, records).

**Deeper layers:**
- Account base via growth accounting — but **expansion within accounts dominates** (land-and-expand),
  so the Expansion term and NRR are the central nodes, not new logos.
- Usage per account = `# apps/workloads × calls per workload × adoption depth`; typically tracks the
  customer's own growth.
- `NDR = (Start + Expansion − Contraction − Churn) / Start`. Heavy/power users contribute
  disproportionately.

**Frameworks:** usage-based revenue = accounts × units × price/unit; NRR/NDR as the central node;
growth accounting with the Expansion term emphasized.
Sources: https://schematichq.com/blog/why-usage-based-billing-is-taking-over-saas · https://future.com/north-star-metrics/

---

## 9. Token-based AI products (LLM apps & AI APIs)

A special case of usage-based (#8), but distinctive enough to model on its own because **margin,
output quality, and pricing shape are first-class growth drivers**, not afterthoughts.

**Top metric:** Revenue — but track **contribution margin** alongside it, since inference is real COGS:
```
Revenue      = Active accounts × Tokens (or calls) per account × Price per unit
Contribution = Revenue − Inference cost     (Inference cost = tokens × cost per token)
```
Common pricing shapes change the middle term: **per-token**, **credits/usage packs**, **per-seat**,
or **hybrid (seat + overage)**. Identify which one the product uses before decomposing.

**Deeper layers:**
- **Margin as a driver:** `Gross margin % = 1 − (inference cost / revenue)`. Levers: model routing
  (cheaper model for easy queries), caching, prompt/context efficiency, fine-tuned smaller models.
  For many AI products margin is the *binding constraint* — high revenue growth with negative unit
  economics is a trap the diagnosis should flag.
- **Activation = time-to-first-valuable-output**, not just signup→first-call. The "aha" is the user
  getting a genuinely useful result. Decompose: `signup → first prompt → first good output → habitual use`.
- **Retention is driven by output quality & reliability** (accuracy, latency, consistency), more than
  by feature breadth. Weak retention here usually traces to quality, not onboarding.
- **Usage per account** often **rides the customer's own product growth** (land-and-expand) — so
  expansion/NRR dominates, as in #8. `NDR = (Start + Expansion − Contraction − Churn) / Start`.
- **Influence-lens nuance:** thin "wrapper" products over a foundation model have low switching costs
  and weak influence over differentiation; proprietary data, workflow integration, and fine-tuning
  raise both retention and influence.

**Diagnostic flags specific to AI products:**
- Revenue growing but margin shrinking → focus is *cost/margin*, not acquisition.
- High signup, low first-valuable-output → focus is *activation / prompt-to-value*.
- Good activation, poor week-4 retention → focus is *output quality/reliability*, not features.

**Frameworks:** usage-based revenue model (#8) + growth accounting with Expansion emphasized; unit
economics / contribution margin; activation-to-value funnel.
Sources (see #8): https://schematichq.com/blog/why-usage-based-billing-is-taking-over-saas · https://future.com/north-star-metrics/

---

## Picking and adapting a template

1. Start from the user's **objective** (sets the root) and **business model** (picks the template).
2. If the objective isn't the template's default root (e.g. they want *retention* on a marketplace,
   not GMV), **re-root** the tree: put their objective at top and pull the relevant branches up.
3. Expand to 3–5 layers, keeping branches MECE. Replace generic nodes with the product's real steps.
4. At any "active users" or "recurring revenue" node, decompose with the growth-accounting identity.
5. Where the user lacks numbers, mark each node **H/M/L** for volume and for conversion/drop-off based
   on what they do know — that's enough to find leverage.
