# Undergraduate Ghidra Python examples

Two short, read-only examples for running Python 3 inside Ghidra.

| File | Contains | Purpose |
|---|---|---|
| [HelloGhidra.zip](HelloGhidra.zip) | `HelloGhidra.py` | Prints the Python runtime and current program name to confirm the scripting setup. |
| [WindowsApiPreview.zip](WindowsApiPreview.zip) | `WindowsApiPreview.py` | Prints up to five recognized imported API/external-function symbols, their DLL/library names, and their Ghidra external-symbol locations. |

**Password for both ZIP files: `infected`**

These archives contain Python examples, not PMA binaries. The scripts do not
execute the program being analyzed or change its bytes. An imported symbol is
static evidence, not proof that an API call executed. An external-symbol location
is not an instruction address or raw file offset.

## Download and extract

1. Open a ZIP link above and use GitHub's **Download raw file** control to save the
   actual archive. Do not save the GitHub web page as a ZIP.
2. Extract the archive with 7-Zip or another compatible archive tool, using password
   `infected`.
3. Put the extracted `.py` files in a writable script folder in your course analysis VM.
   Extract the ZIP first; Script Manager runs the Python file, not the ZIP.

## Run in Ghidra

The examples target **Ghidra 12.1.4, JDK 21, and CPython 3 through PyGhidra**.
The course installation walkthrough covers missing prerequisites. A terminal
Python installation alone does not configure Ghidra's Python scripting provider.

1. Start the approved Ghidra installation in PyGhidra mode:
   - **Linux:** `<GhidraInstall>/support/pyghidraRun`
   - **Windows:** `<GhidraInstall>\support\pyghidraRun.bat`
2. Open an approved imported program in **CodeBrowser** and let the intended
   static analysis finish.
3. Choose **Window → Script Manager**.
4. Use **Script Directories / Bundle Manager** to add and enable the folder holding
   the extracted `.py` files, then use **Refresh Script List**.
5. Find the scripts under **Undergraduate → Examples**, or select **Scripts** and
   filter by filename. Keep `# @runtime PyGhidra` in each script's header.
6. Run **HelloGhidra.py** first. Open **Window → Console** and confirm CPython 3
   and the actual open program name.
7. Run **WindowsApiPreview.py**. Compare a displayed API name, library, and
   external-symbol location with Ghidra's external symbols. Fewer than five results
   can be legitimate if fewer external functions are recognized.

If no program is open, the scripts print an explanatory message. If Python 3 syntax
fails, check that you selected PyGhidra rather than legacy Jython. If a script is
missing, check the folder's Enable setting, filename, category/filter, and refresh.

## How these examples support the project

Use them as attributed starter examples and explain any adaptations. They are not
a complete project solution. The full undergraduate project requires your own tool
covering all three categories: Windows API-use evidence, defined strings, and
recognized functions, with validation and a chronological AI-prompting history.
Use the designated existing PMA lab copies for static analysis only; no PMA files
are supplied in this folder.
