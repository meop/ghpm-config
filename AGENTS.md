# AGENTS.md

## Scope

This repository is the package registry consumed by [ghpm](https://github.com/meop/ghpm). `repo.toml` maps the short package name users enter to a GitHub repository path and a one-sentence description.

## Working conventions

- One `[name]` section per package, with `uri` and `descr`.
- `uri` is a `github.com/owner/repository` path with no URL scheme.
- `descr` is a single sentence, ending in a period, under ~75 characters. Say what the tool is, not why it is good — no marketing adjectives, no emoji, no leading "A tool that".
- Use the shortest unambiguous package name as the section key. Quote a key containing a dot, e.g. `["llama.cpp"]`.
- Preserve alphabetical ordering when adding or renaming entries.
- `release-tracking.md` is the source of truth for release coverage, linkage,
  Windows ABI/toolchain, investigation branches, and upstream submissions.
  Keep `repo.toml` limited to registry data.
- Avoid unrelated registry cleanup in a focused package change.

## What belongs here

Tools that publish prebuilt release assets on GitHub for the platforms ghpm targets. A tool that is really installed some other way — an AUR helper, a winget-only app — does not belong in the registry just because it has a GitHub repo.

## Validation

- Parse `repo.toml` with a TOML parser after editing it, and confirm every entry has both `uri` and `descr`.
- Check for duplicate keys and confirm each changed GitHub repository path is spelled correctly.
- Run `git diff --check` before committing.
