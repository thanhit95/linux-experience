# DEVELOPMENT LIBRARIES AND TOOLS

## LIBRARIES AND SDKs

### C++

#### Ubuntu

```shell
sudo apt install gcc g++ gdb make
```

Extra libs:

```shell
sudo apt install libboost-all-dev
sudo apt install libpoco-dev
```

&nbsp;

#### Manjaro

```shell
sudo pacman -S gcc gdb make
```

&nbsp;

### JAVA

Update later.

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

#### Config: Editor font and terminal font

&nbsp;

#### Extensions

- Markdown:
  - yzhang - Markdown All in One.
  - shd101wyy - Markdown Preview Enhanced.
  - David Anson - markdownlint.
- Front-end:
  - ritwickdey - Live Server.
  - ms-vscode - Live Preview.
- Miscellaneous:
  - ms-vscode - Hex Editor.

&nbsp;

### Eclipse

Goto menu Windows ⟶ Preferences:

- General ⟶ Appearance ⟶ Colors and Fonts
- Java ⟶ Code Style ⟶ Formatter
  - Tab policy: Spaces only
  - Indentation size: 4
  - Tab size: 4
- Java ⟶ Editor ⟶ Save Actions
  - Check "Additional actions".
  - Click on button "Configure..."
    - Code Organizing ⟶ Formatter: Check "Remove trailing whitespace".
