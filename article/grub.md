# GRUB

## WHAT IS GRUB

> The GRUB (Grand Unified Bootloader) is a bootloader available from the GNU project. A bootloader is very important as it is impossible to start an operating system without it. It is the first program which starts when the program is switched on. The bootloader transfers the control to the operating system kernel.

&nbsp;

## GRUB CONFIG FILE

The grub config is at `/boot/grub/grub.cfg`.

However, editing this config file may cause problems to the bootloader. For safety, this config file should be made from `/etc/default/grub`.

The scenario is this:

```text
                       grub-mkconfig
/etc/default/grub ----------------------> /boot/grub/grub.cfg
```

- Step 1. Edit file `/etc/default/grub`.
- Step 2. Update grub config using this command:
  - `sudo grub-mkconfig -o /boot/grub/grub.cfg`

Notes:

- Try `grub2-mkconfig` if command `grub-mkconfig` is not found.
- In Debian-based distros and Manjaro, you can use the command: `sudo update-grub`
  - Simply, it is a wrapper of `grub-mkconfig`

&nbsp;

## INSTALL GRUB TO DISK

Use the command: `sudo grub-install`

> With the traditional BIOS GRUB, `grub-install` will (re)write the part of the GRUB embedded in the Master Boot Record, and encode into it the physical disk block numbers from where to read the next part of GRUB. It will also determine from which partition the actual GRUB configuration file (`/boot/grub/grub.cfg`) will be read. An important factor here is the `/boot/grub/device.map` file, which tells GRUB how BIOS's (and therefore GRUB's) device numbering maps to Linux disk devices.
>
> With the UEFI GRUB, the main part of the GRUB bootloader will be located as a file in the EFI System Partition, typically as `/boot/efi/EFI/<name of distribution>/grubx64.efi` or similar. This bootloader pathname is stored in system NVRAM (= the place where BIOS settings are stored) in the UEFI boot variables. The main part of GRUB may be completely self-contained (and must be if Secure Boot is in use!) or it may load additional functionality as GRUB modules, typically from the `/boot/grub` directory of the Linux distribution it's part of.
>
> The UEFI boot variables will identify the disk the system should use to look for the EFI System Partition and the bootloader file inside it. You can view these variables yourself, using `efibootmgr -v` command. The `grub-install` command will update those variables, unless you use the `--no-nvram` option to specify otherwise.
>
> As a result, with both traditional BIOS and UEFI, running `grub-install` can update your bootloader to read a completely different GRUB configuration file on a completely different disk - although the details of that process will be completely different.
>
> With UEFI, you can actually change your boot device selection from within the OS, with either `efibootmgr` or `grub-install`. But `grub-install` is a massive overkill for that: if both your installations are UEFI and have their own separate ESP partitions, they will have their own UEFI boot variables and selecting between them can easily be done with `efibootmgr`, or indeed in the UEFI BIOS settings.

--- telcoM ---

&nbsp;

> `grub-install` installs the binary part(s) of GRUB, `update-grub` produces just the configuration file.

--- telcoM ---

&nbsp;

## REFERENCES

- <https://www.tutorialspoint.com/what-is-grub-in-linux>
- <https://unix.stackexchange.com/questions/465189/update-grub-vs-grub-install/465207>
