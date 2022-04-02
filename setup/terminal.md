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
  - Split tab vertical: Ctrl + Alt + R
  - Split tab horizontal: Ctrl + Alt + D
  - Close terminal: Ctr + Shift + X
  - Focus terminal above: Alt + Up
  - Focus terminal below: Alt + Down
  - Focus terminal on the left: Alt + Left
  - Focus terminal on the right: Alt + Right
  - Move the terminal split handle right: Ctrl + Shift + Right
  - Move the terminal split handle left: Ctrl + Shift + Left
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
  - Toggle transparency: Ctrl + Alt + O

### Nautilus context menu

Menu name: Open in Guake

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

### Nautilus context menu

Menu name: Open in Guake

- Command: `tilix`
- Command parameters: `-w '%f'`
