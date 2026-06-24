# Product Growth Skills

A public [Claude](https://claude.com) plugin marketplace of product-growth skills.

Currently includes two plugins, designed to work in sequence — diagnose where to focus, then design
what to test:

### `product-growth` — Product Growth Diagnosis

Helps a founder, PM, or growth person figure out **where to focus their product growth
efforts**. It runs a structured diagnosis:

1. Understands your product, business model, stage, and current metrics (conversationally —
   estimates with High/Medium/Low when you don't have hard numbers).
2. Builds a **driver tree** rooted at your objective (objective × business model), rendered as a
   color-coded Mermaid "growth map" with Leverage/Influence scores on each driver.
3. Scores candidate drivers on three lenses — **Leverage, Influence, and Compounding** — and ranks
   them into a shortlist with a clear **top 3**.
4. Hands back a markdown report and points you toward designing experiments for your top bet.

It ships with driver-tree templates for 9 business models: B2B SaaS, B2C subscription,
marketplace, e-commerce/DTC, fintech/transactional, ad-supported, social/UGC, usage-based, and
token-based AI products.

### `experiment-design` — Growth Experiment Design

Picks up where the diagnosis leaves off. Given a **focus area** (e.g. activation, retention,
free→paid), it:

1. Brainstorms candidate experiments through five lenses (mechanism, history, product, customer,
   market — including an optional scan for real-world examples from comparable products).
2. Scores them with **ICE** (Impact, Confidence, Ease) and shortlists.
3. Recommends a **top-3 portfolio** balanced across impact, learning, and speed.
4. Designs each one to a sufficient standard — hypothesis, primary metric, 1–3 intervention options,
   guardrails, risks, sample/duration, and **right-sized stats** (it flags when a powered A/B test
   doesn't fit your traffic and gives minimum-viable guidance instead).

It ships with two references: a playbook of common experiments by focus area, and a methods + stats
toolbox.

## Install

In Claude Code (or Cowork), add this marketplace and install the plugins:

```
/plugin marketplace add hdham9/product-growth-skills
/plugin install product-growth@product-growth-skills
/plugin install experiment-design@product-growth-skills
```

Then just describe your situation — e.g. *"we've plateaued at 8k MAU and I don't know what to focus
on to grow"* — and the skill will run a diagnosis.

## How they fit together

Use them in sequence: **`product-growth`** tells you *where* to focus, then **`experiment-design`**
turns that focus area into *what to test*. The diagnosis ends by handing off to the experiment
design; the experiment design starts from a focus area (which you can paste from the diagnosis or
just describe).

## What these skills don't do

They help you decide where to grow and what to test — then deliberately stop at a few seams. They
don't run the experiments for you, set up analytics or instrumentation, write marketing/pricing copy,
or analyze results after a test has finished. Those are separate jobs (a results-readout skill may
join the suite later).

## Repository layout

```
product-growth-skills/
├── .claude-plugin/
│   └── marketplace.json          # the marketplace catalog
└── plugins/
    ├── product-growth/
    │   ├── .claude-plugin/
    │   │   └── plugin.json
    │   └── skills/
    │       └── product-growth-diagnosis/
    │           ├── SKILL.md
    │           └── references/
    │               └── driver-trees.md        # driver-tree templates by business model
    └── experiment-design/
        ├── .claude-plugin/
        │   └── plugin.json
        └── skills/
            └── growth-experiment-design/
                ├── SKILL.md
                └── references/
                    ├── experiment-patterns.md  # common experiments by focus area
                    └── experiment-methods.md   # methods + right-sized stats
```

## License

[Apache-2.0](./LICENSE).

## Contributing

Issues and pull requests welcome.
