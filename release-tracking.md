# Release target inventory

`repo.toml` is intentionally only the ghpm package registry. This document is
the source of truth for release-target coverage, ABI/linkage details, local
fork work, and upstream discussions.

## Target terminology

| Term | Meaning |
| --- | --- |
| Windows MSVC | A Rust `*-pc-windows-msvc` target, or native MSVC toolchain. |
| Windows GNU family | A Rust `*-pc-windows-gnu` target using the MinGW-w64 ABI, or ARM64's `aarch64-pc-windows-gnullvm` LLVM/MinGW counterpart. |
| Windows MinGW-Clang | Clang built in MSYS2 for the MinGW-w64 ABI; not MSVC. |
| Windows Go | A Go `GOOS=windows` binary; neither MSVC nor MinGW. |
| Linux musl static | No dynamic musl loader is required at runtime. |

Do not infer an ABI from an `.exe` filename. Record a release target, build
workflow, or inspected binary. A project can intentionally publish both GNU
and MSVC x64 assets while publishing only MSVC for Windows ARM64.

## Windows ABI inventory

These are current upstream release facts, not target requests. `Yes` in the
ARM64 column means a released Windows ARM64 asset exists today.

| Project | Windows x64 assets | Windows ARM64 asset | Notes |
| --- | --- | --- | --- |
| bottom | GNU and MSVC | MSVC | Both x64 ABIs coexist. |
| dust | GNU and MSVC | MSVC | Both x64 ABIs coexist. |
| fd | GNU and MSVC | MSVC | Both x64 ABIs coexist. |
| fastfetch | MinGW-Clang | MinGW-Clang | MSYS2 `CLANG64` and `CLANGARM64`; DLLs are bundled. |
| lsd | GNU and MSVC | No | Windows ARM64 remains a gap. |
| Neovim | MSVC | MSVC | Native Visual Studio toolchain for both architectures. |
| ouch | GNU and MSVC | MSVC | Both x64 ABIs coexist. |
| pastel | GNU and MSVC | No | Windows ARM64 remains a gap. |
| qsv | GNU and MSVC | MSVC | The GNU asset is x64-only. |
| ripgrep | GNU and MSVC | MSVC | Both x64 ABIs coexist. |
| sd | GNU and MSVC | Not yet released | PR #354 runs ARM64 MSVC and GNU-family jobs natively; neither ARM64 artifact has been released yet. |
| vivid | GNU and MSVC | No | Windows ARM64 remains a gap. |

### Windows GNU-family parity audit

Rust does not provide `aarch64-pc-windows-gnu`; its ARM64 GNU-family target is
`aarch64-pc-windows-gnullvm`. These rows distinguish an architecture gap from
the narrower GNU-family ABI gap. They are based on current release assets.

| Project | Existing Windows x64 GNU asset | ARM64 status | GNU-family parity disposition |
| --- | --- | --- | --- |
| bottom, dust, fd, ouch, qsv, ripgrep | Yes | MSVC asset exists | Functional ARM64 coverage exists; `gnullvm` is the remaining ABI-parity addition. |
| fastfetch | MinGW-Clang | MinGW-Clang | Complete within its chosen MinGW-Clang family. |
| lsd, pastel, vivid | Yes | No ARM64 asset | Architecture coverage is the first gap; decide whether a future addition should ship MSVC, `gnullvm`, or both. |
| sd | Yes | No released ARM64 asset | PR #354 adds native ARM64 MSVC and `gnullvm` release lanes; both are proven in fork CI. |

### Windows ARM64 campaign changes

This table answers a different question: what each branch or submitted change
does. It must not be read as a list of all Windows releases.

