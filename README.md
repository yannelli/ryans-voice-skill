# Ryan's Voice

The `ryan-voice` skill, packaged as a plugin marketplace for Claude Code, Codex, and Cursor.

The skill writes and edits text in Ryan Yannelli's voice. It is built from his writing, 2013 to 2026: proposals, contracts, offer letters, instructions, letters, filings, investor documents, and articles.

## Install

Claude Code:

```sh
claude plugin marketplace add yannelli/ryans-voice-skill
claude plugin install ryan-voice@ryans-voice-skill
```

Codex:

```sh
codex plugin marketplace add yannelli/ryans-voice-skill
codex plugin add ryan-voice@ryans-voice-skill
```

Cursor CLI:

```sh
agent plugin marketplace add https://github.com/yannelli/ryans-voice-skill.git
```

Then install `ryan-voice` from `/plugin` in a session. In the Cursor IDE, a team admin adds the repo under Dashboard, Plugins & MCPs, Add Marketplace.

If a local copy exists at `~/.claude/skills/ryan-voice`, remove it after installing so the skill loads once.

## Layout

| Path | Used by |
| --- | --- |
| `.claude-plugin/marketplace.json` | Claude Code marketplace |
| `.agents/plugins/marketplace.json` | Codex marketplace |
| `.cursor-plugin/marketplace.json` | Cursor marketplace |
| `plugins/ryan-voice/plugin.json` | Agent Plugins manifest (Codex, Cursor) |
| `plugins/ryan-voice/.claude-plugin/plugin.json` | Claude Code plugin |
| `plugins/ryan-voice/.codex-plugin/plugin.json` | Codex plugin (older fallback path) |
| `plugins/ryan-voice/.cursor-plugin/plugin.json` | Cursor plugin |
| `plugins/ryan-voice/skills/ryan-voice/SKILL.md` | The skill |
| `plugins/ryan-voice/skills/ryan-voice/examples/<category>/` | Anonymized samples, one per file, in business, legal, technical, support, personal, social, and editing folders, loaded on demand |

## Updating

1. Edit `SKILL.md` or a file in `examples/`. Examples keep invented names, figures, and details, with no text copied from a source document.
2. Bump `version` in all four plugin manifests and in `.cursor-plugin/marketplace.json`. Clients cache by version.
3. Run `claude plugin validate .` and `claude plugin validate plugins/ryan-voice`.

Manifest fields, the skill format, sources, and install notes for each client are in [docs/INDEX.md](docs/INDEX.md).
