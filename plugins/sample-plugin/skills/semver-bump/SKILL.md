---
name: semver-bump
description: Decide the next version number under Semantic Versioning 2.0.0. Use when the user asks what version to release next, whether a change is a major/minor/patch bump, or how to update a package's version field.
---

# Semantic Versioning Bump

Decide the next `MAJOR.MINOR.PATCH` version under Semantic Versioning 2.0.0
(https://semver.org/).

## Format

```
MAJOR.MINOR.PATCH[-PRERELEASE][+BUILD]
```

- **MAJOR** — incompatible API changes.
- **MINOR** — backward-compatible functionality added.
- **PATCH** — backward-compatible bug fixes.
- **PRERELEASE** — optional, e.g. `1.2.0-rc.1`. Denotes a version that is unstable and may not
  satisfy the intended compatibility requirements.
- **BUILD** — optional metadata, e.g. `1.2.0+20130313144700`. Ignored when comparing versions.

## Workflow

1. Ask the user for the current version and a description of the changes (or read the diff/changelog
   they provide).
2. Classify each change:
   - Any removed or incompatibly changed public API, config format, or CLI flag → **MAJOR**.
   - Any new backward-compatible feature or public API addition → **MINOR**.
   - Any backward-compatible bug fix only → **PATCH**.
3. Pick the highest-priority classification across all changes (MAJOR beats MINOR beats PATCH).
4. Apply exactly one bump:
   - MAJOR bump → increment MAJOR, reset MINOR and PATCH to 0.
   - MINOR bump → increment MINOR, reset PATCH to 0.
   - PATCH bump → increment PATCH only.
5. While the major version is `0` (initial development), treat the whole public API as unstable:
   anything can change in a MINOR or PATCH bump; use MAJOR only when the user says the project is
   ready to declare a stable `1.0.0`.
6. State the resulting version and a one-line reason ("MINOR: added an optional `--dry-run` flag,
   no existing behavior changed").
7. If asked to also update the manifest (`package.json`, `*.csproj`, `pyproject.toml`, etc.), show
   the new version string and let the user confirm before editing the file yourself.

## Examples

| Current | Change | New | Why |
|---|---|---|---|
| `1.4.2` | Added an optional parameter with a default value | `1.5.0` | backward-compatible addition |
| `1.4.2` | Fixed a null-reference crash | `1.4.3` | backward-compatible fix |
| `1.4.2` | Removed a public method | `2.0.0` | breaking change |
| `0.3.1` | Renamed a public method | `0.4.0` | pre-1.0, still MINOR unless promoting to stable |

## Common mistakes

- Bumping MAJOR for a deprecation notice alone — only the removal itself is breaking.
- Treating every pre-1.0 change as MAJOR — pre-1.0 breaking changes are MINOR bumps by convention.
- Combining multiple changes and averaging their severity instead of taking the highest one.
- Forgetting build metadata (`+BUILD`) does not affect version precedence or comparisons.
