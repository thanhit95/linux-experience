# LINUX OS OPTIMIZATION

## CONTENT

### Increase download speed of package managers

Fedora:

Edit file `/etc/dnf/dnf.conf`, add 2 lines:

```text
max_parallel_downloads=8
fastestmirror=True
```

And then `sudo dnf upgrade --refresh`

### Disable unimportant services

Disable and stop/mask these services:

- Bluetooh (in case rarely using bluetooth):
  - bluetooth.service
  - blueman-mechanism.service
- Printer:
  - cups.service
  - cups-browsed.service
- Network:
  - ModemManager.service (in case computer acting like a modem)
  - NetworkManager-wait-online.service (waiting for network to come online)
- Snap Store:
  - snapd.socket (call snapd.service)
  - snapd.service (snap package management)
  - snapd.seeded.service
- Apps:
  - teamviewerd.service
  - anydesk.service
- Ubuntu:
  - whoopsie.service and apport-forward.socket and apport-autoreport.path (send error report to Ubuntu/Canonical)
  - motd-news.timer (message of the day)
- Manjaro:
  - pkgfile-update.timer
  - pkgfile-update.service
- Miscellaneous:
  - systemd-timesyncd.service (time sync)
  - fwupd-refresh.timer (allowing session software to update firmware)

Notes:

```shell
systemd-analyze blame
systemd-analyze critical-chain
```

### Remove unnecessary packages

#### Common

Clean journal (systemd / log):

```shell
journalctl --disk-usage
sudo journalctl --vacuum-size=100M
```

#### Ubuntu

```shell
sudo apt autoremove

# extra: remove temporary cache used by apt
sudo apt clean
```

#### Manjaro

Clean package:

```shell
# clean cache
sudo pacman -Sc
sudo pamac clean --build-files

# remove orphaned packages by pacman
# try listing them first
pacman -Qtdq
sudo pacman -R $(pacman -Qtdq)

# remove orphaned packages by pamac
sudo pamac remove --orphans
```

### About applications

- Turn off some startup applications.
- Disable Java in Libre Office. Goto menu Tools ⟶ Options:
  - LibreOffice ⟶ Advanced ⟶ Java Options.
    - Uncheck "Use a Java runtime environment".

### Disable Bluetooth driver

If you rarely use Bluetooth, you can probably increase the battery life of your laptop a lot by disabling the Bluetooth driver (instead of simply disabling the Bluetooth feature).

Run this command:

```shell
echo "blacklist btusb" | sudo tee /etc/modprobe.d/blacklist-bluetooth.conf
```

This command will create a file at `/etc/modprobe.d/blacklist-bluetooth.conf` with the content `blacklist btusb`.

Remember to reboot computer.

To re-enable Bluetooh driver, simply remove file `/etc/modprobe.d/blacklist-bluetooth.conf`.

## REFERENCES

- <https://easylinuxtipsproject.blogspot.com/p/speed-mint.html>
