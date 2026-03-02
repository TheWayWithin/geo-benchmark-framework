# GEO Benchmark Framework

The open, auditable methodology behind [AISearchArena.com](https://aisearcharena.com) — an independent benchmark evaluating AI search optimization (GEO/AEO) tools.

## What is this?

This repository contains the complete scoring framework used to evaluate GEO tools:

- **51 scoring dimensions** across 6 categories, each with defined weights
- **128 evaluation prompts** (2-3 per dimension) used by the AI consensus panel
- **6 AI model configurations** that form the multi-model evaluation panel
- **Track definitions** specifying which dimensions apply to which tool categories

Everything that determines how a tool is scored is here — publicly auditable by vendors, practitioners, and researchers.

## Repository Structure

```
geo-benchmark-framework/
├── README.md
├── CHANGELOG.md
├── LICENSE                          # CC BY 4.0
│
├── methodology/
│   └── v1.0/
│       ├── overview.md              # Philosophy, scoring approach, principles
│       ├── dimensions.yaml          # All 51 dimensions with prompts & weights
│       └── models.yaml              # AI models used for evaluation
│
└── tracks/
    └── geo-platform.yaml            # GEO Platform Track (51 dimensions)
```

## Scoring Categories

| Category | Dimensions | Weight | What it measures |
|----------|-----------|--------|------------------|
| AI Search Visibility | 8 | 22% | How well a tool tracks and improves presence in AI-generated responses |
| Content Optimization | 9 | 20% | Content analysis, semantic scoring, and AI-readability features |
| Technical Implementation | 9 | 18% | Schema markup, llms.txt, APIs, integrations, and performance |
| Analytics & Reporting | 8 | 14% | AI-specific analytics, competitive benchmarking, and data export |
| User Experience | 8 | 13% | Dashboard usability, onboarding, documentation, and collaboration |
| Market & Value | 9 | 13% | Pricing, support, scalability, and vendor transparency |
| **Total** | **51** | **100%** | |

## How Scoring Works

1. **Standardized Prompts** — Each dimension has 2-3 evaluation prompts. One is randomly selected per evaluation run, reducing systematic bias from prompt phrasing.

2. **6-Model Consensus** — Every tool is evaluated by 6 independent AI models (GPT-4o, Claude Sonnet 4.6, Gemini 2.0 Flash, Command R+, Mistral Large, Llama 3.1 405B). Each model scores the tool 0-10 on each dimension.

3. **Median Synthesis** — The median score across models is used (not the mean), making results robust to outlier evaluations. A minimum of 4/6 models must respond for a valid score.

4. **Weighted Composite** — Dimension scores are combined using the weights defined in `dimensions.yaml`. If a dimension is marked N/A for a tool, remaining weights are renormalized to sum to 1.0.

5. **Confidence Tags** — Each score receives a confidence tag based on inter-model agreement:
   - **High** — Standard deviation ≤ 0.5
   - **Medium** — Standard deviation ≤ 1.5
   - **Low** — Standard deviation > 1.5
   - **Insufficient Data** — Fewer than 4 models responded

## For Vendors

If your tool is evaluated by AISearchArena, this is exactly how you're being scored. Every dimension, weight, and prompt is visible here.

**To understand your scores:**
1. Read `methodology/v1.0/dimensions.yaml` — find each dimension's weight and the exact prompts used
2. Read `methodology/v1.0/overview.md` — understand the scoring philosophy and principles
3. Read `tracks/geo-platform.yaml` — see which dimensions apply to your tool category

**Questions or corrections?** Open an issue on this repository or contact us through [AISearchArena.com](https://aisearcharena.com).

## Versioning

The framework follows semantic versioning:

- **v1.x** — Same 51 dimensions; prompt refinements or weight adjustments only
- **v2.x** — Dimensions added or removed (breaks historical comparisons)
- **v3.x** — Complete methodology redesign

Each benchmark cycle is permanently linked to one framework version. Upgrading the framework starts a new cycle — old results are never re-scored.

## Contributing

We welcome contributions that improve the fairness and comprehensiveness of the benchmark:

- **Prompt improvements** — Better evaluation prompts that reduce ambiguity
- **Weight adjustments** — Evidence-based arguments for rebalancing category weights
- **New dimensions** — Proposals for dimensions that capture important capabilities we're missing
- **Corrections** — Factual errors in methodology documentation

Please open an issue to discuss before submitting a PR.

## License

This work is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). You may use, adapt, and build upon this framework with attribution.

---

Built by [AI Search Mastery](https://aisearchmastery.com) for the GEO/AEO practitioner community.
