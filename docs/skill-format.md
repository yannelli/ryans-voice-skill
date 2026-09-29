# Skill format and supporting files

Created: 09/29/2026
Last updated: 09/29/2026

The skill follows the Agent Skills spec (agentskills.io), which Claude Code, Codex, and Cursor all load.

## Directory

- `SKILL.md` is required: YAML frontmatter, then Markdown instructions.
- Any other files or folders are allowed. The spec names `scripts/`, `references/`, and `assets/` as conventions, and this skill adds `examples/`.
- `SKILL.md` links to supporting files with relative paths from the skill root (`examples/proposal.md`), one level deep.

## Frontmatter

- `name`: 1 to 64 characters, lowercase letters, digits, and hyphens, and it matches the parent folder name.
- `description`: 1 to 1024 characters, says what the skill does and when to use it.
- Optional: `license`, `compatibility` (up to 500 characters), `metadata` (string map), `allowed-tools` (experimental).

## Loading

1. The client loads `name` and `description` for every skill at startup (~100 tokens).
2. The full `SKILL.md` body loads when the skill activates. The spec recommends under 5000 tokens and under 500 lines.
3. Supporting files load only when the agent reads them, so each example file stays focused on one genre.

## Source

- https://agentskills.io/specification (fetched 09/29/2026, no version shown on the page)
