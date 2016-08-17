This article describes how to automatically log in to a [virtual console](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") at the end of the [boot process](/index.php/Boot_process "Boot process"). This article only covers console log-ins; see [Start X at login](/index.php/Start_X_at_login "Start X at login") for information about automatic login into [Xorg](/index.php/Xorg "Xorg").

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Virtual console](#Virtual_console)
    *   [1.2 Serial console](#Serial_console)
*   [2 See also](#See_also)

## Configuration

Configuration relies on systemd [drop-in files](/index.php/Systemd#Editing_provided_units "Systemd") to override the default parameters passed to *[agetty](/index.php/Agetty "Agetty")*.

Configuration differs for virtual versus serial consoles. In most cases, you want to set up automatic login on a virtual console, (whose device name is `tty*N*`, where `*N*` is a number). The configuration of automatic login for serial consoles will be slightly different. Device names of the serial consoles look like `ttyS*N*`, where `*N*` is a number.

### Virtual console

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

## See also

*   [Change default runlevel/target to boot into](/index.php/Systemd#Change_default_target_to_boot_into "Systemd")