# Benchmark Frontier: Six Years of LLM Capability Growth (2020–2026)

Tracks how large language model capability has evolved from 2020 to 2026 using 1,276 benchmark results across 113 models and 23 organizations. Visualizes the state-of-the-art frontier, ranks organizations and models, measures benchmark saturation, and quantifies yearly improvement rates across reasoning, math, coding, and knowledge tasks.

## Overview

This project performs an end-to-end exploratory analysis of public LLM benchmark scores spanning the GPT-3 era (2020) through the most recent frontier releases (2026). It answers questions like:

- How fast has model capability improved on each benchmark, in percentage points per year?
- Which benchmarks are already "solved" (saturated) and which still have headroom?
- Which organizations currently lead, based on their most recent models?
- Which benchmarks tend to move together across models (e.g. does math skill correlate with coding skill)?
- Where do today's frontier models stand on the hardest, newest benchmarks?

## Dataset

`benchmark_scores.csv` — 1,276 rows, one row per model/benchmark pair.

| Column | Description |
|---|---|
| `model_id` | Unique model identifier |
| `model_name` | Model name (e.g. GPT-4o, Claude, Gemini) |
| `organization` | Releasing organization (23 total, e.g. OpenAI, Google, Anthropic, Meta, DeepSeek, Mistral, xAI) |
| `release_date` | Model release date |
| `benchmark` | Benchmark name (15 total) |
| `benchmark_type` | Capability category (knowledge, reasoning, math, coding, etc.) |
| `score` | Raw score |
| `max_score` | Maximum possible score |
| `score_pct` | Score as a percentage |

**Benchmarks covered:** MMLU, MMLU-Pro, HellaSwag, ARC-Challenge, BBH, GPQA Diamond, GSM8K, MATH, AIME 2024, HumanEval, SWE-Bench Verified, LiveCodeBench, TruthfulQA, MMMU, Chatbot Arena ELO.

## Project Structure

```
.
├── benchmark_scores.csv                                   # Source data
├── llm-benchmarks-capabilities-2020-2026-eda-trends.ipynb  # Main analysis notebook
├── PROJECT_DESCRIPTION.md                                  # Detailed project write-up
└── README.md                                                # This file
```

## Notebook Sections

1. **Load & clean data** — parse dates, check for missing values
2. **Dataset summary** — model/organization/benchmark counts, score distribution
3. **Capability growth over time** — per-benchmark scatter plots with a state-of-the-art (SOTA) frontier line, static and interactive (Plotly)
4. **Organization comparison** — ranks organizations by their most recent model's average score
5. **Benchmark saturation analysis** — boxplots showing which benchmarks are solved vs. still hard
6. **Leaderboard** — composite ranking of top models by average score across all benchmarks evaluated
7. **Cross-benchmark correlation** — heatmap of which benchmarks move together across models
8. **Rate-of-progress modeling** — linear regression of score vs. time per benchmark (pct points/year, R²)
9. **Frontier vs. hard benchmarks** — recent models evaluated only on the newest, hardest benchmarks

## What Changed from the Original Notebook

The notebook originally provided was built for a different dataset (`pricing_history.csv`, a Kaggle path not present in this project) and analyzed token **pricing** trends. It has been rewritten to load and analyze `benchmark_scores.csv`, replacing pricing-specific logic (MoM/YoY price change, CAGR, price-drop detection) with capability-specific analysis (SOTA frontier tracking, benchmark saturation, leaderboard, cross-benchmark correlation, and yearly capability growth rate). The notebook has been executed end-to-end and runs without errors.

## Tech Stack

- Python 3
- pandas, numpy
- matplotlib, seaborn
- plotly
- scipy
- scikit-learn (`LinearRegression`)

## Getting Started

```bash
pip install pandas numpy matplotlib seaborn plotly scipy scikit-learn jupyter
jupyter notebook llm-benchmarks-capabilities-2020-2026-eda-trends.ipynb
```

Make sure `benchmark_scores.csv` is in the same directory as the notebook (the notebook loads it via a relative path).

## Possible Next Steps

- Normalize benchmarks whose definitions changed over time (e.g. MMLU vs. MMLU-Pro) before computing long-run trends
- Add a model-size or compute axis (if available) to study scaling laws alongside benchmark trends
- Build an interactive dashboard (e.g. Streamlit) on top of the leaderboard and frontier views

## License

Add your preferred license here (e.g. MIT).
