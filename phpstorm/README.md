# PhpStorm

Backups of PhpStorm JVM and IDE-level configuration.

## Files

- **`phpstorm64.exe.vmoptions`** — JVM options (heap, GC, code cache, font
  rendering). Filename is the Windows-specific form.
- **`idea.properties`** — PhpStorm runtime properties, tuned for large
  monorepos (bigger intellisense/content-load limits, dynamic classpath for
  long Windows classpaths, custom index/log paths, network timeouts, build
  parallelism).

## Install Locations

Drop the files into the per-version config directory for your platform. Both
files override IDE defaults on next start.

| OS      | Path                                                              |
| ------- | ----------------------------------------------------------------- |
| Windows | `%APPDATA%\JetBrains\PhpStorm<version>\`                          |
| macOS   | `~/Library/Application Support/JetBrains/PhpStorm<version>/`      |
| Linux   | `~/.config/JetBrains/PhpStorm<version>/`                          |

Replace `<version>` with the installed release, e.g. `PhpStorm2025.1`.

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
- Heap is sized 4 GB min / 16 GB max. Machines with <16 GB RAM should lower
  `-Xmx` before applying.
- `build.parallel.compilation.threads=8` assumes an 8+ core CPU. Adjust to
  match the target machine.
