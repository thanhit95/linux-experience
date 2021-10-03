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
# choose the best system mirrorlist
sudo pacman-mirrors --fasttrack
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
- Adobe Source Han.
- Terminus.

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
- Super + T: text editor (mousepad).
- Super + Y: text editor (gedit).
- Ctrl + Shift + Esc: launch system monitor.
- Super + D: hide all windows.
- Super + I: system settings.
- Alt + Tab: switch between windows.
- Super + Tab: switch between applications.
- Super + Left: view split on left.
- Super + Right: view split on right.
- Super + Up: maximize window.
- Alt + Space: activate the window menu.

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

To change font weight of GTK theme, especial file manager, we need to edit or create file: `~/.config/gtk-3.0/gtk.css`.

```text
* { font-weight: 500; }
.nautilus * { font-weight: 500 }
.thunar * { font-weight: 500 }
XfdesktopIconView.view { font-weight: 500 }
```

&nbsp;

### X11 COMPATIBILITY IN WAYLAND

Read [x11-compatibility-in-wayland.md](/article/x11-compatibility-in-wayland.md).

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

- Chrome.
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

DISK DRIVE:

- GParted
- baobab (Disk Usage Analyzer)

UTILITIES:

- PDF reader: Okular, Evince
- Photos: Eye of Gnome (eog), gThumb
- System info: gnome-system-monitor, htop, neofetch
- Archiver: peazip, unrar
- Prevent computer from sleeping: caffeine
- Remote desktop: AnyDesk
- Screen recorder: OBS, vokoscreenNG
- wine & winetricks
- Clean disk: bleachbit
- Nautilus context menu manager: filemanager-actions
- Locate file fast: mlocate
  - Run command: `locate file-name`
  - Note: `sudo updatedb` first

&nbsp;

### SHELL: ZSH

Read [zsh.md](zsh.md).

&nbsp;

### DEVELOPMENT LIBRARIES AND TOOLS

Read [dev.md](dev.md).

&nbsp;

### POST CONFIGURATION

- Manjaro:
  - Avoid frustrating when user enters incorrect password for many times.
    - First, have a look at the output from `cat /etc/pam.d/login` to make sure that you use `pam_faillock.so`.
    - Edit file `/etc/security/faillock.conf`
    - Set `deny = 0`

- Set default apps:
  - Web: Chrome
  - Music, Video: VLC media player
  - Photos: Eye of Gnome (Image Viewer)
  - Text Editor: mousepad (command: `xdg-mime default org.xfce.mousepad.desktop text/plain`)

- Web browser:
  - Home page: turn off unwanted things.
  - Languages ⟶ spell checking: turn off.

- File manager:
  - Note: If you use Nautilus, you should install `filemanager-actions`.
  - Add peazip to context menu.
  - Add VS Code to context menu.
    - `filemanager-actions` command:
      - Path: `code`
      - Param: `%B`

- Libre Office:
  - Disable spell checking (Tools ⟶ Automatic Spell Checking).
