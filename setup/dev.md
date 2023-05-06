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
git config --global user.name "thanhit95"
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
```

### Development environment - VS Code

Install extension: LaTeX Workshop by James Yu ([ref](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop))

#### Common settings

```text
"latex-workshop.latex.autoBuild.run": "never",
"latex-workshop.latex.watch.pdf.delay": 500,
```

When turn off `autoBuild` setting, I prefer hotkey `Ctrl + Alt + B` to build manually (defined in `@command:latex-workshop.build`)

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

Each time compiling, it produces some temporary files in the same `project_name` directory, which makes me confusing like this:

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

So I decide to change temporary directory by the setting:

```text
"latex-workshop.latex.outDir": "%DIR%/../ztmp_latex/%RELATIVE_DIR%"
```

where `%DIR%` refers to the absolute project directory path (`/home/me/Documents/project_name_A`) and `%RELATIVE_DIR%` refers to the name of project directory (`project_name_A`).

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
