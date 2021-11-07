# SETUP: DEVELOPMENT LIBRARIES AND TOOLS

## LIBRARIES AND SOFTWARE DEVELOPMENT KITS

### C++

#### Ubuntu

```shell
sudo apt install gcc g++ gdb make
# or
sudo apt install build-essential
```

#### Manjaro

```shell
sudo pacman -S gcc gdb make
```

#### General

Extra libs:

```text
libboost-all-dev
libpoco-dev
```

&nbsp;

### JAVA

Read [dev-java.md](dev-java.md).

---

## TOOLS

### Visual Studio Code

#### Config: Remove trailing whitespace on save

Goto File ⟶ Preferences ⟶ Settings ⟶ User Settings.

Search for and check config "Files: Trim Trailing Whitespace".

Or edit config json file:

```text
"files.trimTrailingWhitespace": true
```

#### Config: Keyboard Shortcuts

- Editor Font Zoom In: <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>=</kbd>
- Editor Font Zoom Out: <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>-</kbd>
- Editor Font Zoom Reset: <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>0</kbd>

#### Extensions

- Theme:
  - Color Theme:
    - teabyii - Ayu
    - binaryify - One Dark Pro
    - Mahmoud Ali - Atom One Dark Theme
    - yomed - Dracula Soft Syntax Theme
  - Icon Theme:
    - Philipp Kief - Material Icon Theme
- Markdown:
  - yzhang - Markdown All in One
  - shd101wyy - Markdown Preview Enhanced
  - David Anson - markdownlint
- Web:
  - ritwickdey - Live Server
  - ms-vscode - Live Preview
- Miscellaneous:
  - ms-vscode - Hex Editor
  - trybick - Terminal Zoom
  - MoshFeu - Compare Folders
  - tomoki1207 - vscode-pdf

#### Miscellaneous config

- Editor font and terminal font.

- Extensions: markdownlint:

Disable "MD024: Multiple headings with the same content" by editing the `settings.json` file:

```json
"markdownlint.config": {
    "MD024": false
}
```

&nbsp;

### Eclipse

Goto menu Windows ⟶ Preferences:

- General ⟶ Appearance ⟶ Colors and Fonts
- General ⟶ Editors ⟶ Text Editors ⟶ Spelling
- Java ⟶ Code Style ⟶ Formatter
  - Tab policy: Spaces only
  - Indentation size: 4
  - Tab size: 4
- Java ⟶ Editor ⟶ Save Actions
  - Check "Additional actions".
  - Click on button "Configure..."
    - Code Organizing ⟶ Formatter: Check "Remove trailing whitespace".
