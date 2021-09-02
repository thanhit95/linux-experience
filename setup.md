# MY PERSONAL LINUX ENVIRONMENT SETUP

## DESCRIPTION

My personal Linux environment setup for a new PC. It might be useful for you.

Depend on each section, there are some specific files in this repo which guide you in detail.

&nbsp;

## CONTENTS

### RIGHT AFTER OS SETUP

Update package information from Internet.

- Ubuntu:

```shell
sudo apt update
```

- Manjaro:

```shell
sudo pacman -Syy
```

&nbsp;

Adjust wrong time between Linux and Windows (dual boot).

```shell
timedatectl set-local-rtc 1 --adjust-system-clock
```

&nbsp;

Remove unwanted fonts:

- Noto suite.

&nbsp;

### VIETNAMESE INPUT

Chosen method: ibus-bamboo.

Follow instructions from this link:

<https://github.com/BambooEngine/ibus-bamboo>.

Goto system settings:

- Add ibus-bamboo to "input source".
- Config keyboard shortcut for switching between input sources.

&nbsp;

### KEYBOARD SHORTCUTS

Note: Goto system settings.

- Super + E: file manager (or home folder).
- Super + W: web browser.
- Super + D: hide all windows.
- Super + I: system settings.
- Alt + Tab: switch between windows (instead of the default way: switch between applications).

&nbsp;

### DESKTOP ENVIRONMENT AND THEME

Theme:

- Directory location:
  - Global: ```/usr/share/themes```
  - Local: ```~/.themes```

- Icons:
  - Global: ```/usr/share/icons```
  - Local: ```~/.icons```

For GNOME: Execute app "Extensions" and config as my taste.

- Extension "Dash to Dock": Decrease size, make it transparent.

For XFCE:

To change font weight of theme, especial Thunar file manager, we need to edit or create file: ```~/.config/gtk-3.0/gtk.css```.

```text
* { font-weight: 500; }
.thunar * { font-weight: 500 }
XfdesktopIconView.view { font-weight: 500 }
```

&nbsp;

### DESKTOP WALLPAPERS

App: Variety.

Homepage: <https://peterlevi.com/variety>.

**Notes for Manjaro GNOME:**

To run Variety correctly, we run it in terminal to see all output messages.

Before installing Variety, we must install its dependencies:

```shell
sudo pacman -S python-pip
```

&nbsp;

### MANJARO GNOME: FIX TOPBAR APPINDICATOR

In Manjaro GNOME, apps might not display its icon on topbar (such as Variety, caffeine).

Before fixing the issue, make sure the GNOME extension "AppIndicator" was turned on.

To fix this, for an example - Variety wallpaper changer, run it with an environment variable using this command:

```shell
GDK_BACKEND=x11 variety

or

env GDK_BACKEND=x11 variety
```

To add environment variable ```GDK_BACKEND``` permanently, please take a look at my note of environment variables. Basically, we add the variable in ```.bash_profile``` (bash) or ```.zprofile``` (zsh).

&nbsp;

### PACKAGES

INTERNET BROWSERS:

- Brave.
- Firefox.

FONTS:

- List of fonts:
  - Monospace: JetBrains Mono, Roboto Mono, Consolas.
  - Noto suite (to support multiple languages).
  - DejaVu suite (great display font).
  - Droid suite (to support multiple languages, a lightweight alternative of Noto suite).
  - Liberation suite (a "standard font suite" for many Linux distros).
  - Sans: Source Sans Pro.
  - Serif: Source Serif Pro.

- List of softwares:
  - gnome-font-viewer.
  - font-manager (<https://github.com/FontManager/font-manager>).

OFFICE:

- Libre Office.

MULTIMEDIA & GRAPHICS:

- VLC media player.
- GIMP.

UTILITIES:

- PDF reader: Okular, Evince.
- Photos: gThumb.
- System info: gnome-system-monitor, htop, neofetch.
- Archiver: peazip, unrar.
- Prevent computer from sleeping: caffeine.
- Remote desktop: AnyDesk.
- Screen recorder: OBS, vokoscreenNG.
- wine & winetricks.
- Clean disk: bleachbit.

&nbsp;

### SHELL: ZSH

Follow instructions from [setup-zsh.md](setup-zsh.md).

&nbsp;

### DEVELOPMENT LIBRARIES AND TOOLS

Read [setup-dev.md](setup-dev.md).

&nbsp;

### POST CONFIGURATION: FILE MANAGER

- Add peazip to context menu.
- Add VS Code to context menu.
