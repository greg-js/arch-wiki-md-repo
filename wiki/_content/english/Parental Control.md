Several methods exist to protect and limit child activity on a computer.

**Note:** Any security features will be effective only on the level you enforce them. For example, even after installing a parental control application in the operating system, the child may bypass it by downloading and booting any Linux distribution live image.

## Contents

*   [1 Applications](#Applications)
*   [2 Whitelist with Tinyproxy and Firehol](#Whitelist_with_Tinyproxy_and_Firehol)
*   [3 OpenDNS Parental Control](#OpenDNS_Parental_Control)
*   [4 Editing /etc/hosts](#Editing_.2Fetc.2Fhosts)
*   [5 Browser add-ons](#Browser_add-ons)

## Applications

*   **timekpr** — A program controlling use of user accounts. It can limit by access duration with the daemon *timed*, and configure at what time users can log in. A client in the traybar warns the users about their time running out, while administration is done in a graphical GTK GUI.

	[https://launchpad.net/timekpr](https://launchpad.net/timekpr) || [timekpr](https://aur.archlinux.org/packages/timekpr/)

*   **timeoutd** — A lightweight alternative to timekpr, it scans `/var/run/utmp` every minute and checks `/etc/timeouts` for an entry matching a restricted user. Restrictions are based on idle time, login time, maximum time, and time of day.

	|| [timeoutd](https://aur.archlinux.org/packages/timeoutd/)

*   **logkeys** — A daemon that logs keypresses into a logfile for later inspection. The log file resides by default in `/var/log`, but it is recommended to move it to an encrypted partition; it will for example contain every password entered in the system. Use the --keymap option if using a localized, non-US keyboard. For supervision purposes, the `--no-func-keys` option is recommended.

	[https://github.com/kernc/logkeys](https://github.com/kernc/logkeys) || [logkeys-git](https://aur.archlinux.org/packages/logkeys-git/)

*   [DansGuardian](/index.php/DansGuardian "DansGuardian"). If you wish, you might even set up an Arch based router running DansGuardian and enforce all other devices in your physical network to connect to the internet through this router.

## Whitelist with Tinyproxy and Firehol

The following description will enable you to filter any user's access to the internet with a whitelist of url-s using [firehol](https://aur.archlinux.org/packages/firehol/) and [tinyproxy](https://www.archlinux.org/packages/?name=tinyproxy) (or [tinyproxy-git](https://aur.archlinux.org/packages/tinyproxy-git/)).

`/etc/tinyproxy/tinyproxy.conf` consists of the following changes:

```
FilterURLs On
FilterDefaultDeny Yes
Filter "/etc/tinyproxy/whitelist"

```

`/etc/tinyproxy/whitelist` should hold the url's that will be only allowed accessed by selected users. A silly example:

```
(www|wiki|static).archlinux.org
google.com

```

`/etc/firehol/firehol.conf` should contain the following line:

```
transparent_proxy "80 443" 8888 "nobody root bin myaccount"

```

where myaccount is my account that should no be filtered by Tinyproxy.

## OpenDNS Parental Control

[OpenDNS](http://www.opendns.com/home-solutions/parental-controls/) provides free DNS services as an alternative to your ISP's default servers. Furthermore, they provide optional filtering capabilities. Different levels of filtering is possible; see the OpenDNS main page for details.

For dynamic IP addresses, it is a good idea to keep them updated on OpenDNS. Use [ddclient](https://www.archlinux.org/packages/?name=ddclient) and edit `/etc/ddclient/ddclient.conf` as follows:

```
# OpenDNS.com account-configuration
use=web, web=myip.dnsomatic.com
server=updates.opendns.com
protocol=dyndns2
login=myopendns@email.address
password=myopendnspassword
myhostname

```

You may sometimes even set up your router to use OpenDNS, therefore allowing protection spanning on all devices connected to that router.

## Editing /etc/hosts

You may configure your [/etc/hosts](https://en.wikipedia.org/wiki/Hosts_(file) file to block access to certain domains. A more draconian approach is to only allow domains explicitly stated in `/etc/hosts`, as described [here](https://help.ubuntu.com/community/ParentalControls#Do_It_Yourself_Whitelisting). If you do this, please remember that this will affect your whole system, so for example pacman may be unable to connect to the update server unless you make a proper binding in your `/etc/hosts`.

## Browser add-ons

Several add-ons exist for web browsers to filter web content. Some of them can even block out pages examining on their body, not only on their URL. Be warned, however, that this is not a very secure way. Starting Firefox in safe mode, messing with the Firefox profile directory or Firefox profile manager are obvious ways to attempt to shut down Firefox-based add-ons. If all else fails, the kid may simply use a different browser.