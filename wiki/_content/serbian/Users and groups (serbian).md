User groups are used on GNU/Linux for [access control](https://en.wikipedia.org/wiki/Access_control#Computer_security "wikipedia:Access control") – members of a group are granted access to devices and files belonging to that group. `/etc/group` is the file that defines the groups on the system ([group(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/group.5) for details).

This article provides a list of common groups and their purpose along with an overview of group manipulation commands.

## Contents

*   [1 Korisne grupe](#Korisne_grupe)
*   [2 Group list](#Group_list)
*   [3 Group manipulation](#Group_manipulation)
    *   [3.1 List groups](#List_groups)
    *   [3.2 Find group ownership](#Find_group_ownership)
    *   [3.3 Manage group membership](#Manage_group_membership)
    *   [3.4 Manage groups](#Manage_groups)

## Korisne grupe

Preporučene grupe koje korisnik treba da postavi za svoje korisnički nalog.

*   **audio** - za pristup audio hardveru
*   **floppy** - za pristup flopiu (ovo u slačaju samo ko ga poseduje)
*   **lp** - za pristup štampačima
*   **optical** - za pristup CD ili DVD čitačima (npr. puštanje CD-a)
*   **power** - used with power options (e.g. shutdown with power button)
*   **storage** - za uređivanje skladišnog prostora
*   **video** - za video aceleraciju
*   **wheel** - za [sudo](/index.php/Sudo "Sudo") privilegije

## Group list

<caption>A list of groups and their function (sorted alphabetically)</caption>
| Group | Affected files | Purpose |
| adm | /var/log/* | Read access to log files in /var/log |
| audio | /dev/sound/*, /dev/snd/*, /dev/misc/rtc0 | Access to sound hardware. |
| avahi |
| bin | /usr/bin/* | Right to modify binaries only by root, but right to read or executed by anyone. (Please modify this for better understanding...) |
| camera | Access to [Digital Cameras](/index.php/Digital_Cameras "Digital Cameras"). |
| clamav | /var/lib/clamav/*, /var/log/clamav/* |
| daemon |
| dbus | /var/run/dbus |
| disk | /dev/sda[1-9], /dev/sdb[1-9], etc | Access to block devices not affected by other groups such as optical,floppy,storage. |
| floppy | /dev/fd[0-9] | Access to floppy drives. |
| ftp | /srv/ftp |
| games | /var/games | Access to some game software. |
| gdm |
| hal | /var/run/hald, /var/cache/hald |
| http |
| kmem | /dev/port, /dev/mem, /dev/kmem |
| locate | /usr/bin/locate, /var/lib/locate, /var/lib/slocate, /var/lib/mlocate | Right to use updatedb command. |
| log | /var/log/* | Access to log files in /var/log, |
| lp | /etc/cups, /var/log/cups, /var/cache/cups, /var/spool/cups | Access to printer hardware |
| mem |
| mail | /usr/bin/mail |
| network | Right to change network settings such as when using a [NetworkManager](/index.php/NetworkManager "NetworkManager"). |
| networkmanager | Requirement for your user to connect wirelessly with [NetworkManager](/index.php/NetworkManager "NetworkManager"). This group is not included with Arch by default so it must be added manually. |
| nobody | Unprivileged group. |
| ntp |
| optical | /dev/sr[0-9], /dev/sg[0-9] | Access to optical devices such as CD,CD-R,DVD,DVD-R. |
| policykit |
| power | Right to use [suspend](/index.php/Pm-utils "Pm-utils") utils. |
| rfkill |
| root | /* -- ALL FILES! | Complete system administration and control (root, admin) |
| scanner | /var/lock/sane | Access to scanner hardware. |
| smmsp | sendmail group |
| storage | Access to removable drives such as USB hard drives, flash/jump drives, MP3 players. |
| stb-admin |
| sys | Right to admin printers in CUPS. |
| thinkpad | /dev/misc/nvram | Right for ThinkPad users using tools such as [tpb](/index.php/Tpb "Tpb"). |
| tty | /dev/tty, /dev/vcc, /dev/vc, /dev/ptmx |
| users | Standard users group. |
| uucp | /dev/ttyS[0-9] /dev/tts/[0-9] | Serial & USB devices such as modems, handhelds, RS 232/serial ports. |
| vboxusers | /dev/vboxdrv | Right to use VirtualBox software. |
| video | /dev/fb/0, /dev/misc/agpgart | Access to video capture devices, DRI/3D hardware acceleration. |
| vmware | Right to use VMware software. |
| wheel | Right to use [sudo](/index.php/Sudo "Sudo") (setup with visudo), Also affected by PAM |

## Group manipulation

### List groups

Display group membership with the `groups` command:

```
$ groups [user]

```

If `user` is omitted, the current user's group names are displayed.

The `id` command provides additional detail, such as the user's UID and associated GIDs:

```
$ id [user]

```

To list all groups on the system:

```
$ cat /etc/group

```

### Find group ownership

List files owned by a group with the `find` command:

```
# find / -group [group]

```

### Manage group membership

Add users to a group with the `gpasswd` command:

```
# gpasswd -a [user] [group]

```

To remove users from a group:

```
# gpasswd -d [user] [group]

```

If the user is currently logged in, he/she must log out and in again for the change to have effect.

### Manage groups

Create new groups with the `groupadd` command:

```
# groupadd [group]

```

To delete existing groups:

```
# groupdel [group]

```