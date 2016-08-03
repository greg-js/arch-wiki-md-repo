Users and groups are used on GNU/Linux for [access control](https://en.wikipedia.org/wiki/access_control#Computer_security "wikipedia:access control")—that is, to control access to the system's files, directories, and peripherals. Linux offers relatively simple/coarse access control mechanisms by default. For more advanced options, see [ACL](/index.php/ACL "ACL") and [PAM#Configuration How-Tos](/index.php/PAM#Configuration_How-Tos "PAM").

## Contents

*   [1 Overview](#Overview)
*   [2 Permissions and ownership](#Permissions_and_ownership)
*   [3 File list](#File_list)
*   [4 User management](#User_management)
    *   [4.1 Example adding a user](#Example_adding_a_user)
    *   [4.2 Example adding a system user](#Example_adding_a_system_user)
    *   [4.3 Other examples of user management](#Other_examples_of_user_management)
    *   [4.4 Username change tips](#Username_change_tips)
*   [5 User database](#User_database)
*   [6 Group management](#Group_management)
*   [7 Group list](#Group_list)
    *   [7.1 User groups](#User_groups)
    *   [7.2 System groups](#System_groups)
    *   [7.3 Software groups](#Software_groups)
    *   [7.4 Unused groups](#Unused_groups)
        *   [7.4.1 Pre-systemd groups](#Pre-systemd_groups)

## Overview

A *user* is anyone who uses a computer. In this case, we are describing the names which represent those users. It may be Mary or Bill, and they may use the names Dragonlady or Pirate in place of their real name. All that matters is that the computer has a name for each account it creates, and it is this name by which a person gains access to use the computer. Some system services also run using restricted or privileged user accounts.

Managing users is done for the purpose of security by limiting access in certain specific ways. The superuser (root) has complete access to the operating system and its configuration; it is intended for administrative use only. Unprivileged users can use the [su](/index.php/Su "Su") and [sudo](/index.php/Sudo "Sudo") programs for controlled privilege escalation.

Any individual may have more than one account, as long as they use a different name for each account they create. Further, there are some reserved names which may not be used such as "root".

Users may be grouped together into a "group", and users may be added to an existing group to utilize the privileged access it grants.

**Note:** The beginner should use these tools carefully and stay away from having anything to do with any other *existing* user account, other than their own.

## Permissions and ownership

From [In UNIX Everything is a File](http://ph7spot.com/musings/in-unix-everything-is-a-file):

	The UNIX operating system crystallizes a couple of unifying ideas and concepts that shaped its design, user interface, culture and evolution. One of the most important of these is probably the mantra: "everything is a file," widely regarded as one of the defining points of UNIX.

	This key design principle consists of providing a unified paradigm for accessing a wide range of input/output resources: documents, directories, hard-drives, CD-ROMs, modems, keyboards, printers, monitors, terminals and even some inter-process and network communications. The trick is to provide a common abstraction for all of these resources, each of which the UNIX fathers called a "file." Since every "file" is exposed through the same API, you can use the same set of basic commands to read/write to a disk, keyboard, document or network device.

From [Extending UNIX File Abstraction for General-Purpose Networking](http://www.intel-research.net/Publications/Pittsburgh/101220041324_277.pdf):

	A fundamental and very powerful, consistent abstraction provided in UNIX and compatible operating systems is the file abstraction. Many OS services and device interfaces are implemented to provide a file or file system metaphor to applications. This enables new uses for, and greatly increases the power of, existing applications — simple tools designed with specific uses in mind can, with UNIX file abstractions, be used in novel ways. A simple tool, such as cat, designed to read one or more files and output the contents to standard output, can be used to read from I/O devices through special device files, typically found under the `/dev` directory. On many systems, audio recording and playback can be done simply with the commands, "`cat /dev/audio > myfile`" and "`cat myfile > /dev/audio`," respectively.

Every file on a GNU/Linux system is owned by a user and a group. In addition, there are three types of access permissions: read, write, and execute. Different access permissions can be applied to a file's owning user, owning group, and others (those without ownership). One can determine a file's owners and permissions by viewing the long listing format of the [ls](/index.php/Ls "Ls") command:

 `$ ls -l /boot/` 
```
total 13740
drwxr-xr-x 2 root root    4096 Jan 12 00:33 grub
-rw-r--r-- 1 root root 8570335 Jan 12 00:33 initramfs-linux-fallback.img
-rw-r--r-- 1 root root 1821573 Jan 12 00:31 initramfs-linux.img
-rw-r--r-- 1 root root 1457315 Jan  8 08:19 System.map26
-rw-r--r-- 1 root root 2209920 Jan  8 08:19 vmlinuz-linux
```

The first column displays the file's permissions (for example, the file `initramfs-linux.img` has permissions `-rw-r--r--`). The third and fourth columns display the file's owning user and group, respectively. In this example, all files are owned by the *root* user and the *root* group.

 `$ ls -l /media/` 
```
total 16
drwxrwx--- 1 root vboxsf 16384 Jan 29 11:02 sf_Shared
```

In this example, the `sf_Shared` directory is owned by the *root* user and the *vboxsf* group. It is also possible to determine a file's owners and permissions using the stat command:

Owning user:

 `$ stat -c %U /media/sf_Shared/`  `root` 

Owning group:

 `$ stat -c %G /media/sf_Shared/`  `vboxsf` 

Access rights:

 `$ stat -c %A /media/sf_Shared/`  `drwxrwx---` 

Access permissions are displayed in three groups of characters, representing the permissions of the owning user, owning group, and others, respectively. For example, the characters `-rw-r--r--` indicate that the file's owner has read and write permission, but not execute (`rw-`), whilst users belonging to the owning group and other users have only read permission (`r--` and `r--`). Meanwhile, the characters `drwxrwx---` indicate that the file's owner and users belonging to the owning group all have read, write, and execute permissions (`rwx` and `rwx`), whilst other users are denied access (`---`). The first character represents the file's type.

List files owned by a user or group with the *find* utility:

```
# find / -group *group*

```

```
# find / -user *user*

```

A file's owning user and group can be changed with the *chown* (change owner) command. A file's access permissions can be changed with the *chmod* (change mode) command.

See [man chown](http://linux.die.net/man/1/chown), [man chmod](http://linux.die.net/man/1/chmod), and [Linux file permissions](http://www.linux.com/learn/tutorials/309527-understanding-linux-file-permissions) for additional detail.

## File list

**Warning:** Do not edit these files by hand. There are utilities that properly handle locking and avoid invalidating the format of the database. See [#User management](#User_management) and [#Group management](#Group_management) for an overview.

| File | Purpose |
| `/etc/shadow` | Secure user account information |
| `/etc/passwd` | User account information |
| `/etc/gshadow` | Contains the shadowed information for group accounts |
| `/etc/group` | Defines the groups to which users belong |
| `/etc/sudoers` | List of who can run what by sudo |
| `/home/*` | Home directories |

## User management

To list users currently logged on the system, the *who* command can be used. To list all existing user accounts including their properties stored in the [user database](#User_database), run `passwd -Sa` as root. See `passwd(1)` for the description of the output format.

To add a new user, use the *useradd* command:

```
# useradd -m -g *initial_group* -G *additional_groups* -s *login_shell* *username*

```

*   `-m` creates the user home directory as `/home/*username*`. Within their home directory, a non-root user can write files, delete them, install programs, and so on.
*   `-g` defines the group name or number of the user's initial login group. If specified, the group name must exist; if a group number is provided, it must refer to an already existing group. If not specified, the behaviour of *useradd* will depend on the `USERGROUPS_ENAB` variable contained in `/etc/login.defs`. The default behaviour (`USERGROUPS_ENAB yes`) is to create a group with the same name as the username, with `GID` equal to `UID`.
*   `-G` introduces a list of supplementary groups which the user is also a member of. Each group is separated from the next by a comma, with no intervening spaces. The default is for the user to belong only to the initial group.
*   `-s` defines the path and file name of the user's default login shell. After the boot process is complete, the default login shell is the one specified here. Ensure the chosen shell package is installed if choosing something other than [Bash](/index.php/Bash "Bash").

**Warning:** In order to be able to log in, the login shell must be one of those listed in `/etc/shells`, otherwise the [PAM](/index.php/PAM "PAM") module `pam_shell` will deny the login request. In particular, do not use the `/usr/bin/bash` path instead of `/bin/bash`, unless it is properly configured in `/etc/shells`.

**Note:** The password for the newly created user must then be defined, using *passwd* as shown in [#Example adding a user](#Example_adding_a_user).

When the login shell is intended to be non-functional, for example when the user account is created for a specific service, `/usr/bin/nologin` may be specified in place of a regular shell to politely refuse a login (see `nologin(8)`).

### Example adding a user

On a typical desktop system, use the following command to add a new user named `archie`, specify Bash as their login shell and add them to the [wheel](#User_groups) group:

```
# useradd -m -G wheel -s /bin/bash archie

```

**Tip:** Do not worry about adding the user to other groups now. If later on you will install a particular application, or perform a specific configuration, that requires explicitly adding the user to a group, the wiki will remind you to do it in the specific article that you will be following.

Although it is not required to protect the newly user `archie` with a password, it is highly recommend to do so:

```
# passwd archie

```

**Tip:** Bash is the default value for the shell (as indicated by `useradd -D`), so you can omit the `-s` option except if you want to use something else.

The above "useradd" command will also automatically create a group called `archie` with the same GID as the UID of the user `archie` and makes this the default group for `archie` on login. Making each user have their own group (with group name same as user name and GID same as UID) is the preferred way to add users.

You could also make the default group something else, e.g. `study`:

```
# useradd -m -g study -G wheel -s /bin/bash archie

```

Note that, in multi-user systems, using a single default group (e.g. `users`) for every user is not recommended. The reason is that typically, the method for facilitating shared write access for specific groups of users is setting user [umask](/index.php/Umask "Umask") value to `002`, which means that the default group will by default always have write access to any file you create. See also [User Private Groups](https://security.ias.edu/how-and-why-user-private-groups-unix).

In the recommended scenario, where the default group has the same name as the user name, all files are by default writeable only for the user who created them. To allow write access to a specific group, shared files/folders can be made writeable by default for everyone in this group and the owning group can be automatically fixed to the group which owns the parent directory by setting the setgid bit on this directory:

```
# chmod g+s *our_shared_directory*

```

Otherwise the file creator's default group (usually the same as the user name) is used.

If a GID change is required temporarily you can also use the *newgrp* command to change the user's default GID to another GID at runtime. For example, after executing `newgrp *groupname*` files created by the user will be associated with the `*groupname*` GID, without requiring a re-login. To change back to the default GID, execute *newgrp* without a groupname.

### Example adding a system user

System users can be used to run processes/daemons under a different user, protecting (e.g. with [chown](/index.php/Chown "Chown")) files and/or directories and more examples of computer hardening.

With the following command a system user without shell access and without a `home` directory is created (optionally append the `-U` parameter to create a group with the same name as the user, and add the user to this group):

```
# useradd -r -s /usr/bin/nologin *username*

```

### Other examples of user management

To change a user's login name:

```
# usermod -l *newname* *oldname*

```

To change a user's home directory:

```
# usermod -d /my/new/home -m *username*

```

The `-m` option also automatically creates the new directory and moves the content there.

**Tip:** You can create a link from the user's former home directory to the new one. Doing this will allow programs to find files that have hardcoded paths.
```
# ln -s /my/new/home/ /my/old/home

```

Make sure there is **no** trailing `/` on `/my/old/home`.

To add a user to other groups use (`*additional_groups*` is a comma-separated list):

```
# usermod -aG *additional_groups* *username*

```

**Warning:** If the `-a` option is omitted in the *usermod* command above, the user is removed from all groups not listed in `*additional_groups*` (i.e. the user will be member only of those groups listed in `*additional_groups*`).

Alternatively, *gpasswd* may be used. Though the username can only be added (or removed) from one group at a time.

```
# gpasswd --add *username* *group*

```

To enter user information for the [GECOS](#User_database) comment (e.g. the full user name), type:

```
# chfn *username*

```

(this way *chfn* runs in interactive mode).

Alternatively the GECOS comment can be set more liberally with:

```
# usermod -c "Comment" *username*

```

To mark a user's password as expired, requiring them to create a new password the first time they log in, type:

```
# chage -d 0 *username*

```

User accounts may be deleted with the *userdel* command.

```
# userdel -r *username*

```

The `-r` option specifies that the user's home directory and mail spool should also be deleted.

**Tip:** The [adduser](https://aur.archlinux.org/packages/adduser/) script allows carrying out the jobs of *useradd*, *chfn* and *passwd* interactively. See also [FS#32893](https://bugs.archlinux.org/task/32893).

### Username change tips

**Warning:** Make certain that you are not logged in as the user whose name you are about to change. Open a new tty (`Ctrl+Alt+F1`) and log in as root or as another user and su to root. usermod should prevent you from doing this by mistake.

Changing a username is safe and easy when done properly, just use the [usermod](#Other_examples_of_user_management) command. If the user is associated to a group with the same name, you can rename this with the [groupmod](#Group_management) command.

Alternatively, the `/etc/passwd` file can be edited directly, see [#User database](#User_database) for an introduction to its format.

Also keep in mind the following notes:

*   If you are using [sudo](/index.php/Sudo "Sudo") make sure you update your `/etc/sudoers` to reflect the new username(s) (via the visudo command as root).
*   If you modified your PATH statement in your `~/.bashrc`, make sure you change it to reflect the new username.
*   Likewise, be sure you change any config file such as `/etc/rc.local` or whatever if you are pointing it to a script or mountpoint, etc. within the old user's home directory.
*   Personal [crontabs](/index.php/Cron#Crontab_format "Cron") need to be adjusted by renaming the user's file in `/var/spool/cron` from the old to the new name, and then opening `crontab -e` to change any relevant paths and have it adjust the file permissions accordingly.
*   [Wine's](/index.php/Wine "Wine") personal folders/files' contents in `~/.wine/drive_c/users`, `~/.local/share/applications/wine/Programs` and possibly more need to be manually renamed/edited.
*   The procedure to [enable spell checking](/index.php/Firefox#Enable_spell_checking "Firefox") in Firefox may need to be redone, or else the check-as-you-type spelling might not work after renaming the user.
*   Certain Thunderbird addons, like [Enigmail](http://enigmail.mozdev.org/home/index.php), may need to be reinstalled.
*   Anything on your system (desktop shortcuts, shell scripts, etc.) that uses an absolute path to your home dir (i.e. `/home/oldname`) will need to be changed to reflect your new name. To avoid these problems in shell scripts, simply use the `~` or `$HOME` variables for home directories.
*   Also do not forget to edit accordingly the configuration files in `/etc` that relies on your absolute path (i.e. Samba, CUPS, so on). A nice way to learn what files you need to update involves using the grep command this way: `# grep -r {old_user} *`

## User database

Local user information is stored in the plain-text `/etc/passwd` file: each of its lines represents a user account, and has seven fields delimited by colons.

```
*account:password:UID:GID:GECOS:directory:shell*

```

Where:

*   `*account*` is the user name. This field can not be blank. Standard *NIX naming rules apply.
*   `*password*` is the user password.
    **Warning:** The `passwd` file is world-readable, so storing passwords (hashed or otherwise) in this file is insecure. Instead, Arch Linux uses [shadowed passwords](/index.php/Security#Password_hashes "Security"): the `password` field will contain a placeholder character (`x`) indicating that the hashed password is saved in the access-restricted file `/etc/shadow`. For this reason it is recommended to always change passwords using the **passwd** command.

*   `*UID*` is the numerical user ID. In Arch, the first login name (after root) is UID 1000 by default; subsequent UID entries for users should be greater than 1000.
*   `*GID*` is the numerical primary group ID for the user. Numeric values for GIDs are listed in [/etc/group](#Group_management).
*   `*GECOS*` is an optional field used for informational purposes; usually it contains the full user name, but it can also be used by services such as *finger* and managed with the [chfn](#Other_examples_of_user_management) command. This field is optional and may be left blank.
*   `*directory*` is used by the login command to set the `$HOME` environment variable. Several services with their own users use `/`, but normal users usually set a folder under `/home`.
*   `*shell*` is the path to the user's default [command shell](/index.php/Command_shell "Command shell"). This field is optional and defaults to `/bin/bash`.

Example:

```
jack:x:1001:100:Jack Smith,some comment here,,:/home/jack:/bin/bash

```

Broken down, this means: user `jack`, whose password is in `/etc/shadow`, whose UID is 1001 and whose primary group is 100\. Jack Smith is his full name and there is a comment associated to his account; his home directory is `/home/jack` and he is using [Bash](/index.php/Bash "Bash").

The *pwck* command can be used to verify the integrity of the user database. It can sort the user list by GID at the same time, which can be helpful for comparison:

```
# pwck -s

```

Note that the Arch Linux defaults of the files are created as .pacnew files by new releases of the [filesystem](https://www.archlinux.org/packages/?name=filesystem) package. Unless Pacman outputs related messages for action, these *.pacnew* files can, and should, be disregarded/removed. New required default users and groups are added automatically by the packages' install script.

## Group management

`/etc/group` is the file that defines the groups on the system (`man group` for details).

Display group membership with the `groups` command:

```
$ groups *user*

```

If `*user*` is omitted, the current user's group names are displayed.

The `id` command provides additional detail, such as the user's UID and associated GIDs:

```
$ id *user*

```

To list all groups on the system:

```
$ cat /etc/group

```

Create new groups with the `groupadd` command:

```
# groupadd *group*

```

Add users to a group with the `gpasswd` command:

```
# gpasswd -a *user* *group*

```

Modify an existing group with `groupmod`; e.g. to rename `old_group` group to `new_group` whilst preserving gid (all files previously owned by `old_group` will be owned by `new_group`):

```
# groupmod -n *new_group* *old_group*

```

**Note:** This will change a group name but not the numerical GID of the group.

To delete existing groups:

```
# groupdel *group*

```

To remove users from a group:

```
# gpasswd -d *user* *group*

```

If the user is currently logged in, he/she must log out and in again for the change to take effect.

The *grpck* command can be used to verify the integrity of the system's group files.

Updates to the [filesystem](https://www.archlinux.org/packages/?name=filesystem) package create .pacnew files. Alike the .pacnew files for the [#User database](#User_database), these can be disregarded/removed, because the install script adds any new required groups.

## Group list

### User groups

Workstation/desktop users often add their non-root user to some of following groups to allow access to peripherals and other hardware and facilitate system administration:

| Group | Affected files | Purpose |
| adm | Administration group, similar to `wheel`. |
| ftp | `/srv/ftp/` | Access to files served by [FTP](https://en.wikipedia.org/wiki/FTP "wikipedia:FTP") servers. |
| games | `/var/games` | Access to some game software. |
| http | `/srv/http/` | Access to files served by [HTTP](https://en.wikipedia.org/wiki/HTTP "wikipedia:HTTP") servers. |
| log | Access to log files in `/var/log/` created by [syslog-ng](/index.php/Syslog-ng "Syslog-ng"). |
| rfkill | `/dev/rfkill` | Right to control wireless devices power state (used by [rfkill](https://www.archlinux.org/packages/?name=rfkill)). |
| sys | Right to administer printers in [CUPS](/index.php/CUPS "CUPS"). |
| systemd-journal | `/var/log/journal/*` | Can be used to provide read-only access to the systemd logs, as an alternative to `adm` and `wheel` [[1]](https://cgit.freedesktop.org/systemd/systemd/tree/README?id=fdbbf0eeda929451e2aaf34937a72f03a225e315#n190). Otherwise, only user generated messages are displayed. |
| users | Standard users group. |
| uucp | `/dev/ttyS[0-9]+`, `/dev/tts/[0-9]+`, `/dev/ttyUSB[0-9]+`, `/dev/ttyACM[0-9]+` | RS-232 serial ports and devices connected to them. |
| wheel | Administration group, commonly used to give access to the [sudo](/index.php/Sudo "Sudo") and [su](/index.php/Su "Su") utilities (neither uses it by default, configurable in `/etc/pam.d/su` and `/etc/pam.d/su-l`). It can also be used to gain full read access to [journal](/index.php/Systemd#Journal "Systemd") files. |

### System groups

The following groups are used for system purposes and are not likely to be used by users:

| Group | Affected files | Purpose |
| dbus | used internally by [dbus](https://www.archlinux.org/packages/?name=dbus) |
| kmem | `/dev/port`, `/dev/mem`, `/dev/kmem` |
| mail | `/usr/bin/mail` |
| nobody | Unprivileged group. |
| polkitd | [polkit](/index.php/Polkit "Polkit") group. |
| proc | `/proc/*pid*/` | A group authorized to learn processes information otherwise prohibited by `hidepid=` mount option of the [proc filesystem](https://www.kernel.org/doc/Documentation/filesystems/proc.txt). The group must be explicitly set with the `gid=` mount option. |
| root | `/*` | Complete system administration and control (root, admin). |
| smmsp | [sendmail](/index.php/Sendmail "Sendmail") group. |
| tty | `/dev/tty`, `/dev/vcc`, `/dev/vc`, `/dev/ptmx` |

### Software groups

These groups are used by certain non-essential software. Sometimes they are used just internally, in these cases you should not add your user into these groups. See the main page for the software for details.

**Note:**

*   Do **not** create the groups manually, they will be created with [correct GID](/index.php/DeveloperWiki:UID_/_GID_Database "DeveloperWiki:UID / GID Database") when the relevant package is installed. [FS#42182](https://bugs.archlinux.org/task/42182)
*   A later removal of the package does not remove the respective user/group again. This is intentional because any files created during its usage would otherwise be left orphaned as a potential security risk.

| Group | Affected files | Purpose |
| adbusers | devices nodes under `/dev/` | Right to access [Android](/index.php/Android "Android") Debugging Bridge. |
| avahi |
| bumblebee | `/run/bumblebee.socket` | Right to launch applications with Bumblebee to utilize NVIDIA Optimus GPUs. |
| cdemu | `/dev/vhba_ctl` | Right to use [CDemu](/index.php/CDemu "CDemu") drive emulation. |
| clamav | `/var/lib/clamav/*`, `/var/log/clamav/*` | Used by [Clam AntiVirus](/index.php/Clam_AntiVirus "Clam AntiVirus"). |
| gdm | X server authorization directory (ServAuthDir) | [GDM](/index.php/GDM "GDM") group. |
| locate | `/usr/bin/locate`, `/var/lib/locate`, `/var/lib/mlocate`, `/var/lib/slocate` | Right to use [updatedb](https://en.wikipedia.org/wiki/updatedb "wikipedia:updatedb") command. |
| mpd | `/var/lib/mpd/*`, `/var/log/mpd/*`, `/var/run/mpd/*`, optionally music directories | [MPD](/index.php/MPD "MPD") group. |
| ntp | `/var/lib/ntp/*` | [NTPd](/index.php/NTPd "NTPd") group. |
| thinkpad | `/dev/misc/nvram` | Used by ThinkPad users for access to tools such as [tpb](/index.php/Tpb "Tpb"). |
| vboxsf | virtual machines' shared folders | Used by [VirtualBox](/index.php/VirtualBox "VirtualBox"). |
| vboxusers | `/dev/vboxdrv` | Right to use VirtualBox software. |
| vmware | Right to use [VMware](/index.php/VMware "VMware") software. |
| wireshark | Right to capture packets with [Wireshark](/index.php/Wireshark "Wireshark"). |

### Unused groups

Following groups are currently of no use for anyone:

| Group | Affected files | Purpose |
| bin | none | Historical |
| daemon |
| mem |
| network | Unused by default. Can be used e.g. for granting access to NetworkManager (see [NetworkManager#Set up PolicyKit permissions](/index.php/NetworkManager#Set_up_PolicyKit_permissions "NetworkManager")). |
| power |

#### Pre-systemd groups

Before arch migrated to [systemd](/index.php/Systemd "Systemd"), users had to be manually added to these groups in order to be able to access the corresponding devices. This way has been deprecated in favour of [udev](/index.php/Udev "Udev") marking the devices with a `uaccess` tag and *logind* assigning the permissions to users dynamically via [ACLs](/index.php/ACL "ACL") according to which session is currently active. Note that the session must not be broken for this to work (see [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") to check it).

There are some notable exceptions which require adding a user to some of these groups: for example if you want to allow users to access the device even when they are not logged in. However, note that adding users to the groups can even cause some functionality to break (for example, the `audio` group will break fast user switching and allows applications to block software mixing).

| Group | Affected files | Purpose |
| audio | `/dev/audio`, `/dev/snd/*`, `/dev/rtc0` | Direct access to sound hardware, for all sessions. It is still required to make [ALSA](/index.php/ALSA "ALSA") and [OSS](/index.php/OSS "OSS") work in remote sessions, see [ALSA#User privileges](/index.php/ALSA#User_privileges "ALSA"). |
| camera | Access to [Digital Cameras](/index.php/Digital_Cameras "Digital Cameras"). |
| disk | `/dev/sd[a-z][1-9]` | Access to block devices not affected by other groups such as `optical`, `floppy`, and `storage`. |
| floppy | `/dev/fd[0-9]` | Access to floppy drives. |
| input | `/dev/input/event[0-9]*`, `/dev/input/mouse[0-9]*` | Access to input devices. Introduced in systemd 215 [[2]](http://lists.freedesktop.org/archives/systemd-commits/2014-June/006343.html). |
| lp | `/dev/lp[0-9]*`, `/dev/parport[0-9]*`, `/etc/cups`, `/var/log/cups`, `/var/cache/cups`, `/var/spool/cups` | Access to parallel port devices (printers and others) and read-only access to [CUPS](/index.php/CUPS "CUPS") files. If you run a non-printer parallel port device, see [FS#50009](https://bugs.archlinux.org/task/50009) for implied problems. |
| kvm | `/dev/kvm` | Access to virtual machines using [KVM](/index.php/KVM "KVM"). |
| optical | `/dev/sr[0-9]`, `/dev/sg[0-9]` | Access to optical devices such as CD and DVD drives. |
| scanner | `/var/lock/sane` | Access to scanner hardware. |
| storage | Access to removable drives such as USB hard drives, flash/jump drives, MP3 players; enables the user to mount storage devices. |
| video | `/dev/fb/0`, `/dev/misc/agpgart` | Access to video capture devices, 2D/3D hardware acceleration, framebuffer ([X](/index.php/X "X") can be used *without* belonging to this group). |