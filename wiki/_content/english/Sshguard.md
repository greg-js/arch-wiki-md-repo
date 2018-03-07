Related articles

*   [fail2ban](/index.php/Fail2ban "Fail2ban")
*   [ssh](/index.php/Ssh "Ssh")

**Warning:** Using an IP blacklist will stop trivial attacks but it relies on an additional daemon and successful logging (the partition containing /var can become full, especially if an attacker is pounding on the server). Additionally, with the knowledge of your IP address, the attacker can send packets with a spoofed source header and get you locked out of the server. [SSH keys](/index.php/SSH_keys "SSH keys") provide an elegant solution to the problem of brute forcing without these problems.

[sshguard](http://www.sshguard.net) is a daemon that protects [SSH](/index.php/SSH "SSH") and other services against brute-force attacks, similar to [fail2ban](/index.php/Fail2ban "Fail2ban").

sshguard is different from the latter in that it is written in C, is lighter and simpler to use with fewer features while performing its core function equally well.

sshguard is not vulnerable to most (or maybe any) of the log analysis [vulnerabilities](https://web.archive.org/web/20120625102244/http://www.ossec.net/main/attacking-log-analysis-tools) that have caused problems for similar tools.

## Contents

*   [1 Installation](#Installation)
*   [2 Setup](#Setup)
    *   [2.1 FirewallD](#FirewallD)
    *   [2.2 UFW](#UFW)
    *   [2.3 iptables](#iptables)
    *   [2.4 nftables](#nftables)
*   [3 Usage](#Usage)
    *   [3.1 systemd](#systemd)
    *   [3.2 syslog-ng](#syslog-ng)
*   [4 Configuration](#Configuration)
    *   [4.1 Blacklisting threshold](#Blacklisting_threshold)
    *   [4.2 Moderate banning example](#Moderate_banning_example)
    *   [4.3 Aggressive banning](#Aggressive_banning)
*   [5 Tips and Tricks](#Tips_and_Tricks)
    *   [5.1 Unbanning](#Unbanning)
        *   [5.1.1 iptables](#iptables_2)
        *   [5.1.2 nftables](#nftables_2)
    *   [5.2 Logging](#Logging)

## Installation

[Install](/index.php/Install "Install") the [sshguard](https://www.archlinux.org/packages/?name=sshguard) package.

## Setup

sshguard works by monitoring `/var/log/auth.log`, syslog-ng or the [systemd journal](/index.php/Systemd#Journal "Systemd") for failed login attempts. For each failed attempt, the offending host is banned from further communication for a limited amount of time. The default amount of time the offender is banned starts at 120 seconds, and is increases by a factor of 1.5 every time it fails another login. sshguard can be configured to permanently ban a host with too many failed attempts.

Both temporary and permanent bans are done by adding an entry into the "sshguard" chain in iptables that drops all packets from the offender. The ban is then logged to syslog and ends up in `/var/log/auth.log`, or the systemd journal if the latter is being used.

You must configure one of the following firewalls to be used with sshguard in order for blocking to work.

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

Then add a rule to jump to the `sshguard` chain from the `INPUT` chain. This rule must be added **before** any other rules processing the ports that sshguard is protecting. Use the following line to protect FTP and SSH or see [this documentation](http://www.sshguard.net/docs/setup/#netfilter-iptables) for more examples.

```
# iptables -A INPUT -m multiport -p tcp --destination-ports 21,22 -j sshguard

```

To save the rules:

```
# iptables-save > /etc/iptables/iptables.rules

```

**Note:** For IPv6, repeat the same steps with *ip6tables* and save the rules with *ip6tables-save* to `/etc/iptables/ip6tables.rules`.

#### nftables

Edit `/etc/sshguard.conf` and change the value of `BACKEND` to the following:

 `/etc/sshguard.conf`  `BACKEND="/usr/lib/sshguard/sshg-fw-nft-sets"` 

Additionally you will need to [edit](/index.php/Edit "Edit") the `sshguard.service` so that [iptables](/index.php/Iptables "Iptables") is not run:

```
[Service]
ExecStartPre= 

```

When you [start/enable](/index.php/Start/enable "Start/enable") the `sshguard.service`, two new tables named `sshguard` in the `ip` and `ip6` address families are added which filter incoming traffic through sshguard's list of IP addresses. The chains in the `sshguard` table have a priority of -10 and will be processed before other rules of lower priority. See [sshguard-setup(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sshguard-setup.7) and [nftables](/index.php/Nftables "Nftables") for more information.

## Usage

### systemd

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `sshguard.service`.

### syslog-ng

If you have [syslog-ng](https://www.archlinux.org/packages/?name=syslog-ng) installed, you may start sshguard directly from the command line instead.

```
/usr/sbin/sshguard -l /var/log/auth.log -b /var/db/sshguard/blacklist.db

```

## Configuration

Configuration is done in `/etc/sshguard.conf` which is required for *sshguard* to start. A commented example is located at `/usr/share/doc/sshguard/sshguard.conf.sample`.

**Note:** Piped commands and runtime flags in *sshguard's* systemd units [are not supported](https://sourceforge.net/p/sshguard/mailman/message/35709860/). Such flags can be modified in the configuration file.

### Blacklisting threshold

By default in the Arch-provided configuration file, offenders become permanently banned once they reach a "danger" level of 120 (or 12 failed logins; see [attack dangerousness](https://www.sshguard.net/docs/terminology/#attack-dangerousness) for more details). This behavior can be modified by prepending a danger level to the blacklist file.

```
BLACKLIST_FILE=200:/var/db/sshguard/blacklist.db

```

The `200:` in this example tells sshguard to permanently ban a host after achieving a danger level of 200.

Finally [restart](/index.php/Restart "Restart") `sshguard.service`

### Moderate banning example

A slightly more aggressive banning rule than the default one is proposed here to illustrate various options. It monitors [sshd](/index.php/Sshd "Sshd") and [vsftpd](/index.php/Vsftpd "Vsftpd") via logs from the *systemd journal*. It blocks attackers after 2 attempts for 180 sec with subsequent block time longer by a factor of 1.5\. Note that this multiplicative delay feature is internal and not controlled by the below settings. The attackers are remembered for up to 3600 sec and permanently blacklisted after 10 attempts (10 attempts having each a cost of 10, explaining the "100" parameter in the blacklist setting). It blocks not only the attacker's IP but all the IPv4 subnet 24 ([CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing "wikipedia:Classless Inter-Domain Routing") notation).

```
BACKEND="/usr/lib/sshguard/sshg-fw-iptables"
LOGREADER="LANG=C /usr/bin/journalctl -afb -p info -n1 -t sshd -t vsftpd -o cat"
THRESHOLD=20
BLOCK_TIME=180
DETECTION_TIME=3600
BLACKLIST_FILE=100:/var/db/sshguard/blacklist.db
IPV4_SUBNET=24

```

### Aggressive banning

For some users under constant attack, a more aggressive banning policy can be adopted. If you are confident that accidental failed logins are unlikely, you can instruct SSHGuard to permanently ban hosts after a single failed login. Modify the parameters in the configuration file in the following way:

```
THRESHOLD=10
BLACKLIST_FILE=10:/var/db/sshguard/blacklist.db

```

Finally [restart](/index.php/Restart "Restart") `sshguard.service`.

Also, to prevent multiple authentication attempts during a single connection, you may want to change `/etc/ssh/sshd_config` by defining:

```
MaxAuthTries 1

```

[Restart](/index.php/Restart "Restart") `sshd.service` for this change to take effect.

## Tips and Tricks

### Unbanning

If you ban *yourself*, you can wait to get unbanned automatically or use iptables or nftables to unban yourself.

#### iptables

First check if your IP is banned by sshguard:

```
# iptables --list sshguard --line-numbers --numeric

```

Then use the following command to unban, with the line-number as identified in the former command:

```
# iptables --delete sshguard *line-number*

```

You will also need to remove the IP address from `/var/db/sshguard/blacklist.db` in order to make unbanning persistent.

#### nftables

Remove your IP address from the `attackers` set:

```
# nft delete element *family* sshguard attackers { *ip_address* }

```

where `*family*` is either `ip` or `ip6`.

### Logging

To see what is being passed to sshguard, examine the script in `/usr/lib/systemd/scripts/sshguard-journalctl` and the systemd service `sshguard.service`. An equivalent command to view the logs in the terminal:

```
$ journalctl -afb -p info SYSLOG_FACILITY=4 SYSLOG_FACILITY=10

```