# Releasing

One repository feeds every platform, and each platform picks up changes in its own way. A release is what keeps them on the same version.

## Versions

The plugin follows [Semantic Versioning](https://semver.org):

- **patch** (0.2.0 → 0.2.1): wording of skills, README, `GEMINI.md`, evals;
- **minor** (0.2.1 → 0.3.0): a new skill, a new tool on the server, a new manifest;
- **major** (0.3.0 → 1.0.0): a tool renamed or removed, or a tool argument that changes meaning. This breaks the skills and saved prompts of existing users.

The server keeps its tools compatible between major releases: tools are not renamed or removed, arguments keep their meaning. New fields in answers are fine.

## What a release is

1. `version` in `.claude-plugin/plugin.json` and `gemini-extension.json`, the same in both.
2. A `## X.Y.Z` section in `CHANGELOG.md`, moved from `## Unreleased`.
3. A git tag `vX.Y.Z` on that commit, and a GitHub Release for the tag.

CI fails when the two versions differ, when `CHANGELOG.md` has no section for the version, or when a tag does not equal `v` plus the version. Tags `v*` are protected by a repository ruleset: they cannot be moved or deleted, so a published version never changes under its users. A mistake is fixed with the next patch release.

Claude Code keeps users on the installed `version` until it changes, so every release must raise it.

## Tool descriptions

`evals/tools-list.json` is a snapshot of the server's `instructions` and `tools/list`: names, titles, descriptions, input schemas and annotations. CI compares it with the live server on every push and every Monday. When the server changes a description, CI fails until the snapshot is updated in a commit. The git diff of this file between two tags is what changed for the model, and the stores must see it:

- a changed description goes into `CHANGELOG.md`;
- OpenAI must rescan the server (step 6 below).

To refresh the snapshot, run the commands of the CI step "Server tools match evals/tools-list.json" and commit the file it writes.

## Checklist

Write down how long each step took; the next release plan depends on it.

1. Run the golden prompt set (`evals/golden-prompts.yaml`) and, if skills changed, the skill prompts (`evals/skill-prompts.yaml`) in at least one client. Results go into the release notes.
2. Raise `version` in both manifests, move `## Unreleased` to `## X.Y.Z` in `CHANGELOG.md`, commit, push to `main`, wait for green CI.
3. Tag and publish the release:

   ```
   git tag -a vX.Y.Z -m "vX.Y.Z"
   git push origin vX.Y.Z
   gh release create vX.Y.Z --title vX.Y.Z --notes "<the CHANGELOG section>"
   ```

   Wait for green CI on the tag.
4. **Claude plugin directory** follows the release tag, not `main`, so unfinished work never reaches review. In the plugin's settings, set the tracked tag to `vX.Y.Z`, then **Check for new commits**. Each new commit is validated and scanned again; the result is on the **Versions** tab. The listing serves the previous version until the new one is published.
5. **Grok Build marketplace** pins a commit. Open a pull request to `xai-org/plugin-marketplace` that sets `sha` of the `econdash` entry in `.grok-plugin/marketplace.json` to the tag's commit (`git rev-parse vX.Y.Z^{commit}`), run `python3 scripts/generate-plugin-index.py` and `python3 scripts/validate-catalog.py` in that repository, and wait for code-owner review.
6. **ChatGPT / Codex.** Server changes reach ChatGPT without a new package: OpenAI scans the server daily; to rescan at once, open **MCPs**, select the server and choose **Rescan** under **Issues**. Changes to skills or listing metadata need a new ZIP with the new `version`: open the plugin, **Upload plugin to make changes**. Only one review can be active per plugin; to replace a package under review, cancel the review first.
7. **Gemini CLI** users of a git install are offered the update when `main` moves; users of a release install get the GitHub Release marked **Latest**. The gallery crawls tagged repositories daily. Nothing to do beyond step 3.
8. **MCP Registry**: only if the server's `server.json` changed, publish it with `mcp-publisher publish`.
9. If tools or sign-in changed, update the [MCP documentation](https://econdash.org/docs/mcp).

## Once a month

Check that every listing shows the same version: Claude (**Versions** tab), the `sha` in `xai-org/plugin-marketplace`, the ChatGPT package version, the latest GitHub Release, the MCP Registry entry.

Also open the repository's **Actions** tab: GitHub disables scheduled workflows in a public repository after 60 days without activity, and the weekly tool description check then stops without an error. Re-enable it there if it is off.
