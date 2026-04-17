# Learning Repo Builder (Tool‑Agnostic Guide)

This guide mirrors the Codex skill but can be used with Claude or other tools.

## Goal
Create a structured learning repo for any technical topic by:
1) Curating sources
2) Summarizing each source
3) Writing synthesis notes
4) Exporting a NotebookLM‑ready bundle

## Minimal Inputs
- Topic
- Time window (e.g., last 2 years)
- Companies (optional; use defaults if unsure)
- Focus stages (optional; use defaults if unsure)
- Output path

## Suggested Defaults (Guided Mode)
- Ads recsys: Meta, Pinterest, Google; focus: retrieval, ranking, serving, infra, experimentation
- Organic recsys: YouTube, Netflix, Pinterest, TikTok; focus: retrieval, ranking, engagement, evaluation, serving
- LLM systems: OpenAI, Google, Anthropic, Meta; focus: training, inference, systems, alignment, evaluation

## Repo Structure
```
README.md
sources/corpus.csv
summaries/
syntheses/
exports/
```

## Source Table Fields
`company,source_type,title,url,date,domain,stage,key_contribution,key_metrics,methods,tradeoffs,notes`

## Summary Template (one file per source)
- Title
- Source, URL, Date, Domain, Stage
- Summary
- Key Contributions
- Results / Metrics
- Methods / Architecture Notes
- Tradeoffs / Constraints
- Why It Matters

## Synthesis Notes
Create 2–4 notes that connect concepts across companies/stages (e.g., retrieval vs ranking; infra tradeoffs; foundation models).

## NotebookLM Bundle
Concatenate all summaries into `exports/notebooklm_bundle.md`, grouped by stage.


## How to run (Codex)

Example (guided mode):
```
Use $learning-repo-builder to create a learning repo on ads recommender systems.
```

Example (advanced mode):
```
Use $learning-repo-builder with:
- topic: organic recommender systems
- time_window_years: 2
- companies: YouTube, Netflix, Pinterest, TikTok
- focus: retrieval, ranking, engagement, evaluation, serving
- output_path: personal/recsys-organic-learning
```

