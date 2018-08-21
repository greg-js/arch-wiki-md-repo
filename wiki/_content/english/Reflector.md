Related articles

*   [Mirrors](/index.php/Mirrors "Mirrors")
*   [Pacman](/index.php/Pacman "Pacman")

[Reflector](http://xyne.archlinux.ca/projects/reflector/) is a script which can retrieve the latest mirror list from the [MirrorStatus](https://www.archlinux.org/mirrors/status/) page, filter the most up-to-date mirrors, sort them by speed and overwrite the file `/etc/pacman.d/mirrorlist`.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Examples](#Examples)
*   [3 Automation](#Automation)
    *   [3.1 Pacman hook](#Pacman_hook)
    *   [3.2 Systemd service](#Systemd_service)
    *   [3.3 Systemd timer](#Systemd_timer)
    *   [3.4 Reflector-timer package](#Reflector-timer_package)
    *   [3.5 Cron task](#Cron_task)

## Installation

[Install](/index.php/Install "Install") the [reflector](https://www.archlinux.org/packages/?name=reflector) package.

## Usage

**Warning:**

*   In the following examples, `/etc/pacman.d/mirrorlist` will be overwritten. Make a backup before proceeding.
*   Make sure the resulting `/etc/pacman.d/mirrorlist` does not contain entries that you consider untrustworthy before syncing or updating with [Pacman](/index.php/Pacman "Pacman").

To see all of the available commands, run the following command:

```
# reflector --help

```

### Examples

Verbosely rate and sort the five most recently synchronized mirrors by download speed, and overwrite the file `/etc/pacman.d/mirrorlist`:

```
# reflector --verbose --latest 5 --sort rate --save /etc/pacman.d/mirrorlist

```

Select the 200 most recently synchronized HTTP or HTTPS mirrors, sort them by download speed, and overwrite the file `/etc/pacman.d/mirrorlist`:

```
# reflector --latest 200 --protocol http --protocol https --sort rate --save /etc/pacman.d/mirrorlist

```

Select the HTTPS mirrors synchronized within the last 12 hours and located in either France or Germany, sort them by download speed, and overwrite the file `/etc/pacman.d/mirrorlist`:

```
# reflector --country France --country Germany --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist

```

## Automation

### Pacman hook

You can also create a [pacman hook](/index.php/Pacman_hook "Pacman hook") that will run *reflector* and remove the *.pacnew* file created every time [pacman-mirrorlist](https://www.archlinux.org/packages/?name=pacman-mirrorlist) gets an upgrade.

 `/etc/pacman.d/hooks/mirrorupgrade.hook` 
```
[Trigger]
Operation = Upgrade
Type = Package
Target = pacman-mirrorlist

[Action]
Description = Updating pacman-mirrorlist with reflector and removing pacnew...
When = PostTransaction
Depends = reflector
Exec = /bin/sh -c "reflector --country 'United States' --latest 200 --age 24 --sort rate --save /etc/pacman.d/mirrorlist; rm -f /etc/pacman.d/mirrorlist.pacnew"

```

Make sure to substitute in your desired arguments for *reflector*.

### Systemd service

This is an example of service unit that waits for the network to be up and online before running reflector:

 `/etc/systemd/system/reflector.service` 
```
[Unit]
Description=Pacman mirrorlist update
Wants=network-online.target
After=network-online.target

[Service]
Type=oneshot
ExecStart=/usr/bin/reflector --protocol https --latest 30 --number 20 --sort rate --save /etc/pacman.d/mirrorlist

[Install]
RequiredBy=multi-user.target
```

[starting](/index.php/Start "Start") `reflector.service` will update the mirrorlist. To update the mirrorlist every time the computer boots, [enable](/index.php/Enable "Enable") the service.

**Note:** For more information on the implementation of the network dependency, see [Systemd#Running services after the network is up](/index.php/Systemd#Running_services_after_the_network_is_up "Systemd").

### Systemd timer

If you want to run `reflector.service` on a weekly basis, create an associated *.timer*:

 `/etc/systemd/system/reflector.timer` 
```
[Unit]
Description=Run reflector weekly

[Timer]
OnCalendar=Mon *-*-* 7:00:00
RandomizedDelaySec=15h
Persistent=true

[Install]
WantedBy=timers.target
```

And then just [start](/index.php/Start "Start") the `reflector.timer`.

### Reflector-timer package

[Install](/index.php/Install "Install") [reflector-timer](https://aur.archlinux.org/packages/reflector-timer/) to run *reflector* weekly.

The default configuration, which can be edited to fit one's needs, is:

 `/usr/share/reflector-timer/reflector.conf` 
```
AGE=6
COUNTRY=Germany
LATEST=30
NUMBER=20
SORT=rate
### remove an entry if you don't want it as available protocol
PROTOCOL1='-p http'
PROTOCOL2='-p https'
PROTOCOL3='-p ftp'
PROTOCOL4='-p rsync'
```

Be sure to [enable](/index.php/Enable "Enable") `reflector.timer`.

### Cron task

To update the mirrorlist daily, consider the following:

 `/etc/cron.daily/mirrorlist` 
```
#!/bin/bash

# Get the country thing
/usr/bin/reflector -c "India" -p http --sort rate > /etc/pacman.d/mirrorlist

# Work through the alternatives
/usr/bin/reflector -p http  --latest 20 -p https -p ftp --sort rate >> /etc/pac
man.d/mirrorlist
```