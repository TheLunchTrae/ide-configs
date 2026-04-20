# ide-configs

Personal backups of IDE configuration files, one folder per IDE.

## Contents

- [`phpstorm/`](./phpstorm) — PhpStorm JVM options and IDE properties, tuned
  for large monorepos.

Each IDE folder has its own `README.md` documenting install locations and
any per-file notes.

## Restoring a Config

1. Open the IDE's folder in this repo.
2. Follow the `README.md` in that folder to find the on-disk install path
   for your OS.
3. Copy the relevant file(s) into place and restart the IDE.

## Adding a New IDE

1. Create a sibling folder named after the vendor (e.g. `vscode/`, `zed/`).
2. Add the config file(s) verbatim — no reformatting.
3. Write a short `README.md` covering what the files do and where they live
   on Windows / macOS / Linux.

See [`CLAUDE.md`](./CLAUDE.md) for conventions when Claude Code is helping
edit this repo.
