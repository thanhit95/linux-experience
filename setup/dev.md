# SETUP: DEVELOPMENT LIBRARIES AND TOOLS

## LIBRARIES AND SOFTWARE DEVELOPMENT KITS

### C/C++

```shell
# FEDORA
sudo dnf groupinstall c-development
# or with additional tools
sudo dnf groupinstall c-development development-tools


# UBUNTU
sudo apt install gcc g++ gdb make
# or
sudo apt install build-essential


# MANJARO
sudo pacman -S gcc gdb make
# or
sudo pacman -S --needed base-devel
```

Extra libs: `libboost-all-dev libpoco-dev`

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

- Go back: <kbd>Alt</kbd> + <kbd>Left</kbd>
- Go forward: <kbd>Alt</kbd> + <kbd>Right</kbd>
- Editor Font Zoom In: <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>=</kbd>
- Editor Font Zoom Out: <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>-</kbd>
- Editor Font Zoom Reset: <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>0</kbd>
- editor.action.transformToLowercase: <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>L</kbd>
- editor.action.transformToUppercase: <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>U</kbd>
- cursorHome: <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>PageUp</kbd>
- cursorEnd: <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>PageDown</kbd>

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
  - shd101wyy (Yiyi Wang) - Markdown Preview Enhanced
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

- To change font size:
  - `-J-Dawt.useSystemAAFontSettings=on` or `-J-Dawt.useSystemAAFontSettings=lcd`
  - `--fontsize 14`
  - `-J-Dswing.aatext=true`
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
git config --global user.name "thanh"

# Exist 2 files: ed25519_git and ed25519_git.pub
ssh-add $HOME/.ssh/ed25519_git
# Double check by these 2 commands:
ssh-add -L
ssh -vT git@github.com
# Output:
# Server accepts key: you@example.com ED25519 SHA256:dasduiasdyuas/dwdsa/dasodasdasuhddfsahiudhasui agent
# Authenticated to github.com ([30.210.277.104]:22) using "publickey"
```

---

## LATEX

### Base packages

Ubuntu

```shell
sudo apt install texlive-full
```

Manjaro

```shell
sudo pacman -S texlive-most texlive-bin
# Choose packages: texlive-core,texlive-fontsextra,texlive-formatsextra,texlive-bibtexextra,texlive-latexextra,texlive-pictures,texlive-publishers,texlive-science
```

### Development environment - VS Code

Install extension: LaTeX Workshop by James Yu ([ref](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop))

The reason is that I find out that `VS Code with LaTeX Workshop` provides me with a great tool that has rich features such as auto-complete, auto-build, preview in real time, modern user interface, syntax highlighting, and more.

#### Common settings

```text
"latex-workshop.latex.autoBuild.run": "never",
"latex-workshop.latex.watch.pdf.delay": 500,
```

When turning off `autoBuild` setting, I prefer the hotkey `Ctrl + Alt + B` to build manually (defined in `@command:latex-workshop.build`)

#### Settings: Temporary output directories

Here is my working latex directories:

```text
├── project_name_A
│   └── main.tex
├── project_name_B
│   └── main.tex
└── project_name_C
    ├── main.tex
    ├── chapter1.tex
    ├── chapter2.tex
    └── img
        ├── img1.jpg
        └── img2.svg
```

Each time the tool compiles, it produces some temporary files in the same `project_name` directory, which makes me confused like this:

```text
└── project_name_A
    ├── main.tex
    ├── main.aux
    ├── main.fdb_latexmk
    ├── main.fls
    ├── main.log
    ├── main.pdf
    └── main.synctex.gz
```

So I decide to change the temporary directory by setting:

```text
"latex-workshop.latex.outDir": "%DIR%/../ztmp_latex/%RELATIVE_DIR%"
```

where `%DIR%` refers to the absolute project directory path (`/home/me/Documents/project_name_A`) and `%RELATIVE_DIR%` refers to the name of the project directory (`project_name_A`).

The final project directory template should be:

```text
├── project_name_A
│   └── main.tex
├── project_name_B
│   └── main.tex
├── project_name_C
│   ├── main.tex
│   ├── chapter1.tex
│   ├── chapter2.tex
│   └── img
│       ├── img1.jpg
│       └── img2.svg
└── ztmp_latex
    ├── project_name_A
    │   ├── main.aux
    │   ├── ...
    │   └── main.pdf
    ├── project_name_B
    │   ├── main.aux
    │   ├── ...
    │   └── main.pdf
    └── project_name_C
        ├── main.aux
        ├── ...
        └── main.pdf
```

#### Settings: Extra

Add argument `--shell-escape` in case compiling with svg images.

```text
"latex-workshop.latex.tools": [
  {
      "name": "latexmk",
      "command": "latexmk",
      "args": [
          "--shell-escape",
          "-synctex=1",
          "-interaction=nonstopmode",
          "-file-line-error",
          "-pdf",
          "-outdir=%OUTDIR%",
          "%DOC%"
      ],
      "env": {}
  },
  ...
]
```