| Project | x64 ABI before change | ARM64 ABI under test/change | What changed | State |
| --- | --- | --- | --- | --- |
| Atuin | MSVC | MSVC | Native build and cargo-dist package proof. | Proof passed; issue #3056 is closed after a maintainer recalled an earlier unspecified failure. |
| Delta | MSVC | MSVC | Native release packaging and smoke coverage. | Issues [#2223](https://github.com/dandavison/delta/issues/2223) and [#2227](https://github.com/dandavison/delta/issues/2227); issue-first. |
| GDU | Go | Go | Add Windows ARM64 to the Go release matrix. | [PR #647](https://github.com/dundee/gdu/pull/647) open. |
| Glow, Gum, VHS | Go | Go | Shared Charm release configuration would need an ARM64 row. | Idea discussions open; no active worktree required. |
| Procs | MSVC | MSVC | Add native ARM regression build and ARM64 ZIP. | [PR #961](https://github.com/dalance/procs/pull/961) open. |
| SD | GNU and MSVC | MSVC and GNU family (`gnullvm`) | Run both ARM64 Windows release lanes on `windows-11-arm`, package ZIPs by target triple, and provision the GNU-family linker. | [PR #354](https://github.com/chmln/sd/pull/354) open; both fork smokes passed. |
| Typos | MSVC | MSVC | Add native ARM CI and a Windows ARM64 release ZIP. | [PR #1602](https://github.com/crate-ci/typos/pull/1602) open. |
| Restic | Go | Go | Native build passed; VSS must be compared with x64. | Upstream [#3596](https://github.com/restic/restic/issues/3596); TODO committed to fork branch. |

### ABI baseline audit

Before adding an ARM64 asset, compare it with the released x64 asset for the
same operating system. Do not substitute MSVC, GNU, or musl merely because it
is easier to build.

| Change set | Existing x64 baseline | Proposed ARM64 variant | Audit result |
| --- | --- | --- | --- |
| GDU [PR #647](https://github.com/dundee/gdu/pull/647) | Go | Go | Same toolchain family. |
| SD [PR #354](https://github.com/chmln/sd/pull/354) | GNU and MSVC | MSVC and GNU family (`gnullvm`) | Valid: preserves both released x64 ABI families; native fork smokes built and packaged each ARM64 variant. |
| Procs [PR #961](https://github.com/dalance/procs/pull/961) | MSVC | MSVC | Same ABI family. |
| Typos [PR #1602](https://github.com/crate-ci/typos/pull/1602) | MSVC | MSVC | Same ABI family. |
| Delta branch | MSVC | MSVC | Same ABI family; issue-first upstream. |
| Atuin branch | MSVC | MSVC | Same ABI family; no upstream PR. |
| Hexyl, Hyperfine, Pastel, Vivid Linux PRs | Linux x64 musl | Linux ARM64 musl | Same libc family; each x64 musl asset exists today. |
| mdBook [PR #3207](https://github.com/rust-lang/mdBook/pull/3207) | Linux x64 GNU | Linux ARM64 GNU | Same libc family. |

There is no submitted change that adds Windows ARM64 MSVC to a project with
only a Windows x64 GNU release. Several projects publish both x64 ABIs; this
must be checked per project, not inferred from one asset filename.

## Known release coverage gaps

| Project | Missing or exceptional variant | Upstream tracking | Current disposition |
| --- | --- | --- | --- |
| age | Windows ARM64 | [#733](https://github.com/FiloSottile/age/issues/733) | Not under active fork work. |
| Atuin | Windows ARM64; portable Windows shell startup | [#3056](https://github.com/atuinsh/atuin/issues/3056) | See campaign table; WiX branch is separate. |
| Delta | Windows ARM64; Linux ARM64 musl | [#2223](https://github.com/dandavison/delta/issues/2223), [#2227](https://github.com/dandavison/delta/issues/2227) | Issue-first. |
| GDU | Windows ARM64 | [PR #647](https://github.com/dundee/gdu/pull/647) | Open PR. |
| Glow, Gum, VHS | Windows ARM64 | Glow [discussion #1025](https://github.com/charmbracelet/glow/discussions/1025), Gum [#1139](https://github.com/charmbracelet/gum/discussions/1139), VHS [#780](https://github.com/charmbracelet/vhs/discussions/780) | Charm asks for an idea discussion before a PR. |
| grpcurl | Windows ARM64 | [#541](https://github.com/fullstorydev/grpcurl/issues/541) | Not under active fork work. |
| helix | Windows ARM64 | [#10872](https://github.com/helix-editor/helix/issues/10872) | Not under active fork work. |
| hexyl | Linux ARM64 musl | [PR #292](https://github.com/sharkdp/hexyl/pull/292) | Open PR; static artifact proven. |
| hyperfine | Linux ARM64 musl | [PR #924](https://github.com/sharkdp/hyperfine/pull/924) | Open PR; static artifact proven. |
| lsd | Windows ARM64 | [PR #1236](https://github.com/lsd-rs/lsd/pull/1236) | Upstream tracking exists. |
| mdBook | Windows ARM64; Linux ARM64 GNU | [PR #3207](https://github.com/rust-lang/mdBook/pull/3207) | Open PR covers Linux ARM64 GNU; Windows ARM64 remains separate. |
| pastel | Windows ARM64; Linux ARM64 musl | [PR #322](https://github.com/sharkdp/pastel/pull/322) | Open PR covers Linux musl; Windows ARM64 remains separate. |
| Procs | Windows ARM64 | [PR #961](https://github.com/dalance/procs/pull/961) | Open PR. |
| QSV | Windows ARM64; Linux ARM64 musl | [#2945](https://github.com/dathere/qsv/issues/2945) | ARM64-musl build reaches `qsvdp`, then the hosted runner terminates it; no code failure established. |
| Restic | Windows ARM64 | [#3596](https://github.com/restic/restic/issues/3596) | Requires native VSS/fs-snapshot comparison. |
| SD | Windows ARM64; Linux ARM64 GNU | [PR #354](https://github.com/chmln/sd/pull/354) | Open PR covers native Windows ARM64 MSVC and GNU-family lanes; Linux ARM64 GNU is already in the release workflow but awaits a new release. |
| shfmt | Windows ARM64 | [#1077](https://github.com/mvdan/sh/issues/1077) | Not under active fork work. |
| Typos | Windows ARM64 | [PR #1602](https://github.com/crate-ci/typos/pull/1602) | Open PR. |
| Vivid | Windows ARM64; Linux ARM64 musl | [PR #233](https://github.com/sharkdp/vivid/pull/233) | Linux-musl PR merged; Windows ARM64 remains separate. |
| zellij | Windows ARM64 | [PR #5090](https://github.com/zellij-org/zellij/pull/5090) | Upstream tracking exists. |

## Linux musl linkage exceptions

These projects publish a musl-labelled release that is dynamically linked, so
the asset needs a compatible musl runtime/loader and is not a portable static
musl binary.

| Project | Tracking or reason |
| --- | --- |
| Bun | [#23910](https://github.com/oven-sh/bun/issues/23910) requests a static binary. |
| Claude Code | Bundled through Bun; same runtime model. |
| Fastfetch | [#2102](https://github.com/fastfetch-cli/fastfetch/issues/2102) was declined because the plugin architecture uses dynamic loading. |
| OpenCode | Current musl asset is dynamic. |
| pnpm | Current musl asset is dynamic. |
| PowerShell | Dynamic musl package is deliberate for its runtime/dependency model. |

## Windows portable-installer work

Portable Winget ZIP installs can expose shell hooks through symlinks. Windows
SSH installations may not follow those links, so shell startup breaks. The
desired user experience is a signed MSI/WiX-style installer rather than a
portable symlink layout.

| Project | Fork branch | Status |
| --- | --- | --- |
| Atuin | `winget-wix-installer` | WIP cargo-dist WiX/MSI configuration; separate from Windows ARM64 work. |
| fzf | `winget-wix-installer` | WIP investigation/configuration. |
| Yazi | `winget-wix-installer` | WIP investigation/configuration. |
| Zoxide | `winget-wix-installer` | WIP investigation/configuration. |

## Fork and submission lifecycle

- A canonical clone lives at `/vol/code/<upstream-org>/<repo>`, with `origin`
  for upstream and `fork` for `meop/<repo>`.
- Temporary worktrees are removed after their branch is committed and pushed.
- Retain a fork while it backs an open PR, active discussion, or current branch.
- Remove a dropped project from this document and `repo.toml`, then delete its
  `meop` fork and canonical clone only when explicitly requested.
