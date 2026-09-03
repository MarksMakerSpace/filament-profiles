# Slicer print logger

A post-processing script for Bambu Studio, OrcaSlicer, PrusaSlicer and other PrusaSlicer-based slicers. When you slice (Bambu Studio) or export G-code (the others), it asks "Log this print?" and, if you say yes, opens your browser on [3D Filament Profiles](https://3dfilamentprofiles.com) with the print already filled in. Pick which spool each filament came from, click Subtract, done. The weight comes off your spool and the print shows up in your print history.

It replaces the manual "drop the sliced file on My Print" step. Same result, no drag and drop.

Help page with screenshots: <https://3dfilamentprofiles.com/help/automatic-print-logging>

## What it needs

Two versions of the script do the same thing. Pick one:

- **Windows: `3dfp-print-log.ps1`.** Runs on the PowerShell that is already on every Windows PC. Nothing to install.
- **macOS, Linux, or Python on Windows: `3dfp-print-log.py`.** Needs Python 3 (3.8 or newer). Windows: [python.org](https://www.python.org/downloads/). macOS: `python3` in a terminal will offer to install it. Linux: you already have it.

No extra packages either way. Both scripts only use what ships with the system.

## Install

1. Download the script and put it somewhere permanent (not Downloads):
   - Windows: [`3dfp-print-log.ps1`](https://raw.githubusercontent.com/MarksMakerSpace/filament-profiles/main/tools/slicer-print-log/3dfp-print-log.ps1)
   - macOS / Linux / Python on Windows: [`3dfp-print-log.py`](https://raw.githubusercontent.com/MarksMakerSpace/filament-profiles/main/tools/slicer-print-log/3dfp-print-log.py)
2. In your slicer, open the print settings and find the post-processing scripts box:
   - Bambu Studio / OrcaSlicer: Print Settings, Others, Post-processing scripts
   - PrusaSlicer: Print Settings, Output options, Post-processing scripts
3. Add one line, quoting both paths.

   Windows (PowerShell). This path is the same on every Windows install:

   ```
   "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -ExecutionPolicy Bypass -File "C:\Users\you\3dfp\3dfp-print-log.ps1"
   ```

   Windows (Python). The slicer needs the real `python.exe`. Plain `py` or `python` will not work here: since Python 3.11 the `py` launcher is an app alias, not a file. The folder name changes with each Python version, so get the exact path by running this in a terminal and paste what it prints:

   ```
   py -c "import sys; print(sys.executable)"
   ```

   ```
   "C:\Users\you\AppData\Local\Python\pythoncore-3.14-64\python.exe" "C:\Users\you\3dfp\3dfp-print-log.py"
   ```

   macOS / Linux:

   ```
   "/usr/bin/python3" "/Users/you/3dfp/3dfp-print-log.py"
   ```

   Not sure where Python is on macOS or Linux? Run `which python3` in a terminal.

4. Slice a plate. A small dialog asks whether to log it. Click Log it and your browser opens. If you're not signed in it asks you to log in first, then brings you straight back.

## Options

Options go after the script path on the same line, for example `"python3" "3dfp-print-log.py" --no-ask` or `... -File "3dfp-print-log.ps1" --no-ask`. Both scripts take the same options.

| Option | What it does |
| --- | --- |
| `--no-ask` | Skip the "Log this print?" dialog and always open the browser |
| `--dry-run` | Print the URL instead of opening the browser (handy for testing from a terminal) |
| `--debug` | Write what the slicer passed us (arguments, environment, G-code header) to `~/3dfp-print-log-debug.txt` |
| `--base-url URL` | Send to a different site (development / staging) |

## When does it run?

- **Bambu Studio 2.x** runs post-processing scripts as soon as a plate finishes slicing, so you get the dialog on every slice, including before Send to Printer. Say Skip on the ones you don't print.
- **Older Bambu Studio** only ran them on File, Export, Export G-code, not on Send or on the sliced .3mf export.
- **OrcaSlicer** runs them on export; some versions don't run them on Send. If nothing happens on Send, use Export G-code.
- **PrusaSlicer** runs them on export.

## What gets sent

Only a handful of comment lines the slicer already writes into the G-code header, plus the same values it exposes as `SLIC3R_*` environment variables: filament type, brand, colour and profile name, printer model, slicer version, grams and length used, and print time. In Bambu Studio it also reads the project (3MF) file name and, when available, the plate number from Bambu Studio's own temp folder.

No toolpaths, no model geometry, nothing else from the G-code. The data goes into the URL that opens in your browser; nothing is uploaded until you click Subtract on the site.

## Bugs and ideas

Open an issue in this repo. Include the output of a `--debug` run if it's about a specific slicer or file.
