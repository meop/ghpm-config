# ghpm-config

Package repo registry for [ghpm](https://github.com/meop/ghpm).

## repo.toml

A flat table mapping short names to GitHub repos (no top-level key):

```toml
fzf = "github.com/junegunn/fzf"
gh = "github.com/cli/cli"
```

ghpm downloads this file and caches it locally at `~/.ghpm/repo/github.com/meop/ghpm-config/repo.toml`. The cache is refreshed by `ghpm refresh`.

## Adding repos

Open a PR editing `repo.toml`. The key is the short name users type, the value is the full `github.com/owner/repo` path.

## License

[MIT](LICENSE)
