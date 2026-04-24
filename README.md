# ghpm-config

Package repo registry for [ghpm](https://github.com/meop/ghpm).

## repos.yaml

Maps short names to GitHub repos:

```yaml
repos:
  fzf: github.com/junegunn/fzf
  gh: github.com/cli/cli
```

ghpm downloads this file and caches it locally at `~/.ghpm/repos/github.com/meop/ghpm-config/repos.yaml`. The cache is refreshed during `ghpm update`.

## Adding repos

Open a PR editing `repos.yaml`. The key is the short name users type, the value is the full `github.com/owner/repo` path.

## License

[MIT](LICENSE.txt)
