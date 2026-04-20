# Rider

Backups of JetBrains Rider JVM and IDE-level configuration. Based on the
`phpstorm/` config — same tuning, adapted for Rider paths and filenames.

Captured against **Rider 2026.1** on **Windows 11 64-bit**.

## Files

- **`rider64.exe.vmoptions`** — JVM options (heap, GC, code cache, font
  rendering). Filename is the Windows-specific form.
- **`idea.properties`** — Rider runtime properties, tuned for large
  monorepos (bigger intellisense/content-load limits, dynamic classpath for
  long Windows classpaths, custom index/log paths, network timeouts, build
  parallelism).

## Install Locations

Drop the files into the per-version config directory for your platform. Both
files override IDE defaults on next start.

| OS      | Path                                                           |
| ------- | -------------------------------------------------------------- |
| Windows | `%APPDATA%\JetBrains\Rider<version>\`                          |
| macOS   | `~/Library/Application Support/JetBrains/Rider<version>/`      |
| Linux   | `~/.config/JetBrains/Rider<version>/`                          |

Replace `<version>` with the installed release, e.g. `Rider2026.1`.

You can also open these from inside Rider via
**Help → Edit Custom VM Options…** and **Help → Edit Custom Properties…** —
the IDE will create the files in the right place for you.

## Platform-Specific vmoptions Filename

The vmoptions filename varies by OS. If you want the same JVM tuning
cross-platform, rename/duplicate as needed:

| OS      | Filename                 |
| ------- | ------------------------ |
| Windows | `rider64.exe.vmoptions`  |
| macOS   | `rider.vmoptions`        |
| Linux   | `rider64.vmoptions`      |

Two lines in this vmoptions file are Windows-only and should be dropped from
macOS/Linux copies:

- `-Dsun.awt.keepWorkingSetOnMinimize=true`
- `-Dawt.useSystemAAFontSettings=lcd` (Windows subpixel AA; macOS ignores,
  Linux depends on fontconfig)

The `ide.win.frame.decoration=true` line in `idea.properties` is likewise
Windows-only and harmless elsewhere.

## Notes

- Rider 2020.2+ **merges** this vmoptions file with the bundled defaults,
  so only overrides need to live here — don't "restore" defaults that look
  missing.
- `idea.properties` sets `idea.system.path` and `idea.log.path` to
  `${user.home}/.Rider/system` and `${user.home}/.Rider/log`. This moves
  caches and logs **out of** the default JetBrains location — intentional,
  but handy to remember when debugging "where did my indexes go?"
- Heap is sized 4 GB min / 16 GB max. Machines with <16 GB RAM should lower
  `-Xmx` before applying. Large .NET solutions often benefit from the
  higher max.
