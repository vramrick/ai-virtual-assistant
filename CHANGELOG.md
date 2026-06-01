## Changelog
All notable changes to this project will be documented in this file.
The format is based on Keep a Changelog, and this project adheres to Semantic Versioning.

## [Unreleased]

### Added
- `APP_LLM_MAX_RETRIES` setting (default `3`). Controls how many times an LLM call retries on HTTP 429 or 5xx errors before surfacing the failure. Set to `1` on self-hosted endpoints where retries are unnecessary.

### Changed
- LLM calls retry transient endpoint failures (HTTP 429 / 5xx) with exponential backoff and jitter.
- The agent surfaces a rate-limit-specific message ("The model service is rate-limited right now. Please try again in a moment.") when the upstream LLM is throttled, alongside the existing generic rephrase fallbacks for other failure modes.

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