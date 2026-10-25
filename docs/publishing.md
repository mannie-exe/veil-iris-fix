# Publishing

The GitHub workflow runs checks and builds on Linux, Windows and macOS for main
branch pushes and pull requests. Only a `v<mod_version>` tag enables the release
job. It publishes matching binary/source JARs, a complete source ZIP and
SHA-256/SHA-512 manifests after all three builds succeed.

Update `mod_version`, `RELEASE_NOTES.md` and verification evidence before tagging.
The tag must resolve to the checked-out commit. Never replace published assets.
Documentation-only changes need no version bump or tag.

With that tag's CI artifacts downloaded into `build/ci/build-<runner>/`, use:

```sh
python3 tools/release.py v<version> --stage-only
```

This verifies and stages artifacts without publishing. The staging destination
`build/release` must not already exist. Without `--stage-only`, the script creates
a draft prerelease, uploads its assets, then makes it public.

Modrinth publication is deferred; no upload workflow is configured. Preserve
upstream attribution and the license notices when distributing the patch.
