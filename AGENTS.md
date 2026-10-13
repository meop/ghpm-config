# AGENTS.md

## Scope

This repository is the package registry consumed by [ghpm](https://github.com/meop/ghpm). `repo.toml` maps the short package name users enter to a GitHub repository path, a one-sentence description, and any other names the package goes by.

## Working conventions

- One `[name]` section per package, with `uri` and `descr`, and `aliases` where the package has another name.
- `uri` is a `github.com/owner/repository` path with no URL scheme.
- `descr` is a single sentence, ending in a period, under ~75 characters. Say what the tool is, not why it is good — no marketing adjectives, no emoji, no leading "A tool that".
- `aliases` is a sorted list of other names the tool is commonly called — its project name where the key is the binary (`ripgrep` for `rg`), or the binary where the key is the project (`difft` for `difftastic`). A name several unrelated tools share is not an alias (`tldr` is every tldr client's binary, `sg` is already a Linux command), since typing it would not say which was meant. An alias is a whole name ghpm's acting commands accept in place of the key, so it must not be another entry's key or alias. Do not add one to help a search along: `ghpm find` already reads the repository path and `descr`, and matches the start of any word. Leave the field out when there is no other name.
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
- Confirm no alias repeats a key or another entry's alias.
- Check for duplicate keys and confirm each changed GitHub repository path is spelled correctly.
- Run `git diff --check` before committing.
