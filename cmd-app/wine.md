# WINE

## WHAT IS WINE?

> Wine (originally an acronym for "Wine Is Not an Emulator") is a compatibility layer capable of running Windows applications on several POSIX-compliant operating systems, such as Linux, macOS, & BSD. Instead of simulating internal Windows logic like a virtual machine or emulator, Wine translates Windows API calls into POSIX calls on-the-fly, eliminating the performance and memory penalties of other methods and allowing you to cleanly integrate Windows applications into your desktop.

&nbsp;

## INSTALLATION

### Ubuntu

`sudo apt install wine64`

Also install or download winetricks, which is the script to install various redistributable runtime libraries in Wine.

### Manjaro

```shell
sudo pacman -S wine
sudo pacman -S winetricks
```

&nbsp;

## COMMANDS

**Initialize Windows directory:**

- Initialize in default directory (`~/.wine`):
  - `wine init`
- Initialize in custom directory:
  - `WINEPREFIX=path/to/dir wine init`

Note: If we intent to use custom directory persistently, we should add WINEPREFIX to login/non-login shell.

&nbsp;
**Configure settings:**

`winecfg`

&nbsp;
**Run a Windows executable file:**

`wine path/to/app.exe`

&nbsp;
**Run winecfg as Win32:**

`WINEARCH=win32 winecfg`

&nbsp;
**Reboot Windows:**

`wineboot`
