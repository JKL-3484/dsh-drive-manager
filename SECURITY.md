# Security Notes

`dsh-drive-manager` is a read-only disk dashboard for Windows. This file is intended for the dsh.so security scanner and manual reviewers.

## Network

- The plugin has **no outbound network requests**.
- It does not fetch, upload, or submit disk contents.
- HTTP routes are local DSH routes (`/api/drive-manager/*`) used by the panel.

## File access

- Reads directory names, file sizes, modification times, and known configuration files (`Preferences`, `libraryfolders.vdf`, registry download paths).
- Does **not** read file contents.
- Does **not** delete, move, rename, or write files in scanned directories.
- Custom top-level directories are listed by name only; their contents are not recursively sized.

## Subprocesses

- `powershell.exe` is used only for `Get-CimInstance Win32_LogicalDisk` to enumerate fixed drives.
- `reg.exe` is used only for `reg query` of download/Steam paths.
- `explorer.exe` is spawned only when the user clicks “在资源管理器中打开”; it opens the selected folder and does not execute scanned files.

## Destructive operations

There is no `fs.rm`, `unlink`, `rmdir`, `Remove-Item`, or delete endpoint. Green items are instructions for the user; the plugin does not clean anything automatically.

## Secrets

No API keys, tokens, passwords, or credentials are stored in this repository.

## Reporting

Please open an issue at <https://github.com/JKL-3484/dsh-drive-manager/issues>.
