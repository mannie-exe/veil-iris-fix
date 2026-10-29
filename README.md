# Veil Iris Fix (archived)

This repository is archived and is no longer maintained. Its framebuffer correction
is maintained in [Create Sky Compat](https://github.com/mannie-exe/create-sky-compat),
Use [0.6.1 or later](https://github.com/mannie-exe/create-sky-compat/releases/tag/v0.6.1)
for the incorporated adapter and subsequent single-block shader correction.
No further standalone releases or fixes are planned.

Create Sky Compat requires no content mods and offers independent startup switches.
Use its optional `rendering.veil_framebuffer` adaptation with the supported Veil/Iris
combination. Remove the standalone Veil Iris Fix JAR when enabling that replacement.
See the replacement's [configuration](https://github.com/mannie-exe/create-sky-compat/blob/main/docs/configuration.md)
and [verification limits](https://github.com/mannie-exe/create-sky-compat/blob/main/docs/development/verification.md).

The source, release history, licenses, and earlier verification remain available
for reference. Incorporation does not turn historical standalone checks into
verification of new adapters. This is an independent patch, not an upstream Veil
or Iris release.

## Project history

> Veil Iris Fix was a narrow client patch for Veil 4.3.2 and Iris
> 1.8.14-beta.1+mc1.21.1, including Veil bundled by Sable 2.0.6. It restored separate
> read/draw framebuffer bindings around shader activation and selected Iris's
> active world target appropriately. It followed
> [Veil PR #213](https://github.com/FoundryMC/Veil/pull/213).
>
> Version 0.1.0 included native macOS arm64 checks with Complementary Unbound
> r5.9.3 and Euphoria Patches 1.10.5, covering Ponder, burner flames, inventory,
> and shader reload. Those checks did not establish other drivers or shader packs.

Historical implementation, build, verification, and publishing records remain in
[docs/development.md](docs/development.md), [docs/verification.md](docs/verification.md),
and [docs/publishing.md](docs/publishing.md). Active dependency updates, fixes, and
releases belong to Create Sky Compat.

## License

LGPL-3.0-only. See [NOTICE](NOTICE), [LGPLv3](LICENSE.LESSER.txt), and
[GPLv3](LICENSE.txt). These notices also accompany the incorporated component.
