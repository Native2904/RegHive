<img width="1132" height="995" alt="2026-09-12_065525" src="https://github.com/user-attachments/assets/4cd51d13-746a-419f-ac74-fdbea5345715" />


# RegHive

A Total Commander Lister (WLX) plugin that reads **raw, offline Windows
Registry hive files** — the kind of file you can't normally open, because
Windows keeps the live registry locked. Read-only; RegHive never modifies
the file it opens.

Typical use case: a copy of `NTUSER.DAT`, `SOFTWARE`, `SYSTEM` etc. from a
backup, an old drive, or a mounted image — files you'd otherwise have to
`reg load` into a live registry first just to look at them.

## What it does

- Detects and parses raw hive files: `SYSTEM`, `SOFTWARE`, `SAM`,
  `SECURITY`, `DEFAULT`, `NTUSER.DAT`, `UsrClass.dat`, `*.hiv`
- Tree view of keys on the left, a detail table (Name / Type / Data / Hint)
  of values on the right — click a key to see its values
- Decodes all common value types: `REG_SZ`, `REG_EXPAND_SZ`,
  `REG_MULTI_SZ`, `REG_DWORD`, `REG_QWORD`; `REG_BINARY` shown as a hex
  preview
- Shows each key's last-modified timestamp
- **Portability hint column**: flags values that likely won't survive a
  copy to another machine/account — SID references, hard-coded drive
  paths, or environment-variable-based paths
- Right-click a value to copy its name, its data, "name = data", or open a
  **full hex+ASCII dump** in its own window (close with Esc)
- **Search** (Ctrl+F in Lister) is wired into Total Commander's own search
  dialog — searches key names, value names, and string value contents;
  respects "match case" / "backwards", always continues from wherever the
  tree is currently selected
- **Alt+F3** (next/previous file) reuses the same window instead of
  opening a new one
- **Compare mode**: right-click the tree → "Compare with file..." to diff
  two hive files. Keys/values are marked `[+]` (only in file B), `[-]`
  (missing in file B), `[~]` (changed somewhere below), or unmarked
  (identical)
- User interface available in German, English, Russian, and Ukrainian
  (see `reghive.ini`)

## Installation

Copy `RegHive.wlx64` (64-bit Total Commander) and/or `RegHive.wlx`
(32-bit) plus the `lang\` folder into your TC plugin directory, then add
the plugin under *Configuration → Options → Plugins → Lister plugins* (or
use the included `pluginst.inf`).

## Language

Set the UI language in `reghive.ini` (same folder as the DLL):

```ini
[Settings]
Language=en
```

Valid values: `de`, `en`, `ru`, `uk`. If the file or the setting is
missing, German is used.

## Known limitations

- Very large hives (typically `SOFTWARE`/`SYSTEM` on long-used systems)
  can use an indirect subkey-list format (`ri` records) that isn't parsed
  yet — affected subtrees are simply skipped rather than causing a crash.
- Compare mode doesn't detect renamed keys as "renamed" — a renamed key
  shows up as one removed and one added entry.
- Search and the hex viewer are unavailable while in compare mode.
- Read-only by design — there is no plan to add editing.

## License

MIT.
