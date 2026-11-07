# Releasing

Releases are built from the main repository and published to this repository's
GitHub Releases by `scripts/release.sh` there. The only thing committed here is
the "latest release" block of the README, which the script updates.

## Artifact naming

| Artifact | Producer (main repository) |
|----------|----------------------------|
| `SakuraLens-<version>-macos-aarch64.dmg` | `just release-macos` |
| `SakuraLens-<version>-macos-aarch64.zip` | `just release-macos` |
| `SakuraLens-<version>-linux-x86_64.tar.gz` | `just package-linux` |
| `SakuraLens-<version>-windows-x86_64.zip` | `just package-windows` |
| `checksums.txt` | `scripts/release.sh`, from the files above |

`<version>` is `<workspace version>-<channel>.<YYYYMMDD>.<short sha>`, for
example `0.4.0-beta.20261107.6357b144`; the tag is `v<version>`.

## Steps

From the main repository, with the commit to release pushed to `origin/main`:

```bash
just release-macos      # builds, signs and notarizes on this Mac
just package-linux      # builds on the Linux host
just package-windows    # builds on the Windows host
just release --title "SakuraLens 0.4.0 — <headline>" --notes notes.md
```

`just release` checks that the version's commit is on `origin/main` and that
every archive is in `dist/`, writes `checksums.txt`, tags the commit, creates the
release here with its assets, publishes the launch manifest
(`versions.json`), and commits the latest-release line to this repository's
`main`. Add `--dry-run` to see what it would do.

The macOS build is notarized and stapled; check it with
`spctl -a -vv /Applications/SakuraLens.app` (`accepted`, `source=Notarized
Developer ID`).
