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

Search for and check config "Files: Trim Trailing Whitespace"; Or edit config json file:

```text
"files.trimTrailingWhitespace": true
```

#### Config: Title Bar Custom Style

Goto File ⟶ Preferences ⟶ Settings ⟶ User Settings.

Config: `Window: Title Bar Style` ⟶ Set value = `native`

#### Config: Smooth scrolling

Goto File ⟶ Preferences ⟶ Settings ⟶ User Settings.

Config name: `Workbench ⟶ List: Smooth Scrolling`

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
    - Dracula Theme - Dracula Official
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

### NetBeans

Edit file `netbeans-XX/netbeans/etc/netbeans.conf` where `netbeans-XX` is installed NetBeans directory. Add options into `netbeans_default_options`:

- To change font size: `-J-Dawt.useSystemAAFontSettings=on --fontsize 14`
- Other options: `-J-Dsun.java2d.dpiaware=false -J-Dsun.java2d.uiScale=1`

Menu Tools ⟶ Options

- Editor ⟶ Formatting:
  - Language: All Languages
  - Tab size: 4
- Editor ⟶ On Save:
  - Language: All Languages
  - Reformat: All Lines
  - Remove Trailing Whitespace From: All Lines
- Fonts & Colors:
  - Font: JetBrains Mono 16
- Appearance:
  - Document Tabs: Enable Multi-row tabs: Max row count: 2

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

&nbsp;

### git

```shell
git config --global user.email "you@example.com"
git config --global user.name "thanhit95"
```
