# Changelog

All notable changes to this plugin are listed here. Versions follow [Semantic Versioning](https://semver.org).

## Unreleased

- `plugin.json` and `mcp.json` (Agent Plugins 1.0): the package for ChatGPT and Codex, with the listing (name, subtitle, description, starter prompts, category, links, brand colours), review prompts and test cases, and release notes; the icon is `assets/icon.png`. CI checks it against the OpenAI listing limits and keeps its version equal to the other manifests.
- `RELEASING.md`: three manifests share the version; how to build the ChatGPT ZIP; do not change the tag tracked by the Claude directory while a publish request is waiting.

## 0.3.1

- `SECURITY.md`: how to report a vulnerability in the plugin, the MCP server or econdash.org; linked from the README.
- README: how to use the plugin in the Claude apps (claude.ai, Desktop, Cowork). Adding the plugin does not add its connector; connect EconDash from the plugin's Connectors tab, otherwise Claude has no EconDash tools.
- `RELEASING.md`: Claude Code and Grok Build install the current `main`, so unfinished work stays on a branch; xAI's bot pins the HEAD of `main`, so check that its pull request points at the release commit.
- Server: `get_full_series` returns up to 1500 values per call instead of 2500, so the largest result stays under Claude Code's 25,000-token limit for tool output. Ask for earlier periods with `end_year`. `evals/tools-list.json` updated.
- Server: the instructions and the `search_indicators` description now say what the catalogue holds (the ten categories and typical topics) and that every value comes with its source, licence and chart link. With web search available, models called EconDash on more data questions that do not name it. `evals/tools-list.json` updated.

## 0.3.0

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
