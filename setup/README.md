# MY PERSONAL LINUX ENVIRONMENT SETUP

## DESCRIPTION

My personal Linux environment setup for a new computer. It might be useful for you.

Depend on each section, there are some specific files in this repo which guide you in detail.

&nbsp;

## CONTENT

### RIGHT AFTER OS SETUP

Update package information from Internet.

Ubuntu:

```shell
sudo apt update
```

Manjaro:

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

<https://github.com/BambooEngine/ibus-bamboo>

Goto system settings:

- Add ibus-bamboo to "input source".
- Config keyboard shortcut for switching between input sources.

&nbsp;

### KEYBOARD SHORTCUTS

Note: Goto system settings.

- Ctrl + Alt + T: terminal.
- Super + E: file manager (or home folder).
- Super + W: web browser.
- Super + T: text editor.
- Super + D: hide all windows.
- Super + I: system settings.
- Alt + Tab: switch between windows.
- Super + Tab: switch between applications.
- Super + Left: View split on left.
- Super + Right: View split on right.
- Super + Up: Maximize window.
- Alt + Space: Activate the window menu.

&nbsp;

### DESKTOP ENVIRONMENT AND THEME

Theme:

- Theme directory location:
  - Global: `/usr/share/themes`
  - Local: `~/.themes`

- Icon directory location:
  - Global: `/usr/share/icons`
  - Local: `~/.icons`

For GNOME: Execute app "Extensions" and config as my taste.

- Extension "Dash to Dock": Decrease size, make it transparent.

For XFCE:

To change font weight of theme, especial Thunar file manager, we need to edit or create file: `~/.config/gtk-3.0/gtk.css`.

```text
* { font-weight: 500; }
.thunar * { font-weight: 500 }
XfdesktopIconView.view { font-weight: 500 }
```

&nbsp;

### X11 COMPATIBILITY IN WAYLAND

A lot of apps that prefer running in X11 in the old days, so if they run in Wayland then some errors would occur.

To make X11 compatible in Wayland in system-wide settings:

- Edit `/etc/profile`
- Add `export GDK_BACKEND=x11`

If you use `zsh`, make sure `/etc/zsh/zprofile` gets source from `/etc/profile`.

Or, if you only want to make changes in user-wide settings:

- Edit `~/.profile`
- Add `export GDK_BACKEND=x11`

A note for the shell, make sure that:

- bash: `.bash_profile` gets source from `~/.profile`
- zsh: `.zprofile` gets source from `~/.profile`

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

Variety might not display its icon on topbar, to fix this:

- Make sure the GNOME extension "AppIndicator" was turned on.
- Run Variety with `GDK_BACKEND=x11`:
  - `GDK_BACKEND=x11 variety`, or
  - `env GDK_BACKEND=x11 variety`

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

GRAPHICS:

- GIMP.

AUDIO AND VIDEO:

- Player:
  - VLC media player
- Audio:
  - [Audacity](https://www.audacityteam.org)
  - [Kid3 Audio Tagger](https://kid3.kde.org/)
- Video:
  - [AviDemux](http://avidemux.sourceforge.net)
  - [MKVToolNix](https://mkvtoolnix.download)
  - Inviska MKV Extract
- Lib:
  - ffmpeg

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
- Nautilus context menu manager: filemanager-actions.

&nbsp;

### SHELL: ZSH

Read [zsh.md](zsh.md).

&nbsp;

### DEVELOPMENT LIBRARIES AND TOOLS

Read [dev.md](dev.md).

&nbsp;

### POST CONFIGURATION

- Web browser:
  - Home page: turn off unwanted things.
  - Languages ⟶ spell checking: turn off.

- File manager:
  - Note: If you use Nautilus, you should install `filemanager-actions`.
  - Add peazip to context menu.
  - Add VS Code to context menu.

- Manjaro:
  - Avoid frustrating when user enters incorrect password for many times.
    - First, have a look at the output from `cat /etc/pam.d/login` to make sure that you use `pam_faillock.so`.
    - Edit file `/etc/security/faillock.conf`
    - Set `deny = 0`
