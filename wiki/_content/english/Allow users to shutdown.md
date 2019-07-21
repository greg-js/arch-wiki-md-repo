<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Button and Lid events](#Button_and_Lid_events)
*   [2 Using systemd-logind](#Using_systemd-logind)
*   [3 Using sudo](#Using_sudo)
    *   [3.1 Users without sudo privileges](#Users_without_sudo_privileges)
*   [4 Creating aliases](#Creating_aliases)

## Button and Lid events

The suspend, poweroff and hibernate button presses and lid close events are handled by *logind* as described in [Power management#ACPI events](/index.php/Power_management#ACPI_events "Power management") page.

## Using systemd-logind

If you're using [systemd](/index.php/Systemd "Systemd") (which is default in Arch Linux) and [install](/index.php/Install "Install") [polkit](https://www.archlinux.org/packages/?name=polkit), users with non-remote session can issue power-related commands as long as [the session is not broken](/index.php/General_troubleshooting#Session_permissions "General troubleshooting").

To check if your session is active

```
$ loginctl show-session $XDG_SESSION_ID --property=Active

```

The user can then use *systemctl* commands in the command line, or add them to menus:

```
$ systemctl poweroff
$ systemctl reboot

```

Other commands can be used as well, including `systemctl suspend` and `systemctl hibernate`. See the *System Commands* section in [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1)

You can also run this over dbus with:

```
$ dbus-send --system --print-reply --dest=org.freedesktop.login1 /org/freedesktop/login1 "org.freedesktop.login1.Manager.PowerOff" boolean:true
$ dbus-send --system --print-reply --dest=org.freedesktop.login1 /org/freedesktop/login1 "org.freedesktop.login1.Manager.Reboot" boolean:true

```

Note that the above will require interactive user authentication, unless you create a custom polkit rule on e.g. `/etc/polkit-1/rules.d/00-reboot-nopassword.rules`

```
polkit.addRule(function(action, subject) {
    if (action.id == "org.freedesktop.login1.reboot-multiple-sessions" && subject.user == "myusername")
    {
        return polkit.Result.YES;
    }
});

```

## Using sudo

[Install](/index.php/Install "Install") [sudo](https://www.archlinux.org/packages/?name=sudo), and give the user [sudo privileges](/index.php/Sudo "Sudo"). The user will then be able to use the `sudo systemctl` commands (e.g. `sudo systemctl poweroff`, `sudo systemctl reboot`, `sudo systemctl suspend` and `sudo systemctl hibernate`). See the *System Commands* section in [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1)

### Users without sudo privileges

If users should only be allowed to use shutdown commands, but not have other sudo privileges, then, as root, add the following to the end of `/etc/sudoers` using the `visudo` command. Substitute *user* for your username and *hostname* for the machine's hostname.

```
*user* *hostname* =NOPASSWD: /usr/bin/systemctl poweroff,/usr/bin/systemctl halt,/usr/bin/systemctl reboot

```

Now your user can shutdown with `sudo systemctl poweroff`, and reboot with `sudo systemctl reboot`. Users wishing to power down a system can also use `sudo systemctl halt`. Use the `NOPASSWD:` tag only if you do not want to be prompted for your password.

## Creating aliases

For convenience, you can add these [aliases](/index.php/Bash#Aliases "Bash") to your user's `~/.bashrc` if you have it enabled (or to `/etc/bash.bashrc` for system-wide settings):

```
alias reboot="sudo systemctl reboot"
alias poweroff="sudo systemctl poweroff"
alias halt="sudo systemctl halt"

```

This can also be done by installing [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat). This package creates symbolic links of the respective name to systemctl.