# AGENTS.md — rider/

Scoped guidance for coding agents editing files under `rider/`.
The repo-root `AGENTS.md` still applies — this file adds Rider-specific
references on top of it.

## Reference docs

- **JetBrains Rider — Tuning the IDE**:
  <https://www.jetbrains.com/help/rider/Tuning_the_IDE.html>
  Source of truth for JVM options and documented `idea.properties` keys.

## Caveats

- The doc page above is **not exhaustive**. Many real, supported keys
  don't appear there (e.g. `idea.system.path`, `idea.log.path`). **Absence
  from the page is not proof a key is invalid** — verify against the
  bundled `bin/idea.properties` and `idea.log` startup warnings before
  deleting anything on that basis.
- Since 2020.2, Rider **merges** the user vmoptions file with the bundled
  defaults, so the committed `*.vmoptions` file should contain only
  *overrides*, not the full default list. Don't "restore" defaults that
  look missing — they're being inherited.
- These configs were seeded from `phpstorm/` and share its tuning
  assumptions (large monorepo, 16 GB+ RAM, 8+ cores). Some properties
  carried over from PhpStorm target the IntelliJ JPS Java build process
  and likely have no effect in Rider, which uses MSBuild for .NET. The
  JPS build-process keys (`compiler.max.heap.size`,
  `build.parallel.compilation.threads`) have been dropped from
  `idea.properties` for that reason. `idea.dynamic.classpath` stays: it
  shortens command lines for JVMs the IDE or its plugins start,
  so it can't be ruled inert. `idea.dynamic.classpath.jar` was dropped:
  the IDE reads it from saved settings, not from `idea.properties`.
