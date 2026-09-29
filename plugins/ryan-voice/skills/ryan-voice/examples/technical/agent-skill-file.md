# Agent Instructions: Skill File

Basis: Composed from SKILL.md rules and the wording of Ryan's own edits to SKILL.md sections 0 to 3 and 6; no source document

What to notice:
- A numbered precedence list comes first, with the user's latest instruction at number 1.
- Rules use "Label: Sentence", with the sentence after the colon capitalized: "One line per change: Start with the verb, then the thing that changed."
- Conditions stay inline: "(if applicable)", "unless they change behavior a user can see".
- Short related clauses join with a comma: "Use the checklist when it fits the release, skip items that don't apply."
- "each with the action the user has to take:" is a colon lead-in to the sub-points.

## Skill file

```text
# Release notes

Write release notes for a tagged version from the PRs merged since the last tag.

## 0. Precedence

1. The user's latest instruction wins over any rule in this file.
2. When a PR description conflicts with the diff, go with the diff.
3. Never invent a feature, fix, or ticket number. If a PR has no description, use its commit subjects.

## 1. What goes in

- One line per change: Start with the verb, then the thing that changed. "Adds CSV export to the Invoices page."
- Group by type: Added, Changed, Fixed, Removed. Skip a group when it's empty.
- Internal work: Refactors, test-only PRs, and CI changes are left out unless they change behavior a user can see.
- PR links: Put the PR number at the end of each line (if applicable).

## 2. Wording

- Name the screen, setting, or command: "Settings > Billing > Download Invoice". A vague area like "the billing section" makes the reader go looking.
- Breaking changes go first in their own section, each with the action the user has to take:
  - "API: The /v2/bookings endpoint is removed on 12/01/2026. Move to /v3/bookings."
  - "Settings: Time zone is now set per location. Check each location after updating."
- Digits for numbers and versions, dates as MM/DD/YYYY.
- Flat tone: No "exciting", "powerful", or "game-changing".

## 3. When unsure

- A PR you can't classify: Put it under Changed and list it in the summary for review.
- Missing version number: Stop and ask, don't guess from the branch name.
- Use the checklist when it fits the release, skip items that don't apply.
```
