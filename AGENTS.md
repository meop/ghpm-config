# AGENTS.md

## Scope

This repository is the package registry consumed by [ghpm](https://github.com/meop/ghpm). `repo.toml` is a flat mapping from the short package name users enter to a `github.com/owner/repository` path.

## Working conventions

- Keep `repo.toml` flat; do not add a top-level table.
- Use the shortest unambiguous package name as the key and omit URL schemes from repository values.
- Preserve alphabetical ordering when adding or renaming entries.
- Avoid unrelated registry cleanup in a focused package change.

## Validation

- Parse `repo.toml` with a TOML parser after editing it.
- Check for duplicate keys and confirm each changed GitHub repository path is spelled correctly.
- Run `git diff --check` before committing.
