# Release tracking

Work to close release gaps: what is open upstream, what is merged and waiting for a release, and what is proven but
not submitted. The rules, including the Starship and zellij registry exceptions, are in
[release-policy.md](release-policy.md); each project's current release variants are in
[release-matrix.md](release-matrix.md).

## Open upstream submissions

| Project | Change | Upstream | State | Proof |
| --- | --- | --- | --- | --- |
| Atuin | Windows ARM64 (MSVC), native `windows-11-arm` runner, and an `atuin-server` ARM64 zip | [PR #4575](https://github.com/atuinsh/atuin/pull/4575), covers [#3056](https://github.com/atuinsh/atuin/issues/3056) | Open, no maintainer review; v18.24.5 shipped without ARM64. #3056 was closed as not planned after the default cross-compile failed: cargo-xwin passes clang-cl `/imsvc` flags to `ring`'s `clang` build ([run](https://github.com/meop/atuin/actions/runs/33228562158)). The PR sits on #4527's MSI installer, so `.github/build-setup.yml` installs WiX 3.14.1 on `windows-11-arm`. | On `windows-11-arm` with the release job's setup and `dist build`, the zip and MSI build, and the MSI installs per-user and per-machine, passes `atuin --version` with only System32 on `PATH`, and uninstalls ([run](https://github.com/meop/atuin/actions/runs/41611295544)). |
| Delta | Windows ARM64 (MSVC) | [#2223](https://github.com/dandavison/delta/issues/2223), [PR #2267](https://github.com/dandavison/delta/pull/2267) | Open, no review; the issue had no reply before it either. | Native build packaged by `before_deploy.sh` on current `main` ([run](https://github.com/meop/delta/actions/runs/37178086572)). |
| Delta | Linux ARM64 musl | [#2227](https://github.com/dandavison/delta/issues/2227), [PR #2268](https://github.com/dandavison/delta/pull/2268) | Open, no review. Third-party [PR #2236](https://github.com/dandavison/delta/pull/2236) makes the same change, but without `musl-tools` and with an unrelated README badge. | Static, stripped binary and `.deb` from the same [run](https://github.com/meop/delta/actions/runs/37178086572). |
| direnv | The pwsh hook keeps `$LASTEXITCODE` across a directory change (the problem mise fixed in [PR #15315](https://github.com/jdx/mise/pull/15315), released in v2026.11.1) | [#1657](https://github.com/direnv/direnv/issues/1657), [PR #1658](https://github.com/direnv/direnv/pull/1658) | Open, no maintainer response. nixbot's `aarch64-linux` `test-zsh` check fails on the PR; the change only touches the pwsh hook, and nixbot passes on `master`. | The PR adds a check to `test/direnv-test.ps1`; the other checks pass. |
| Ghostty | Config docs: load order of `config` and `config.ghostty`, and when `config-file` includes load (after CLI flags, so an include wins) | Discussion [#14828](https://github.com/ghostty-org/ghostty/discussions/14828), [website PR #500](https://github.com/ghostty-org/website/pull/500) | Open, no maintainer review; the discussion is labeled `needs-confirmation` with no maintainer answer. A non-maintainer confirmed `Config.load` loads every include after CLI flags; changing that would need its own issue. A code PR needs a Vouch Request written by hand, and only if a maintainer wants a code change. | Lint and build pass ([run](https://github.com/meop/website/actions/runs/41685747714)). |
| hexyl | Windows ARM64 (MSVC) | [PR #291](https://github.com/sharkdp/hexyl/pull/291) | Open, green CI, no review. | Fork release matrix. |
| hexyl | Linux ARM64 musl | [PR #292](https://github.com/sharkdp/hexyl/pull/292) | Open, green CI, no review. | Static artifact proven. |
| Komac | `update` matches previous installers in general | [#1841](https://github.com/russellbanks/Komac/issues/1841), [PR #1935](https://github.com/russellbanks/Komac/pull/1935) | Open, no review. It goes further than #1934 (merged, below); #1841 has a repro and a status of its six items. | Test results as a comment on [#1935](https://github.com/russellbanks/Komac/pull/1935#issuecomment-6371546081). |
| lsd | Windows ARM64 `gnullvm` | [PR #1244](https://github.com/lsd-rs/lsd/pull/1244) | Open. The existing `i686-pc-windows-gnu` job fails to install its toolchain on `windows-latest`, independent of this change; noted in the description. | `+crt-static` was the only option of three that started without MSYS2 ([experiment](https://github.com/meop/lsd/actions/runs/37169967049)); full [release matrix](https://github.com/meop/lsd/actions/runs/37170362416). |
| lsd | Enforce the committed lockfile in CI | [PR #1237](https://github.com/lsd-rs/lsd/pull/1237) | Open. | — |
| ouch | Windows ARM64 `gnullvm` | Proposal issue [#1094](https://github.com/ouch-org/ouch/issues/1094) | Open; branch `windows-arm64-gnullvm` is ready for a PR if they agree. MSYS2 clang compiles the C and C++ codecs; bzip3's bindgen gets MSYS2's libclang plus `--target=aarch64-w64-mingw32`, since clang rejects the `gnullvm` suffix. | Build, 117 tests, and a run without MSYS2 [passed](https://github.com/meop/ouch/actions/runs/37183581297). |
| pastel | Windows ARM64 (MSVC and `gnullvm`) | [PR #320](https://github.com/sharkdp/pastel/pull/320) | Open, no review. | Full [release matrix](https://github.com/meop/pastel/actions/runs/37170366243), including a run without MSYS2. |
| pastel | Linux ARM64 musl | [PR #322](https://github.com/sharkdp/pastel/pull/322) | Open, green CI, no review. | Static artifact proven. |
| ripgrep | Windows ARM64 `gnullvm` (release and CI) | [PR #3579](https://github.com/BurntSushi/ripgrep/pull/3579) | Open. Adds a CI lane too, as `bb0cbae` did for ARM64 MSVC, since the maintainer drops release targets whose CI breaks (`79d393a`). | Fork CI including the new lane [passed](https://github.com/meop/ripgrep/actions/runs/40630540721); release build, a run without MSYS2 and a PCRE2 search [passed](https://github.com/meop/ripgrep/actions/runs/40630540435). |
| rv | Shell hooks and Ruby install: the PowerShell prompt hook keeps `$?` and `$LASTEXITCODE`; the Nushell hook is appended instead of replacing every `pre_execution` hook, and gets PATH as a list and unset variables as `null`; the fish test runs with fish 4; `rv ruby install` without an exact version no longer reinstalls an installed Ruby | Issues [#824](https://github.com/spinel-coop/rv/issues/824), [#825](https://github.com/spinel-coop/rv/issues/825), [#826](https://github.com/spinel-coop/rv/issues/826), [#833](https://github.com/spinel-coop/rv/issues/833); PRs [#827](https://github.com/spinel-coop/rv/pull/827), [#828](https://github.com/spinel-coop/rv/pull/828), [#829](https://github.com/spinel-coop/rv/pull/829), [#830](https://github.com/spinel-coop/rv/pull/830), [#834](https://github.com/spinel-coop/rv/pull/834) | Open, no maintainer response. #834's `cargo-deny (advisories)` failure comes from advisories in dependencies (RUSTSEC-2026-0384 in tokio, RUSTSEC-2026-0385), not the change. | Upstream CI passes on #827 to #830, and on #834 apart from `cargo-deny`. |
| SD | Windows ARM64 (MSVC and `gnullvm`), with a static libunwind | [#329](https://github.com/chmln/sd/issues/329) (closed), [PR #354](https://github.com/chmln/sd/pull/354) | Open, no review, upstream CI not run. | `gnullvm` binary runs without MSYS2 ([run](https://github.com/meop/sd/actions/runs/37170389227)); [test workflow](https://github.com/meop/sd/actions/runs/37170388821) passes. |
| Vivid | Windows ARM64 `gnullvm` | [PR #245](https://github.com/sharkdp/vivid/pull/245) | Open. | Full [release matrix](https://github.com/meop/vivid/actions/runs/37170364801), including a run without MSYS2. |
| zellij | Windows ARM64 | [PR #5090](https://github.com/zellij-org/zellij/pull/5090) | Third-party PR, open with no review. | — |
| zoxide | WiX/MSI installer for winget | [#1180](https://github.com/ajeetdsouza/zoxide/issues/1180), [PR #1345](https://github.com/ajeetdsouza/zoxide/pull/1345) | Open, CI green, no review; the maintainer asked for this PR in #1180. | [Smoke](https://github.com/meop/zoxide/actions/runs/39567897889) on x64 and ARM64. |
| Gum, VHS | Windows ARM64 | Gum [#1139](https://github.com/charmbracelet/gum/discussions/1139), VHS [#780](https://github.com/charmbracelet/vhs/discussions/780) | Idea discussions, no response. Needs the [meta#305](https://github.com/charmbracelet/meta/pull/305) change in `goreleaser-full.yaml` (Gum) and `goreleaser-vhs.yaml` (VHS). | Fork smokes on `windows-arm64-release`. |

## Merged, awaiting a release

| Project | Change | Merged | Latest release |
| --- | --- | --- | --- |
| bottom | Windows ARM64 `gnullvm` starts without MSYS2: `+crt-static` in `.cargo/config.toml` ([PR #2302](https://github.com/ClementTsang/bottom/pull/2302)). 0.15.0's zip and MSI import `libunwind.dll` and exit `0xC0000135` without MSYS2 ([run](https://github.com/meop/bottom/actions/runs/41610843630)); the nightly's gnullvm `btm.exe` imports only Windows system DLLs. The maintainer split our `AllowSameVersionUpgrades` WiX change into their own [PR #2304](https://github.com/ClementTsang/bottom/pull/2304), credited to us, and in it unpinned MSYS2's clang package. | 2026-11-04 | 0.15.0 (2026-11-01) |
| Komac | `update` keeps nested installer files for multi-exe ZIPs it can't detect, which unblocks Yazi's winget submissions ([PR #1934](https://github.com/russellbanks/Komac/pull/1934); test results in [this comment](https://github.com/russellbanks/Komac/pull/1934#issuecomment-6371549943)) | 2026-11-08 | v2.17.2 (2026-11-03) |
| Glow | Windows ARM64 ([meta#305](https://github.com/charmbracelet/meta/pull/305), by a maintainer) | 2026-09-30 | v3.0.0 (2026-08-11) |
| helix | Windows ARM64 ([PR #15557](https://github.com/helix-editor/helix/pull/15557), not ours) | 2026-05-25 | 25.07.1 (2025-07-18) |
| lsd | Windows ARM64 MSVC ([PR #1236](https://github.com/lsd-rs/lsd/pull/1236)) | 2026-08-16 | v1.2.0 (2025-10-12) |
| mdBook | Windows ARM64 ([PR #3193](https://github.com/rust-lang/mdBook/pull/3193)), Linux ARM64 GNU ([PR #3207](https://github.com/rust-lang/mdBook/pull/3207)) | 2026-08-17, 2026-09-02 | v0.5.4 (2026-07-06) |
| Procs | Windows ARM64 ([PR #961](https://github.com/dalance/procs/pull/961)) | 2026-09-07 | v0.14.12 (2026-06-25) |
| SD | Linux ARM64 GNU (already in the release workflow) | — | v1.1.0 (2026-02-25) |
| Vivid | Windows ARM64 MSVC ([PR #228](https://github.com/sharkdp/vivid/pull/228)), Linux ARM64 musl ([PR #233](https://github.com/sharkdp/vivid/pull/233)) | 2026-08-17, 2026-08-31 | v0.11.1 (2026-04-09) |
| xan | Windows ARM64 MSVC and Linux ARM64 musl ([PR #1186](https://github.com/medialab/xan/pull/1186)); the maintainer moved the musl build to `ubuntu-latest` with cross, which the fork proof used but the PR missed | 2026-10-06 | 0.61.0 (2026-09-11); pre-release [0.62.0-rc.2](https://github.com/medialab/xan/releases/tag/0.62.0-rc.2) ships both targets, tested on ARM64 Windows and Linux |
| Yazi | WiX/MSI installers for stable and nightly ([PR #4473](https://github.com/sxyazi/yazi/pull/4473), the maintainer's; see [packaging work](#packaging-work)), and the MSIs in the winget `installers-regex` ([`bdd3dbd`](https://github.com/sxyazi/yazi/commit/bdd3dbdd86943d4249ea40c3a7560ec9e708cd04), from our comment on #4440) | 2026-11-02, 2026-11-04 | v26.9.1 (2026-09-01); the `nightly` release ships both MSIs |

When a release ships, check [release-matrix.md](release-matrix.md), and move the project's pending entry into
`repo.toml` if its platform gap is closed.

## Proven in a fork, not submitted

Windows ARM64 `gnullvm` builds are established elsewhere (about 210 GitHub workflows build
`aarch64-pc-windows-gnullvm`, including git, HandBrake, Microsoft's windows-rs, and R packages, since R on Windows ARM64
uses an LLVM MinGW toolchain), and btm, dust, fd and qsv ship one. `windows-11-arm` has MSYS2 at `C:\msys64`, though
its image list says it is omitted: bottom's [PR #2290](https://github.com/ClementTsang/bottom/pull/2290) installs clang
with that `pacman` ([run](https://github.com/ClementTsang/bottom/actions/runs/40924718297)). Its maintainer objected to a
new `setup-msys2` dependency, and fd's asked the same, so offer `pacman` first.

| Project | Change | Proof | Next step |
| --- | --- | --- | --- |
| Starship | Native Linux ARM64 GNU release lane (branch deleted; the run stands) | [Passed](https://github.com/meop/starship/actions/runs/33569201148). | None planned: ARM64 already ships a static musl build. |

## Handoffs and blocked work

| Project | Blocker | State |
| --- | --- | --- |
| Restic | Windows ARM64 releases ([#3596](https://github.com/restic/restic/issues/3596)) | Branch `windows-arm64-release` (fork PR `meop/restic#1`, notes in `WINDOWS-ARM64-TODO.md`) has the VSS fix: `vss_windows.go` rejected arm64, and the `VSS_ID` GUIDs were passed as pointers where arm64 passes them in two registers. With both fixed, `--use-fs-snapshot` backs up and restores on ARM64, and the full test suite matches x64. Next: add `arm64` to `helpers/build-release-binaries` (which lists only `386` and `amd64` for Windows; releases are built locally), trace the self-update asset name, then offer the fix upstream. A reporter on #3596 offered to test a patch on hardware. Tracked in `/vol/code/windows-arm64-todo.md`. |
| cabal, hadolint, ShellCheck | No native Windows ARM64 GHC | Cross-compiling works: [ghc#24603](https://gitlab.haskell.org/ghc/ghc/-/work_items/24603) closed with MR !13856, and cabal's side merged in [cabal#10705](https://github.com/haskell/cabal/pull/10705). Upstream's native compiler ([ghc#25974](https://gitlab.haskell.org/ghc/ghc/-/work_items/25974)) is claimed but idle, with related work stalled: RTS linker [ghc#26760](https://gitlab.haskell.org/ghc/ghc/-/work_items/26760), split sections [ghc#26763](https://gitlab.haskell.org/ghc/ghc/-/work_items/26763), draft MR !15346 for tables-next-to-code, C calling convention [ghc#27684](https://gitlab.haskell.org/ghc/ghc/-/work_items/27684). Local branch `wip/windows-aarch64-native` has a native GHC (built from Linux, with an AArch64 RTS linker for Template Haskell), and native `cabal.exe`, `shellcheck.exe` and `hadolint.exe` build and run with it. Releases still need that GHC work upstream, and released fixes in hsc2hs, network and Cabal 3.12 (or hadolint on Cabal >= 3.16); details in the branch's `windows-aarch64/TODO.md`, next steps in `/vol/code/windows-arm64-todo.md`. hadolint has an open winget request ([#1217](https://github.com/hadolint/hadolint/issues/1217)). |
| OpenCode | Windows ARM64 `#pty` shell sessions ([#45875](https://github.com/anomalyco/opencode/issues/45875), closed) | The TUI works since the Bun 1.4.2 bump ([PR #47446](https://github.com/anomalyco/opencode/pull/47446)). `bun-pty` 0.4.11 ships an ARM64 DLL ([bun-pty#46](https://github.com/sursaone/bun-pty/pull/46)), and [PR #54689](https://github.com/anomalyco/opencode/pull/54689) moved `dev`, the 2.x line, to it. 2.x GitHub releases ship `opencode-windows-arm64.zip` with 0.4.11, but GitHub's latest release is still a 1.x (v1.19.5), cut from the `v1` branch, which pins 0.4.8. Waiting for 2.x to become the latest release. |

### Packaging work

Scope: the four shell-integrated tools (Atuin, fzf, Yazi, zoxide), whose failure is noticed immediately because a shell
init hook runs them. Not all ghpm tools.

The problem: winget installs these as portable ZIPs, which put a symlink in `%LOCALAPPDATA%\Microsoft\WinGet\Links`. The
link is created by whoever runs winget, normally a non-elevated terminal. An administrator's SSH session is elevated
(OpenSSH logs admins on with their full token), and Windows' redirection trust stops an elevated process from following
a link a less privileged process created: "The path cannot be traversed because it contains an untrusted mount point"
(error 448). A standard user is unaffected (both sides run at medium integrity); a local "Run as administrator" terminal
is affected the same way. `windows-msi-test/repro-ssh.ps1` on the zoxide fork reproduces it for any winget id and MSI;
it needs the user logged in at the console, since it installs from a medium-integrity interactive task.

The fix: an MSI per architecture alongside the ZIP, as Starship and PowerShell ship, installing a real executable under
Program Files with its own machine PATH entry, so there is no link. The goal is parity across the four: the same winget
install methods (MSI by default, ZIP still available) and scoop packages. Scoop needs nothing: its shims are real `.exe`
files, not links, as are ghpm's.

winget manifests: zoxide, fzf and Yazi run winget-releaser on each release, and widening its installers filter to
include the MSI makes their manifests update themselves. The public test repo `meop/winget-manifest-test` proves it
(Komac `update --dry-run` on the test assets, then winget on `windows-latest` and `windows-11-arm`; green in
[run](https://github.com/meop/winget-manifest-test/actions/runs/39874259707) and, for Yazi,
[run](https://github.com/meop/winget-manifest-test/actions/runs/39875214984)): the manifest gets a `wix` installer
(machine scope, ProductCode, UpgradeCode) beside the ZIP per architecture, as Starship's does; a fresh `winget install`
picks the MSI, and `--installer-type portable` gets the ZIP. An existing portable install stays portable on
`winget upgrade`, so those users need to uninstall and reinstall once. Komac 2.17 drops `NestedInstallerFiles` for ZIPs
with more than one exe, so Yazi's next submission fails validation until a Komac release ships #1934;
winget-releaser@main always installs the latest Komac.

| Project | State | Next step |
| --- | --- | --- |
| Atuin | Shipped: the MSI ([PR #4527](https://github.com/atuinsh/atuin/pull/4527), as `19b66e7`) is in releases since v18.24.3, x64 only, installing per-user by default with a machine option. The maintainer reworked our branch: a generated license page, an icon, and a hand-maintained `main.wxs`. The v18.24.4 x64 MSI installs per-user from a non-elevated task, `atuin --version` passes in a new admin SSH session, and uninstall is clean. ARM64 comes with PR #4575 (above), and `windows-11-arm` needs WiX 3.14.1 installed (cargo-dist `github-build-setup`). | Atuin has no winget automation: a community member updates its winget-pkgs manifest, which lists only the portable ZIP. The manifest test assumed machine scope, so re-test against the per-user default, then add the MSI there. |
| fzf | Shipped in v0.75.0: the maintainer's [PR #4948](https://github.com/junegunn/fzf/pull/4948), built on our commit from issue [#4943](https://github.com/junegunn/fzf/issues/4943), with a draft release published after the MSIs upload, MSI hashes in the checksum file, no MSI for `-rc` versions, and a read-only winget token. Tested on glass: the x64 MSI installs from a non-elevated task (UAC auto-approves), a real `fzf.exe` under `Program Files\fzf\bin` passes `--version` from the machine PATH in a new admin SSH session, and uninstall removes the files and the PATH entry. The release flow from real tags on the fork: [v0.99.11](https://github.com/meop/fzf/actions/runs/41690922173), [v0.99.12](https://github.com/meop/fzf/actions/runs/41691463845), [v0.99.13-rc1](https://github.com/meop/fzf/actions/runs/41692334350). Not covered: macOS notarization, `RELEASE_PAT`, a real winget submission, retrying over an existing draft, and UAC on ARM64. | Check winget-pkgs picked up the MSI from v0.75.0. |
| Yazi | Merged, in the `nightly` release (see above): the maintainer's PR #4473 repackages the release ZIP with a short `assets/msi.wxs` (machine scope and machine PATH, as ours) in a separate `build-msi` job, and `bdd3dbd` puts the MSIs in `installers-regex`. The nightly x64 MSI installs from a non-elevated task, `yazi` and `ya` pass `--version` in a new admin SSH session, and uninstall is clean. Yazi's `AGENTS.md` tells AI agents not to create issues, PRs or comments, and to mark any they're asked to make so they get closed: write anything for Yazi by hand. | Wait for a Yazi release, and for the Komac release that ships #1934. |
| zoxide | PR #1345 open (above). MSI proven in CI and on a real x64 machine, and #1180's SSH failure reproduced with the portable install. Real-machine test steps are on fork branch `winget-wix-smoke` (`WINDOWS-MSI-TEST.md`, fork PR `meop/zoxide#1`). | After it ships, check the winget-pkgs PR matches the tested manifest. |

## Backlog

Gaps with no work started.

| Project | Gap |
| --- | --- |
| difftastic | Linux ARM64 musl, to match x64's static musl build. |
| taplo | The `taplo-full` variant dropped in 0.10.0 (see [release-matrix.md](release-matrix.md#project-notes)). |

## Pending registry entries

Projects with a platform gap. Move an entry into `repo.toml`, in alphabetical order, once a release closes the gap.

```toml
[atuin]
uri = "github.com/atuinsh/atuin"
descr = "Shell history replacement with sync, search, and stats."

[cabal]
uri = "github.com/haskell/cabal"
descr = "Command-line tool for building and packaging Haskell projects."

[delta]
uri = "github.com/dandavison/delta"
descr = "Syntax-highlighting pager for git, diff, and grep output."

[glow]
uri = "github.com/charmbracelet/glow"
descr = "Render markdown on the terminal with styling."

[gum]
uri = "github.com/charmbracelet/gum"
descr = "Interactive prompts and styling primitives for shell scripts."

[hadolint]
uri = "github.com/hadolint/hadolint"
descr = "Dockerfile linter that checks inline shell with ShellCheck."

[helix]
uri = "github.com/helix-editor/helix"
descr = "A post-modern modal text editor."

[hexyl]
uri = "github.com/sharkdp/hexyl"
descr = "Command-line hex viewer with colored output."

[lsd]
uri = "github.com/lsd-rs/lsd"
descr = "An ls with colors, icons, and a tree view."

[mdbook]
uri = "github.com/rust-lang/mdBook"
descr = "Build a browsable book from a set of markdown files."

[pastel]
uri = "github.com/sharkdp/pastel"
descr = "Generate, analyze, convert, and manipulate colors."

[procs]
uri = "github.com/dalance/procs"
descr = "A modern replacement for ps."

[restic]
uri = "github.com/restic/restic"
descr = "Fast, secure, deduplicating backup program."

[sd]
uri = "github.com/chmln/sd"
descr = "Intuitive find and replace on the command line, a sed alternative."

[shellcheck]
uri = "github.com/koalaman/shellcheck"
descr = "Static analysis tool for shell scripts."

[vhs]
uri = "github.com/charmbracelet/vhs"
descr = "Script terminal recordings and render them to GIF or video."

[vivid]
uri = "github.com/sharkdp/vivid"
descr = "Themeable LS_COLORS generator with a rich filetype database."

[xan]
uri = "github.com/medialab/xan"
descr = "CSV toolkit for the command line."
```

## Clone and fork inventory

Every canonical clone under `/vol/code` and every `meop` fork used for release work.

| Project | Clone | Fork | Branches |
| --- | --- | --- | --- |
| Atuin | yes | yes | `dist/windows-arm64-native` (PR #4575), `dist/windows-arm64-native-smoke`, `dist/windows-arm64-msi-smoke` (both fork-only) |
| bottom | yes | yes | none |
| Charm meta | yes | yes | none (for the Gum/VHS change) |
| Delta | yes | yes | `ci/windows-arm64-release-pr` (PR #2267), `ci/linux-arm64-musl-release-pr` (PR #2268) |
| fzf | yes | yes | none |
| GHC | yes (from gitlab.haskell.org) | not yet: check the gitlab.haskell.org account is verified (steps in the branch's `windows-aarch64/TODO.md`) | `wip/windows-aarch64-native` (local; native Windows ARM64 GHC) |
| ghc-windows-aarch64 | yes | own repo | Public test repo for the GHC branch's Windows AArch64 builds: releases hold the bindist, `test-ghc.yml` checks it on `windows-11-arm` |
| Ghostty website | yes | yes | `docs/config-load-order` (website PR #500) |
| Gum, VHS | yes | yes | `windows-arm64-release` (fork smoke for the meta change) |
| hexyl | yes | yes | `ci/linux-arm64-musl-release-pr` (PR #292); PR #291's branch on the fork only |
| Komac | yes | yes | `merge-previous-installers` (PR #1935) |
| lsd | yes | yes | `ci/windows-arm64-gnullvm` (PR #1244); PR #1237's branch on the fork only |
| mise | yes | yes | none |
| OpenCode | yes | no | none |
| ouch | yes | yes | `windows-arm64-gnullvm` (awaiting issue #1094), `windows-arm64-gnullvm-smoke` |
| pastel | yes | yes | `ci/linux-arm64-musl-release-pr` (PR #322); PR #320's branch `ci/platform-release-matrix` on the fork |
| Restic | yes | yes | `windows-arm64-release` (fork PR `meop/restic#1`), `research/windows-arm64-handoff` (fork-only notes) |
| ripgrep | yes | yes | `ci/windows-arm64-gnullvm` (PR #3579), `windows-arm64-gnullvm-smoke` (fork-only) |
| SD | yes | yes | `ci/windows-arm64-release-pr` (PR #354) |
| Starship | yes | yes | none |
| Vivid | yes | yes | `ci/windows-arm64-gnullvm` (PR #245) |
| winget-manifest-test | yes | own repo | Public test repo for winget manifests: release `test-assets` holds the test ZIPs and MSIs, which Komac PR #1935's results link to |
| Yazi | yes | yes | none |
| zoxide | yes | yes | `winget-msi` (PR #1345), `winget-wix-smoke` (fork-only; real-machine test notes, fork PR `meop/zoxide#1`) |
