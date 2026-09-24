# AGENTS.md

Rules for editing the **playwright-mcp** skill. User-facing guidance lives in `SKILL.md`. `README.md` is the human skim layer.

## File roles

| File | Role |
| --- | --- |
| `SKILL.md` | Trigger, screenshot path-resolution rules, troubleshooting |
| `references/SETUP.md` | First-time installation walkthrough: extension, token, editor config |
| `README.md` | Short human summary |

One owner per concern.

## Editing

- Bump `metadata.version` by the release-versioning skill's rules for skills.
- Quote every frontmatter string value. Keys stay unquoted. Never use a YAML block scalar (`>` or `|`) for `name` or `description`; the bundled validator only parses a quoted single-line value.
- No em dashes, and no semicolons used to join what should be separate sentences. Use commas, periods, parentheses, or "to".
- Capitalized bullets and parallel list voice.
- Keep the README version badge and install path in sync with `SKILL.md`'s `metadata.version` and `name`.

## Before finishing

- `references/SETUP.md` is reachable from a direct loading condition in `SKILL.md`.
- `metadata.version` bumped as the release-versioning skill requires, and the README badge matches it.
- `README.md`'s install path directory matches the frontmatter `name` exactly (no `-skill` suffix).
