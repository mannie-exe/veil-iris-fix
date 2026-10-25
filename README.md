# Veil Iris Fix

Client compatibility patch for Minecraft 1.21.1, NeoForge 21.1.264, Veil 4.3.2
(bundled by Sable 2.0.6), and Iris 1.8.14-beta.1+mc1.21.1. It restores framebuffer
bindings around Veil shader activation and selects Iris's active world target.
Its rendering correction is verified in an isolated Create Sky client. Install
it on clients only; it is separate from Create Sky Compat and the resource patches.

Veil's shipped Iris injection binds a world framebuffer during offscreen rendering,
including Aeronautics' propeller Ponder scene. Its separate `apply`/`clear` methods
cannot share a `@Share` local. This patch wraps both complete methods, including
those original injections. GUI/shadow rendering restores the previous read/draw
target immediately; world rendering uses `bindDefault`. Clear and exceptional
exits restore the saved bindings. Repeated apply calls retain the original target.

The correction follows [Veil PR #213](https://github.com/FoundryMC/Veil/pull/213).
It does not replace shaders, Ponder scenes, or the resource-only pack fixes JAR.
See `NOTICE` for attribution and the included LGPL-3.0 license files.

## Build and checks

Use Java 21 and run `./gradlew check build`. Outputs are in `build/libs/`.
Gradle downloads pinned compile/test inputs; no third-party binaries are bundled.
The checked-in wrapper pins Gradle 9.2.1 and its distribution checksum.

The isolated test loads the released Veil injection alongside this mixin, verifies
both wrappers enclose it, and executes the transformed patch methods with controlled
GL/Iris boundaries. Cases cover no active pipeline, a non-Iris pipeline, GUI,
shadow and world passes, repeated apply/clear, and failures in apply/clear. These
checks validate transformation and state handling, not GPU output or gameplay.
The built archive was inspected: it contains the patch class, client mixin
configuration, expanded dependency/version metadata and license notices, with
no test classes or bundled third-party JARs.

## Native verification and updates

On 2026-10-24, the isolated Create Sky client reproduced the missing propeller
Ponder scene with Complementary Unbound r5.9.3 + Euphoria Patches 1.10.5 enabled.
The same scene rendered without shaders, while Create's mechanical press rendered
with shaders. Adding only this patch restored the propeller scene, its UI and
later animation stages with shaders enabled; the mechanical press still rendered.
The command was `/ponder aeronautics:wooden_propeller` (the thrust storyboard).

Native-tested JAR SHA-256:
`31c784adc24fa2e8d83b5bcebf0aed4e61d9f0be568d630ac1e28767ef34487f`.
The release JAR is `f4144a2bfef7dcd60fed8a0647dc60d356d4ab9fe3ebb36f1647a119b6a183bc`;
only its repository URL metadata differs from that native-tested artifact.
The client used Java 21.0.13 on macOS arm64, the dependency versions above and a
copied Resource Review world. `./gradlew check build` also passed, including the
server-side transformation check. Veil PR #213 remained open at inspection.

The same patch also rendered the propeller scene with shaders disabled, a
redstone-powered hot-air burner in-world, and inventory items while the burner
remained visible. Iris's reload hotkey restored both the world flame and Ponder
rendering. A 12.6-second native capture contained progressing scene frames; still
captures also covered the beginning and later thrust stages. Logs contained no
Mixin application failures. This verifies the selected macOS renderer/shader
combination, not every shader pack or graphics driver.

The baseline already logged Veil `Unsupported Uniform Type: bool` errors;
this patch does not claim to fix those. Initial offline lab sessions stalled on
shutdown before and after adding the patch; another session saved all dimensions
and exited normally. The final fixture refresh also stalled during disconnect
and needed SIGTERM; its saved fixture placements passed the stopped-world check.
The shutdown cause was not isolated or attributed to this patch.

When updating the patch or its dependencies, use a disposable client matching the pack:

1. Reproduce Aeronautics' propeller thrust section with the unpatched shader stack.
2. Add the patch only to that isolated client. Verify the same scene with shaders
   enabled/disabled, a working Ponder scene, burner flames in-world, inventory,
   and a shader reload. Inspect logs for mixin/shader/OpenGL errors.
3. Confirm no second copy exists in bundled mods or overrides. Reference the
   verified published artifact through a pinned client-only empack dependency.
   Keep it out of server distributions.

Iris is required by this patch. An installation without Iris should omit the
patch rather than load it as a general Veil fix. A dedicated-server mixin check is
separate from a full server startup.

When Sable/Veil or Iris changes, inspect the nested Veil artifact, exact upstream
implementation and shader wrapper call paths. Update build input hashes and mod
version constraints together, then rerun transformation and native checks. Remove
the patch once the selected upstream artifact restores framebuffer state, guards
GUI/shadow passes and selects the correct Iris target. A merged issue/PR alone is
not proof that a released artifact contains the fix.

## GitHub releases

The build workflow checks Linux, Windows and macOS. A tag matching `mod_version`
publishes only byte-identical binary/source JARs from those jobs, with complete
source and SHA-256/SHA-512 manifests. Update `RELEASE_NOTES.md` before tagging.
`python3 tools/release.py v<version> --stage-only` validates downloaded CI artifacts
without publishing. Do not replace existing release assets. Modrinth publication
is deferred.
