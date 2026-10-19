# SakuraLens Releases

[![Discord](https://img.shields.io/badge/Discord-join%20the%20community-5865F2?logo=discord&logoColor=white)](https://discord.gg/2DbshCqaD)

Downloadable builds of [SakuraLens](https://github.com/HiganSakura/SakuraLens)
— a local git diff workspace with a design/verify workflow, an agent API and an
MCP server.

**This repository contains no source code.** It only hosts the artifacts
attached to [Releases](../../releases). For the source, build instructions and
documentation, see the
[main repository](https://github.com/HiganSakura/SakuraLens).

## Download

Open the [latest release](../../releases/latest) and pick the artifact for your
platform.

### macOS app

| File | Notes |
|------|-------|
| `SakuraLens-<version>-macos-<arch>.dmg` | Drag-to-**Applications** installer |
| `SakuraLens-<version>-macos-<arch>.zip` | Zipped `.app` bundle |

`<arch>` is `aarch64` (Apple silicon) or `x86_64` (Intel).

The app is **ad-hoc signed, not notarized**, so Gatekeeper blocks the first
launch. Either right-click the app and choose **Open**, or clear the quarantine
flag once:

```bash
xattr -dr com.apple.quarantine /Applications/SakuraLens.app
```

### Command-line binaries

| File | Notes |
|------|-------|
| `skln-<target>.tar.gz` | Static `skln` binary for the given Rust target |

Unpack and put `skln` on your `PATH`:

```bash
tar -xzf skln-<target>.tar.gz
install -m 0755 skln /usr/local/bin/skln
skln --repo /path/to/repo
```

Targets follow Rust's triple naming, for example
`aarch64-apple-darwin`, `x86_64-apple-darwin`,
`x86_64-unknown-linux-gnu` and `x86_64-pc-windows-msvc`.

## Verify downloads

Every release ships a `checksums.txt` with SHA-256 sums:

```bash
shasum -a 256 -c checksums.txt
```

## Releasing

See [RELEASING.md](RELEASING.md) for how the artifacts are produced and
uploaded by hand.

## Community

Questions, feedback, or release news — join the Discord:
<https://discord.gg/2DbshCqaD>

## License

[MIT](LICENSE) © Jakku Sakura
