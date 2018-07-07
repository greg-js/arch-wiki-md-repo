Related articles

*   [Display manager](/index.php/Display_manager "Display manager")

A [getty](https://en.wikipedia.org/wiki/getty_(Unix) "w:getty (Unix)") is the generic name for a program which manages a terminal line and its connected terminal. Its purpose is to protect the system from unauthorized access. Generally, each getty process is started by [systemd](/index.php/Systemd "Systemd") and manages a single terminal line.

## Contents

*   [1 Installation](#Installation)
*   [2 Add additional virtual consoles](#Add_additional_virtual_consoles)
*   [3 Automatic login to virtual console](#Automatic_login_to_virtual_console)
    *   [3.1 Virtual console](#Virtual_console)
    *   [3.2 Serial console](#Serial_console)
    *   [3.3 Nspawn console](#Nspawn_console)
*   [4 Have boot messages stay on tty1](#Have_boot_messages_stay_on_tty1)
*   [5 See also](#See_also)

## Installation

*agetty* is the default getty in Arch Linux, as part of the [util-linux](https://www.archlinux.org/packages/?name=util-linux) package. It modifies the TTY settings while waiting for a login so that the newlines are not translated to CR-LFs. This tends to cause a "staircase effect" for messages printed to the console. Agetty manages virtual consoles and six of these virtual consoles are provided by default in Arch Linux. They are usually accessible by pressing `Ctrl+Alt+F1` through `Ctrl+Alt+F6`.

Alternatives include:

*   **mingetty** — A minimal getty which allows automatic logins.

	[mingetty](https://aur.archlinux.org/packages/mingetty/) || [mingetty](https://aur.archlinux.org/packages/mingetty/)

*   **fbgetty** — A console getty like mingetty, which supports framebuffers.

	[http://projects.meuh.org/fbgetty/](http://projects.meuh.org/fbgetty/) || [fbgetty](https://aur.archlinux.org/packages/fbgetty/)

*   **mgetty** — A versatile program to handle all aspects of a modem under Unix.

	[http://mgetty.greenie.net/](http://mgetty.greenie.net/) || [mgetty](https://aur.archlinux.org/packages/mgetty/)

## Add additional virtual consoles

Open the file `/etc/systemd/logind.conf` and set the option **NAutoVTs=6** to the number of virtual terminals that you want at boot.

If you wish to start one temporarily, you can start a getty service at the desired TTY by typing:

```
$ systemctl start getty@ttyN.service

```

## Automatic login to virtual console

Configuration relies on systemd [drop-in files](/index.php/Systemd#Editing_provided_units "Systemd") to override the default parameters passed to *agetty*.

Configuration differs for virtual versus serial consoles. In most cases, you want to set up automatic login on a virtual console, (whose device name is `tty*N*`, where `*N*` is a number). The configuration of automatic login for serial consoles will be slightly different. Device names of the serial consoles look like `ttyS*N*`, where `*N*` is a number.

### Virtual console

**Warning:** [It has been reported](https://bbs.archlinux.org/viewtopic.php?id=238576) that this method may interfere with the hibernating process.

[Edit the provided unit](/index.php/Systemd#Editing_provided_units "Systemd") either manually by creating the following drop-in snippet, or by running `systemctl edit getty@tty1` and pasting its content:

 `/etc/systemd/system/getty@tty1.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=-/usr/bin/agetty --autologin *username* --noclear %I $TERM
```

**Tip:** The option `Type=idle` found in the default `getty@.service` will delay the service startup until all jobs (state change requests to units) are completed in order to avoid polluting the login prompt with boot-up messages. When [starting X automatically](/index.php/Start_X_at_login "Start X at login"), it may be useful to start `getty@tty1.service` immediately by adding `Type=simple` into the [drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet"). Both the init system and *startx* can be [silenced](/index.php/Silent_boot "Silent boot") to avoid the interleaving of their messages during boot-up.

If you want to use a *tty* other than *tty1*, see [systemd FAQ](/index.php/Systemd_FAQ#How_do_I_change_the_default_number_of_gettys.3F "Systemd FAQ").

### Serial console

Create the following file (and leading directories):

 `/etc/systemd/system/serial-getty@ttyS0.service.d/autologin.conf` 
```
[Service]
ExecStart=
ExecStart=-/usr/bin/agetty --autologin *username* -s %I 115200,38400,9600 vt102
```

### Nspawn console

To configure auto-login for a [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") container, override *console-getty* service:

 `/etc/systemd/system/console-getty.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStart=-/sbin/agetty --noclear --autologin *username* --keep-baud console 115200,38400,9600 $TERM
```

## Have boot messages stay on tty1

By default, Arch has the `getty@tty1` service enabled. The service file already passes `--noclear`, which stops agetty from clearing the screen. However [systemd](/index.php/Systemd "Systemd") clears the screen before starting it. To disable this behavior, create `/etc/systemd/system/getty@tty1.service.d/noclear.conf`:

 `/etc/systemd/system/getty@tty1.service.d/noclear.conf` 
```
[Service]
TTYVTDisallocate=no
```

This overrides only `TTYVTDisallocate` for *agetty* on TTY1, and leaves the global service file `/usr/lib/systemd/system/getty@.service` untouched. See [Systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd").

**Note:**

*   Make sure to remove `quiet` from the [kernel parameters](/index.php/Kernel_parameter "Kernel parameter").
*   Late KMS starting may cause the first few boot messages to clear. See [KMS#Early KMS start](/index.php/KMS#Early_KMS_start "KMS") or [KMS#Disabling modesetting](/index.php/KMS#Disabling_modesetting "KMS").

## See also

*   [Systemd#Change default target to boot into](/index.php/Systemd#Change_default_target_to_boot_into "Systemd")
*   [The TTY demystified](http://www.linusakesson.net/programming/tty/)
*   [Wikipedia:Tty (unix)](https://en.wikipedia.org/wiki/Tty_(unix) "wikipedia:Tty (unix)")