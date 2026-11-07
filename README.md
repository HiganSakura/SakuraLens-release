# SakuraLens Releases

[![Discord](https://img.shields.io/badge/Discord-join%20the%20community-5865F2?logo=discord&logoColor=white)](https://discord.gg/2DbshCqaD)

Downloadable builds of [SakuraLens](https://github.com/HiganSakura/SakuraLens)
— a local git diff workspace with a design/verify workflow, an agent API and an
MCP server.

**This repository contains no source code.** It only hosts the artifacts
attached to [Releases](../../releases). For the source, build instructions and
documentation, see the
[main repository](https://github.com/HiganSakura/SakuraLens).

<!-- latest:start -->
**Latest release: [0.4.0](../../releases/tag/v0.4.0-beta.20261107.g8b712bd8)** (`v0.4.0-beta.20261107.g8b712bd8`)
<!-- latest:end -->

## Download

Open the [latest release](../../releases/latest) and pick the file for your
platform.

| Platform | File | Notes |
|----------|------|-------|
| macOS (Apple silicon) | `SakuraLens-<version>-macos-aarch64.dmg` | Drag-to-**Applications** installer |
| macOS (Apple silicon) | `SakuraLens-<version>-macos-aarch64.zip` | Zipped `.app` bundle; what the in-app updater downloads |
| Linux (x86_64) | `SakuraLens-<version>-linux-x86_64.tar.gz` | The `skln` binary |
| Windows (x86_64) | `SakuraLens-<version>-windows-x86_64.zip` | `skln.exe` |

### macOS

The app is signed with a Developer ID and notarized, so it opens like any
other app: drag it to **Applications** and launch it.

### Linux and Windows

Unpack the archive and run `skln` (`skln.exe` on Windows) on a repository:

```bash
tar -xzf SakuraLens-<version>-linux-x86_64.tar.gz
./skln /path/to/repo
```

## Verify downloads

Every release ships a `checksums.txt` with SHA-256 sums:

```bash
shasum -a 256 -c checksums.txt
```

## Updates

The macOS app looks for a newer release when it opens, at most once a day. It asks
this repository's releases and the product page's manifest, and uses whichever has the
newer version. When there is one, an **Update** chip appears in the header: it shows
what changed in that release and lets you install it and restart, or open its release
page here. Versions follow [semantic versioning](https://semver.org); a beta is older than
the release it leads to.

The Linux and Windows builds do not replace themselves: download the new archive from
the release page.

## Releasing

See [RELEASING.md](RELEASING.md) for how the artifacts are produced and
published.

## Community

Questions, feedback, or release news — join the Discord:
<https://discord.gg/2DbshCqaD>
