# Verification

## Native rendering, 2026-10-24

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
The client used Minecraft 1.21.1, NeoForge 21.1.264, Sable 2.0.6 with nested
Veil 4.3.2, Iris 1.8.14-beta.1+mc1.21.1 and Java 21.0.13 on macOS arm64 in a
disposable test world. `./gradlew check build` also passed, including the
server-side transformation check. Veil PR #213 was open at the 2026-10-24 inspection.

The same patch also rendered the propeller scene with shaders disabled, a
redstone-powered hot-air burner in-world, and inventory items while the burner
remained visible. Iris's reload hotkey restored both the world flame and Ponder
rendering. A 12.6-second native capture contained progressing scene frames; still
captures also covered the beginning and later thrust stages. Logs contained no
Mixin application failures. This verifies the selected macOS renderer/shader
combination, not every shader pack or graphics driver.

The baseline logged Veil `Unsupported Uniform Type: bool` errors; this patch does
not fix them. Some isolated sessions stalled during shutdown both before and
after installation. The cause was not isolated or attributed to this patch.
Rendering checks do not establish shutdown reliability.
