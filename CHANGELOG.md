# Changelog

All notable changes to this plugin are listed here. Versions follow [Semantic Versioning](https://semver.org).

## Unreleased

- Skills `macro-research`, `compare-economies` and `cite-economic-data` in `skills/`, with indicator coverage notes and citation formats in `references/`. `evals/skill-prompts.yaml` lists the questions each skill is written for.
- Golden prompt set `evals/golden-prompts.yaml`: 60 English and 10 Russian questions (direct, indirect, negative, edge) with expected tool calls and recorded values, to measure when a model calls EconDash.

## 0.1.0

- First release: connects the assistant to the EconDash MCP server at `https://mcp.econdash.org/mcp`.
- Manifests for Claude Code (`.claude-plugin/plugin.json`, own marketplace), Grok Build and Gemini CLI (`gemini-extension.json`, `GEMINI.md`).
