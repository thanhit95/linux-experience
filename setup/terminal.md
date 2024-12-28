# SETUP: TERMINAL EMULATORS

## GUAKE

### Install

```shell
# UBUNTU
sudo dnf install guake

# MANJARO
sudo pacman -S guake
```

### Config

Hotkey in System Settings ⟶ Keyboard:

- Command: `guake -t`
- Shortcut: Alt + Esc

Startup:

- Start Guake at login

Configurations (Preferences):

- Main Window:
  - Geometry: Increase height

- Keyboard shortcuts:
  - General
    - Toggle visibility: (blank)
    - Search terminal: Ctrl + Shift + F
  - Tab management:
    - New tab (or new session): Ctrl + Shift + T
    - Close tab (or close session): Ctrl + Shift + W
  - Split management
    - Split tab vertical: Ctrl + Shift + P
    - Split tab horizontal: Ctrl + Shift + O
    - Close terminal: Ctr + Shift + X
    - Focus terminal on the left/right/above/below: Ctrl + Shift + [Left/Right/Up/Down]
    - Move the terminal split handle left/right/up/down: Alt + Shift + [Left/Right/Up/Down]
  - Navigation
    - Go to previous tab (or previous session): Ctrl + Page Up
    - Go to next tab (or next session): Ctrl + Page Down / Ctrl + Tab
    - Move current tab left: (blank)
    - Move current tab right: (blank)
    - Page down: Shift + Page Down
    - Page up: Shift + Page Up
    - Scroll down: Page Down
    - Scroll up: Page Up
  - Appearance
    - Increase height: Ctrl + Alt + .
    - Decrease height: Ctrl + Alt + ,
    - Increase transparency: Ctrl + Alt + L
    - Decrease transparency: Ctrl + Alt + K
    - Toggle transparency: Ctrl + Alt + ;
    - Zoom in: Ctrl + = (or Ctrl + =)
    - Zoom out: Ctrl + -

- Apperance:
  - (Color theme) Built-in scheme: Highway or Dimmed Monokai or Harper

### Nautilus context menu

Menu name: Open Guake here

- Command: `guake`
- Command parameters: `--show -n 'NewTab' -e 'cd %f'`

&nbsp;

## TILIX

### Install

```shell
# UBUNTU
sudo dnf install tilix

# MANJARO
sudo pacman -S tilix
```

### Troubleshooting

If Tilix shows error related to configs when we open it:

- Make a symlink: `ln -s /etc/profile.d/vte-2.91.sh /etc/profile.d/vte.sh`
- Add source to bashrc / zshrc:

```text
if [ $TILIX_ID ] || [ $VTE_VERSION ]; then
    source /etc/profile.d/vte.sh
fi
```

### Config

Hotkey in System Settings ⟶ Keyboard:

- Command: `tilix`
- Shortcut: Ctrl + Esc

Configurations (Preferences):

- The same as Guake's shortcuts
- Apperance:
  - Color theme: Orchis

&nbsp;

## MISCELLANEOUS

- Terminal size: 100 (width) x 30 (height)

- New terminal in GNOME: command `ptyxis`
