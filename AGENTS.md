# Veil Iris Fix

Keep this a narrow client compatibility mod. README owns supported versions,
verification and the upstream removal condition. Follow sibling dh-polygon-fix
build conventions; no world data, downloaded JARs or decompiled source in Git.

Preserve the exact Sable/nested Veil and Iris input hashes and runtime guards.
Review upstream before changing them. The original Veil injection must remain
inside the wrapped method; test actual transformed bytecode and restoration on
normal and exceptional paths. `./gradlew check build` is required after code or
build changes. Controlled GL/Iris tests do not establish native rendering.

Use disposable Minecraft instances for shader/Ponder checks. Leave running play
instances untouched. Keep the candidate uninstalled until native verification;
do not commit, push or publish without authorization. Document current behavior
and limits directly, without a separate review ledger.
