# AGENTS.md

## Scope

This repository is the package registry consumed by [ghpm](https://github.com/meop/ghpm). `repo.toml` maps the short package name users enter to a GitHub repository path and a one-sentence description.

## Working conventions

- One `[name]` section per package, with `uri` and `descr`.
- `uri` is a `github.com/owner/repository` path with no URL scheme.
- `descr` is a single sentence, ending in a period, under ~75 characters. Say what the tool is, not why it is good — no marketing adjectives, no emoji, no leading "A tool that".
- Use the shortest unambiguous package name as the section key. Quote a key containing a dot, e.g. `["llama.cpp"]`.
- Preserve alphabetical ordering when adding or renaming entries.
- Release documents: `release-policy.md` has the rules for what belongs in the
  registry and how release variants are judged. `release-matrix.md` records
  each project's current release variants, and
  `release-tracking.md` tracks ongoing work, open submissions, pending registry
  entries, and fork branches. Keep `repo.toml` limited to registry data.
- Avoid unrelated registry cleanup in a focused package change.

## What belongs here

Tools whose latest GitHub release ships prebuilt assets for every platform ghpm targets: Windows x64, Windows ARM64, Linux x64, Linux ARM64, and macOS ARM64. A tool missing any of these waits as a pending entry in `release-tracking.md` until a release closes the gap. Exceptions and drop rules are in the release policy. A tool that is really installed some other way — an AUR helper, a winget-only app — does not belong in the registry just because it has a GitHub repo.

## Validation

- Parse `repo.toml` with a TOML parser after editing it, and confirm every entry has both `uri` and `descr`.
- Check for duplicate keys and confirm each changed GitHub repository path is spelled correctly.
- Run `git diff --check` before committing.
