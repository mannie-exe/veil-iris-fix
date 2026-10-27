# Veil Iris Fix

Keep this a narrow client compatibility mod. README owns installation,
support and the upstream removal condition.
`docs/development.md` owns implementation and update procedures;
`docs/verification.md` owns dated evidence; `docs/publishing.md` owns releases.
Keep world data, downloaded JARs and decompiled source out of Git.

Preserve the exact Sable/nested Veil and Iris input hashes and runtime guards.
Review upstream before changing them. The original Veil injection must remain
inside the wrapped method; test actual transformed bytecode and restoration on
normal and exceptional paths. `./gradlew check build` is required after code or
build changes. Controlled GL/Iris tests do not establish native rendering.

Use disposable Minecraft instances for shader/Ponder checks. Leave running play
instances untouched. Verify rendering before distributing behavior changes;
do not commit, push or publish without authorization. Document current behavior
and limits directly, without a separate review ledger.

Keep patch decisions tied to exact released artifacts, not mod names or an open
upstream issue alone. Check the affected propeller Ponder scene and working control
scenes with shaders enabled and disabled. Verify resource reload and framebuffer
restoration when those paths change. Record the upstream condition that permits
retiring the fix; do not absorb unrelated terrain or resource-pack changes.
