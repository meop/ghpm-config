# ghpm-config

Package repo registry for [ghpm](https://github.com/meop/ghpm).

## repo.toml

One section per package, keyed by the short name users type:

```toml
[fzf]
uri = "github.com/junegunn/fzf"
descr = "Command-line fuzzy finder."
```

- `uri` — the `github.com/owner/repo` path, no scheme.
- `descr` — one sentence saying what the tool is. Shown by `ghpm find` and `ghpm info`.

ghpm downloads this file and caches it locally at `~/.ghpm/repo/github.com/meop/ghpm-config/repo.toml`. The cache is refreshed by `ghpm refresh`.

ghpm also accepts the older flat form (`fzf = "github.com/junegunn/fzf"`) in any `repo.toml` it reads, so a personal registry needs no `descr`.

## Adding repos

Open a PR editing `repo.toml`, keeping entries in alphabetical order. Registry entries are for tools that ship prebuilt release assets on GitHub for the platforms ghpm targets; a tool better installed by a system package manager belongs in that manager, not here.

## License

[MIT](LICENSE)
