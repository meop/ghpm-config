# ghpm-config

Package alias registry for [ghpm](https://github.com/meop/ghpm).

## aliases.yaml

Maps short names to GitHub repos:

```yaml
aliases:
  fzf: github.com/junegunn/fzf
  gh: github.com/cli/cli
```

ghpm downloads this file and caches it locally at `~/.ghpm/aliases/github.com/meop/ghpm-config/aliases.yaml`. The cache is refreshed during `ghpm update`.

## Adding aliases

Open a PR editing `aliases.yaml`. The key is the short name users type, the value is the full `github.com/owner/repo` path.

## License

[MIT](LICENSE.txt)
