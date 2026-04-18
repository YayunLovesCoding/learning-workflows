---
name: learning-repo-builder
description: Build a reusable learning repo for a topic (e.g., ads recsys, organic recsys, LLM systems) by curating sources, generating summaries, syntheses, and a NotebookLM bundle. Use when the user wants a structured learning corpus, summaries, or study assets.
---

# Learning Repo Builder

## Overview
This skill creates a structured learning repo for any technical topic by (1) curating sources, (2) generating concise summaries, (3) writing synthesis notes, and (4) exporting a NotebookLM‑ready bundle.

## Modes

### Guided (default)
Use when the user does not specify companies, focus areas, or time window.
- Ask for only the topic if missing.
- Use presets from `references/presets.md` for companies and focus.
- Default time window: last 2 years for blogs; include foundational papers.

### Advanced
Use when the user specifies companies, focus, or time window.
- Respect provided parameters.
- Still add 2–5 foundational papers relevant to the topic.

## Required Inputs
Collect or infer these:
- `topic`
- `time_window_years` (default 2)
- `companies` (from presets if guided)
- `focus` (stages/subdomains; from presets if guided)
- `output_path` (workspace path for repo)

## Workflow

### 1) Create repo scaffold
Create this structure in `output_path`:
```
README.md
sources/corpus.csv
summaries/
syntheses/
exports/
```

### 2) Build the corpus
- Use web search to find relevant engineering blogs and papers within the time window.
- Add foundational papers even if outside the window.
- Store all sources in `sources/corpus.csv` with fields:
  `company,source_type,title,url,date,domain,stage,key_contribution,key_metrics,methods,tradeoffs,notes`
- Verify dates/URLs from sources and preserve traceability in the source table.

### 3) Generate summaries
- One Markdown file per source in `summaries/`.
- Format:
  - Title
  - Source, URL, Date, Domain, Stage
  - Summary
  - Key Contributions
  - Results / Metrics
  - Methods / Architecture Notes
  - Tradeoffs / Constraints
  - Why It Matters
- Use citations while researching non-obvious facts, metrics, and claims, but persist only repo-safe attribution in files written to disk.
- Never write raw tool citation markers into repo files. Forbidden examples: `citeturn0view0`, `cite...`, `turn0search0`, `turn4view1`.
- Repo-safe attribution should use the existing `Source`, `URL`, and `Date` fields, plus optional Markdown footnotes or a short `Sources` section when extra attribution is needed.

### 4) Write syntheses
Create 2–4 synthesis notes that connect sources across stages or themes, in `syntheses/`.
Examples: retrieval vs ranking, infra tradeoffs, foundation models, experimentation.

### 5) NotebookLM bundle
Concatenate summaries into `exports/notebooklm_bundle.md`, grouped by stage.

### 6) Sanitize outputs
- Before finishing, scan `README.md`, `summaries/`, `syntheses/`, and `exports/` for leaked raw citation markers such as `cite`, `turn`, or `turn0search`.
- Remove or replace leaked markers before saving files. Final repo artifacts must read cleanly as plain Markdown outside the chat tool.
- If attribution is still needed after cleanup, convert it to repo-safe text such as footnotes, normal Markdown links, or a `Sources` section.

## Notes
- Prioritize accuracy and source verification over speed.
- Do not fabricate metrics or claims.
- If a source is paywalled or inaccessible, note it in `notes` and move on.
- Use tool-native citations only during research and reasoning, not in repo files committed to disk.

## Presets
Use `references/presets.md` for guided mode defaults and focus lists.
