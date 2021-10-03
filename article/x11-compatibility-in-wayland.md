# X11 COMPATIBILITY IN WAYLAND

## DESCRIPTION

A lot of apps that prefer running in X11 in the old days, so if they run in Wayland then some issues would occur.

## SETUP

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

## SOLVE ERRORS

### Cannot change settings when run app with sudo

Symptom:

- Run the app: `sudo app-name`.
- Change app settings.
- The error message occurs: `failed to commit changes to dconf: Error spawning command line "dbus-launch --autolaunch..."`.

To fix this, run the app with the command:

`sudo dbus-launch app-name`

&nbsp;

## MISCELLANEOUS NOTES

Find out which display server is being used:

`echo $XDG_SESSION_TYPE`
