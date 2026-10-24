# Changelog

All notable changes to this plugin are listed here. Versions follow [Semantic Versioning](https://semver.org).

## Unreleased

- Gemini CLI: shorter extension description for the gallery, naming all ten categories. Gemini CLI loads the skills from `skills/` too; the README now says so. CI applies the skills' wording rules to `GEMINI.md` and keeps it under 60 lines.
- Skills `macro-research`, `compare-economies` and `cite-economic-data` in `skills/`, with indicator coverage notes and citation formats in `references/`. `evals/skill-prompts.yaml`: 117 questions the skills are written for, covering all ten categories, with near misses where no skill should load.
- Golden prompt set `evals/golden-prompts.yaml`: 60 English and 10 Russian questions (direct, indirect, negative, edge) with expected tool calls and recorded values, to measure when a model calls EconDash.

## 0.1.0

- First release: connects the assistant to the EconDash MCP server at `https://mcp.econdash.org/mcp`.
- Manifests for Claude Code (`.claude-plugin/plugin.json`, own marketplace), Grok Build and Gemini CLI (`gemini-extension.json`, `GEMINI.md`).
