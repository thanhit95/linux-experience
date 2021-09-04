# GRUB

## WHAT IS GRUB

> The GRUB (Grand Unified Bootloader) is a bootloader available from the GNU project. A bootloader is very important as it is impossible to start an operating system without it. It is the first program which starts when the program is switched on. The bootloader transfers the control to the operating system kernel.

&nbsp;

## GRUB CONFIG FILE

The grub config is at `/boot/grub/grub.cfg`.

However, editing this config file may cause problem to the bootloader. For safety, this config file should be made from `/etc/default/grub`.

The scenario is this:

```text
                       update-grub
/etc/default/grub ---------------------> /boot/grub/grub.cfg
```

- Step 1. Edit file `/etc/default/grub`.
- Step 2. Update grub config using this command:
  - `sudo update-grub`

&nbsp;

## REFERENCES

- <https://www.tutorialspoint.com/what-is-grub-in-linux>
