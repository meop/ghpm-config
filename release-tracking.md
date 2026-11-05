# Release tracking

Ongoing work to close release gaps, as of 2026-10-04 (packaging work and upstream submissions updated 2026-11-05). The rules, including
the Starship and zellij registry exceptions, are in
[release-policy.md](release-policy.md); each project's current release
variants are in [release-matrix.md](release-matrix.md).

## Open upstream submissions

| Project | Change | Upstream | State | Proof |
| --- | --- | --- | --- | --- |
| Atuin | Windows ARM64 (MSVC), native `windows-11-arm` runner | [PR #4575](https://github.com/atuinsh/atuin/pull/4575), covers [#3056](https://github.com/atuinsh/atuin/issues/3056) | Opened 2026-10-27, no maintainer review. #3056 was closed as not planned after the default cross-compile failed: cargo-xwin passes clang-cl `/imsvc` flags to `ring`'s `clang` build ([run](https://github.com/meop/atuin/actions/runs/33228562158)). Rebased 2026-11-03 onto #4527: main's `msi` installer now applies to this target too, so `.github/build-setup.yml` installs WiX 3.14.1 on `windows-11-arm`. Also adds an `atuin-server` ARM64 zip. Still no maintainer review on 2026-11-05; v18.24.5 (2026-11-04) shipped without ARM64. | On `windows-11-arm` with the release job's setup and `dist build`, the zip and MSI build, and the MSI installs per-user and per-machine, passes `atuin --version` with only System32 on `PATH`, and uninstalls ([run](https://github.com/meop/atuin/actions/runs/41611295544)). |
| Delta | Windows ARM64 (MSVC) | [#2223](https://github.com/dandavison/delta/issues/2223), [PR #2267](https://github.com/dandavison/delta/pull/2267) | PR opened 2026-10-04 after a month without a reply on the issue. | Native build packaged by `before_deploy.sh` on current `main` ([run](https://github.com/meop/delta/actions/runs/37178086572)). |
| Delta | Linux ARM64 musl | [#2227](https://github.com/dandavison/delta/issues/2227), [PR #2268](https://github.com/dandavison/delta/pull/2268) | PR opened 2026-10-04. Third-party [PR #2236](https://github.com/dandavison/delta/pull/2236) (2026-09-13) makes the same change, but without `musl-tools` and with an unrelated README badge. | Static, stripped binary and `.deb` from the same [run](https://github.com/meop/delta/actions/runs/37178086572). |
| fzf | WiX/MSI installer for winget | Issue [#4943](https://github.com/junegunn/fzf/issues/4943), [PR #4948](https://github.com/junegunn/fzf/pull/4948) (the maintainer's, on our commit) | Issue opened 2026-10-23, since fzf limits PRs to collaborators. The maintainer opened #4948 on 2026-10-29 with release-flow fixes on top of our commit, and is still pushing to it (2026-11-02). They asked for the MSI from [this run](https://github.com/junegunn/fzf/actions/runs/40875423649) to be tested over admin SSH; [results posted](https://github.com/junegunn/fzf/issues/4943#issuecomment-6598828678) 2026-11-03. They then asked for a review of #4948; posted the same day with no blockers and four small suggestions. 2026-11-04/05: they applied all four, made the `msi` job fail if the release is already published (so a re-run can't replace MSIs or resubmit to winget), documented the draft flow in `RELEASE.md`, removed `make release`, and asked for another review; approved 2026-11-05. Waiting for the merge. | [Smoke](https://github.com/meop/fzf/actions/runs/39567886465) on x64 and ARM64. The PR's release flow from real tags on the fork: [v0.99.11](https://github.com/meop/fzf/actions/runs/41690922173), [v0.99.12](https://github.com/meop/fzf/actions/runs/41691463845), [v0.99.13-rc1](https://github.com/meop/fzf/actions/runs/41692334350). |
| Ghostty | Config docs: load order of `config` and `config.ghostty`, and when `config-file` includes load | Discussion [#14828](https://github.com/ghostty-org/ghostty/discussions/14828), [website PR #500](https://github.com/ghostty-org/website/pull/500) | Discussion opened 2026-10-24, labeled `needs-confirmation`, and no maintainer has answered. PR #500 opened 2026-11-03. A code PR needs a Vouch Request written by hand, and only if a maintainer wants a code change. 2026-11-04: a non-maintainer answered our CLI flag question: `Config.load` loads every include after CLI flags, so an include wins, and changing that would need its own issue. 2026-11-05: PR #500's note now says includes load after CLI flags too. No maintainer review yet. | Lint and build pass ([run](https://github.com/meop/website/actions/runs/41685747714)). |
| hexyl | Windows ARM64 (MSVC) | [PR #291](https://github.com/sharkdp/hexyl/pull/291) | Open since 2026-08-16; green CI, no review. | Fork release matrix. |
| hexyl | Linux ARM64 musl | [PR #292](https://github.com/sharkdp/hexyl/pull/292) | Open since 2026-08-31; green CI, no review. | Static artifact proven. |
| Komac | `update` drops what analysis can't detect (blocks Yazi's winget submissions) | [#1841](https://github.com/russellbanks/Komac/issues/1841), [PR #1934](https://github.com/russellbanks/Komac/pull/1934), [PR #1935](https://github.com/russellbanks/Komac/pull/1935) | 2026-10-23: commented on #1841 with a repro and a status of its six items; #1934 restores nested installer files for multi-exe ZIPs (Yazi), #1935 (stacked on it) proposes matching previous installers in general. No CI yet (first-time contributor). | Test results as comments on [#1934](https://github.com/russellbanks/Komac/pull/1934#issuecomment-6371549943) and [#1935](https://github.com/russellbanks/Komac/pull/1935#issuecomment-6371546081). |
| lsd | Windows ARM64 `gnullvm` | [PR #1244](https://github.com/lsd-rs/lsd/pull/1244) | Opened 2026-10-04. The existing `i686-pc-windows-gnu` job fails to install its toolchain on `windows-latest`, independent of this change; noted in the description. | `+crt-static` was the only option of three that started without MSYS2 ([experiment](https://github.com/meop/lsd/actions/runs/37169967049)); full [release matrix](https://github.com/meop/lsd/actions/runs/37170362416). |
| lsd | Enforce the committed lockfile in CI | [PR #1237](https://github.com/lsd-rs/lsd/pull/1237) | Open since 2026-08-16. | — |
| ouch | Windows ARM64 `gnullvm` | Proposal issue [#1094](https://github.com/ouch-org/ouch/issues/1094) | Opened 2026-10-04; branch `windows-arm64-gnullvm` is ready for a PR if they agree. MSYS2 clang compiles the C and C++ codecs; bzip3's bindgen gets MSYS2's libclang plus `--target=aarch64-w64-mingw32`, since clang rejects the `gnullvm` suffix. | Build, 117 tests, and a run without MSYS2 [passed](https://github.com/meop/ouch/actions/runs/37183581297). |
| pastel | Windows ARM64 (MSVC and `gnullvm`) | [PR #320](https://github.com/sharkdp/pastel/pull/320) | Open since 2026-08-16, no review; `gnullvm` added 2026-10-04. | Full [release matrix](https://github.com/meop/pastel/actions/runs/37170366243), including a run without MSYS2. |
| pastel | Linux ARM64 musl | [PR #322](https://github.com/sharkdp/pastel/pull/322) | Open since 2026-08-31; green CI, no review. | Static artifact proven. |
| ripgrep | Windows ARM64 `gnullvm` (release and CI) | [PR #3579](https://github.com/BurntSushi/ripgrep/pull/3579) | Opened 2026-10-28. Adds a CI lane too, as `bb0cbae` did for ARM64 MSVC, since the maintainer drops release targets whose CI breaks (`79d393a`). | Fork CI including the new lane [passed](https://github.com/meop/ripgrep/actions/runs/40630540721); release build, a run without MSYS2 and a PCRE2 search [passed](https://github.com/meop/ripgrep/actions/runs/40630540435). |
| SD | Windows ARM64 (MSVC and `gnullvm`) | [#329](https://github.com/chmln/sd/issues/329) (closed), [PR #354](https://github.com/chmln/sd/pull/354) | Open since 2026-09-01, no review, upstream CI not run. Static-libunwind fix pushed 2026-10-04. | `gnullvm` binary runs without MSYS2 ([run](https://github.com/meop/sd/actions/runs/37170389227)); [test workflow](https://github.com/meop/sd/actions/runs/37170388821) passes. |
| Vivid | Windows ARM64 `gnullvm` | [PR #245](https://github.com/sharkdp/vivid/pull/245) | Opened 2026-10-04. | Full [release matrix](https://github.com/meop/vivid/actions/runs/37170364801), including a run without MSYS2. |
| zellij | Windows ARM64 | [PR #5090](https://github.com/zellij-org/zellij/pull/5090) | Third-party PR open since 2026-04 with no review. | — |
| zoxide | WiX/MSI installer for winget | [#1180](https://github.com/ajeetdsouza/zoxide/issues/1180), [PR #1345](https://github.com/ajeetdsouza/zoxide/pull/1345) | The maintainer asked for an MSI PR on 2026-05-10; PR opened 2026-10-22, CI green, no review yet. | [Smoke](https://github.com/meop/zoxide/actions/runs/39567897889) on x64 and ARM64. |
| Gum, VHS | Windows ARM64 | Gum [#1139](https://github.com/charmbracelet/gum/discussions/1139), VHS [#780](https://github.com/charmbracelet/vhs/discussions/780) | Idea discussions, no response. Needs the [meta#305](https://github.com/charmbracelet/meta/pull/305) change in `goreleaser-full.yaml` (Gum) and `goreleaser-vhs.yaml` (VHS). | Fork smokes on `windows-arm64-release`. |

## Merged, awaiting a release

| Project | Change | Merged | Latest release |
| --- | --- | --- | --- |
| bottom | Windows ARM64 `gnullvm` starts without MSYS2: `+crt-static` in `.cargo/config.toml` ([PR #2302](https://github.com/ClementTsang/bottom/pull/2302)). 0.15.0's zip and MSI import `libunwind.dll` and exit `0xC0000135` without MSYS2 ([run](https://github.com/meop/bottom/actions/runs/41610843630)). The maintainer split our `AllowSameVersionUpgrades` WiX change into their own [PR #2304](https://github.com/ClementTsang/bottom/pull/2304), credited to us, and in it unpinned MSYS2's clang package. The 2026-11-04 nightly's gnullvm `btm.exe` imports only Windows system DLLs. | 2026-11-04 | 0.15.0 (2026-11-01) |
| Glow | Windows ARM64 ([meta#305](https://github.com/charmbracelet/meta/pull/305), by a maintainer) | 2026-09-30 | v3.0.0 (2026-08-11) |
| helix | Windows ARM64 ([PR #15557](https://github.com/helix-editor/helix/pull/15557), not ours) | 2026-05-25 | 25.07.1 (2025-07-18) |
| lsd | Windows ARM64 MSVC ([PR #1236](https://github.com/lsd-rs/lsd/pull/1236)) | 2026-08-16 | v1.2.0 (2025-10-12) |
| mdBook | Windows ARM64 ([PR #3193](https://github.com/rust-lang/mdBook/pull/3193)), Linux ARM64 GNU ([PR #3207](https://github.com/rust-lang/mdBook/pull/3207)) | 2026-08-17, 2026-09-02 | v0.5.4 (2026-07-06) |
| Procs | Windows ARM64 ([PR #961](https://github.com/dalance/procs/pull/961)) | 2026-09-07 | v0.14.12 (2026-06-25) |
| SD | Linux ARM64 GNU (already in the release workflow) | — | v1.1.0 (2026-02-25) |
| Vivid | Windows ARM64 MSVC ([PR #228](https://github.com/sharkdp/vivid/pull/228)), Linux ARM64 musl ([PR #233](https://github.com/sharkdp/vivid/pull/233)) | 2026-08-17, 2026-08-31 | v0.11.1 (2026-04-09) |
| xan | Windows ARM64 MSVC and Linux ARM64 musl ([PR #1186](https://github.com/medialab/xan/pull/1186)); the maintainer moved the musl build to `ubuntu-latest` with cross, which the fork proof used but the PR missed | 2026-10-06 | 0.61.0 (2026-09-11); pre-release [0.62.0-rc.2](https://github.com/medialab/xan/releases/tag/0.62.0-rc.2) ships both targets, tested on ARM64 Windows and Linux |
| Yazi | WiX/MSI installers for stable and nightly ([PR #4473](https://github.com/sxyazi/yazi/pull/4473), the maintainer's, not ours; see [packaging work](#packaging-work)), and the MSIs in the winget `installers-regex` ([`bdd3dbd`](https://github.com/sxyazi/yazi/commit/bdd3dbdd86943d4249ea40c3a7560ec9e708cd04), from our comment on #4440) | 2026-11-02, 2026-11-04 | v26.9.1 (2026-09-01); the `nightly` release ships both MSIs |

When a release ships, check [release-matrix.md](release-matrix.md), and move
the project's pending entry into `repo.toml` if its platform gap is closed.

## Proven in a fork, not submitted

Windows ARM64 `gnullvm` builds are established elsewhere (about 210 GitHub
workflows build `aarch64-pc-windows-gnullvm`, including git, HandBrake,
Microsoft's windows-rs, and R packages, since R on Windows ARM64 uses an LLVM
MinGW toolchain), and btm, dust, fd and qsv now ship one. `windows-11-arm` has
MSYS2 at `C:\msys64`, though its image list says it is omitted: bottom's
[PR #2290](https://github.com/ClementTsang/bottom/pull/2290) installs clang
with that `pacman`
([run](https://github.com/ClementTsang/bottom/actions/runs/40924718297)). Its
maintainer objected to a new `setup-msys2` dependency, and fd's asked the same,
so offer `pacman` first.

| Project | Branch | Change | Proof | Next step |
| --- | --- | --- | --- | --- |
| zoxide | `winget-wix-installer` | WiX MSI beside the portable ZIP, as Starship ships. | On x64 and real ARM64 Windows the MSI installs a real `zoxide.exe` of the right architecture, the machine PATH finds it, it runs over SSH, and uninstall is clean ([run](https://github.com/meop/zoxide/actions/runs/37183594306)). A winget-style symlink on the machine PATH also ran over SSH on the runner, so CI does not reproduce #1180; On glass the MSI installs, runs over SSH and uninstalls cleanly. #1180 is reproduced (2026-10-05, `windows-msi-test/repro-ssh.ps1`): a portable install made from a normal desktop session leaves a user-created link, and an administrator's elevated SSH session refuses to follow it (error 448, Windows redirection trust); the MSI install has no link and works. | PR (the maintainer asked for it in #1180); the reproduction script is reusable for the fzf, yazi and Atuin MSIs. Real-machine test steps are on fork branch `winget-wix-smoke` (`WINDOWS-MSI-TEST.md`, fork PR `meop/zoxide#1`). |
| Starship | `linux-arm64-gnu-smoke` | Native Linux ARM64 GNU release lane. | [Passed](https://github.com/meop/starship/actions/runs/33569201148) 2026-09-01. | Low value: ARM64 already ships a static musl build. |

## Handoffs and blocked work

| Project | Blocker | State |
| --- | --- | --- |
| Restic | VSS on Windows ARM64 ([#3596](https://github.com/restic/restic/issues/3596)) | Handed to the Windows ARM64 host: branch `windows-arm64-release` with `WINDOWS-ARM64-TODO.md`, fork PR `meop/restic#1`. The native build works except `--use-fs-snapshot`: `vss_windows.go` rejects arm64, and relaxing that crashes in `IsVolumeSupported`, likely because ARM64 passes the 16-byte `VSS_ID` by value in two registers (needs a split like the 386 case). A 2026-10-03 reporter on #3596 offered to test a patch on hardware. Releases are built locally, and `helpers/build-release-binaries` lists only `386` and `amd64` for Windows, so `arm64` must be added there too. |
| cabal, hadolint, ShellCheck | GHC cannot build native Windows ARM64 | Cross-compiling works: [ghc#24603](https://gitlab.haskell.org/ghc/ghc/-/work_items/24603) (opened 2024-03) closed with MR !13856, merged 2025-05, and cabal's side merged in [cabal#10705](https://github.com/haskell/cabal/pull/10705). A native compiler ([ghc#25974](https://gitlab.haskell.org/ghc/ghc/-/work_items/25974)) is claimed by gulin.serge but idle since 2025-05; it plans to test under Wine because GHC's CI has no Windows ARM64. Work resumed in 2026-01 (RTS linker [ghc#26760](https://gitlab.haskell.org/ghc/ghc/-/work_items/26760), split sections [ghc#26763](https://gitlab.haskell.org/ghc/ghc/-/work_items/26763), draft MR !15346 for tables-next-to-code) and stalled after mid-January; [ghc#27684](https://gitlab.haskell.org/ghc/ghc/-/work_items/27684) (C calling convention) opened 2026-08. Options: help finish the native compiler with real Windows ARM64 hardware, or build these projects with the existing cross compiler and validate on the ARM64 host. No forks or handoff branches yet. hadolint has an open Winget request ([#1217](https://github.com/hadolint/hadolint/issues/1217)). 2026-10-04: with local branch `wip/windows-aarch64-native` (GHC built from Linux, plus an AArch64 RTS linker for Template Haskell), native `cabal.exe`, `shellcheck.exe` and `hadolint.exe` build and run on resin (Windows 11 ARM64). Releases still need that GHC work upstream and released fixes in hsc2hs, network and Cabal 3.12 (or hadolint on Cabal >= 3.16); details in the branch's `windows-aarch64/TODO.md`. |
| OpenCode | Windows ARM64 `#pty` shell sessions ([#45875](https://github.com/anomalyco/opencode/issues/45875)) | The TUI works since the Bun 1.4.2 bump ([PR #47446](https://github.com/anomalyco/opencode/pull/47446)). `bun-pty` 0.4.11 ships an ARM64 DLL ([bun-pty#46](https://github.com/sursaone/bun-pty/pull/46)); [PR #54689](https://github.com/anomalyco/opencode/pull/54689) bumped it on `dev` and closed #45875 on 2026-10-12. `dev` is the 2.x line (tags `v2.0.x`/`v2.1.x`, no GitHub releases or npm versions yet), and a user confirmed it works in 2.0.29 on #4340. Stable 1.x releases are cut from the `v1` branch, and the latest, v1.19.5 (2026-10-28), still pins 0.4.8. 2.x GitHub releases exist since 2026-10-29 (v2.2.5, 2026-10-30, ships `opencode-windows-arm64.zip` and pins 0.4.11), but GitHub's latest release is still v1.19.5. Waiting for 2.x to become the latest release. |

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

winget manifests: zoxide, fzf and Yazi run winget-releaser on each release.
The zoxide and fzf changes widen its installers filter to include the MSI, so
their manifests update themselves; Yazi's maintainer made the same change on
2026-11-04 (see the table below). Tested 2026-10-22 in the public test repo
`meop/winget-manifest-test` (Komac `update --dry-run` on the test assets, then
winget on `windows-latest` and `windows-11-arm`; all green in
[run](https://github.com/meop/winget-manifest-test/actions/runs/39874259707)
and, for Yazi, [run](https://github.com/meop/winget-manifest-test/actions/runs/39875214984)):
the manifest gets a `wix` installer (machine scope, ProductCode, UpgradeCode)
beside the ZIP per architecture, as Starship's does; a fresh `winget install`
picks the MSI, and `--installer-type portable` gets the ZIP. An existing
portable install stays portable on `winget upgrade`, so those users need to
uninstall and reinstall once. Komac 2.17 drops `NestedInstallerFiles` for ZIPs
with more than one exe, so Yazi's next submission fails validation, MSI or not;
winget-releaser@main always installs the latest Komac. Fixes are in Komac PR
#1934 and #1935 (see above). Scoop needs nothing: its shims are real `.exe`
files, not links, as are ghpm's.

The fix: an MSI per architecture alongside the ZIP, as Starship and
PowerShell ship, installing a real executable under Program Files with its
own machine PATH entry, so there is no link. The goal is parity across the
four: the same winget install methods (MSI by default, ZIP still available)
and scoop packages.

| Project | Branch | State |
| --- | --- | --- |
| Atuin | `winget-msi` (PR #4527, merged) | MSI proven: redone on current main with cargo-dist 0.31.0 (`atuin-server` keeps its installers); fork smoke with the ARM64 commit builds and installs, runs over SSH and uninstalls on x64 and ARM64 ([run](https://github.com/meop/atuin/actions/runs/37311895415)); on glass the portable install fails over elevated SSH and the MSI works (2026-10-05). With the ARM64 change, `windows-11-arm` needs WiX 3.14.1 installed (cargo-dist `github-build-setup`); see the branch notes. Atuin has no winget automation: its winget-pkgs manifest is updated by a community member, so the MSI also needs adding there after the first release that ships it. 2026-10-21: rebased onto upstream; smoke re-run [passed](https://github.com/meop/atuin/actions/runs/39567882355) on x64 and ARM64. 2026-10-23: PR #4527 opened; the MSI now installs `LICENSE` ([run](https://github.com/meop/atuin/actions/runs/40029066758)). 2026-10-28: landed as `19b66e7` after the maintainer pushed changes to our branch: a per-user install by default with a machine option, a generated license page, an icon, and a hand-maintained `main.wxs`. Shipped in v18.24.3, x64 only. Next: winget-pkgs moved to 18.24.5 but still lists only the portable ZIP, and the manifest test above assumed machine scope, so re-test against the per-user default before adding the MSI there. 2026-11-03: the v18.24.4 x64 MSI installs per-user from a non-elevated task, `atuin --version` passes in a new admin SSH session, and uninstall is clean. |
| fzf | `winget-msi` (issue #4943, base of PR #4948) | MSI proven: fork smoke run builds both MSIs as release.yml does (WiX moved to a Windows job; it does not run on macOS) and installs, runs over SSH and uninstalls on x64 and ARM64 ([run](https://github.com/meop/fzf/actions/runs/37306258749)); on glass the portable install fails over elevated SSH and the MSI works (2026-10-05). 2026-10-21: rebased onto upstream; smoke re-run [passed](https://github.com/meop/fzf/actions/runs/39567886465) on x64 and ARM64. 2026-10-23: fzf limits PRs to collaborators, so issue #4943 offers the branch. 2026-10-29: the maintainer opened PR #4948 keeping our commit, and added: goreleaser creates a draft that is published after the MSIs upload (otherwise `winget.yml` could read the release before they exist), MSI hashes in the checksum file, no MSI for `-rc` versions, and `GITHUB_TOKEN` in place of the protected environment. 2026-11-02: a read-only winget token and `replace_existing_draft`. 2026-11-03: tested their x64 MSI on glass from a non-elevated task, where UAC auto-approves: it elevates, a real `fzf.exe` under `Program Files\fzf\bin` passes `--version` from the machine PATH in a new admin SSH session, and uninstall removes the files and the PATH entry. Results posted on #4943. Later that day, ran the PR's flow from real tags on the fork, with goreleaser on Ubuntu, no notarization, `GITHUB_TOKEN` and a stub in place of winget-releaser: the draft publishes and becomes latest, MSI checksums match and survive a re-run, an `-rc` tag gets no MSIs and skips winget, and on x64 and ARM64 an upgrade leaves one entry and one PATH entry and uninstall restores PATH. Not covered: macOS builds and notarization, `RELEASE_PAT`, a real winget submission, retrying over an existing draft, and UAC on ARM64. Review posted on #4948. 2026-11-05: the maintainer applied the suggestions and added more release-flow hardening; approved. |
| Yazi | `winget-msi` (issue #4440, superseded by PR #4473) | MSI proven: `cargo xtask dist` now builds it (the WIP's separate step had failed silently every time); fork smoke installs `yazi` and `ya`, runs over SSH and uninstalls on x64 and ARM64 ([run](https://github.com/meop/yazi/actions/runs/37309773805)); on glass the portable install fails over elevated SSH and the MSI works (2026-10-05). Yazi's AI policy needs a design issue approved first and human-written issue, PR and commit text. 2026-10-21: rebased onto upstream; smoke re-run [passed](https://github.com/meop/yazi/actions/runs/39567889770) on x64 and ARM64. 2026-10-23: design issue #4440 opened. 2026-11-02: the maintainer landed their own [PR #4473](https://github.com/sxyazi/yazi/pull/4473) and closed the issue: a separate `build-msi` job repackages the release ZIP with a short `assets/msi.wxs` (machine scope and machine PATH, as ours), where ours built inside `cargo xtask dist`. It leaves `installers-regex` in `publish.yml` at `.zip` only, so the MSIs will not reach winget. 2026-11-03: the `nightly` x64 MSI installs from a non-elevated task, `yazi` and `ya` pass `--version` in a new admin SSH session, and uninstall is clean. Proposed that one-line change the same day. 2026-11-04: the maintainer applied it in `bdd3dbd` and declined pinning WiX's version. The same commit's `AGENTS.md` tells AI agents not to create issues, PRs or comments, and to mark any they're asked to make so they get closed, so write anything for Yazi by hand. Not released yet, and the Komac fix still blocks submissions. |
| zoxide | `winget-msi` (PR #1345) | MSI proven in CI and on a real x64 machine, and #1180's SSH failure reproduced with the portable install. The maintainer asked for this PR ([#1180](https://github.com/ajeetdsouza/zoxide/issues/1180)). 2026-10-21: rebased onto upstream; smoke re-run [passed](https://github.com/meop/zoxide/actions/runs/39567897889) on x64 and ARM64. 2026-10-22: PR #1345 opened. After it ships, check the winget-pkgs PR matches the tested manifest. |

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

Every canonical clone under `/vol/code` and every `meop` fork used for release
work.

| Project | Clone | Fork | Branches |
| --- | --- | --- | --- |
| Atuin | yes | yes | `dist/windows-arm64-native` (PR #4575), `dist/windows-arm64-native-smoke`, `dist/windows-arm64-msi-smoke` (both fork-only) |
| bottom | yes | yes | `ci/windows-gnullvm-crt-static` (PR #2302, merged), `windows-arm64-crt-static-smoke` (fork-only); both can go |
| Charm meta | yes | yes | none (for the Gum/VHS change) |
| Delta | yes | yes | `ci/windows-arm64-release-pr` (PR #2267), `ci/linux-arm64-musl-release-pr` (PR #2268) |
| fzf | yes | yes | `winget-msi` (issue #4943, base of PR #4948), `winget-wix-installer`, `winget-wix-smoke` (fork-only) |
| GHC | yes (from gitlab.haskell.org) | no; your gitlab.haskell.org account needs verification first (steps in the branch's `windows-aarch64/TODO.md`) | `wip/windows-aarch64-native` (local; native Windows ARM64 GHC) |
| ghc-windows-aarch64 | yes | own repo | Public test repo for the GHC branch's Windows AArch64 builds: releases hold the bindist, `test-ghc.yml` checks it on `windows-11-arm` |
| Ghostty website | yes | yes | `docs/config-load-order` (website PR #500) |
| Gum, VHS | yes | yes | `windows-arm64-release` (fork smoke for the meta change) |
| hexyl | yes | yes | `ci/linux-arm64-musl-release-pr` (PR #292); PR #291's branch on the fork only |
| Komac | yes | yes | `fix-update-nested-files` (PR #1934), `merge-previous-installers` (PR #1935) |
| lsd | yes | yes | `ci/windows-arm64-gnullvm` (PR #1244); PR #1237's branch on the fork only |
| mise | yes | yes | none |
| OpenCode | yes | no | none |
| ouch | yes | yes | `windows-arm64-gnullvm` (awaiting issue #1094) |
| pastel | yes | yes | `ci/linux-arm64-musl-release-pr` (PR #322); PR #320's branch `ci/platform-release-matrix` on the fork |
| Restic | yes | yes | `windows-arm64-release` (handoff; fork PR `meop/restic#1`) |
| ripgrep | yes | yes | `ci/windows-arm64-gnullvm` (PR #3579), `windows-arm64-gnullvm-smoke` (fork-only) |
| SD | yes | yes | `ci/windows-arm64-release-pr` (PR #354) |
| Starship | yes | yes | `linux-arm64-gnu-smoke` |
| Vivid | yes | yes | `ci/windows-arm64-gnullvm` (PR #245) |
| winget-manifest-test | yes | own repo | Public test repo for winget manifests: release `test-assets` holds the test ZIPs and MSIs, which Komac PR #1935's results link to |
| Yazi | yes | yes | none |
| zoxide | yes | yes | `winget-msi` (PR #1345), `winget-wix-installer`, `winget-wix-smoke` (fork-only; real-machine test notes, fork PR `meop/zoxide#1`) |
