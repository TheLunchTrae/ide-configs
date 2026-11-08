# PhpStorm

Backups of PhpStorm JVM and IDE-level configuration.

Captured against **PhpStorm 2026.1** on **Windows 11 64-bit**.

## Files

- **`phpstorm64.exe.vmoptions`** — JVM options (heap, compact object
  headers). Filename is the Windows-specific form.
- **`idea.properties`** — PhpStorm runtime properties, tuned for large
  monorepos (bigger intellisense/content-load limits, dynamic classpath for
  long Windows command lines, custom index/log paths, UI tweaks).

## Install Locations

Drop the files into the per-version config directory for your platform. Both
files override IDE defaults on next start.

| OS      | Path                                                              |
| ------- | ----------------------------------------------------------------- |
| Windows | `%APPDATA%\JetBrains\PhpStorm<version>\`                          |
| macOS   | `~/Library/Application Support/JetBrains/PhpStorm<version>/`      |
| Linux   | `~/.config/JetBrains/PhpStorm<version>/`                          |

Replace `<version>` with the installed release, e.g. `PhpStorm2026.1`.

You can also open these from inside PhpStorm via
**Help → Edit Custom VM Options…** and **Help → Edit Custom Properties…** —
the IDE will create the files in the right place for you.

## Platform-Specific vmoptions Filename

The vmoptions filename varies by OS. If you want the same JVM tuning
cross-platform, rename/duplicate as needed:

| OS      | Filename                   |
| ------- | -------------------------- |
| Windows | `phpstorm64.exe.vmoptions` |
| macOS   | `phpstorm.vmoptions`       |
| Linux   | `phpstorm64.vmoptions`     |

## Notes

- `idea.properties` sets `idea.system.path` and `idea.log.path` to
  `${user.home}/.PhpStorm/system` and `${user.home}/.PhpStorm/log`. This
  moves caches and logs **out of** the default JetBrains location — intentional,
  but handy to remember when debugging "where did my indexes go?"
- Heap is sized 4 GB min / 8 GB max (aggressive baseline for a
  multi-million-LOC monorepo on my 64 GB Windows 11 machine; PhpStorm 2026.1
  runs on JBR 25).
  Raise `-Xmx` only if the Memory Indicator shows post-GC usage
  sustained above 80%. Larger heaps hurt more than they help — full-GC
  pauses scale with heap and every extra GB is a GB stolen from the
  Windows file cache.
- `caches.indexerThreadsCount` is deliberately unset. The IDE already
  indexes on (logical CPUs − 1) threads, so only set it to cap indexing
  below that.
