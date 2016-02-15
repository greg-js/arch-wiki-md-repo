## Fixing Fn Keys

If the Fn Keys do not work or exhibit incorrect behavior(e.g brightness keys suspending the laptop) it can be fixed doing the following:

In `/etc/default/grub` find the line that says `GRUB_CMDLINE_LINUX=""` and add the following kernel parameters:

```
acpi_osi=Linux acpi_backlight=vendor

```

Then, in `/etc/modprobe.d/blacklist.conf` add the following line:

```
blacklist toshiba_acpi

```

If `blacklist.conf` doesn't exist, create it.

Finally do `sudo update-grub` and reboot.