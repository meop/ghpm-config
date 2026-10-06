# Release matrix

Release variants of every project in `repo.toml` and every pending entry in
[release-tracking.md](release-tracking.md#pending-registry-entries), from each
project's latest GitHub release as of 2026-10-04; delta, gdu, hyperfine, qsv
and typos refreshed 2026-10-06. The rules for judging these
are in [release-policy.md](release-policy.md).

## Legend

- **ABI or libc name** (MSVC, GNU, gnullvm, MinGW, musl): taken from the asset
  name. Verify against the release workflow or the binary before relying on it.
- **yes**: an asset exists, but its name does not say which toolchain or libc.
  Go projects ship static binaries named only by OS and architecture.
- **plain**: an unlabeled build shipped alongside a labeled one, for example a
  default glibc build next to a musl build.
- **missing**: no asset for that platform.
- **Uploaded by**: the account that uploaded the release assets. Anything other
  than GitHub Actions usually means the release was built or uploaded outside
  GitHub Actions (see [release-policy.md](release-policy.md#release-process-preference)).
  Bot accounts such as `astral-releases-bot[bot]` run in CI.

## Matrix

| Project | Listed | Release | Windows x64 | Windows ARM64 | Linux x64 | Linux ARM64 | macOS ARM64 | Uploaded by |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| actionlint | registry | v1.7.12 (2026-03-30) | yes | yes | yes | yes | yes | GitHub Actions |
| age | registry | v1.3.2 (2026-08-29) | yes | yes | yes | yes | yes | GitHub Actions |
| ast-grep | registry | 0.45.3 (2026-08-31) | MSVC | MSVC | GNU | GNU | yes | GitHub Actions |
| atuin | pending | v18.23.0 (2026-09-22) | MSVC | **missing** | GNU, musl | GNU, musl | yes | GitHub Actions |
| bat | registry | v0.26.1 (2025-12-02) | MSVC | MSVC | GNU, musl | GNU, musl | yes | GitHub Actions |
| biome | registry | @biomejs/biome@2.5.15 (2026-09-30) | yes | yes | musl, plain | musl, plain | yes | GitHub Actions |
| btm | registry | 0.14.9 (2026-08-27) | GNU, MSVC | MSVC | GNU, musl | GNU, musl, plain | yes | GitHub Actions |
| bun | registry | bun-v1.4.2 (2026-09-05) | yes | yes | musl, plain | musl, plain | yes | dylan-conway |
| cabal | pending | cabal-install-v3.18.2.0 (2026-09-30) | MinGW | **missing** | yes | yes | yes | GitHub Actions |
| caddy | registry | v2.11.7 (2026-10-03) | yes | yes | yes | yes | yes | GitHub Actions |
| chezmoi | registry | v2.73.0 (2026-09-28) | yes | yes | musl, plain | yes | yes | twpayne |
| claude | registry | v2.1.289 (2026-10-03) | yes | yes | musl, plain | musl, plain | yes | ashwin-ant |
| codegraph | registry | v1.6.2 (2026-10-03) | yes | yes | yes | yes | yes | GitHub Actions |
| codex | registry | rust-v0.162.0-alpha.9 (2026-10-03) | MSVC, plain | MSVC, plain | GNU, musl, plain | GNU, musl, plain | yes | GitHub Actions |
| croc | registry | v11.5.4 (2026-09-26) | yes | yes | yes | yes | yes | GitHub Actions |
| curlie | registry | v1.8.2 (2025-03-07) | yes | yes | yes | yes | yes | rs |
| delta | pending | 0.20.1 (2026-10-04) | MSVC | **missing** | GNU, musl | GNU | yes | GitHub Actions |
| deno | registry | v2.9.7 (2026-09-17) | MSVC | MSVC | GNU | GNU | yes | GitHub Actions |
| difftastic | registry | 0.71.0 (2026-09-18) | MSVC | MSVC | GNU, musl | GNU | yes | GitHub Actions |
| direnv | registry | v2.37.1 (2025-07-20) | yes | yes | yes | yes | yes | GitHub Actions |
| dive | registry | v0.13.1 (2025-03-29) | yes | yes | yes | yes | yes | wagoodman |
| dprint | registry | 0.60.1 (2026-10-03) | MSVC | MSVC | GNU, musl, plain | GNU, musl, plain | yes | GitHub Actions |
| dua | registry | v2.45.1 (2026-09-30) | MSVC | MSVC | musl | musl | yes | GitHub Actions |
| duf | registry | v0.9.1 (2025-09-08) | yes | yes | yes | yes | yes | muesli |
| dust | registry | v1.2.6 (2026-09-16) | GNU, MSVC | MSVC | GNU, musl | GNU, musl | yes | GitHub Actions |
| fastfetch | registry | 2.69.0 (2026-09-25) | MinGW-Clang | MinGW-Clang | musl, plain | yes | yes | GitHub Actions |
| fd | registry | v10.5.0 (2026-08-26) | GNU, MSVC | MSVC | GNU, musl | GNU, musl | yes | GitHub Actions |
| fzf | registry | v0.74.4 (2026-09-12) | yes | yes | yes | yes | yes | junegunn |
| gdu | registry | v5.38.0 (2026-10-05) | yes | yes | yes | yes | yes | GitHub Actions |
| git-lfs | registry | v3.8.0 (2026-08-28) | yes | yes | yes | yes | yes | chrisd8088 |
| glow | pending | v3.0.0 (2026-08-11) | yes | **missing** | yes | yes | yes | GitHub Actions |
| golangci-lint | registry | v2.14.0 (2026-09-24) | yes | yes | yes | yes | yes | GitHub Actions |
| goreleaser | registry | v2.18.2 (2026-09-17) | yes | yes | yes | yes | yes | GitHub Actions |
| grpcurl | registry | v1.9.4 (2026-08-31) | yes | yes | yes | yes | yes | GitHub Actions |
| gum | pending | v2.0.2 (2026-09-24) | yes | **missing** | yes | yes | yes | GitHub Actions |
| hadolint | pending | v2.15.1 (2026-07-31) | yes | **missing** | yes | yes | yes | GitHub Actions |
| helix | pending | 25.07.1 (2025-07-18) | yes | **missing** | yes | yes | yes | GitHub Actions |
| hexyl | pending | v0.17.0 (2026-02-14) | MSVC | **missing** | GNU, musl | GNU | yes | GitHub Actions |
| hyperfine | registry | v1.21.0 (2026-10-05) | MSVC | MSVC | GNU, musl | GNU, musl | yes | GitHub Actions |
| jq | registry | jq-1.8.2 (2026-06-20) | yes | yes | yes | yes | yes | GitHub Actions |
| just | registry | 1.58.0 (2026-08-03) | MSVC | MSVC | musl | musl | yes | GitHub Actions |
| k9s | registry | v0.51.0 (2026-06-06) | yes | yes | yes | yes | yes | derailed |
| lazydocker | registry | v0.25.2 (2026-04-19) | yes | yes | yes | yes | yes | jesseduffield |
| lazygit | registry | v0.65.1 (2026-09-13) | yes | yes | yes | yes | yes | stefanhaller |
| llama.cpp | registry | b11382 (2026-10-04) | yes | yes | yes | yes | yes | GitHub Actions |
| lsd | pending | v1.2.0 (2025-10-12) | GNU, MSVC | **missing** | GNU, musl | GNU, musl | yes | GitHub Actions |
| mdbook | pending | v0.5.4 (2026-07-06) | MSVC | **missing** | GNU, musl | musl | yes | GitHub Actions |
| mise | registry | v2026.10.1 (2026-10-03) | yes | yes | musl, plain | musl, plain | yes | mise-en-dev |
| nerd-fonts | registry | v3.5.1 (2026-08-21) | n/a | n/a | n/a | n/a | n/a | — |
| nu | registry | 0.116.0 (2026-09-26) | MSVC | MSVC | GNU, musl | GNU, musl | yes | GitHub Actions |
| nvim | registry | v0.12.5 (2026-08-23) | MSVC | MSVC | yes | yes | yes | GitHub Actions |
| opencode | registry | v1.18.34 (2026-09-30) | yes | yes | musl, plain | musl, plain | yes | opencode-agent[bot] |
| ouch | registry | 0.8.3 (2026-09-13) | GNU, MSVC | MSVC | GNU, musl | GNU, musl | yes | GitHub Actions |
| pastel | pending | v0.12.0 (2026-02-14) | GNU, MSVC | **missing** | GNU, musl | GNU | yes | GitHub Actions |
| pnpm | registry | v12.9.1 (2026-10-03) | yes | yes | musl, plain | musl, plain | yes | GitHub Actions |
| procs | pending | v0.14.12 (2026-06-25) | yes | **missing** | yes | yes | yes | GitHub Actions |
| psnwdl | registry | v0.1.1 (2026-08-08) | yes | yes | yes | yes | yes | GitHub Actions |
| pwsh | registry | v7.6.6 (2026-09-08) | yes | yes | musl, plain | yes | yes | jshigetomi |
| qsv | registry | 24.0.0 (2026-10-05) | GNU, MSVC | gnullvm, MSVC | GNU, musl | GNU, musl | yes | GitHub Actions |
| rclone | registry | v1.75.1 (2026-09-04) | yes | yes | yes | yes | yes | ncw |
| restic | pending | v0.19.1 (2026-07-05) | yes | **missing** | yes | yes | yes | fd0 |
| rg | registry | 15.2.0 (2026-07-15) | GNU, MSVC | MSVC | musl | GNU, musl | yes | GitHub Actions |
| ruff | registry | 0.16.10 (2026-10-01) | MSVC | MSVC | GNU, musl | GNU, musl | yes | astral-automations-bot[bot] |
| rv | registry | v0.7.1 (2026-09-24) | MSVC | MSVC | GNU, musl | GNU, musl | yes | GitHub Actions |
| scc | registry | v4.1.0 (2026-09-07) | yes | yes | yes | yes | yes | boyter |
| sd | pending | v1.1.0 (2026-02-25) | GNU, MSVC | **missing** | GNU, musl | musl | yes | GitHub Actions |
| shellcheck | pending | v0.11.0 (2025-08-04) | yes | **missing** | yes | yes | yes | GitHub Actions, koalaman |
| sops | registry | v3.13.3 (2026-07-23) | yes | yes | yes | yes | yes | GitHub Actions |
| starship | registry (exception) | v1.26.0 (2026-06-28) | MSVC | MSVC | GNU, musl | musl | yes | GitHub Actions |
| stern | registry | v1.34.0 (2026-05-02) | yes | yes | yes | yes | yes | GitHub Actions |
| taplo | registry | 0.10.0 (2025-05-23) | yes | yes | yes | yes | yes | panekj |
| task | registry | v3.54.0 (2026-10-01) | yes | yes | yes | yes | yes | GitHub Actions |
| tealdeer | registry | v1.9.0 (2026-08-24) | MSVC | MSVC | musl | musl | yes | GitHub Actions |
| tree-sitter | registry | v0.27.0 (2026-08-30) | yes | yes | yes | yes | yes | GitHub Actions |
| typos | pending | v1.51.0 (2026-10-06) | MSVC | **missing** | musl | musl | yes | GitHub Actions |
| uv | registry | 0.12.23 (2026-10-03) | MSVC | MSVC | GNU, musl | GNU, musl | yes | astral-releases-bot[bot] |
| vhs | pending | v0.12.1 (2026-09-24) | yes | **missing** | yes | yes | yes | GitHub Actions |
| vivid | pending | v0.11.1 (2026-04-09) | GNU, MSVC | **missing** | GNU, musl | GNU | yes | GitHub Actions |
| watchexec | registry | v2.7.4 (2026-10-02) | MSVC | MSVC | GNU, musl | GNU, musl | yes | GitHub Actions |
| xan | pending | 0.61.0 (2026-09-11) | MSVC | **missing** | GNU, musl | GNU | yes | GitHub Actions |
| yazi | registry | v26.9.1 (2026-09-01) | MSVC | MSVC | GNU, musl | GNU, musl | yes | GitHub Actions |
| yq | registry | v4.54.1 (2026-09-29) | yes | yes | yes | yes | yes | GitHub Actions |
| zellij | registry (exception) | v0.45.1 (2026-08-28) | MSVC | **missing** | musl | musl | yes | GitHub Actions |
| zoxide | registry | v0.10.0 (2026-07-04) | MSVC | MSVC | musl | musl, plain | yes | GitHub Actions |

## Notes

### Linux musl linkage

These musl-labelled releases are dynamically linked, so they need a musl
loader and are not portable static binaries.

| Project | Reason |
| --- | --- |
| Bun | Dynamic by design; [#16056](https://github.com/oven-sh/bun/issues/16056) requests a static musl release binary and [#16699](https://github.com/oven-sh/bun/issues/16699) tracks static `--compile` output. |
| Claude Code | Bundled through Bun; same runtime model. |
| Fastfetch | [#2102](https://github.com/fastfetch-cli/fastfetch/issues/2102) was declined because the plugin architecture uses dynamic loading. |
| OpenCode | Current musl asset is dynamic. |
| pnpm | Current musl asset is dynamic. |
| PowerShell | Deliberate: it ships a multi-file runtime, not a single binary. |

### Project notes

| Project | Note |
| --- | --- |
| cabal | GitHub release assets began with 3.18; earlier releases were on haskell.org. Windows x64 is a MinGW build. |
| chezmoi | Ships glibc, musl, and static Go builds for Linux x64; the plain Linux ARM64 build is static Go, so no libc gap. |
| codex | The latest unmarked release is an alpha tag; stable `rust-v*` releases ship the same platforms. |
| Delta | macOS x64 was dropped on purpose ([#2074](https://github.com/dandavison/delta/pull/2074)). Release CI has been partly broken since 0.19.0 ([#2127](https://github.com/dandavison/delta/issues/2127)). |
| Fastfetch | Windows builds use MSYS2 `CLANG64` and `CLANGARM64` with bundled DLLs, complete within that family. |
| llama.cpp | Releases are numbered build tags (`b<n>`); Linux builds are named `ubuntu`. |
| mdBook | `deploy.yml` builds and uploads assets in GitHub Actions when a release is created. |
| nerd-fonts | Fonts; target platforms do not apply. |
| PowerShell | Linux x64 ships glibc and dynamic musl; Linux ARM64 ships glibc only. Not a gap: musl here is an Alpine runtime package, not a static binary. |
| qsv | ARM64 builds ship only `qsv` and `qsvlite`: `qsvdp` and `qsvmcp` are not built for ARM64 Linux (their Polars link runs the hosted ARM runner out of memory), nor `qsvmcp` for Windows ARM64. |
| Restic | Releases are built locally with the `restic/builder` container. |
| ShellCheck | The Windows x64 asset is a bare `shellcheck-<version>.zip`. |
| taplo | 0.10.0 was built outside CI and uploaded by a maintainer. It dropped every `taplo-full-*` asset that 0.9.3 and earlier shipped from GitHub Actions, with no issue explaining why ([#834](https://github.com/tamasfe/taplo/issues/834) covers packaging only). |
