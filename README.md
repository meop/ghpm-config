# ghpm-config

Package repo registry for [ghpm](https://github.com/meop/ghpm).

## repo.toml

One section per package, keyed by the short name users type:

```toml
[rg]
uri = "github.com/BurntSushi/ripgrep"
descr = "Recursively search directories with regex, respecting gitignore."
aliases = ["ripgrep"]
```

- `uri` — the `github.com/owner/repo` path, no scheme.
- `descr` — one sentence saying what the tool is. Shown by `ghpm find` and `ghpm info`, and searched by `ghpm find`.
- `aliases` — optional. Other names the tool is commonly called. `ghpm add ripgrep` installs `rg`, and `remove`, `sync` and `info` accept the alias the same way; the package is always installed under its key.

ghpm downloads this file and caches it locally at `~/.ghpm/repo/github.com/meop/ghpm-config/repo.toml`. The cache is refreshed by `ghpm refresh`.

ghpm also accepts the older flat form (`fzf = "github.com/junegunn/fzf"`) in any `repo.toml` it reads, so a personal registry needs no `descr` or `aliases`.

## Adding repos

Open a PR editing `repo.toml`, keeping entries in alphabetical order. Registry entries are for tools whose GitHub releases ship prebuilt assets for Windows x64 and ARM64, Linux x64 and ARM64, and macOS ARM64 (see [release-matrix.md](release-matrix.md) and [release-tracking.md](release-tracking.md) for tools with gaps); a tool better installed by a system package manager belongs in that manager, not here.

## License

[MIT](LICENSE)
