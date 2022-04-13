# SETUP: TERMINAL EMULATORS

## GUAKE

### Install

```shell
sudo pacman -S guake
```

### Config

Config shortcut in System Settings ⟶ Keyboard:

- Command: `guake -t`
- Shortcut: Alt + Esc

Config General:

- Start Guake at login

Config Main Window:

- Geometry: Increase height

Config Shortcuts:

- General
  - Toggle visibility: (blank)
  - Search terminal: Ctrl + Shift + F
- Split management
  - Split tab vertical: Ctrl + Shift + P
  - Split tab horizontal: Ctrl + Shift + O
  - Close terminal: Ctr + Shift + X
  - Focus terminal on the left/right/above/below: Ctrl + Shift + [Left/Right/Up/Down]
  - Move the terminal split handle left/right: Ctrl + Alt + [Left/Right]
- Navigation
  - Go to previous tab: Ctrl + Page Up
  - Go to next tab: Ctrl + Page Down
  - Move current tab left: (blank)
  - Move current tab right: (blank)
- Appearance
  - Increase height: Ctrl + Alt + .
  - Decrease height: Ctrl + Alt + ,
  - Increase transparency: Ctrl + Alt + L
  - Decrease transparency: Ctrl + Alt + K
  - Toggle transparency: Ctrl + Alt + ;
  - Zoom in: Ctrl + = (or Ctrl + =)
  - Zoom out: Ctrl + -

### Nautilus context menu

Menu name: Open Guake here

- Command: `guake`
- Command parameters: `--show -n 'NewTab' -e 'cd %f'`

&nbsp;

## TILIX

### Install

```shell
sudo pacman -S tilix
```

### Config

Config shortcut in System Settings ⟶ Keyboard:

- Command: `tilix`
- Shortcut: Ctrl + Esc

Config shortcuts: The same as Guake's shortcuts

### Nautilus context menu

Menu name: Open Tilix here

- Command: `tilix`
- Command parameters: `-w '%f'`