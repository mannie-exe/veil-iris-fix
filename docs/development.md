# Development

## Framebuffer handling

Veil 4.3.2's Iris injection binds a world framebuffer during offscreen rendering,
including Aeronautics' propeller Ponder scene. Its separate `apply` and `clear`
methods cannot share a `@Share` local.

`ShaderWrapperMixin` wraps both complete methods, including their original
injections. GUI and shadow rendering restore the previous read/draw targets
immediately; world rendering uses `bindDefault`. Clear and exceptional exits
restore the saved bindings. Repeated apply calls retain the original target.
The patch does not replace shaders or Ponder scenes.

## Build and checks

Use Java 21 and the checked-in Gradle wrapper:

```sh
./gradlew check build
```

Outputs are in `build/libs/`. Gradle downloads pinned compile/test inputs and
verifies the Sable archive, its nested Veil JAR and Iris against expected hashes.
No third-party binaries are bundled. The wrapper pins Gradle 9.2.1 and its
distribution checksum.

The tests load Veil's released injection alongside the patch and verify that
both wrappers enclose it. They execute the transformed methods with controlled
GL/Iris boundaries, covering absent and non-Iris pipelines, GUI, shadow and world
passes, repeated apply/clear, and failures in either method. `check` also runs a
server-side transformation probe. These checks establish transformation and state
handling, not GPU output, gameplay or a complete server startup.

## Dependency updates

When Sable, Veil or Iris changes, inspect the nested Veil artifact, upstream
implementation and shader-wrapper call paths. Update build input hashes and
runtime version constraints together. Confirm that the original Veil injections
remain inside the wrappers and rerun transformation tests.

Use a disposable client with the intended dependency and shader versions:

1. Reproduce the propeller thrust scene without the patch using
   `/ponder aeronautics:wooden_propeller`. Compare a working scene such as Create's
   mechanical press with shaders enabled.
2. Add only the patch. Check the same scenes with shaders enabled and disabled,
   powered burner flames in-world, inventory rendering and an Iris shader reload.
3. Inspect logs for Mixin, shader and OpenGL failures. Record the tested artifact,
   platform and shader versions in [verification](verification.md).
4. Check distributions for duplicate patch copies and client-only placement.

Remove this patch once the selected upstream artifact restores framebuffer state,
guards GUI/shadow passes and selects the correct Iris target. Inspect the actual
release artifact rather than relying only on an issue or PR status.
