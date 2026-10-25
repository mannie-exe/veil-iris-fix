# Veil Iris Fix

Corrects framebuffer handling when Veil shaders run alongside Iris. This restores
rendering in offscreen scenes such as Aeronautics' propeller Ponder animation.

## Installation

Download the binary JAR from [GitHub releases](https://github.com/mannie-exe/veil-iris-fix/releases)
and place it in the client's `mods/` directory. Do not use the sources JAR or
install the patch on a dedicated server. No configuration is required.

| Dependency | Supported version |
| --- | --- |
| Minecraft | 1.21.1 |
| NeoForge | 21.1.264 or later in the 21.1 series |
| Java | 21 |
| Veil | 4.3.2, tested as bundled by Sable 2.0.6 |
| Iris | 1.8.14-beta.1+mc1.21.1 |

Veil and Iris are required. This is not a general Veil fix for installations
without Iris. Create Sky is not required, and the patch needs no resource pack.

## Behavior and limits

The patch restores the framebuffer bindings around Veil shader activation and
uses Iris's active world target during world rendering. It follows
[Veil PR #213](https://github.com/FoundryMC/Veil/pull/213).

Native checks cover macOS arm64 with Complementary Unbound r5.9.3 and Euphoria
Patches 1.10.5, including Ponder, burner flames, inventory and shader reload.
Other shader packs and drivers are not established by those checks. Veil's
existing `Unsupported Uniform Type: bool` errors are outside this correction.
See [verification](docs/verification.md) for the exact artifacts and test limits.

Remove the patch when the installed upstream release contains the complete
correction. An upstream PR merging does not establish that a particular release
includes it. Follow the [dependency update procedure](docs/development.md#dependency-updates)
before changing Veil or Iris versions.

## Development

Use Java 21 and `./gradlew check build`. See [development](docs/development.md)
for implementation and tests, and [publishing](docs/publishing.md) for releases.

## License

LGPL-3.0-only. See [NOTICE](NOTICE), [LGPLv3](LICENSE.LESSER.txt), and
[GPLv3](LICENSE.txt). This is an independent compatibility patch.
