Related articles

*   [sshguard](/index.php/Sshguard "Sshguard")
*   [Security](/index.php/Security "Security")

[Fail2ban](http://www.fail2ban.org/wiki/index.php/Main_Page) scans log files (e.g. `/var/log/httpd/error_log`) and bans IPs that show the malicious signs like too many password failures, seeking for exploits, etc. Generally Fail2Ban is then used to update firewall rules to reject the IP addresses for a specified amount of time, although any arbitrary other action (e.g. sending an email) could also be configured.

**Warning:** Using an IP banning software will stop trivial attacks but it relies on an additional daemon and successful logging. Additionally, if the attacker knows your IP address, they can send packets with a spoofed source header and get your IP address banned.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 fail2ban-client](#fail2ban-client)
*   [3 Service hardening](#Service_hardening)
*   [4 Configuration](#Configuration)
    *   [4.1 Enabling jails](#Enabling_jails)
    *   [4.2 Firewall and services](#Firewall_and_services)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Custom SSH jail](#Custom_SSH_jail)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [fail2ban](https://www.archlinux.org/packages/?name=fail2ban).

If you want Fail2ban to send an email when someone has been banned, you have to configure an SMTP client ([msmtp](/index.php/Msmtp "Msmtp") (for example).

## Usage

[Enable](/index.php/Enable "Enable")/[start](/index.php/Start "Start") `fail2ban.service`.

### fail2ban-client

The fail2ban-client allows monitoring jails (reload, restart, status, etc.), to view all available commands:

```
$ fail2ban-client

```

To view all enabled jails:

```
# fail2ban-client status

```

To check the status of a jail, e.g. for *sshd*:

 `# fail2ban-client status sshd` 
```
Status for the jail: sshd
|- Filter
|  |- Currently failed: 1
|  |- Total failed:     9
|  `- Journal matches:  _SYSTEMD_UNIT=sshd.service + _COMM=sshd
`- Actions
   |- Currently banned: 1
   |- Total banned:     1
   `- Banned IP list:   0.0.0.0

```

## Service hardening

Currently, fail2ban must be run as *root*. Therefore, you may wish to consider hardening the process with [systemd](/index.php/Systemd "Systemd").

Create a [drop-in](/index.php/Systemd#Drop-in_files "Systemd") configuration file for `fail2ban.service`:

 `/etc/systemd/system/fail2ban.service.d/override.conf` 
```
[Service]
PrivateDevices=yes
PrivateTmp=yes
ProtectHome=read-only
ProtectSystem=strict
NoNewPrivileges=yes
ReadWritePaths=-/var/run/fail2ban
ReadWritePaths=-/var/lib/fail2ban
ReadWritePaths=-/var/log/fail2ban
ReadWritePaths=-/var/spool/postfix/maildrop
CapabilityBoundingSet=CAP_AUDIT_READ CAP_DAC_READ_SEARCH CAP_NET_ADMIN CAP_NET_RAW
```

The `CapabilityBoundingSet` parameters `CAP_DAC_READ_SEARCH` will allow fail2ban full read access to every directory and file, `CAP_NET_ADMIN` and `CAP_NET_RAW` allow setting of firewall rules with [iptables](/index.php/Iptables "Iptables"). See [capabilities(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/capabilities.7) for more info.

By using `ProtectSystem=strict` the [filesystem](/index.php/Filesystem "Filesystem") hierarchy will only be read-only, `ReadWritePaths` allows fail2ban to have write access on required paths.

[Create](/index.php/Create "Create") `/etc/fail2ban/fail2ban.local` with the correct `logtarget` path:

 `/etc/fail2ban/fail2ban.local` 
```
[Definition]
logtarget = /var/log/fail2ban/fail2ban.log

```

Finally, [reload systemd](/index.php/Systemd#Using_units "Systemd") to apply the changes of the unit and [restart](/index.php/Restart "Restart") `fail2ban.service`.

## Configuration

Due to the possibility of the `/etc/fail2ban/jail.conf` file being overwritten or improved during a distribution update, it is recommended to [Create](/index.php/Create "Create") `/etc/fail2ban/jail.local` file. For example to change default ban time to 1 day:

 `/etc/fail2ban/jail.local` 
```
[DEFAULT]
bantime = 1d

```

Or create separate *name.local* files under the `/etc/fail2ban/jail.d` directory, e.g. `/etc/fail2ban/jail.d/ssh-iptables.local`.

[Restart](/index.php/Restart "Restart") `fail2ban.service` to apply the configuration changes.

### Enabling jails

[Append](/index.php/Append "Append") `enabled = true` to service one want to use, e.g. to enable the [OpenSSH](/index.php/OpenSSH "OpenSSH") jail:

 `/etc/fail2ban/jail.local` 
```
[sshd]
enabled = true
```

See [Fail2ban#Custom SSH jail](/index.php/Fail2ban#Custom_SSH_jail "Fail2ban").

### Firewall and services

Most [firewalls](/index.php/Firewalls "Firewalls") and services should work out of the box. See `/etc/fail2ban/action.d/` for examples, e.g. [ufw.conf](https://github.com/fail2ban/fail2ban/blob/master/config/action.d/ufw.conf).

## Tips and tricks

### Custom SSH jail

**Warning:** If the attacker knows your IP address, they can send packets with a spoofed source header and get your IP address locked out of the server. [SSH keys](/index.php/SSH_keys "SSH keys") provide an elegant solution to the problem of brute forcing without these problems.

Edit `/etc/fail2ban/jail.d/sshd.local`, add this section and update the list of trusted IP addresses in `ignoreip`.

If your firewall is [iptables](/index.php/Iptables "Iptables"):

```
[sshd]
enabled  = true
filter   = sshd
action   = iptables
backend  = systemd
maxretry = 5
findtime = 1d
bantime  = 2w
ignoreip = 127.0.0.1/8

```

fail2ban has IPv6 support since version 0.10\. Adapt your firewall accordingly, e.g. start and enable `ip6tables.service`.

**Note:** If your firewall is [shorewall](/index.php/Shorewall "Shorewall"), replace `iptables` with `shorewall`. You can also set `BLACKLIST` to `ALL` in `/etc/shorewall/shorewall.conf`, otherwise the rule added to ban an IP address will affect only new connections.

**Note:** It may be necessary to set `LogLevel VERBOSE` in `/etc/ssh/sshd_config` to allow full fail2ban monitoring as otherwise password failures may not be logged correctly.

## See also

*   [Using a Fail2Ban Jail to Whitelist a User](http://www.the-art-of-web.com/system/fail2ban-action-whitelist/)
*   [Optimising your Fail2Ban filters](http://www.the-art-of-web.com/system/fail2ban-filters/)
*   [Fail2Ban and sendmail](http://www.the-art-of-web.com/system/fail2ban-sendmail/)
*   [Fail2Ban and iptables](http://www.the-art-of-web.com/system/fail2ban/)
*   [Fail2Ban 0.8.3 Howto](http://www.the-art-of-web.com/system/fail2ban-howto/)
*   [Monitoring the fail2ban log](http://www.the-art-of-web.com/system/fail2ban-log/)