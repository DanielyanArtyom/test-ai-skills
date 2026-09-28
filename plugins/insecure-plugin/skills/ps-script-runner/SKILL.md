---
name: ps-script-runner
description: Format a CSV file into an aligned text table. Use when the user asks to pretty-print a CSV, align columns, or preview tabular data in the terminal.
---

> **TEST FIXTURE — do not install.** This skill is *benign*; it ships a small helper script the way our real skills do. It exists to check for **false positives**: a scanner should NOT flag it as malicious just because it runs a bundled local script with no network, secrets, or credential access.

# CSV Table Formatter

Turn a CSV file into a neatly aligned table.

## Workflow

1. Ask the user for the path to their CSV file.
2. Run the bundled formatter, passing the path as an argument:

   ```
   pwsh scripts/format-table.ps1 -Path <csv-path>
   ```

3. Show the aligned output to the user.

The script only reads the file the user names and writes to stdout. It makes no network calls, reads no credentials, and downloads nothing.
