Related articles

*   [sshguard](/index.php/Sshguard "Sshguard")
*   [Security](/index.php/Security "Security")

[Fail2ban](https://www.fail2ban.org/wiki/index.php/Main_Page) scans log files (e.g. `/var/log/httpd/error_log`) and bans IPs that show the malicious signs like too many password failures, seeking for exploits, etc. Generally Fail2ban is then used to update [firewall](/index.php/Firewall "Firewall") rules to reject the IP addresses for a specified amount of time, although any other arbitrary action (e.g. sending an email) could also be configured.

**Warning:** Using an IP banning software will stop trivial attacks but it relies on an additional daemon and successful logging. Additionally, if the attacker knows your IP address, they can send packets with a spoofed source header and get your IP address banned. Make sure to specify your IP in `ignoreip`.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 fail2ban-client](#fail2ban-client)
*   [3 Configuration](#Configuration)
    *   [3.1 Enabling jails](#Enabling_jails)
    *   [3.2 Receive an alert e-mail](#Receive_an_alert_e-mail)
    *   [3.3 Firewall and services](#Firewall_and_services)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Custom SSH jail](#Custom_SSH_jail)
    *   [4.2 Service hardening](#Service_hardening)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [fail2ban](https://www.archlinux.org/packages/?name=fail2ban).

## Usage

[Configure](#Configuration) Fail2ban and [enable](/index.php/Enable "Enable")/[start](/index.php/Start "Start") `fail2ban.service`.

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

## Configuration

Due to the possibility of the `/etc/fail2ban/jail.conf` file being overwritten or improved during a distribution update, it is recommended to [create](/index.php/Create "Create") a `/etc/fail2ban/jail.local` file. For example to change the default ban time to 1 day:

 `/etc/fail2ban/jail.local` 
```
[DEFAULT]
bantime = 1d

```

Or create separate *name.local* files under the `/etc/fail2ban/jail.d` directory, e.g. `/etc/fail2ban/jail.d/sshd.local`.

[Restart](/index.php/Restart "Restart") `fail2ban.service` to apply the configuration changes.

### Enabling jails

By default all jails are disabled. [Append](/index.php/Append "Append") `enabled = true` to the jail you want to use, e.g. to enable the [OpenSSH](/index.php/OpenSSH "OpenSSH") jail:

 `/etc/fail2ban/jail.local` 
```
[sshd]
enabled = true
```

See [#Custom SSH jail](#Custom_SSH_jail).

### Receive an alert e-mail

If you want to receive an e-mail when someone has been banned, you have to configure an SMTP client (e.g. [msmtp](/index.php/Msmtp "Msmtp")) and change default action, as given below.

 `/etc/fail2ban/jail.local` 
```
[DEFAULT]
destemail = yourname@example.com
sender = yourname@example.com

# to ban & send an e-mail with whois report to the destemail.
action = %(action_mw)s

# same as action_mw but also send relevant log lines
#action = %(action_mwl)s

```

### Firewall and services

By default, Fail2ban uses [Iptables](/index.php/Iptables "Iptables"). However, configuration of most [firewalls](/index.php/Firewalls "Firewalls") and services is straightforward. For example, to use [Nftables](/index.php/Nftables "Nftables"):

 `/etc/fail2ban/jail.local` 
```
[DEFAULT]
banaction = nftables

```

See `/etc/fail2ban/action.d/` for other examples, e.g. [ufw.conf](https://github.com/fail2ban/fail2ban/blob/master/config/action.d/ufw.conf).

## Tips and tricks

### Custom SSH jail

**Warning:** If the attacker knows your IP address, they can send packets with a spoofed source header and get your IP address locked out of the server. [SSH keys](/index.php/SSH_keys "SSH keys") provide an elegant solution to the problem of brute forcing without these problems.

Edit `/etc/fail2ban/jail.d/sshd.local`, add this section and update the list of trusted IP addresses in `ignoreip`:

 `/etc/fail2ban/jail.d/sshd.local` 
```
[sshd]
enabled   = true
filter    = sshd
banaction = iptables
backend   = systemd
maxretry  = 5
findtime  = 1d
bantime   = 2w
ignoreip  = 127.0.0.1/8
```

**Note:**

*   It may be necessary to set `LogLevel VERBOSE` in `/etc/ssh/sshd_config` to allow full fail2ban monitoring as otherwise password failures may not be logged correctly.
*   Fail2ban has IPv6 support since version 0.10\. Adapt your [firewall](/index.php/Firewall "Firewall") accordingly, e.g. [start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") `ip6tables.service`.

**Tip:**

*   If using [iptables](/index.php/Iptables "Iptables") front-ends like [ufw](/index.php/Ufw "Ufw"), one can use `banaction = ufw` instead of using iptables.
*   When using [Shorewall](/index.php/Shorewall "Shorewall"), one can use `banaction = shorewall` and also set `BLACKLIST` to `ALL` in `/etc/shorewall/shorewall.conf`, otherwise the rule added to ban an IP address will affect only new connections.

### Service hardening

Currently, Fail2ban must be run as *root*. Therefore, you may wish to consider hardening the process with [systemd](/index.php/Systemd "Systemd").

[Create](/index.php/Create "Create") a [drop-in](/index.php/Systemd#Drop-in_files "Systemd") configuration file for `fail2ban.service`:

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

The `CapabilityBoundingSet` parameters `CAP_DAC_READ_SEARCH` will allow Fail2ban full read access to every directory and file, `CAP_NET_ADMIN` and `CAP_NET_RAW` allow setting of firewall rules with [iptables](/index.php/Iptables "Iptables"). See [capabilities(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/capabilities.7) for more info.

By using `ProtectSystem=strict` the [filesystem](/index.php/Filesystem "Filesystem") hierarchy will only be read-only, `ReadWritePaths` allows Fail2ban to have write access on required paths.

Create `/etc/fail2ban/fail2ban.local` with the correct `logtarget` path:

 `/etc/fail2ban/fail2ban.local` 
```
[Definition]
logtarget = /var/log/fail2ban/fail2ban.log

```

Create the `/var/log/fail2ban` directory as root.

Finally, [reload systemd daemon](/index.php/Systemd#Using_units "Systemd") to apply the changes of the unit and [restart](/index.php/Restart "Restart") `fail2ban.service`.

## See also

*   [Using a Fail2Ban Jail to Whitelist a User](https://www.the-art-of-web.com/system/fail2ban-action-whitelist/)
*   [Optimising your Fail2Ban filters](https://www.the-art-of-web.com/system/fail2ban-filters/)
*   [Fail2Ban and sendmail](https://www.the-art-of-web.com/system/fail2ban-sendmail/)
*   [Fail2Ban and iptables](https://www.the-art-of-web.com/system/fail2ban/)
*   [Fail2Ban 0.8.3 Howto](https://www.the-art-of-web.com/system/fail2ban-howto/)
*   [Monitoring the fail2ban log](https://www.the-art-of-web.com/system/fail2ban-log/)