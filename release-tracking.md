# Release-target fork tracker

This is a working record of fork-only investigation branches. Do not open an
upstream issue or PR merely because a branch exists: each row says what still
needs to be demonstrated.

| Project | Fork branch | Target gap under test | Current evidence | Next gate |
| --- | --- | --- | --- | --- |
| Atuin | `windows-arm64-release-runner-test` | Windows ARM64 MSVC | [full fork smoke passed](https://github.com/meop/atuin/actions/runs/33240919163) | Validate on a Windows ARM64 machine, then update the existing draft work. |
| Delta | `windows-arm64-release` | Windows ARM64 MSVC; Linux ARM64 musl | [Windows ARM64 fork CI passed](https://github.com/meop/delta/actions/runs/33223435577); Linux-musl package smoke is queued | Await the fork-safe Linux-musl packaging result. |
| Procs | `windows-arm64-release` | Windows ARM64 MSVC | Native runner work passed; the overall regression run failed on unrelated lint | Upstream [PR #961](https://github.com/dalance/procs/pull/961) is open; resolve or document the unrelated CI failure. |
| GDU | `windows-arm64-release` | Windows ARM64 | [native smoke passed](https://github.com/meop/gdu/actions/runs/33240626102) | Turn the local Go build proof into the project release-matrix change. |
| Glow | `windows-arm64-release` | Windows ARM64 | [native smoke passed](https://github.com/meop/glow/actions/runs/33240626563) | The shared `charmbracelet/meta` release configuration needs a coordinated change. |
| Gum | `windows-arm64-release` | Windows ARM64 | [native smoke passed](https://github.com/meop/gum/actions/runs/33240627378) | The shared `charmbracelet/meta` release configuration needs a coordinated change. |
| Hurl | `windows-arm64-release` | Windows ARM64 MSVC | Latest [fork smoke failed](https://github.com/meop/hurl/actions/runs/33240735166) | Diagnose the full native build after the vcpkg dependency setup. |
| VHS | `windows-arm64-release` | Windows ARM64 | [native smoke passed](https://github.com/meop/vhs/actions/runs/33240629160) | The shared `charmbracelet/meta` release configuration needs a coordinated change. |
| SD | `windows-arm64-release` | Windows ARM64 MSVC; Linux ARM64 GNU | [Fork smoke passed](https://github.com/meop/sd/actions/runs/33243840862) for both targets | Ready for an upstream proposal when you authorize it. |
| Xan | `windows-arm64-release` | Windows ARM64 MSVC; Linux ARM64 musl | Native musl compilation failed in jemalloc; Cross-based release-action smoke is queued | Await the Cross package result; Windows ARM build remains covered by the same smoke. |
| Restic | `windows-arm64-release` | Windows ARM64 | [Windows ARM test passed](https://github.com/meop/restic/actions/runs/33244335034); the only failure is the expected Linux cloud test without fork secrets | Investigate VSS behavior on a Windows ARM64 machine before proposing release support. |
| QSV | `linux-arm64-abi-release` | Linux ARM64 musl | First native-musl smoke failed in `tikv-jemalloc`; system-allocator rerun is queued | Determine whether the existing Windows-style allocator exception yields a complete package. |
| Hyperfine | `linux-arm64-abi-release` | Linux ARM64 musl | [Fork CICD passed](https://github.com/meop/hyperfine/actions/runs/33243730175), including packaging | Ready for an upstream proposal when you authorize it. |
| Hexyl | `linux-arm64-abi-release` | Linux ARM64 musl | [Fork CICD passed](https://github.com/meop/hexyl/actions/runs/33244053520) | Ready for an upstream proposal when you authorize it. |
| Vivid | `linux-arm64-abi-release` | Linux ARM64 musl | [Fork CICD passed](https://github.com/meop/vivid/actions/runs/33243731116) | Ready for an upstream proposal when you authorize it. |
| mdBook | `linux-arm64-abi-release` | Linux ARM64 GNU | First smoke built successfully but derived the immutable PR ref; a fork-safe package rerun is queued | Await the corrected package artifact. |
| Pastel | `linux-arm64-abi-release` | Linux ARM64 musl | [Fork CICD passed](https://github.com/meop/pastel/actions/runs/33244052431) | Ready for an upstream proposal when you authorize it. |
| Typos | `ci/platform-release-matrix` | Windows ARM64 MSVC | Upstream [PR #1602](https://github.com/crate-ci/typos/pull/1602) is open with a successful fork release matrix | Await upstream release. |
