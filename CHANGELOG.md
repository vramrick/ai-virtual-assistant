## Changelog
All notable changes to this project will be documented in this file.
The format is based on Keep a Changelog, and this project adheres to Semantic Versioning.

## [Unreleased]

### Added
- `APP_LLM_MAX_RETRIES` setting (default `3`). Controls how many times an LLM call retries on HTTP 429 or 5xx errors before surfacing the failure. Set to `1` on self-hosted endpoints where retries are unnecessary.

### Changed
- Default LLM is now `nvidia/nemotron-3-nano-30b-a3b` (was `meta/llama-3.3-70b-instruct`). The 30B MoE model with 3B active parameters returns faster per call on the hosted catalog and is not subject to the same per-minute quota pressure as the flagship Llama 3.3 70B. Override via `APP_LLM_MODELNAME` for self-hosted NIM endpoints.
- The deployment notebook's compose-up cell now passes `--build` so the source-built images include all the changes in this release, rather than pulling the pinned NGC image.
- LLM calls retry transient endpoint failures (HTTP 429 / 5xx) with exponential backoff and jitter.
- The agent surfaces a rate-limit-specific message ("The model service is rate-limited right now. Please try again in a moment.") when the upstream LLM is throttled, alongside the existing generic rephrase fallbacks for other failure modes.
- `get_product_name` and the unstructured retriever's query-rewriting step fall back to deterministic logic when their structured-output LLM call fails or returns no usable response. `get_product_name` falls back to token-overlap substring matching against the supplied product list; query rewriting falls back to the original user query unchanged. Retrieval continues either way.

## [1.1.0] - 2024-12-12

### Added

- [Helm Chart Support](./README.md#helm-chart-deployment) for on prem deployment.
- A [notebook](notebooks/api_usage.ipynb) demonstrating the Agent & Analytics API usage and Feedback retrieval.
- Bug Fixes, stability and security improvements.

### Changed
- Migrated to vaana.ai from Pandas AI for [Structured Retriever Tool](./src/retrievers/structured_data/).
- Refactored [README](/README.md) for a more streamlined developer experience.

## [1.0.0] - 2024-10-23

### Added

- First release.