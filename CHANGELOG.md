# Changelog

All notable changes to this plugin are listed here. Versions follow [Semantic Versioning](https://semver.org).

## Unreleased

- Grok Build: `.grok-plugin/marketplace.json`, so the repository works as a Grok Build marketplace (`grok plugin install econdash@econdash-plugin`). Grok Build rejects a plugin at the marketplace root (`"source": "./"`), so this copy points at the repository URL; Claude Code keeps reading `.claude-plugin/marketplace.json`. CI keeps the two files equal apart from the source.
- `RELEASING.md`: the monthly check also confirms that the weekly CI run is still enabled.

## 0.2.0

- Releases: `RELEASING.md` with the version rules and the checklist for every platform. Tags `vX.Y.Z` must equal the manifests' version and are protected from being moved or deleted.
- `evals/tools-list.json`: snapshot of the server's instructions and tools. CI compares it with the live server on every push and weekly, so a changed tool description cannot slip past a release.
- Server: the `search_indicators` description now says which series the catalogue lacks: individual shares, cryptocurrencies other than the Crypto Fear & Greed Index, tax rates, steel and the Baltic Dry Index.
- Gemini CLI: shorter extension description for the gallery, naming all ten categories. Gemini CLI loads the skills from `skills/` too; the README now says so. CI applies the skills' wording rules to `GEMINI.md` and keeps it under 60 lines.
- Skills `macro-research`, `compare-economies` and `cite-economic-data` in `skills/`, with indicator coverage notes and citation formats in `references/`. `evals/skill-prompts.yaml`: 117 questions the skills are written for, covering all ten categories, with near misses where no skill should load.
- Golden prompt set `evals/golden-prompts.yaml`: 60 English and 10 Russian questions (direct, indirect, negative, edge) with expected tool calls and recorded values, to measure when a model calls EconDash.

## 0.1.0

- First release: connects the assistant to the EconDash MCP server at `https://mcp.econdash.org/mcp`.
- Manifests for Claude Code (`.claude-plugin/plugin.json`, own marketplace), Grok Build and Gemini CLI (`gemini-extension.json`, `GEMINI.md`).
