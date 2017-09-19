Related articles

*   [fail2ban](/index.php/Fail2ban "Fail2ban")
*   [ssh](/index.php/Ssh "Ssh")

**Warning:** Using an IP blacklist will stop trivial attacks but it relies on an additional daemon and successful logging (the partition containing /var can become full, especially if an attacker is pounding on the server). Additionally, if the attacker knows your IP address, they can send packets with a spoofed source header and get you locked out of the server. [SSH keys](/index.php/SSH_keys "SSH keys") provide an elegant solution to the problem of brute forcing without these problems.

[sshguard](http://www.sshguard.net) is a daemon that protects [SSH](/index.php/SSH "SSH") and other services against brute-force attacks, similar to [fail2ban](/index.php/Fail2ban "Fail2ban").

sshguard is different from the latter in that it is written in C, is lighter and simpler to use with fewer features while performing its core function equally well.

sshguard is not vulnerable to most (or maybe any) of the log analysis [vulnerabilities](https://web.archive.org/web/20120625102244/http://www.ossec.net/main/attacking-log-analysis-tools) that have caused problems for similar tools.

## Contents

*   [1 Installation](#Installation)
*   [2 Setup](#Setup)
    *   [2.1 FirewallD](#FirewallD)
    *   [2.2 UFW](#UFW)
    *   [2.3 iptables](#iptables)
*   [3 Usage](#Usage)
    *   [3.1 systemd](#systemd)
    *   [3.2 syslog-ng](#syslog-ng)
*   [4 Configuration](#Configuration)
    *   [4.1 Change danger level](#Change_danger_level)
    *   [4.2 Aggressive banning](#Aggressive_banning)
*   [5 Tips and Tricks](#Tips_and_Tricks)
    *   [5.1 Unbanning](#Unbanning)
    *   [5.2 Logging](#Logging)

## Installation

[Install](/index.php/Install "Install") the [sshguard](https://www.archlinux.org/packages/?name=sshguard) package.

## Setup

sshguard works by monitoring `/var/log/auth.log`, syslog-ng or the systemd journal for failed login attempts. For each failed attempt, the offending host is banned from further communication for a limited amount of time. The default amount of time the offender is banned starts at 7 minutes, and doubles each time he or she fails another login. sshguard can be configured to permanently ban a host with too many failed attempts.

Both temporary and permanent bans are done by adding an entry into the "sshguard" chain in iptables that drops all packets from the offender. The ban is then logged to syslog and ends up in `/var/log/auth.log`, or the systemd journal, if systemd is being used. To make the ban only affect port 22, simply do not send packets going to other ports through the "sshguard" chain.

You must configure a firewall to be used with sshguard in order for blocking to work.

#### FirewallD

sshguard can work with Firewalld. Make sure you have firewalld enabled, configured and setup first. To make sshguard write to your zone of preference, issue the following commands:

```
# firewallctl zone "<zone name>" --permanent add rich-rule "rule source ipset=sshguard4 drop"

```

If you use ipv6, you can issue the same command but substitute sshguard4 with sshguard6\. Finish with

```
# firewall-cmd --reload

```

You can verify the above with

```
# firewall-cmd --info-ipset=sshguard4

```

Finally, in /etc/sshguard.conf, find the line for BACKEND and change it as follows

```
BACKEND="/usr/lib/sshguard/sshg-fw-firewalld"

```

#### UFW

If UFW is installed and enabled, it must be given the ability to pass along DROP control to sshguard. This is accomplished by modifying `/etc/ufw/before.rules` to contain the following lines which should be inserted just after the section for loopback devices.
**Note:** Users running sshd on a non-standard port should substitute that in the final line above (where 22 is the standard).
 `/etc/ufw/before.rules` 
```
# allow all on loopback
-A ufw-before-input -i lo -j ACCEPT
-A ufw-before-output -o lo -j ACCEPT

# hand off control for sshd to sshguard
-N sshguard
-A ufw-before-input -p tcp --dport 22 -j sshguard

```

[Restart](/index.php/Restart "Restart") ufw after making this modification.

#### iptables

**Note:** See [iptables](/index.php/Iptables "Iptables") and [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall") first to set up a firewall.

The main configuration required is creating a chain named `sshguard`, where sshguard automatically inserts rules to drop packets coming from bad hosts:

```
# iptables -N sshguard

```

Then add a rule to jump to the `sshguard` chain from the `INPUT` chain. This rule must be added **before** any other rules processing the ports that sshguard is protecting. See [this example](http://www.sshguard.net/docs/setup/#netfilter-iptables).

```
# iptables -A INPUT -p tcp --dport 22 -j sshguard

```

To save the rules:

```
# iptables-save > /etc/iptables/iptables.rules

```

**Note:** For IPv6, repeat the same steps with *ip6tables* and save the rules with *ip6tables-save* to `/etc/iptables/ip6tables.rules`.

## Usage

### systemd

[Enable](/index.php/Enable "Enable") and start the `sshguard.service`.

### syslog-ng

If you have [syslog-ng](https://www.archlinux.org/packages/?name=syslog-ng) installed, you may start sshguard directly from the command line instead.

```
/usr/sbin/sshguard -l /var/log/auth.log -b /var/db/sshguard/blacklist.db

```

## Configuration

Configuration is done in `/etc/sshguard.conf` which is required for *sshguard* to start. A commented example is located at `/usr/share/doc/sshguard/sshguard.conf.sample`.

**Note:** Piped commands and runtime flags in *sshguards's* systemd units [are not supported](https://sourceforge.net/p/sshguard/mailman/message/35709860/). Such flags can be modified in the configuration file.

### Change danger level

By default in the Arch-provided configuration file, offenders become permanently banned once they have reached a "danger" level of 120 (or 12 failed logins; see [terminology](http://www.sshguard.net/docs/terminology/) for more details). This behavior can be modified by prepending a danger level to the blacklist file.

```
BLACKLIST_FILE=200:/var/db/sshguard/blacklist.db

```

The `200:` in this example tells sshguard to permanently ban a host after achieving a danger level of 200.

Finally [restart](/index.php/Restart "Restart") the `sshguard.service` unit.

### Aggressive banning

For some users under constant attack, it may be beneficial to enable a more aggressive banning policy. If you can be reasonably sure that accidental failed logins are unlikely, then you can instruct SSHGuard to automatically ban hosts with a single failed login. Modify the parameters in the configuration file in the following way:

```
THRESHOLD=10
BLACKLIST_FILE=10:/var/db/sshguard/blacklist.db

```

Finally [restart](/index.php/Restart "Restart") the `sshguard.service` unit.

To prevent multiple authentication attempts during a single connection, you may also want to change /etc/ssh/sshd_config by defining:

```
MaxAuthTries 1

```

You will have to [restart](/index.php/Restart "Restart") the `sshd.service` unit for this change to take effect.

## Tips and Tricks

### Unbanning

If you *yourself* get banned, you can wait to get unbanned automatically or use iptables to unban yourself. First check if your IP is banned by sshguard:

```
# iptables -L sshguard --line-numbers --numeric

```

Then use the following command to unban, with the line-number as identified in the former command:

```
# iptables -D sshguard <line-number>

```

You will also need to remove the IP address from `/var/db/sshguard/blacklist.db` in order to make unbanning persistent.

```
# sed -i '/<ip-address>/d' /var/db/sshguard/blacklist.db

```

### Logging

To see what is being passed to sshguard, examine the script in `/usr/lib/systemd/scripts/sshguard-journalctl` and the systemd service `sshguard.service`. An equivalent command to view the logs in the terminal:

```
$ journalctl -afb -p info SYSLOG_FACILITY=4 SYSLOG_FACILITY=10

```