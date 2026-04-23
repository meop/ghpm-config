# ghpm-config

Package alias registry for [ghpm](https://github.com/meop/ghpm).

## aliases.yaml

Maps short names to GitHub repos:

```yaml
---
fzf: github.com/junegunn/fzf
gh: github.com/cli/cli
```

ghpm downloads this file and caches it locally at `~/.ghpm/aliases.yaml`. The cache is refreshed from this repo during `ghpm update`.

## Adding aliases

Open a PR editing `cfg/aliases.yaml`. The key is the short name users type, the value is the full `github.com/owner/repo` path.

## License

[MIT](LICENSE)
