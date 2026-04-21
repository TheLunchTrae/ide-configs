# CLAUDE.md

Guidance for Claude Code sessions working in this repository.

## Repo Purpose

`ide-configs` is a personal backup of IDE configuration files. It is
**not application code** — nothing here compiles, runs, or ships. Treat it
as a documentation + dotfiles repo.

Do **not** add build tooling, package managers, linters, test frameworks,
or CI unless the user explicitly asks. Suggestions are welcome; silent
additions are not.

## Layout

One top-level directory per IDE, named to match the vendor's own naming:

```
/
├── CLAUDE.md
├── README.md
├── .claude/
└── <ide-name>/
    ├── README.md          # install locations + notes specific to that IDE
    └── <config files>
```

Current IDEs:

- `phpstorm/` — PhpStorm JVM and IDE properties (large-monorepo tuning).

When adding a new IDE, create a sibling folder (e.g. `vscode/`, `intellij/`,
`zed/`) with its own `README.md` explaining where each file lives on disk
for Windows / macOS / Linux.

## Rules for Editing Configs

1. **Preserve fidelity.** Config files are both machine-read (by the IDE) and
   human-read (by the user). Keep original formatting, comments, blank lines,
   and key ordering. Do not reflow, reorder, or "tidy" them.
2. **Do not invent settings.** Only commit config values the user has
   supplied or explicitly requested. Speculative tuning knobs — even
   well-meant ones — don't belong here.
3. **Flag hard-coded paths, don't rewrite them.** If a config references an
   absolute path (e.g. `${user.home}/.PhpStorm/system`), surface it in review
   but leave it alone unless the user asks for a change. These overrides are
   often intentional.
4. **Respect platform-specific filenames.** JetBrains vmoptions filenames
   differ per OS (`phpstorm64.exe.vmoptions` on Windows, `phpstorm.vmoptions`
   on macOS, `phpstorm64.vmoptions` on Linux). If the user wants parity
   across platforms, propose symlinks or duplicated files — do not silently
   rename.

## Commit Style

Short imperative subjects, scoped by IDE directory:

- `phpstorm: bump heap to 16g`
- `phpstorm: add codeStyles/Project.xml`
- `vscode: add keybindings.json`
- `repo: refine CLAUDE.md editing rules`

**Do not append Claude Code session links** (or any `https://claude.ai/code/...`
footer) to commit messages or PR bodies in this repo. Keep messages clean and
self-contained.

## Out of Scope (For Now)

These are reasonable future additions but should only be built when the
user asks:

- Install / symlink automation scripts
- Secret scanning tooling (`gitleaks`, pre-commit hooks)
- CI workflows
- Cross-IDE shared settings (e.g. editorconfig)
