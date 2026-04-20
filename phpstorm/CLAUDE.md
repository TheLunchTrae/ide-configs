# CLAUDE.md — phpstorm/

Scoped guidance for Claude Code when editing files under `phpstorm/`.
The repo-root `CLAUDE.md` still applies — this file adds PhpStorm-specific
references on top of it.

## Reference docs

- **JetBrains PhpStorm — Tuning the IDE**:
  <https://www.jetbrains.com/help/phpstorm/tuning-the-ide.html>
  Source of truth for JVM options (`-Xmx`, `-Xms`, `-XX:NewRatio`) and the
  documented `idea.properties` keys (`idea.max.content.load.filesize`,
  `idea.max.intellisense.filesize`, `idea.cycle.buffer.size`,
  `idea.max.vcs.loaded.size.kb`).

## Caveats

- The doc page above is **not exhaustive**. JetBrains states "PhpStorm
  provides a number of other properties" beyond those listed, and many
  real, supported keys (e.g. `idea.system.path`, `idea.log.path`) don't
  appear there. **Absence from the page is not proof a key is invalid** —
  verify against the bundled `bin/idea.properties` and `idea.log` startup
  warnings before deleting anything on that basis.
- Since 2020.2, PhpStorm **merges** the user vmoptions file with the bundled
  defaults, so the committed `*.vmoptions` file should contain only
  *overrides*, not the full default list. Don't "restore" defaults that
  look missing — they're being inherited.
