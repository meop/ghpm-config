# Release-target fork tracker

This is a working record of fork-only investigation branches. Do not open an
upstream issue or PR merely because a branch exists: each row says what still
needs to be demonstrated.

| Project | Fork branch | Target gap under test | Current evidence | Next gate |
| --- | --- | --- | --- | --- |
| Atuin | `windows-arm64-release-runner-test` | Windows ARM64 MSVC | [full fork smoke passed](https://github.com/meop/atuin/actions/runs/33240919163) | Validate on a Windows ARM64 machine, then update the existing draft work. |
| Delta | `windows-arm64-release` | Windows ARM64 MSVC; Linux ARM64 musl | [Windows ARM64 fork CI passed](https://github.com/meop/delta/actions/runs/33223435577) | Test and package the Linux-musl addition before extending the existing upstream issue. |
| Procs | `windows-arm64-release` | Windows ARM64 MSVC | Native runner work passed; the overall regression run failed on unrelated lint | Upstream [PR #961](https://github.com/dalance/procs/pull/961) is open; resolve or document the unrelated CI failure. |
| GDU | `windows-arm64-release` | Windows ARM64 | [native smoke passed](https://github.com/meop/gdu/actions/runs/33240626102) | Turn the local Go build proof into the project release-matrix change. |
| Glow | `windows-arm64-release` | Windows ARM64 | [native smoke passed](https://github.com/meop/glow/actions/runs/33240626563) | The shared `charmbracelet/meta` release configuration needs a coordinated change. |
| Gum | `windows-arm64-release` | Windows ARM64 | [native smoke passed](https://github.com/meop/gum/actions/runs/33240627378) | The shared `charmbracelet/meta` release configuration needs a coordinated change. |
| Hurl | `windows-arm64-release` | Windows ARM64 MSVC | Latest [fork smoke failed](https://github.com/meop/hurl/actions/runs/33240735166) | Diagnose the full native build after the vcpkg dependency setup. |
| VHS | `windows-arm64-release` | Windows ARM64 | [native smoke passed](https://github.com/meop/vhs/actions/runs/33240629160) | The shared `charmbracelet/meta` release configuration needs a coordinated change. |
| SD | `windows-arm64-release` | Windows ARM64 MSVC; Linux ARM64 GNU | Current release workflow lists both targets, but has not been run from this fork | Change the ARM Windows runner to `windows-11-arm`, then tag-test the real release matrix. |
| Xan | `windows-arm64-release` | Windows ARM64 MSVC; Linux ARM64 musl | No fork run yet | Add both targets to the GitHub Actions release matrix and tag-test it. |
| Restic | `windows-arm64-release` | Windows ARM64 | No fork run yet; [#3596](https://github.com/restic/restic/issues/3596) identifies Windows ARM VSS/COM work | Add a Windows ARM build/test smoke job; investigate VSS behavior before a release change. |
| QSV | `linux-arm64-abi-release` | Linux ARM64 musl | Upstream has repeatedly successful Windows ARM64 build/publish runs; no fork Linux-musl run yet | Identify the custom release-matrix addition and prove a full signed/packageable build on the fork. |
| Hyperfine | `linux-arm64-abi-release` | Linux ARM64 musl | Existing Windows ARM [PR #922](https://github.com/sharkdp/hyperfine/pull/922) has a successful fork matrix; Linux-musl addition untested | Add ARM64 musl to the release matrix and run its packaging path. |
| Hexyl | `linux-arm64-abi-release` | Linux ARM64 musl | Existing Windows ARM [PR #291](https://github.com/sharkdp/hexyl/pull/291) is open; Linux-musl fork CI is queued | Wait for the fork matrix result. |
| Vivid | `linux-arm64-abi-release` | Linux ARM64 musl | Existing Windows ARM [PR #228](https://github.com/sharkdp/vivid/pull/228) is merged; Linux-musl addition untested | Add ARM64 musl to the release matrix and run its packaging path. |
| mdBook | `linux-arm64-abi-release` | Linux ARM64 GNU | Existing Windows ARM [PR #3193](https://github.com/rust-lang/mdBook/pull/3193) is merged; Linux GNU release path untested | Locate the release mechanism, then prove an ARM64 GNU package. |
| Pastel | `linux-arm64-abi-release` | Linux ARM64 musl | Existing Windows ARM [PR #320](https://github.com/sharkdp/pastel/pull/320) is open; Linux-musl fork CI is queued | Wait for the fork matrix result. |
| Tealdeer | — | macOS ARM64 | [#365](https://github.com/tealdeer-rs/tealdeer/issues/365) said an ARM release would be added, but current releases have no macOS assets | Inspect the release path and make a fork proof branch. |
| Typos | `ci/platform-release-matrix` | Windows ARM64 MSVC | Upstream [PR #1602](https://github.com/crate-ci/typos/pull/1602) is open with a successful fork release matrix | Await upstream release. |
