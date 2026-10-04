# Release policy

Rules for which projects ghpm-config lists and how release coverage is judged
and improved. [release-matrix.md](release-matrix.md) records each project's
current release variants; [release-tracking.md](release-tracking.md) tracks
ongoing work.

## Target platforms

ghpm targets five platforms:

- Windows x64 and Windows ARM64
- Linux x64 and Linux ARM64
- macOS ARM64

## Registry inclusion

- A project is listed in `repo.toml` when its latest GitHub release ships
  prebuilt assets for all five target platforms.
- A project with a platform gap waits in
  [release-tracking.md](release-tracking.md#pending-registry-entries) until a
  release closes the gap.
- ABI, libc, linkage, and packaging gaps do not keep a project out of
  `repo.toml`.
- Exceptions kept in `repo.toml` despite a gap, because they are in daily use:
  Starship and zellij.

## Projects to drop

Drop a project from `repo.toml` and the tracking documents, and delete its fork
and clone, when:

- its maintainers decline a target platform (for example shfmt, which ships
  only Go first-class ports, and xh, whose maintainer closed the request
  without comment);
- its release is missing a whole operating system (for example eza, which ships
  no macOS build);
- it is judged not worth carrying (for example hurl, a thin curl wrapper whose
  Windows release bundles curl and libxml2 DLLs).

## Release process preference

Prefer projects whose releases are built and uploaded by GitHub Actions. A
project built on a maintainer's machine or another CI system is harder to
change upstream and is lower priority, though its gaps are still recorded when
the fix is easy. [release-matrix.md](release-matrix.md) shows who uploaded each
release.

## Release variants

| Term | Meaning |
| --- | --- |
| Windows MSVC | A Rust `*-pc-windows-msvc` target, or the native MSVC toolchain. |
| Windows GNU family | A Rust `*-pc-windows-gnu` target (MinGW-w64 ABI), or ARM64's `aarch64-pc-windows-gnullvm` LLVM/MinGW counterpart. Rust has no `aarch64-pc-windows-gnu`. |
| Windows MinGW-Clang | Clang built in MSYS2 for the MinGW-w64 ABI; not MSVC. |
| Windows Go | A Go `GOOS=windows` binary; neither MSVC nor MinGW. |
| Linux musl static | No dynamic musl loader is required at runtime. |

Do not infer an ABI from a filename. Use the release workflow, the target
triple, or an inspected binary.

### Windows ABI parity

Windows ARM64 should ship the same ABI families as Windows x64. If x64 ships
both MSVC and GNU builds, ARM64 ships MSVC and `gnullvm`. Do not substitute one
family because it is easier to build.

`gnullvm` builds link libunwind dynamically by default and import MSYS2's
`libunwind.dll`, so they fail on a machine without MSYS2. Release jobs must set
`CARGO_TARGET_AARCH64_PC_WINDOWS_GNULLVM_RUSTFLAGS=-C target-feature=+crt-static`.
x64 `*-pc-windows-gnu` builds do not need this: Rust ships that target's MinGW
runtime and links libgcc's unwinder statically.

### Linux libc

A missing libc variant is not automatically a gap. `musl` usually means a
static, portable binary, but not always: some projects ship dynamic musl builds
meant for Alpine, and some GNU builds are static. Projects also leave a variant
out on purpose. Count it as a gap when ARM64 lacks what x64 users get, usually
a static binary. A missing ARM64 GNU build is low value when ARM64 already has
a static musl build.

## Proving a change

- Validate in a fork before proposing upstream. Use the project's own release
  tooling where possible, for example a release action's dry-run mode.
- Check the artifact, not only the build: Linux musl binaries have no program
  interpreter, and Windows `gnullvm` binaries start with only `System32` on
  `PATH`.
- Run an ARM64 binary on an ARM64 runner. A binary cross-compiled on x64 is
  handed to an ARM64 job to run.
- GitHub's ARM runners have only versioned labels (`windows-11-arm`,
  `ubuntu-24.04-arm`); otherwise follow the project's existing runner labels.

## Contributing upstream

- Read the project's contribution guide first: its AI policy, and whether it
  wants an issue before a pull request. Follow it.
- Search open issues and pull requests for the same change before opening one,
  including other contributors' work.
- Disclose AI assistance in the description, and add a `Co-Authored-By` trailer
  where the project asks for one.
- Write descriptions from a file with real line breaks. Include the exact
  targets, toolchain, and links to the validating runs.
- Comments on fork pull requests that name an upstream pull request create a
  back-reference on that upstream pull request. Leave upstream numbers out of
  fork-only comments.

## Forks and clones

- A canonical clone lives at `/vol/code/<upstream-org>/<repo>`, with `origin`
  for upstream and `fork` for `meop/<repo>`.
- Remove temporary worktrees once their branch is committed and pushed.
- Keep a fork and clone while they back an open pull request, an active
  discussion, unsubmitted proven work, or a handoff branch.
- Delete smoke and test branches once their runs are cited; Actions runs stay
  viewable after the branch is gone. Delete the fork and clone once the work is
  merged or abandoned.
- Work that needs real Windows ARM64 hardware is handed to the Windows ARM64
  host as a fork branch with a TODO file and a fork pull request, as restic's
  `windows-arm64-release` branch does.
