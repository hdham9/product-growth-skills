# Growth Skills

A public [Claude](https://claude.com) plugin marketplace of product-growth skills.

Currently includes one plugin:

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

## Install

In Claude Code (or Cowork), add this marketplace and install the plugin:

```
/plugin marketplace add hdham9/product-growth-skills
/plugin install product-growth@product-growth-skills
```

Then just describe your situation — e.g. *"we've plateaued at 8k MAU and I don't know what to focus
on to grow"* — and the skill will run a diagnosis.

## What it does NOT do

It diagnoses *where* to focus. It deliberately stops before designing or running specific
experiments, setting up analytics/instrumentation, writing copy, or brainstorming channels — those
are separate jobs.

## Repository layout

```
product-growth-skills/
├── .claude-plugin/
│   └── marketplace.json          # the marketplace catalog
└── plugins/
    └── product-growth/
        ├── .claude-plugin/
        │   └── plugin.json        # the plugin manifest
        └── skills/
            └── product-growth-diagnosis/
                ├── SKILL.md        # the skill
                └── references/
                    └── driver-trees.md   # driver-tree templates by business model
```

## License

[Apache-2.0](./LICENSE).

## Contributing

Issues and pull requests welcome.
