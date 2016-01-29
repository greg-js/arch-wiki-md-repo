# Sshguard

Related articles

*   [fail2ban](/index.php/Fail2ban "Fail2ban")
*   [ssh](/index.php/Ssh "Ssh")

**Warning:** Using an IP blacklist will stop trivial attacks but it relies on an additional daemon and successful logging (the partition containing /var can become full, especially if an attacker is pounding on the server). Additionally, if the attacker knows your IP address, they can send packets with a spoofed source header and get you locked out of the server. [SSH keys](/index.php/SSH_keys "SSH keys") provide an elegant solution to the problem of brute forcing without these problems.

[sshguard](http://www.sshguard.net) is a daemon that protects [SSH](/index.php/SSH "SSH") and other services against brute-force attacks, similar to [fail2ban](/index.php/Fail2ban "Fail2ban").

sshguard is different from the other two in that it is written in C, is lighter and simpler to use with fewer features while performing its core function equally well.

sshguard is not vulnerable to most (or maybe any) of the log analysis [vulnerabilities](http://www.ossec.net/main/attacking-log-analysis-tools) that have caused problems for similar tools.

## Contents

*   [1 Installation](#Installation)
*   [2 Setup](#Setup)
    *   [2.1 UFW](#UFW)
    *   [2.2 iptables](#iptables)
*   [3 Usage](#Usage)
    *   [3.1 systemd](#systemd)
    *   [3.2 syslog-ng](#syslog-ng)
*   [4 Configuration](#Configuration)
    *   [4.1 Change danger level](#Change_danger_level)
    *   [4.2 Aggressive banning](#Aggressive_banning)
*   [5 Tips and Tricks](#Tips_and_Tricks)
    *   [5.1 Unbanning](#Unbanning)

## Installation

[Install](/index.php/Install "Install") the [sshguard](https://www.archlinux.org/packages/?name=sshguard) package.

## Setup

sshguard works by monitoring `/var/log/auth.log`, syslog-ng or the systemd journal for failed login attempts. For each failed attempt, the offending host is banned from further communication for a limited amount of time. The default amount of time the offender is banned starts at 7 minutes, and doubles each time he or she fails another login. sshguard can be configured to permanently ban a host with too many failed attempts.

Both temporary and permanent bans are done by adding an entry into the "sshguard" chain in iptables that drops all packets from the offender. The ban is then logged to syslog and ends up in `/var/log/auth.log`, or the systemd journal, if systemd is being used. To make the ban only affect port 22, simply do not send packets going to other ports through the "sshguard" chain.

You must configure a firewall to be used with sshguard in order for blocking to work.

#### UFW

**Warning:** Currently, ufw-033-3 in [community] is not compatible with the method shown below. Users must use [ufw-bzr](https://aur.archlinux.org/packages/ufw-bzr/)<sup><small>AUR</small></sup> from the AUR.

If UFW is installed and enabled, it must be given the ability to pass along DROP control to sshguard. This is accomplished by modifying `/etc/ufw/before.rules` to contain the following lines which should be inserted just after the section for loopback devices.

**Note:** Users running sshd on a non-standard port should substitute that in the final line above (where 22 is the standard).

 `/etc/ufw/before.rules` 

```
# hand off control for sshd to sshguard
-N sshguard
-A ufw-before-input -p tcp --dport 22 -j sshguard

```

[Restart](/index.php/Restart "Restart") ufw after making this modification.

#### iptables

The main configuration required is creating a chain named "sshguard" in the INPUT chain of iptables where sshguard automatically inserts rules to drop packets coming from bad hosts:

```
# iptables -N sshguard
# iptables -A INPUT -p tcp --dport 22 -j sshguard
# iptables-save > /etc/iptables/iptables.rules

```

If you use IPv6:

```
# ip6tables -N sshguard
# ip6tables -A INPUT -p tcp --dport 22 -j sshguard
# ip6tables-save > /etc/iptables/ip6tables.rules

```

If you do not use IPv6, create and empty file "ip6tables.rules" with:

```
# touch /etc/iptables/ip6tables.rules

```

Finally, [reload](/index.php/Reload "Reload") the `iptables` service.

If you do not currently use iptables and just want to get sshguard up and running without any further impact on your system, these commands will create and save an iptables configuration that does absolutely nothing except allowing sshguard to work:

```
# iptables -F
# iptables -X
# iptables -P INPUT ACCEPT
# iptables -P FORWARD ACCEPT
# iptables -P OUTPUT ACCEPT
# iptables -N sshguard
# iptables -A INPUT -j sshguard 
# iptables-save > /etc/iptables/iptables.rules    

```

To finish saving your iptables configuration. Repeat above steps with `ip6tables` to configure the firewall rules for IPv6 and save them with `ip6tables-save` to `/etc/iptables/ip6tables.rules`.

For more information on using iptables to create powerful firewalls, see [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall").

## Usage

### systemd

[Enable](/index.php/Enable "Enable") and start the `sshguard.service`. The provided systemd unit uses a blacklist located at `/var/db/sshguard/blacklist.db` and pipes journalctl into sshguard for monitoring.

To add optional sshguard arguments, modify the provided service with drop-in snippets as described in [systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd").

### syslog-ng

If you have [syslog-ng](https://www.archlinux.org/packages/?name=syslog-ng) installed, you may start sshguard directly from the command line instead.

```
/usr/sbin/sshguard -l /var/log/auth.log -b /var/db/sshguard/blacklist.db

```

## Configuration

### Change danger level

By default in the Arch-provided systemd unit, offenders become permanently banned once they have reached a "danger" level of 120 (or 12 failed logins; see [terminology](http://www.sshguard.net/docs/terminology/) for more details). This behavior can be modified by prepending a danger level to the blacklist file.

[Edit the provided systemd unit](/index.php/Systemd#Editing_provided_units "Systemd") and change the `ExecStart=` line:

```
[Service]
ExecStart=
ExecStart=/usr/lib/systemd/scripts/sshguard-journalctl "-b 200:/var/db/sshguard/blacklist.db" SYSLOG_FACILITY=4 SYSLOG_FACILITY=10

```

The `200:` in this example tells sshguard to permanently ban a host after achieving a danger level of 200.

Finally [restart](/index.php/Restart "Restart") the `sshguard.service` unit.

### Aggressive banning

For some users under constant attack, it may be beneficial to enable a more aggressive banning policy. If you can be reasonably sure that accidental failed logins are unlikely, then you can instruct SSHGuard to automatically ban hosts with a single failed login. [Edit the provided systemd unit](/index.php/Systemd#Editing_provided_units "Systemd") in the following way:

```
[Service]
ExecStart=
ExecStart=/usr/lib/systemd/scripts/sshguard-journalctl "-a 1 -b 10:/var/db/sshguard/blacklist.db" SYSLOG_FACILITY=4 SYSLOG_FACILITY=10

```

Finally [restart](/index.php/Restart "Restart") the `sshguard.service` unit.

## Tips and Tricks

### Unbanning

If you get banned, you can wait to get unbanned automatically or use iptables to unban yourself. First check if your ip is banned by sshguard:

```
# iptables -L sshguard --line-numbers

```

Then use the following command to unban, with the line-number as identified in the former command:

```
# iptables -D sshguard <line-number>

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Sshguard&oldid=414745](https://wiki.archlinux.org/index.php?title=Sshguard&oldid=414745)"