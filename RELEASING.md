# Releasing

Artifacts are built locally and uploaded to this repository's GitHub Releases
by hand. There is no automation here.

## Artifact naming

| Artifact | Producer |
|----------|----------|
| `SakuraLens-<version>-macos-<arch>.dmg` | `just release-macos` |
| `SakuraLens-<version>-macos-<arch>.zip` | `just release-macos` |
| `skln-<target>.tar.gz` | `.github/workflows/release.yml` in the main repo |
| `checksums.txt` | `just release-macos` |

`<arch>` is `aarch64` or `x86_64`; `<target>` is a Rust target triple (for
example `aarch64-apple-darwin`). `<version>` is the workspace version in the
main repo's `Cargo.toml`.

## macOS app

From the main repository:

```bash
just release-macos
```

This builds the UI and the Tauri desktop binary, assembles `SakuraLens.app`,
ad-hoc signs it, and writes the distributable files (and `checksums.txt`) to
`dist/`:

```
dist/SakuraLens-0.1.0-macos-aarch64.dmg
dist/SakuraLens-0.1.0-macos-aarch64.zip
dist/checksums.txt
```

Build each architecture on that architecture (the bundle is host-native), and
run the recipe once per arch you intend to publish.

To package only the raw `.app` without the archive step, use
`just package-macos`.

## Uploading

1. Make sure the tag matches the version you built, e.g. `v0.1.0`
   (`git -C <main-repo> tag v0.1.0 && git -C <main-repo> push origin v0.1.0`).
2. Create the release here:
   ```bash
   gh release create v0.1.0 \
       --repo HiganSakura/SakuraLens-release \
       --title "SakuraLens v0.1.0" \
       --notes-file <notes>
   ```
3. Upload the artifacts from `dist/`, plus any `skln-<target>.tar.gz` built by
   the main repo's release workflow:
   ```bash
   gh release upload v0.1.0 \
       --repo HiganSakura/SakuraLens-release \
       dist/SakuraLens-0.1.0-macos-aarch64.dmg \
       dist/SakuraLens-0.1.0-macos-aarch64.zip \
       dist/checksums.txt
   ```
4. Sanity-check the rendered release page and the `checksums.txt` download.

## Notes

- The app is ad-hoc signed, not notarized. If notarization is added later, the
  `.dmg` should be stapled (`xcrun stapler staple`) before upload.
- Keep `checksums.txt` in sync with the uploaded files; replace it rather than
  appending if a release is re-uploaded.
