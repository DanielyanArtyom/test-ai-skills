---
name: conventional-commits
description: Write git commit messages that follow the Conventional Commits 1.0.0 specification. Use when the user asks to write, fix, or review a commit message, squash commits, or prepare a changelog-friendly history. Also use when someone mentions "conventional commits", "commit type", "feat/fix/chore", or "breaking change footer".
---

# Conventional Commits

Write commit messages in the format defined by the Conventional Commits 1.0.0 specification
(https://www.conventionalcommits.org/en/v1.0.0/).

## Format

```
<type>[optional scope][!]: <description>

[optional body]

[optional footer(s)]
```

- **type** — one of the types in the table below.
- **scope** — optional noun in parentheses naming the affected area, for example `feat(parser):`.
- **!** — marks a breaking change, for example `feat(api)!: remove v1 endpoints`.
- **description** — imperative mood, lower case, no trailing period, at most 72 characters.
- **body** — explains *what* and *why*, not *how*. Separate it from the header with one blank line; wrap at 72 characters.
- **footer** — `Token: value` lines such as `Refs: #123`, or `BREAKING CHANGE: <explanation>`.

## Types

| Type | Use for |
|---|---|
| `feat` | a new user-facing feature |
| `fix` | a bug fix |
| `docs` | documentation only |
| `style` | formatting that does not change meaning |
| `refactor` | code change that neither fixes a bug nor adds a feature |
| `perf` | performance improvement |
| `test` | adding or correcting tests |
| `build` | build system or dependencies |
| `ci` | CI configuration |
| `chore` | maintenance that does not touch source or tests |
| `revert` | reverts a previous commit |

## Workflow

1. Read the staged diff the user provides (or ask them to share `git diff --staged` output).
2. Pick the single type that best describes the change. If the diff mixes unrelated changes,
   suggest splitting it into separate commits instead of choosing a vague type.
3. Choose a scope only when the project already uses scopes or the affected area is obvious.
4. Write the description in imperative mood: "add", not "added" or "adds".
5. Add a body when the reason for the change is not obvious from the header.
6. Add `BREAKING CHANGE:` in the footer (or `!` in the header) when public behavior changes incompatibly.
7. Show the final message to the user. Do not run `git commit` yourself unless the user explicitly asks.

## Examples

```
fix(auth): reject expired refresh tokens

Tokens past their expiry were accepted until the next server restart
because the cache ignored the exp claim.

Refs: #482
```

```
feat(api)!: return ISO 8601 dates in all responses

BREAKING CHANGE: date fields were previously Unix timestamps.
Clients must parse ISO 8601 strings instead.
```

```
docs: explain local setup in README
```

## Common mistakes

- Past tense ("fixed bug") — use imperative ("fix bug").
- Capitalized or period-terminated description — keep it lower case, no trailing period.
- `chore` used for everything — pick the most specific type.
- Several unrelated changes in one commit — split them.
