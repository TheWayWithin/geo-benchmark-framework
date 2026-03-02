# Changelog

All notable changes to the GEO Benchmark Framework will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.2] - 2026-03-02

### Fixed
- **Model identifiers verified against OpenRouter** — 2 IDs updated to match available models
  - `google/gemini-3-pro` → `google/gemini-3-pro-preview` (stable ID not yet available on OpenRouter)
  - `x-ai/grok-4` → `x-ai/grok-4.1-fast` (grok-4 not yet available on OpenRouter)

## [1.0.1] - 2026-03-02

### Changed
- **Model panel upgraded to v1.3** — all 6 models replaced with frontier versions
  - Determined via cross-analysis of 7 independent LLM evaluations
  - Optimized for provider diversity (US, EU, China), architectural diversity (dense, MoE), and stability (no preview models)

### Model Panel Changes
| Slot | Previous (v1.0) | New (v1.3) | Rationale |
|------|----------------|------------|-----------|
| OpenAI | GPT-4o | GPT-5.2 | Frontier upgrade |
| Anthropic | Claude Sonnet 4.6 | Claude Opus 4.6 | Most powerful Anthropic model |
| Google | Gemini 2.0 Flash | Gemini 3 Pro Preview | Stable frontier (preview — stable ID unavailable) |
| Slot 4 | Command R+ (Cohere) | Grok 4.1 Fast (xAI) | Unique X/Twitter training data relevant to web content |
| Slot 5 | Llama 3.1 405B (Meta) | DeepSeek V3.2 | Geographic diversity (China) + open-source frontier |
| Mistral | Mistral Large (latest) | Mistral Large 3 (2512) | Version-pinned EU provider |

## [1.0.0] - 2026-03-02

### Added
- Initial release of the GEO Benchmark Framework
- 51 scoring dimensions across 6 categories
- 2-3 evaluation prompts per dimension (128 total prompts)
- 6 AI model configurations for consensus evaluation panel
- GEO Platform Track definition covering all 51 dimensions
- Methodology overview documentation
- CC BY 4.0 license

### Categories & Weights
| Category | Dimensions | Weight |
|----------|-----------|--------|
| AI Search Visibility | 8 | 0.22 |
| Content Optimization | 9 | 0.20 |
| Technical Implementation | 9 | 0.18 |
| Analytics & Reporting | 8 | 0.14 |
| User Experience | 8 | 0.13 |
| Market & Value | 9 | 0.13 |
| **Total** | **51** | **1.00** |
