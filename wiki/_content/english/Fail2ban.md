**Warning:** Using an IP blacklist will stop trivial attacks but it relies on an additional daemon and successful logging (the partition containing /var can become full, especially if an attacker is pounding on the server). Additionally, if the attacker knows your IP address, they can send packets with a spoofed source header and get you locked out of the server. [SSH keys](/index.php/SSH_keys "SSH keys") provide an elegant solution to the problem of brute forcing without these problems.

[Fail2ban](http://www.fail2ban.org/wiki/index.php/Main_Page) scans various textual log files and bans IP that makes too many password failures by updating firewall rules to reject the IP address, similar to [Sshguard](/index.php/Sshguard "Sshguard").

**Warning:** For correct function it is essential that the tool parses the IP addresses in the log correctly. You should always **test** the log filters work as intended per application you want to protect.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 systemd](#systemd)
*   [2 Hardening](#Hardening)
    *   [2.1 Capabilities](#Capabilities)
    *   [2.2 Filesystem Access](#Filesystem_Access)
*   [3 Configuration](#Configuration)
    *   [3.1 Default jails](#Default_jails)
    *   [3.2 Paths](#Paths)
    *   [3.3 Custom SSH jail](#Custom_SSH_jail)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [fail2ban](https://www.archlinux.org/packages/?name=fail2ban).

If you want Fail2ban to send an email when someone has been banned, you have to configure [SSMTP](/index.php/SSMTP "SSMTP") (for example).

### systemd

[Enable](/index.php/Enable "Enable") the `fail2ban.service` unit.

## Hardening

Currently, fail2ban must be run as root. Therefore, you may wish to consider hardening the process with systemd. Ref:[systemd for Administrators, Part XII](http://0pointer.de/blog/projects/security.html)

### Capabilities

For added security, consider limiting fail2ban capabilities by specifying `CapabilityBoundingSet` in the [drop-in configuration file](/index.php/Systemd#Editing_provided_units "Systemd") for the provided `fail2ban.service`:

 `/etc/systemd/system/fail2ban.service.d/capabilities.conf` 
```
[Service]
CapabilityBoundingSet=CAP_DAC_READ_SEARCH CAP_NET_ADMIN CAP_NET_RAW
```

In the example above, `CAP_DAC_READ_SEARCH` will allow fail2ban full read access, and `CAP_NET_ADMIN` and `CAP_NET_RAW` allow setting of firewall rules with [iptables](/index.php/Iptables "Iptables"). Additional capabilities may be required, depending on your fail2ban configuration. See `man capabilities` for more info.

### Filesystem Access

**Note:** On some systems this might lead to fail2ban not working. So, first try without, before hardening fail2ban

Consider limiting file system read and write access by using *ReadOnlyDirectories* and *ReadWriteDirectories*, under the `[Service]` section. For example:

```
ReadOnlyDirectories=/
ReadWriteDirectories=/var/run/fail2ban /var/lib/fail2ban /var/spool/postfix/maildrop /tmp /var/log/fail2ban

```

In the example above, this limits the file system to read-only, except for `/var/run/fail2ban` for pid and socket files, and `/var/spool/postfix/maildrop` for [postfix](/index.php/Postfix "Postfix") sendmail. Again, this will be dependent on you system configuration and fail2ban configuration. The `/tmp` directory is needed for some fail2ban actions. Note that adding `/var/log/fail2ban` is necessary if you want fail2ban to log its activity. Make sure all the directories exist, or you will get error code 226 on starting the service. And modify logtarget in `/etc/fail2ban/fail2ban.conf`:

```
logtarget = /var/log/fail2ban/fail2ban.log

```

## Configuration

**Note:** Due to the possibility of the `jail.conf` file being overwritten or improved during a distribution update, it is recommended to provide customizations in a `jail.local` file, or separate *.conf* files under the `jail.d/` directory, e.g. `jail.d/ssh-iptables.conf`.

### Default jails

Jails for many different services are already present in `/etc/fail2ban/jail.conf` but not enabled by default. You can copy the section headers into a .local file of your choice, enable them (and optionally override settings).

### Paths

There currently is no out-of-the-box support for archlinux, but the fedora defaults can make a decent starting point:

```
# cp /etc/fail2ban/paths-fedora.conf /etc/fail2ban/paths-archlinux.conf

```

To activate that configuration, add or alter the following section in the `jail.local` file:

```
[INCLUDES]
before = paths-archlinux.conf

```

[Restart](/index.php/Restart "Restart") `fail2ban.service` to test your configuration. Watch out for "file not found errors" from *fail2ban-client* if the fail2ban service fails to start. Adjust the paths `paths-archlinux.conf` or `jail.local` as needed. Many of the default jails might not work out of the box.

### Custom SSH jail

Edit `/etc/fail2ban/jail.d/jail.conf`, add this section and update the list of trusted IP addresses.

If your firewall is [iptables](/index.php/Iptables "Iptables"):

```
[DEFAULT]
bantime = 864000
ignoreip = 127.0.0.1/8

[sshd]
enabled  = true
filter   = sshd
action   = iptables[name=SSH, port=ssh, protocol=tcp]
           sendmail-whois[name=SSH, dest=your@mail.org, sender=fail2ban@mail.com]
backend  = systemd
maxretry = 5

```

**Note:** If your firewall is [shorewall](/index.php/Shorewall "Shorewall"), replace `iptables[name=SSH, port=ssh, protocol=tcp]` with `shorewall`. You can also set `BLACKLIST` to `ALL` in `/etc/shorewall/shorewall.conf`, otherwise the rule added to ban an IP address will affect only new connections.

Also do not forget to add/change:

```
LogLevel VERBOSE

```

in your `/etc/ssh/sshd_config`. Else, password failures are not logged correctly.

## See also

*   [sshguard](/index.php/Sshguard "Sshguard")