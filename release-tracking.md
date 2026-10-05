# Release tracking

Ongoing work to close release gaps, as of 2026-10-04. The rules, including
the Starship and zellij registry exceptions, are in
[release-policy.md](release-policy.md); each project's current release
variants are in [release-matrix.md](release-matrix.md).

## Open upstream submissions

| Project | Change | Upstream | State | Proof |
| --- | --- | --- | --- | --- |
| Delta | Windows ARM64 (MSVC) | [#2223](https://github.com/dandavison/delta/issues/2223), [PR #2267](https://github.com/dandavison/delta/pull/2267) | PR opened 2026-10-04 after a month without a reply on the issue. | Native build packaged by `before_deploy.sh` on current `main` ([run](https://github.com/meop/delta/actions/runs/37178086572)). |
| Delta | Linux ARM64 musl | [#2227](https://github.com/dandavison/delta/issues/2227), [PR #2268](https://github.com/dandavison/delta/pull/2268) | PR opened 2026-10-04. Third-party [PR #2236](https://github.com/dandavison/delta/pull/2236) (2026-09-13) makes the same change, but without `musl-tools` and with an unrelated README badge. | Static, stripped binary and `.deb` from the same [run](https://github.com/meop/delta/actions/runs/37178086572). |
| dust | Windows ARM64 `gnullvm` | [PR #632](https://github.com/bootandy/dust/pull/632) | Opened 2026-10-04. | Full CI matrix plus a run without MSYS2 [passed](https://github.com/meop/dust/actions/runs/37182269948). The fork's RISC-V job requests `ubuntu-24.04-riscv`, which this account lacks, so fork runs never finish on their own. |
| hexyl | Windows ARM64 (MSVC) | [PR #291](https://github.com/sharkdp/hexyl/pull/291) | Open since 2026-08-16; green CI, no review. | Fork release matrix. |
| hexyl | Linux ARM64 musl | [PR #292](https://github.com/sharkdp/hexyl/pull/292) | Open since 2026-08-31; green CI, no review. | Static artifact proven. |
| lsd | Windows ARM64 `gnullvm` | [PR #1244](https://github.com/lsd-rs/lsd/pull/1244) | Opened 2026-10-04. The existing `i686-pc-windows-gnu` job fails to install its toolchain on `windows-latest`, independent of this change; noted in the description. | `+crt-static` was the only option of three that started without MSYS2 ([experiment](https://github.com/meop/lsd/actions/runs/37169967049)); full [release matrix](https://github.com/meop/lsd/actions/runs/37170362416). |
| lsd | Enforce the committed lockfile in CI | [PR #1237](https://github.com/lsd-rs/lsd/pull/1237) | Open since 2026-08-16. | — |
| ouch | Windows ARM64 `gnullvm` | Proposal issue [#1094](https://github.com/ouch-org/ouch/issues/1094) | Opened 2026-10-04; branch `windows-arm64-gnullvm` is ready for a PR if they agree. MSYS2 clang compiles the C and C++ codecs; bzip3's bindgen gets MSYS2's libclang plus `--target=aarch64-w64-mingw32`, since clang rejects the `gnullvm` suffix. | Build, 117 tests, and a run without MSYS2 [passed](https://github.com/meop/ouch/actions/runs/37183581297). |
| pastel | Windows ARM64 (MSVC and `gnullvm`) | [PR #320](https://github.com/sharkdp/pastel/pull/320) | Open since 2026-08-16, no review; `gnullvm` added 2026-10-04. | Full [release matrix](https://github.com/meop/pastel/actions/runs/37170366243), including a run without MSYS2. |
| pastel | Linux ARM64 musl | [PR #322](https://github.com/sharkdp/pastel/pull/322) | Open since 2026-08-31; green CI, no review. | Static artifact proven. |
| SD | Windows ARM64 (MSVC and `gnullvm`) | [#329](https://github.com/chmln/sd/issues/329) (closed), [PR #354](https://github.com/chmln/sd/pull/354) | Open since 2026-09-01, no review, upstream CI not run. Static-libunwind fix pushed 2026-10-04. | `gnullvm` binary runs without MSYS2 ([run](https://github.com/meop/sd/actions/runs/37170389227)); [test workflow](https://github.com/meop/sd/actions/runs/37170388821) passes. |
| Typos | Windows ARM64 (MSVC) | [PR #1602](https://github.com/crate-ci/typos/pull/1602) | Commits split as requested on 2026-08-28; awaiting re-review. | Fork release matrix. |
| Vivid | Windows ARM64 `gnullvm` | [PR #245](https://github.com/sharkdp/vivid/pull/245) | Opened 2026-10-04. | Full [release matrix](https://github.com/meop/vivid/actions/runs/37170364801), including a run without MSYS2. |
| xan | Windows ARM64 (MSVC) and Linux ARM64 musl | [#1185](https://github.com/medialab/xan/issues/1185), [PR #1186](https://github.com/medialab/xan/pull/1186) | The maintainer welcomed it on 2026-10-05; PR opened the same day. He asked for the targets in the README (added) and to drop the LLM co-author lines on squash (agreed). | Release action in dry-run mode; ARM64 musl binary static and runs on ARM64, `xan.exe` runs on Windows ARM64 ([run](https://github.com/meop/xan/actions/runs/37176732631)). |
| zellij | Windows ARM64 | [PR #5090](https://github.com/zellij-org/zellij/pull/5090) | Third-party PR open since 2026-04 with no review. | — |
| zoxide | WiX/MSI installer for winget | [#1180](https://github.com/ajeetdsouza/zoxide/issues/1180) | Maintainer asked for an MSI PR on 2026-05-10. Not yet submitted; see [packaging work](#packaging-work). | — |
| Gum, VHS | Windows ARM64 | Gum [#1139](https://github.com/charmbracelet/gum/discussions/1139), VHS [#780](https://github.com/charmbracelet/vhs/discussions/780) | Idea discussions, no response. Needs the [meta#305](https://github.com/charmbracelet/meta/pull/305) change in `goreleaser-full.yaml` (Gum) and `goreleaser-vhs.yaml` (VHS). | Fork smokes on `windows-arm64-release`. |

## Merged, awaiting a release

| Project | Change | Merged | Latest release |
| --- | --- | --- | --- |
| GDU | Windows ARM64 ([PR #647](https://github.com/dundee/gdu/pull/647)) | 2026-10-02 | v5.37.0 (2026-08-18) |
| Glow | Windows ARM64 ([meta#305](https://github.com/charmbracelet/meta/pull/305), by a maintainer) | 2026-09-30 | v3.0.0 (2026-08-11) |
| helix | Windows ARM64 ([PR #15557](https://github.com/helix-editor/helix/pull/15557), not ours) | 2026-05-25 | 25.07.1 (2025-07-18) |
| hyperfine | Windows ARM64 ([PR #922](https://github.com/sharkdp/hyperfine/pull/922)), Linux ARM64 musl ([PR #924](https://github.com/sharkdp/hyperfine/pull/924)) | 2026-10-02 | v1.20.0 (2025-11-18) |
| lsd | Windows ARM64 MSVC ([PR #1236](https://github.com/lsd-rs/lsd/pull/1236)) | 2026-08-16 | v1.2.0 (2025-10-12) |
| mdBook | Windows ARM64 ([PR #3193](https://github.com/rust-lang/mdBook/pull/3193)), Linux ARM64 GNU ([PR #3207](https://github.com/rust-lang/mdBook/pull/3207)) | 2026-08-17, 2026-09-02 | v0.5.4 (2026-07-06) |
| Procs | Windows ARM64 ([PR #961](https://github.com/dalance/procs/pull/961)) | 2026-09-07 | v0.14.12 (2026-06-25) |
| qsv | Linux ARM64 musl ([PR #4721](https://github.com/dathere/qsv/pull/4721)), Windows ARM64 `gnullvm` ([PR #4722](https://github.com/dathere/qsv/pull/4722)) | 2026-10-04 | 23.0.1 (2026-09-13) |
| SD | Linux ARM64 GNU (already in the release workflow) | — | v1.1.0 (2026-02-25) |
| Vivid | Windows ARM64 MSVC ([PR #228](https://github.com/sharkdp/vivid/pull/228)), Linux ARM64 musl ([PR #233](https://github.com/sharkdp/vivid/pull/233)) | 2026-08-17, 2026-08-31 | v0.11.1 (2026-04-09) |

When a release ships, check [release-matrix.md](release-matrix.md), and move
the project's pending entry into `repo.toml` if its platform gap is closed.

## Proven in a fork, not submitted

Windows ARM64 `gnullvm` builds are established elsewhere (about 210 GitHub
workflows build `aarch64-pc-windows-gnullvm`, including git, HandBrake,
Microsoft's windows-rs, and R packages, since R on Windows ARM64 uses an LLVM
MinGW toolchain), though no registry project ships one yet.

| Project | Branch | Change | Proof | Next step |
| --- | --- | --- | --- | --- |
| Atuin | `dist/windows-arm64-native` | Add `aarch64-pc-windows-msvc` to cargo-dist and pin it to a `windows-11-arm` custom runner, as every other Atuin target is already pinned to a native runner. `dist generate` leaves `release.yml` unchanged. | Default cross-compile [fails](https://github.com/meop/atuin/actions/runs/33228562158): cargo-xwin passes clang-cl `/imsvc` flags to `ring`'s `clang` build. On current `main`, the native build, `atuin --version`, the dist plan, and the dist-planned package all [pass](https://github.com/meop/atuin/actions/runs/37175505700). | Open the PR. Atuin asks contributors to write the description themselves; #3056 was closed as not planned when the maintainer could not recall the failure. |
| fd | `ci/windows-arm64-gnullvm` | Windows ARM64 `gnullvm` lane on `windows-11-arm`, `+crt-static`. | Full CI matrix plus a run without MSYS2 [passed](https://github.com/meop/fd/actions/runs/37182244324). | fd asks for an issue first, written by you. |
| ripgrep | `ci/windows-arm64-gnullvm` | `gnullvm` release lane; MSYS2 clang also compiles PCRE2. | Release build command plus a run without MSYS2 and a PCRE2 search [passed](https://github.com/meop/ripgrep/actions/runs/37182303411). | Open the PR; ripgrep's AI policy wants the body in your own words. |
| bottom | `ci/windows-arm64-gnullvm` | `gnullvm` release lane in `build_releases.yml`; flows through the existing Windows signing. | Release build command plus a run without MSYS2 [passed](https://github.com/meop/bottom/actions/runs/37182408585). | bottom wants an issue first, written by you. |
| zoxide | `winget-wix-installer` | WiX MSI beside the portable ZIP, as Starship ships. | On x64 and real ARM64 Windows the MSI installs a real `zoxide.exe` of the right architecture, the machine PATH finds it, it runs over SSH, and uninstall is clean ([run](https://github.com/meop/zoxide/actions/runs/37183594306)). A winget-style symlink on the machine PATH also ran over SSH on the runner, so CI does not reproduce #1180; On glass the MSI installs, runs over SSH and uninstalls cleanly. #1180 is reproduced (2026-10-05, `windows-msi-test/repro-ssh.ps1`): a portable install made from a normal desktop session leaves a user-created link, and an administrator's elevated SSH session refuses to follow it (error 448, Windows redirection trust); the MSI install has no link and works. | PR (the maintainer asked for it in #1180); the reproduction script is reusable for the fzf, yazi and Atuin MSIs. Real-machine test steps are on fork branch `winget-wix-smoke` (`WINDOWS-MSI-TEST.md`, fork PR `meop/zoxide#1`). |
| Starship | `linux-arm64-gnu-smoke` | Native Linux ARM64 GNU release lane. | [Passed](https://github.com/meop/starship/actions/runs/33569201148) 2026-09-01. | Low value: ARM64 already ships a static musl build. |

## Handoffs and blocked work

| Project | Blocker | State |
| --- | --- | --- |
| Restic | VSS on Windows ARM64 ([#3596](https://github.com/restic/restic/issues/3596)) | Handed to the Windows ARM64 host: branch `windows-arm64-release` with `WINDOWS-ARM64-TODO.md`, fork PR `meop/restic#1`. The native build works except `--use-fs-snapshot`: `vss_windows.go` rejects arm64, and relaxing that crashes in `IsVolumeSupported`, likely because ARM64 passes the 16-byte `VSS_ID` by value in two registers (needs a split like the 386 case). A 2026-10-03 reporter on #3596 offered to test a patch on hardware. Releases are built locally, and `helpers/build-release-binaries` lists only `386` and `amd64` for Windows, so `arm64` must be added there too. |
| cabal, hadolint, ShellCheck | GHC cannot build native Windows ARM64 | Cross-compiling works: [ghc#24603](https://gitlab.haskell.org/ghc/ghc/-/work_items/24603) (opened 2024-03) closed with MR !13856, merged 2025-05, and cabal's side merged in [cabal#10705](https://github.com/haskell/cabal/pull/10705). A native compiler ([ghc#25974](https://gitlab.haskell.org/ghc/ghc/-/work_items/25974)) is claimed by gulin.serge but idle since 2025-05; it plans to test under Wine because GHC's CI has no Windows ARM64. Work resumed in 2026-01 (RTS linker [ghc#26760](https://gitlab.haskell.org/ghc/ghc/-/work_items/26760), split sections [ghc#26763](https://gitlab.haskell.org/ghc/ghc/-/work_items/26763), draft MR !15346 for tables-next-to-code) and stalled after mid-January; [ghc#27684](https://gitlab.haskell.org/ghc/ghc/-/work_items/27684) (C calling convention) opened 2026-08. Options: help finish the native compiler with real Windows ARM64 hardware, or build these projects with the existing cross compiler and validate on the ARM64 host. No forks or handoff branches yet. hadolint has an open Winget request ([#1217](https://github.com/hadolint/hadolint/issues/1217)). 2026-10-04: with local branch `wip/windows-aarch64-native` (GHC built from Linux, plus an AArch64 RTS linker for Template Haskell), native `cabal.exe`, `shellcheck.exe` and `hadolint.exe` build and run on resin (Windows 11 ARM64). Releases still need that GHC work upstream and released fixes in hsc2hs, network and Cabal 3.12 (or hadolint on Cabal >= 3.16); details in the branch's `windows-aarch64/TODO.md`. |
| OpenCode | Windows ARM64 `#pty` shell sessions ([#45875](https://github.com/anomalyco/opencode/issues/45875)) | The TUI works since the Bun 1.4.2 bump ([PR #47446](https://github.com/anomalyco/opencode/pull/47446)). `bun-pty` 0.4.11 ships an ARM64 DLL ([bun-pty#46](https://github.com/sursaone/bun-pty/pull/46)), but OpenCode still pins 0.4.8; nobody has proposed the bump. |

### Packaging work

Scope: the four shell-integrated tools (Atuin, fzf, Yazi, zoxide), whose
failure is noticed immediately because a shell init hook runs them. Not all
ghpm tools.

The problem: winget installs these as portable ZIPs, which put a symlink in
`%LOCALAPPDATA%\Microsoft\WinGet\Links`. The link is created by whoever runs
winget, normally a non-elevated terminal. An administrator's SSH session is
elevated (OpenSSH logs admins on with their full token), and Windows'
redirection trust stops an elevated process from following a link a less
privileged process created: "The path cannot be traversed because it contains
an untrusted mount point" (error 448). A standard user is unaffected (both
sides run at medium integrity); a local "Run as administrator" terminal is
affected the same way. Reproduced 2026-10-05 for zoxide with
`windows-msi-test/repro-ssh.ps1` on the zoxide fork, which needs the user
logged in at the console (it installs from a medium-integrity interactive
task) and works for any winget id and MSI.

winget manifests: zoxide, fzf and Yazi run winget-releaser on each release,
and each change widens its installers filter to include the MSI, so their
manifests update themselves. Scoop needs nothing: its shims are real `.exe`
files, not links, as are ghpm's.

The fix: an MSI per architecture alongside the ZIP, as Starship and
PowerShell ship, installing a real executable under Program Files with its
own machine PATH entry, so there is no link. The goal is parity across the
four: the same winget install methods (MSI by default, ZIP still available)
and scoop packages.

| Project | Branch | State |
| --- | --- | --- |
| Atuin | `winget-wix-installer` | MSI proven: redone on current main with cargo-dist 0.31.0 (`atuin-server` keeps its installers); fork smoke with the ARM64 commit builds and installs, runs over SSH and uninstalls on x64 and ARM64 ([run](https://github.com/meop/atuin/actions/runs/37311895415)); on glass the portable install fails over elevated SSH and the MSI works (2026-10-05). With the ARM64 change, `windows-11-arm` needs WiX 3.14.1 installed (cargo-dist `github-build-setup`); see the branch notes. Atuin has no winget automation: its winget-pkgs manifest is updated by a community member, so the MSI also needs adding there after the first release that ships it. |
| fzf | `winget-wix-installer` | MSI proven: fork smoke run builds both MSIs as release.yml does (WiX moved to a Windows job; it does not run on macOS) and installs, runs over SSH and uninstalls on x64 and ARM64 ([run](https://github.com/meop/fzf/actions/runs/37306258749)); on glass the portable install fails over elevated SSH and the MSI works (2026-10-05). PR next; fzf's template requires the description in your own words with real-world context. |
| Yazi | `winget-wix-installer` | MSI proven: `cargo xtask dist` now builds it (the WIP's separate step had failed silently every time); fork smoke installs `yazi` and `ya`, runs over SSH and uninstalls on x64 and ARM64 ([run](https://github.com/meop/yazi/actions/runs/37309773805)); on glass the portable install fails over elevated SSH and the MSI works (2026-10-05). Yazi's AI policy needs a design issue approved first and human-written issue, PR and commit text. |
| zoxide | `winget-wix-installer` | MSI proven in CI and on a real x64 machine, and #1180's SSH failure reproduced with the portable install. The maintainer asked for this PR ([#1180](https://github.com/ajeetdsouza/zoxide/issues/1180)). |

## Backlog

Gaps with no work started.

| Project | Gap |
| --- | --- |
| difftastic | Linux ARM64 musl, to match x64's static musl build. |
| taplo | The `taplo-full` variant dropped in 0.10.0 (see [release-matrix.md](release-matrix.md#project-notes)). |

## Pending registry entries

Projects with a platform gap. Move an entry into `repo.toml`, in alphabetical
order, once a release closes the gap.

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

[gdu]
uri = "github.com/dundee/gdu"
descr = "Fast disk usage analyzer with a console interface."

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

[hyperfine]
uri = "github.com/sharkdp/hyperfine"
descr = "Command-line benchmarking tool with statistical analysis."

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

[typos]
uri = "github.com/crate-ci/typos"
descr = "Source code spell checker."

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

Every canonical clone under `/vol/code` and every `meop` fork used for release
work.

| Project | Clone | Fork | Branches |
| --- | --- | --- | --- |
| Atuin | yes | yes | `dist/windows-arm64-native` (proven, awaiting your PR), `winget-wix-installer` |
| bottom | yes | yes | `ci/windows-arm64-gnullvm` (awaiting your issue) |
| Charm meta | yes | yes | none (for the Gum/VHS change) |
| Delta | yes | yes | `ci/windows-arm64-release-pr` (PR #2267), `ci/linux-arm64-musl-release-pr` (PR #2268) |
| dust | yes | yes | `ci/windows-arm64-gnullvm` (PR #632) |
| fd | yes | yes | `ci/windows-arm64-gnullvm` (awaiting your issue) |
| fzf | yes | yes | `winget-wix-installer` |
| GHC | yes (from gitlab.haskell.org) | no; your gitlab.haskell.org account needs verification first (steps in the branch's `windows-aarch64/TODO.md`) | `wip/windows-aarch64-native` (local; native Windows ARM64 GHC) |
| ghc-windows-aarch64 | yes | own repo | Public test repo for the GHC branch's Windows AArch64 builds: releases hold the bindist, `test-ghc.yml` checks it on `windows-11-arm` |
| Gum, VHS | yes | yes | `windows-arm64-release` (fork smoke for the meta change) |
| hexyl | yes | yes | `ci/linux-arm64-musl-release-pr` (PR #292); PR #291's branch on the fork only |
| lsd | yes | yes | `ci/windows-arm64-gnullvm` (PR #1244); PR #1237's branch on the fork only |
| OpenCode | yes | no | none |
| ouch | yes | yes | `windows-arm64-gnullvm` (awaiting issue #1094) |
| pastel | yes | yes | `ci/linux-arm64-musl-release-pr` (PR #322); PR #320's branch `ci/platform-release-matrix` on the fork |
| QSV | yes | yes | `ci/linux-arm64-musl-release` and `ci/windows-arm64-gnullvm` (both merged; delete after the release), `windows-arm64-gnullvm-smoke` (fork-only) |
| Restic | yes | yes | `windows-arm64-release` (handoff; fork PR `meop/restic#1`) |
| ripgrep | yes | yes | `ci/windows-arm64-gnullvm` (awaiting your PR) |
| SD | yes | yes | `ci/windows-arm64-release-pr` (PR #354) |
| Starship | yes | yes | `linux-arm64-gnu-smoke` |
| Typos | no | yes | PR #1602's branch on the fork only |
| Vivid | yes | yes | `ci/windows-arm64-gnullvm` (PR #245) |
| xan | yes | yes | `ci/arm64-release-targets` (PR #1186) |
| Yazi | yes | yes | `winget-wix-installer` |
| zoxide | yes | yes | `winget-wix-installer`, `winget-wix-smoke` (fork-only; real-machine test notes, fork PR `meop/zoxide#1`) |
