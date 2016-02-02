# Parental Control

Several methods exist to protect and limit child activity on a computer.

## Applications

*   **timekpr** — A program controlling use of user accounts. It can limit by access duration with the daemon _timed_, and configure at what time users can log in. A client in the traybar warns the users about their time running out, while administration is done in a graphical GTK GUI.

	[https://launchpad.net/timekpr](https://launchpad.net/timekpr) || [timekpr](https://aur.archlinux.org/packages/timekpr/)<sup><small>AUR</small></sup>

*   **timeoutd** — A lightweight alternative to timekpr, it scans `/var/run/utmp` every minute and checks `/etc/timeouts` for an entry matching a restricted user. Restrictions are based on idle time, login time, maximum time, and time of day.

	|| [timeoutd](https://aur.archlinux.org/packages/timeoutd/)<sup><small>AUR</small></sup>

*   **logkeys** — A daemon that logs keypresses into a logfile for later inspection. The log file resides by default in `/var/log`, but it is recommended to move it to an encrypted partition; it will for example contain every password entered in the system. For supervision purposes, the `--no-func-keys` option is recommended.

	[http://code.google.com/p/logkeys/](http://code.google.com/p/logkeys/) || [logkeys-git](https://aur.archlinux.org/packages/logkeys-git/)<sup><small>AUR</small></sup>

*   **logkeys-keymaps** — Necessary to log keys with logkeys (`--keymap` option) using a localized, non-US keyboard.

	|| [logkeys-keymaps-git](https://aur.archlinux.org/packages/logkeys-keymaps-git/)<sup><small>AUR</small></sup>

## Whitelist with Tinyproxy and Firehol

The following description will enable you to filter any user's access to the internet with a whitelist of url-s using [firehol](https://aur.archlinux.org/packages/firehol/)<sup><small>AUR</small></sup> and [tinyproxy](https://www.archlinux.org/packages/?name=tinyproxy) (or [tinyproxy-git](https://aur.archlinux.org/packages/tinyproxy-git/)<sup><small>AUR</small></sup>).

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=Parental_Control&oldid=374735](https://wiki.archlinux.org/index.php?title=Parental_Control&oldid=374735)"