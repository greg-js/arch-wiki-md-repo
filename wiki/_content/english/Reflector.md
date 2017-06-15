[Reflector](http://xyne.archlinux.ca/projects/reflector/) is a script which can retrieve the latest mirror list from the [MirrorStatus](https://www.archlinux.org/mirrors/status/) page, filter the most up-to-date mirrors, sort them by speed and overwrite the file `/etc/pacman.d/mirrorlist`.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Examples](#Examples)
    *   [2.2 Pacman Hook](#Pacman_Hook)
    *   [2.3 Systemd Service](#Systemd_Service)
    *   [2.4 Systemd Timer](#Systemd_Timer)
        *   [2.4.1 AUR package](#AUR_package)
            *   [2.4.1.1 reflector-timer](#reflector-timer)
            *   [2.4.1.2 reflector-timer-weekly](#reflector-timer-weekly)

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

Select the HTTPS mirrors synchronized within the last 12 hours and located in the US, sort them by download speed, and overwrite the file `/etc/pacman.d/mirrorlist`:

```
# reflector --country 'United States' --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist

```

### Pacman Hook

You can also create a pacman hook that will run *reflector* and remove the `.pacnew` file created every time [pacman-mirrorlist](https://www.archlinux.org/packages/?name=pacman-mirrorlist) gets an upgrade.

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
Exec = /usr/bin/env sh -c "reflector --country 'United States' --latest 200 --age 24 --sort rate --save /etc/pacman.d/mirrorlist; if [[ -f /etc/pacman.d/mirrorlist.pacnew ]]; then rm /etc/pacman.d/mirrorlist.pacnew; fi"

```

Make sure to substitute in your desired arguments for *reflector*.

See [User:Allan/Pacman Hooks](/index.php/User:Allan/Pacman_Hooks "User:Allan/Pacman Hooks") and [DeveloperWiki:Pacman Hooks](/index.php/DeveloperWiki:Pacman_Hooks "DeveloperWiki:Pacman Hooks") for more info on pacman hooks.

### Systemd Service

 `/etc/systemd/system/reflector.service` 
```
[Unit]
Description=Pacman mirrorlist update

[Service]
Type=oneshot
ExecStart=/usr/bin/reflector --protocol https --latest 30 --number 20 --sort rate --save /etc/pacman.d/mirrorlist

```

Then [starting](/index.php/Start "Start") `reflector.service` will update your mirrorlist.

To update your mirrorlist every time your computer boots you can enable the following service definition.

 `/etc/systemd/system/reflector.service` 
```
[Unit]
Description=Pacman mirrorlist update
Requires=network-online.target
After=network-online.target

[Service]
Type=oneshot
ExecStart=/usr/bin/reflector --protocol https --latest 30 --number 20 --sort rate --save /etc/pacman.d/mirrorlist

[Install]
RequiredBy=multi-user.target

```

Make sure you [activate the appropriate services](http://www.freedesktop.org/wiki/Software/systemd/NetworkTarget/) so that `network.target` really reflects your network status.

### Systemd Timer

If you want to run `reflector.service` on a weekly basis:

 `/etc/systemd/system/reflector.timer` 
```
[Unit]
Description=Run reflector weekly

[Timer]
OnCalendar=weekly
RandomizedDelaySec=12h
Persistent=true

[Install]
WantedBy=timers.target

```

And then just [start](/index.php/Start "Start") the `reflector.timer`.

#### AUR package

[Install](/index.php/Install "Install") the [reflector-timer](https://aur.archlinux.org/packages/reflector-timer/) or [reflector-timer-weekly](https://aur.archlinux.org/packages/reflector-timer-weekly/) package to run *reflector* weekly.

##### reflector-timer

The default configuration is:

 `/usr/share/reflector-timer/reflector.conf` 
```
AGE=6
COUNTRY=Germany
LATEST=30
NUMBER=20
SORT=rate

```

To override this configuration, edit `/etc/conf.d/reflector.conf`:

 `/etc/conf.d/reflector.conf` 
```
COUNTRY=US

```

Be sure to [enable](/index.php/Enable "Enable") `reflector.timer`.

##### reflector-timer-weekly

The default configuration is:

 `/etc/reflector.conf` 
```
--save /etc/pacman.d/mirrorlist
--country China
--sort rate

```

Each line (except that begins with '#') should be valid `reflector` option.

Be sure to [enable](/index.php/Enable "Enable") `reflector.timer`.