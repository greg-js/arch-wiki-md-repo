This is intended to be a starting point for creating standard uid and gid numbers.

I really think this should be moved directly into arch at some point and just have a a keyword in PKGBUILD like

```
require_user('user1' 'user2')
require_group('group1')

```

and if they didn't exist they would be created according to this database by makepkg when building or by pacman when installing.

Actually, for this to work, we will need to add the primary and secondary groups to the database as well.

## Users

| Owning Package | User Name | UID |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | root | 0 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | bin | 1 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | daemon | 2 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | mail | 8 |
 news | 9 |
 uucp | 10 |
 ftp | 14 |
 proxy | 15 |
 stunnel | 16 |
 jabber | 17 |
 osiris | 18 |
 slocate | 21 |
 cron | 22 |
 fcron | 23 |
 snort | 29 |
 nagios (coming soon) | 30 |
 nrpe | 31 |
| [rpcbind](https://www.archlinux.org/packages/?name=rpcbind) | rpc | 32 |
 http | 33 |
 named | 40 |
 privoxy | 42 |
| [tor](https://www.archlinux.org/packages/?name=tor) | tor | 43 |
| [nbd](https://www.archlinux.org/packages/?name=nbd) | nbd | 44 |
 mpd | 45 |
 mopidy | 46 |
 nut | 55 |
 tomcat8 | 57 |
 rbldns | 58 |
 rbldnszones | 59 |
 dnslog | 60 |
 dnscache | 61 |
 tinydns | 62 |
 axfrdns | 63 |
 clamav | 64 |
 bitlbee | 65 |
 tomcat6 | 66 |
 minbif | 67 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | uuidd | 68 |
 fax | 69 |
 cyrus | 70 |
 tomcat7 | 71 |
 courier | 72 |
 postfix | 73 |
| [dovecot](https://www.archlinux.org/packages/?name=dovecot) | dovenull | 74 |
| [dovecot](https://www.archlinux.org/packages/?name=dovecot) | dovecot | 76 |
 asterisk | 77 |
 exim | 79 |
 vpopmail | 80 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | dbus | 81 |
 nsvsd | 83 |
 avahi | 84 |
 nx | 85 |
 beaglidx | 86 |
| [ntp](https://www.archlinux.org/packages/?name=ntp) | ntp | 87 |
 postgres | 88 |
 mysql | 89 |
 fetchmail | 90 |
 smtpd | 91 |
 smtpq | 92 |
 smtpf | 93 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | nobody | 99 |
| [polkit](https://www.archlinux.org/packages/?name=polkit) | polkitd | 102 |
| [minio](https://www.archlinux.org/packages/?name=minio) | minio | 103 |
 nm-openconnect | 104 |
 gitlab | 105 |
 cherokee | 106 |
 gitlab-runner | 107 |
 partimag | 110 |
| [x2goserver](https://www.archlinux.org/packages/?name=x2goserver) | x2gouser | 111 |
| [x2goserver](https://www.archlinux.org/packages/?name=x2goserver) | x2goprint | 112 |
 unifi | 113 |
 gdm | 120 |
 lxdm | 121 |
 murmurd | 122 |
 colord | 124 |
 deluge | 125 |
 backuppc | 126 |
 lldpd | 127 |
 pulse | 130 |
 rtkit | 133 |
 netdata | 134 |
 kdm | 135 |
 znc (deprecated, now dynamic) | 136 |
 usbmux | 140 |
 salt | 141 |
 nvidia-persistenced | 143 |
| [nss-pam-ldapd](https://www.archlinux.org/packages/?name=nss-pam-ldapd) | nslcd | 146 |
| [transmission-cli](https://www.archlinux.org/packages/?name=transmission-cli) | transmission | 169 |
| [zabbix-server](https://www.archlinux.org/packages/?name=zabbix-server) | zabbix-server | 170 |
| [zabbix-proxy](https://www.archlinux.org/packages/?name=zabbix-proxy) | zabbix-proxy | 171 |
| [zabbix-agent](https://www.archlinux.org/packages/?name=zabbix-agent) | zabbix-agent | 172 |
 postfwd | 180 |
 smokeping | 181 |
 spamd | 182 |
| [chrony](https://www.archlinux.org/packages/?name=chrony) | chrony | 183 |
| [pdnsd](https://www.archlinux.org/packages/?name=pdnsd) | pdnsd | 184 |
| [polipo](https://www.archlinux.org/packages/?name=polipo) | polipo | 185 |
| [tinyproxy](https://www.archlinux.org/packages/?name=tinyproxy) | tinyproxy | 186 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | systemd-journal-gateway | 191 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | systemd-timesync | 192 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | systemd-network | 193 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | systemd-bus-proxy | 194 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | systemd-resolve | 195 |
| [gitolite](https://www.archlinux.org/packages/?name=gitolite) | gitolite | 196 |
| [rabbitmq](https://www.archlinux.org/packages/?name=rabbitmq) | rabbitmq | 197 |
| [matrix-synapse](https://www.archlinux.org/packages/?name=matrix-synapse) | synapse | 198 |
| [toxcore](https://www.archlinux.org/packages/?name=toxcore) | tox-bootstrapd | 199 |
| [kubernetes](https://aur.archlinux.org/packages/kubernetes/) | kubernetes | 205 |
| [kibana](https://www.archlinux.org/packages/?name=kibana) | kibana | 206 |
| [grafana](https://www.archlinux.org/packages/?name=grafana) | grafana | 207 |
| [consul](https://www.archlinux.org/packages/?name=consul) | consul | 208 |
| [amavisd-new](https://www.archlinux.org/packages/?name=amavisd-new) | amavis | 333 |
| [ceph](https://www.archlinux.org/packages/?name=ceph) | ceph | 340 |
 ldap | 439 |
 oprofile | 492 |
 alias | 7790 |
 qmaild | 7791 |
 qmaill | 7792 |
 qmailp | 7793 |
 qmailq | 7794 |
 qmailr | 7795 |
 qmails | 7796 |

## Groups

| Owning Package | Group Name | GID |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | root | 0 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | bin | 1 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | daemon | 2 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | sys | 3 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | adm | 4 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | tty | 5 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | disk | 6 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | lp | 7 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | mem | 8 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | kmem | 9 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | wheel | 10 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | ftp | 11 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | mail | 12 |
 news | 13 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | uucp | 14 |
 proxy | 15 |
 stunnel | 16 |
 jabber | 17 |
 osiris | 18 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | log | 19 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | utmp | 20 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | locate (ex slocate/mlocate/rlocate) | 21 |
 cron | 22 |
 fcron | 23 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | rfkill | 24 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | smmsp | 25 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | proc | 26 |
 snort | 29 |
 nagios (coming soon) | 30 |
 nrpe | 31 |
| [rpcbind](https://www.archlinux.org/packages/?name=rpcbind) | rpc | 32 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | http | 33 |
 named | 40 |
 privoxy | 42 |
| [tor](https://www.archlinux.org/packages/?name=tor) | tor | 43 |
| [nbd](https://www.archlinux.org/packages/?name=nbd) | nbd | 44 |
 mpd | 45 |
 mopidy | 46 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | games | 50 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | lock | 54 |
 nut | 55 |
 bumblebee | 56 |
 tomcat8 | 57 |
 rbldns | 58 |
 rbldnszones | 59 |
 clamav | 64 |
 bitlbee | 65 |
 tomcat6 | 66 |
 minbif | 67 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | uuidd | 68 |
 cyrus | 70 |
 tomcat7 | 71 |
 courier | 72 |
| [dovecot](https://www.archlinux.org/packages/?name=dovecot) | dovenull | 74 |
 postdrop | 75 |
| [dovecot](https://www.archlinux.org/packages/?name=dovecot) | dovecot | 76 |
 asterisk | 77 |
 kvm | 78 |
 exim | 79 |
 vchkpw | 80 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | dbus | 81 |
 nsvsd | 83 |
 avahi | 84 |
 nx | 85 |
 beaglidx | 86 |
| [ntp](https://www.archlinux.org/packages/?name=ntp) | ntp | 87 |
 postgres | 88 |
 mysql | 89 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | network | 90 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | video | 91 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | audio | 92 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | optical | 93 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | floppy | 94 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | storage | 95 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | scanner | 96 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | input | 97 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | power | 98 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | nobody | 99 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | users | 100 |
| [polkit](https://www.archlinux.org/packages/?name=polkit) | polkitd | 102 |
| [minio](https://www.archlinux.org/packages/?name=minio) | minio | 103 |
 nm-openconnect | 104 |
 gitlab | 105 |
 cherokee | 106 |
 gitlab-runner | 107 |
 vboxusers | 108 |
 vboxsf | 109 |
 partimag | 110 |
| [x2goserver](https://www.archlinux.org/packages/?name=x2goserver) | x2gouser | 111 |
| [x2goserver](https://www.archlinux.org/packages/?name=x2goserver) | x2goprint | 112 |
 unifi | 113 |
 gdm | 120 |
 lxdm | 121 |
 murmurd | 122 |
| [colord](https://www.archlinux.org/packages/?name=colord) | colord | 124 |
 deluge | 125 |
 backuppc | 126 |
 lldpd | 127 |
 vlock | 129 |
 pulse | 130 |
 pulse-access | 131 |
 pulse-rt | 132 |
 rtkit | 133 |
 netdata | 134 |
 kdm | 135 |
 znc (deprecated, now dynamic) | 136 |
 usbmux | 140 |
 salt | 141 |
 docker (deprecated, now dynamic) | 142 |
 nvidia-persistenced | 143 |
 smtpd | 145 |
| [nss-pam-ldapd](https://www.archlinux.org/packages/?name=nss-pam-ldapd) | nslcd | 146 |
| [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli) | wireshark | 150 |
 cgred | 160 |
| [transmission-cli](https://www.archlinux.org/packages/?name=transmission-cli) | transmission | 169 |
| [zabbix-server](https://www.archlinux.org/packages/?name=zabbix-server) | zabbix-server | 170 |
| [zabbix-proxy](https://www.archlinux.org/packages/?name=zabbix-proxy) | zabbix-proxy | 171 |
| [zabbix-agent](https://www.archlinux.org/packages/?name=zabbix-agent) | zabbix-agent | 172 |
 postfwd | 180 |
 smokeping | 181 |
 spamd | 182 |
| [chrony](https://www.archlinux.org/packages/?name=chrony) | chrony | 183 |
| [pdnsd](https://www.archlinux.org/packages/?name=pdnsd) | pdnsd | 184 |
| [polipo](https://www.archlinux.org/packages/?name=polipo) | polipo | 185 |
| [tinyproxy](https://www.archlinux.org/packages/?name=tinyproxy) | tinyproxy | 186 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | systemd-journal | 190 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | systemd-journal-gateway | 191 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | systemd-timesync | 192 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | systemd-network | 193 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | systemd-bus-proxy | 194 |
| [filesystem](https://www.archlinux.org/packages/?name=filesystem) | systemd-resolve | 195 |
| [gitolite](https://www.archlinux.org/packages/?name=gitolite) | gitolite | 196 |
| [rabbitmq](https://www.archlinux.org/packages/?name=rabbitmq) | rabbitmq | 197 |
| [matrix-synapse](https://www.archlinux.org/packages/?name=matrix-synapse) | synapse | 198 |
| [toxcore](https://www.archlinux.org/packages/?name=toxcore) | tox-bootstrapd | 199 |
| [grsec-common](https://www.archlinux.org/packages/?name=grsec-common) | tpe | 200 |
| [grsec-common](https://www.archlinux.org/packages/?name=grsec-common) | audit | 201 |
| [grsec-common](https://www.archlinux.org/packages/?name=grsec-common) | socket-deny-all | 202 |
| [grsec-common](https://www.archlinux.org/packages/?name=grsec-common) | socket-deny-client | 203 |
| [grsec-common](https://www.archlinux.org/packages/?name=grsec-common) | socket-deny-server | 204 |
| [kubernetes](https://aur.archlinux.org/packages/kubernetes/) | kubernetes | 205 |
| [kibana](https://www.archlinux.org/packages/?name=kibana) | kibana | 206 |
| [grafana](https://www.archlinux.org/packages/?name=grafana) | grafana | 207 |
| [consul](https://www.archlinux.org/packages/?name=consul) | consul | 208 |
| [amavisd-new](https://www.archlinux.org/packages/?name=amavisd-new) | amavis | 333 |
| [ceph](https://www.archlinux.org/packages/?name=ceph) | ceph | 340 |
 ldap | 439 |
 oprofile | 492 |
 qmail | 2107 |
 nofiles | 2108 |