# COMMAND: XDG-MIME

## INTRODUCTION

> The XDG MIME Applications specification builds upon the shared MIME database and desktop entries to provide default applications.
> -- Arch Linux wiki --

### mimeapps.list

The XDG standard is the most common for configuring desktop environments. Default applications for each MIME type are stored in mimeapps.list files, which can be stored in several locations. They are searched in the following order, with earlier associations taking precedence over later ones:

| Path                       | Usage                  |
| -------------------------- | ---------------------- |
| `/etc/xdg/mimeapps.list`   | system-wide overrides  |
| `~/.config/mimeapps.list`  | user overrides         |

To view mimeapps.list in user home:

`cat ~/.config/mimeapps.list`

&nbsp;

## COMMANDS

**To get the filetype:**

```shell
$ xdg-mime query filetype foo.txt
text/plain

$ xdg-mime query filetype /etc/
inode/directory

$ xdg-mime query filetype $PWD
inode/directory
```

**To find the default application for a certain extension:**

```shell
$ xdg-mime query default text/plain
org.gnome.gedit.desktop

$ xdg-mime query default inode/directory
org.gnome.Nautilus.desktop
```

**To set an application as default:**

To set Thunar as default file manager:

`xdg-mime default thunar.desktop inode/directory`
