# Plugin manifests for Claude Code, Codex, and Cursor

Created: 09/29/2026
Last updated: 09/29/2026

All three clients install from this one repo. Each client reads its own marketplace file and plugin manifest. All three find skills under `skills/` without a `skills` field.

## Claude Code

- Marketplace: `.claude-plugin/marketplace.json`. Required: `name`, `owner.name`, `plugins[].name`, `plugins[].source`. `claude plugin validate` warns when `description` is missing.
- Plugin: `.claude-plugin/plugin.json`. Only `name` is required.
- Set `version` in `plugin.json` only. When the marketplace entry also has one, `plugin.json` wins.
- Relative sources start with `./`.
- `$schema` is ignored at load time. The schemastore URLs resolve.
- Private repos use your git credentials: an SSH key in `ssh-agent`, or `gh auth login` plus `gh auth setup-git` for HTTPS. `CLAUDE_CODE_PLUGIN_PREFER_HTTPS=1` skips SSH.

## Codex

- Marketplace: `.agents/plugins/marketplace.json`. Fields: `name`, `interface.displayName`, and `plugins[]` with `source` (`{"source": "local", "path": "./plugins/x"}`), `policy.installation`, `policy.authentication`, and `category`.
- Plugin: root `plugin.json` in the Agent Plugins format, with `$schema` `https://agent-plugins.org/schemas/1.0.0/plugin.schema.json`. `$schema` and `name` are required. OpenAI-only settings go under `extensions.com.openai`.
- `.codex-plugin/plugin.json` is the older path and still loads as a fallback.
- Install: `codex plugin marketplace add <owner/repo or path>`, then `codex plugin add <plugin>@<marketplace>`.

## Cursor

- Marketplace: `.cursor-plugin/marketplace.json`. Required: `name`, `owner.name`, `plugins`. `description`, `version`, and `pluginRoot` go under `metadata`.
- `metadata.pluginRoot` prefixes every plugin source. Leave it out when sources already include `plugins/`.
- Plugin: `.cursor-plugin/plugin.json`. Only `name` is required. A `skills` field replaces discovery. Cursor also loads a root Agent Plugins `plugin.json`, and the docs do not say which file wins when both exist.
- CLI install: `agent plugin marketplace add <git URL>` (needs `agent login`), then install from `/plugin`.
- IDE install: team marketplaces only (Teams and Enterprise). Dashboard, Plugins & MCPs, Add Marketplace, Import from Repo. Auto Refresh needs the Cursor GitHub App.

## Checks run on this repo (09/29/2026)

- `claude plugin validate .` and `claude plugin validate plugins/ryan-voice`: passed.
- Claude Code local install into a scratch `CLAUDE_CONFIG_DIR`: installed `ryan-voice@ryans-voice-skill` 1.0.0.
- Codex local install into a scratch `CODEX_HOME`: installed `ryan-voice@ryans-voice-skill` 1.0.0.
- Cursor: not run. `agent plugin marketplace add` needs a logged-in account.

## Sources

- https://code.claude.com/docs/en/plugin-marketplaces
- https://code.claude.com/docs/en/plugins/marketplace-reference
- https://code.claude.com/docs/en/plugins-reference
- https://code.claude.com/docs/en/plugins/host-marketplace
- https://code.claude.com/docs/en/plugins/install
- https://developers.openai.com/codex/plugins/build
- https://developers.openai.com/codex/cli/reference
- https://cursor.com/docs/plugins
- https://cursor.com/docs/reference/plugins
- https://cursor.com/docs/cli/changelog
- https://agent-plugins.org (spec 1.0.0)
