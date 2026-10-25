# Veil Iris Fix 0.1.0

Client-only correction for Minecraft 1.21.1, NeoForge 21.1.264+, Veil 4.3.2
(bundled with Sable 2.0.6) and Iris 1.8.14-beta.1+mc1.21.1.

Restore framebuffer bindings around Veil shader activation and select Iris's
active world target. This restores Aeronautics' propeller Ponder scene when
shaders are enabled. Ordinary world burner rendering, inventory and shader reload
were checked with Complementary Unbound r5.9.3 and Euphoria Patches 1.10.5.

Based on Veil PR #213; attribution and LGPL-3.0 license files are included.
Remove this temporary patch when the selected Veil release contains the complete
correction. This does not fix Veil's existing bool-uniform errors or claim support
for untested shaders/drivers. Do not install it in server packs.
