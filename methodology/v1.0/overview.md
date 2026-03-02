# GEO Benchmark Methodology v1.0

## Purpose

The GEO Benchmark Framework provides a standardized, reproducible methodology for evaluating tools that help websites appear in AI-generated search results — commonly known as Generative Engine Optimization (GEO) or AI Engine Optimization (AEO) tools.

This framework powers [AISearchArena.com](https://aisearcharena.com), an independent monthly benchmark.

## Design Principles

### Independence

Evaluations are conducted without vendor involvement. No vendor pays for inclusion, priority, or favorable treatment. The methodology is public so vendors can audit exactly how they're scored.

### Reproducibility

Given the same tool, the same framework version, and the same AI models, evaluations produce identical results. Scores use median aggregation (not mean), and the synthesis algorithm is deterministic.

### Multi-Model Consensus

No single AI model's opinion determines a score. Every dimension is evaluated by 6 independent models from different providers. This reduces provider-specific biases and produces more balanced assessments.

### Transparency

Every component of the scoring system is public:
- The dimensions and their weights (`dimensions.yaml`)
- The exact evaluation prompts used
- The AI models and their configurations (`models.yaml`)
- The synthesis algorithm (median with confidence tagging)

## Scoring Framework

### Categories

The 51 scoring dimensions are organized into 6 categories:

| Category | Dimensions | Weight | Rationale |
|----------|-----------|--------|-----------|
| **AI Search Visibility** | 8 | 0.22 | Core value proposition — does the tool actually improve AI search presence? |
| **Content Optimization** | 9 | 0.20 | Content is the primary lever for GEO; optimization quality matters deeply |
| **Technical Implementation** | 9 | 0.18 | Schema, structured data, and technical foundations enable AI discoverability |
| **Analytics & Reporting** | 8 | 0.14 | Practitioners need data to justify investment and guide strategy |
| **User Experience** | 8 | 0.13 | Tool usability determines whether capabilities translate to outcomes |
| **Market & Value** | 9 | 0.13 | Pricing, support, and vendor practices affect long-term tool viability |

### Weight Rationale

Weights reflect the relative importance of each category to a practitioner selecting a GEO tool:

- **AI Search Visibility** and **Content Optimization** receive the highest weights because they represent the core promise of GEO tools — making content visible in AI responses.
- **Technical Implementation** is weighted third because strong technical foundations (schema, structured data, llms.txt) are increasingly critical for AI discoverability.
- **Analytics**, **UX**, and **Market & Value** are weighted lower but still meaningful — a tool that delivers results but is unusable or overpriced fails practitioners in practice.

### Dimension Weights

Within each category, individual dimension weights reflect relative importance. Weights across all 51 dimensions sum to exactly 1.0000. See `dimensions.yaml` for the complete list.

## Evaluation Process

### Step 1: Prompt Selection

For each (tool, dimension) pair, one evaluation prompt is randomly selected from the 2-3 available prompts for that dimension. Using multiple prompt variants across evaluation runs reduces systematic bias from specific phrasing.

### Step 2: Multi-Model Evaluation

The selected prompt — contextualized with the tool name, description, and public information — is sent to all 6 AI models simultaneously. Each model independently returns a score from 0 to 10 with a brief justification.

**Models (v1.0):**
- GPT-4o (OpenAI)
- Claude Sonnet 4.6 (Anthropic)
- Gemini 2.0 Flash (Google)
- Command R+ (Cohere)
- Mistral Large (Mistral)
- Llama 3.1 405B (Meta)

All models are accessed through OpenRouter as a unified API gateway.

### Step 3: Score Synthesis

The **median** of all successful model responses is used as the synthesized score. Median is preferred over mean because:
- It is robust to outlier evaluations (one model scoring unusually high or low)
- It produces more stable, reproducible results
- It handles the odd-number case naturally

**Confidence tagging** based on inter-model agreement (standard deviation):
- **High** — StdDev ≤ 0.5 (models strongly agree)
- **Medium** — StdDev ≤ 1.5 (reasonable agreement)
- **Low** — StdDev > 1.5 (significant disagreement)
- **Insufficient Data** — Fewer than 4/6 models responded

Scores with Low or Insufficient Data confidence are flagged for manual review.

### Step 4: Composite Score Calculation

Each tool's composite score is a weighted average of its dimension scores:

```
Composite = Sum(dimension_score_i * weight_i) for all applicable dimensions
```

If a dimension is marked N/A (not applicable to this tool), its weight is excluded and the remaining weights are renormalized to sum to 1.0. This ensures tools aren't penalized for dimensions outside their scope.

### Step 5: Ranking

Tools are ranked by descending composite score using **dense ranking**: tools with identical composite scores receive the same rank. For example: 1st, 2nd, 2nd, 3rd (not 1st, 2nd, 2nd, 4th).

## Score Scale

All scores use a 0-10 scale, rounded to one decimal place (round half up):

| Range | Interpretation |
|-------|---------------|
| 9.0 - 10.0 | Exceptional — industry-leading capability |
| 7.0 - 8.9 | Strong — well-developed, competitive feature |
| 5.0 - 6.9 | Adequate — functional but with notable limitations |
| 3.0 - 4.9 | Below Average — significant gaps or weaknesses |
| 0.0 - 2.9 | Poor — minimal or non-functional capability |

## N/A Handling

A dimension is marked N/A when it genuinely does not apply to a tool's category or scope. For example, a pure analytics tool may receive N/A on "Schema Markup Support."

N/A is not a score — it removes the dimension entirely from that tool's composite calculation with weight renormalization. This prevents tools from being penalized for capabilities outside their product scope.

## Fairness Safeguards

1. **Prompt Rotation** — Multiple prompt variants reduce phrasing bias
2. **Multi-Model Consensus** — 6 models from 6 providers prevent single-model bias
3. **Median Aggregation** — Robust to outlier scores
4. **Public Methodology** — Vendors can audit exactly how they're scored
5. **Vendor Review Window** — 5 business days to submit factual corrections before publication
6. **Audit Packages** — SHA-256 hashed evaluation data for tamper detection
7. **Version Pinning** — Each cycle is linked to a specific framework version; results are never retroactively rescored

## Limitations

This framework evaluates tools based on **publicly available information and AI model assessments**, not hands-on product testing. Key limitations:

- AI models assess based on training data and public information, which may not reflect the latest product updates
- Scores represent a consensus view that may not capture niche strengths visible only through extended use
- The framework evaluates tool capabilities, not implementation quality for any specific use case
- Monthly cadence means scores reflect a point-in-time snapshot

We publish these limitations alongside every benchmark report.

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-03-02 | Initial release: 51 dimensions, 6 categories, 6 AI models |
