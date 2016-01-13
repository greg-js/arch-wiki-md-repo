# Users and groups

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [DeveloperWiki:UID / GID Database](/index.php/DeveloperWiki:UID_/_GID_Database "DeveloperWiki:UID / GID Database")
*   [polkit](/index.php/Polkit "Polkit")
*   [File permissions and attributes](/index.php/File_permissions_and_attributes "File permissions and attributes")

Users and groups are used on GNU/Linux for [access control](https://en.wikipedia.org/wiki/access_control#Computer_security "wikipedia:access control") — that is, to control access to the system's files, directories, and peripherals. Linux offers relatively simple/coarse access control mechanisms by default. For more advanced options, see [ACL](/index.php/ACL "ACL") and [LDAP authentication](/index.php/LDAP_authentication "LDAP authentication").

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
    *   [7.4 Deprecated or unused groups](#Deprecated_or_unused_groups)
        *   [7.4.1 Pre-systemd groups](#Pre-systemd_groups)

## Overview

A _user_ is anyone who uses a computer. In this case, we are describing the names which represent those users. It may be Mary or Bill, and they may use the names Dragonlady or Pirate in place of their real name. All that matters is that the computer has a name for each account it creates, and it is this name by which a person gains access to use the computer. Some system services also run using restricted or privileged user accounts.

Managing users is done for the purpose of security by limiting access in certain specific ways. The superuser (root) has complete access to the operating system and its configuration; it is intended for administrative use only. Unprivileged users can use the [su](/index.php/Su "Su") and [sudo](/index.php/Sudo "Sudo") programs for controlled privilege escalation.

Any individual may have more than one account, as long as they use a different name for each account they create. Further, there are some reserved names which may not be used such as "root".

Users may be grouped together into a "group", and users may be added to an existing group to utilize the privileged access it grants.

**Note:** The beginner should use these tools carefully and stay away from having anything to do with any other _existing_ user account, other than their own.

## Permissions and ownership

From [In UNIX Everything is a File](http://ph7spot.com/musings/in-unix-everything-is-a-file):

_The UNIX operating system crystallizes a couple of unifying ideas and concepts that shaped its design, user interface, culture and evolution. One of the most important of these is probably the mantra: "everything is a file," widely regarded as one of the defining points of UNIX._

_This key design principle consists of providing a unified paradigm for accessing a wide range of input/output resources: documents, directories, hard-drives, CD-ROMs, modems, keyboards, printers, monitors, terminals and even some inter-process and network communications. The trick is to provide a common abstraction for all of these resources, each of which the UNIX fathers called a "file." Since every "file" is exposed through the same API, you can use the same set of basic commands to read/write to a disk, keyboard, document or network device._

From [Extending UNIX File Abstraction for General-Purpose Networking](http://www.intel-research.net/Publications/Pittsburgh/101220041324_277.pdf):

_A fundamental and very powerful, consistent abstraction provided in UNIX and compatible operating systems is the file abstraction. Many OS services and device interfaces are implemented to provide a file or file system metaphor to applications. This enables new uses for, and greatly increases the power of, existing applications — simple tools designed with specific uses in mind can, with UNIX file abstractions, be used in novel ways. A simple tool, such as cat, designed to read one or more files and output the contents to standard output, can be used to read from I/O devices through special device files, typically found under the `/dev` directory. On many systems, audio recording and playback can be done simply with the commands, "`cat /dev/audio > myfile`" and "`cat myfile > /dev/audio`," respectively._

Every file on a GNU/Linux system is owned by a user and a group. In addition, there are three types of access permissions: read, write, and execute. Different access permissions can be applied to a file's owning user, owning group, and others (those without ownership). One can determine a file's owners and permissions by viewing the long listing format of the [ls](/index.php/Core_utilities#ls "Core utilities") command:

 `$ ls -l /boot/` 

```
total 13740
drwxr-xr-x 2 root root    4096 Jan 12 00:33 grub
-rw-r--r-- 1 root root 8570335 Jan 12 00:33 initramfs-linux-fallback.img
-rw-r--r-- 1 root root 1821573 Jan 12 00:31 initramfs-linux.img
-rw-r--r-- 1 root root 1457315 Jan  8 08:19 System.map26
-rw-r--r-- 1 root root 2209920 Jan  8 08:19 vmlinuz-linux
```

The first column displays the file's permissions (for example, the file `initramfs-linux.img` has permissions `-rw-r--r--`). The third and fourth columns display the file's owning user and group, respectively. In this example, all files are owned by the _root_ user and the _root_ group.

 `$ ls -l /media/` 

```
total 16
drwxrwx--- 1 root vboxsf 16384 Jan 29 11:02 sf_Shared
```

In this example, the `sf_Shared` directory is owned by the _root_ user and the _vboxsf_ group. It is also possible to determine a file's owners and permissions using the stat command:

Owning user:

 `$ stat -c %U /media/sf_Shared/`  `root` 

Owning group:

 `$ stat -c %G /media/sf_Shared/`  `vboxsf` 

Access rights:

 `$ stat -c %A /media/sf_Shared/`  `drwxrwx---` 

Access permissions are displayed in three groups of characters, representing the permissions of the owning user, owning group, and others, respectively. For example, the characters `-rw-r--r--` indicate that the file's owner has read and write permission, but not execute (`rw-`), whilst users belonging to the owning group and other users have only read permission (`r--` and `r--`). Meanwhile, the characters `drwxrwx---` indicate that the file's owner and users belonging to the owning group all have read, write, and execute permissions (`rwx` and `rwx`), whilst other users are denied access (`---`). The first character represents the file's type.

List files owned by a user or group with the _find_ utility:

```
# find / -group _group_

```

```
# find / -user _user_

```

A file's owning user and group can be changed with the _chown_ (change owner) command. A file's access permissions can be changed with the _chmod_ (change mode) command.

See [man chown](http://linux.die.net/man/1/chown), [man chmod](http://linux.die.net/man/1/chmod), and [Linux file permissions](http://www.linux.com/learn/tutorials/309527-understanding-linux-file-permissions) for additional detail.

## File list

**Warning:** Do not edit these files by hand. There are utilities that properly handle locking and avoid invalidating the format of the database. See [#User management](#User_management) and [#Group management](#Group_management) for an overview.

<table class="wikitable">

<tbody>

<tr>

<th>File</th>

<th>Purpose</th>

</tr>

<tr>

<td>`/etc/shadow`</td>

<td>Secure user account information</td>

</tr>

<tr>

<td>`/etc/passwd`</td>

<td>User account information</td>

</tr>

<tr>

<td>`/etc/gshadow`</td>

<td>Contains the shadowed information for group accounts</td>

</tr>

<tr>

<td>`/etc/group`</td>

<td>Defines the groups to which users belong</td>

</tr>

<tr>

<td>`/etc/sudoers`</td>

<td>List of who can run what by sudo</td>

</tr>

<tr>

<td>`/home/*`</td>

<td>Home directories</td>

</tr>

</tbody>

</table>

## User management

To list users currently logged on the system, the _who_ command can be used. To list all existing user accounts including their properties stored in the [user database](#User_database), run `passwd -Sa` as root. See `passwd(1)` for the description of the output format.

To add a new user, use the _useradd_ command:

```
# useradd -m -g _initial_group_ -G _additional_groups_ -s _login_shell_ _username_

```

*   `-m` creates the user home directory as `/home/_username_`. Within their home directory, a non-root user can write files, delete them, install programs, and so on.
*   `-g` defines the group name or number of the user's initial login group. If specified, the group name must exist; if a group number is provided, it must refer to an already existing group. If not specified, the behaviour of _useradd_ will depend on the `USERGROUPS_ENAB` variable contained in `/etc/login.defs`. The default behaviour (`USERGROUPS_ENAB yes`) is to create a group with the same name as the username, with `GID` equal to `UID`.
*   `-G` introduces a list of supplementary groups which the user is also a member of. Each group is separated from the next by a comma, with no intervening spaces. The default is for the user to belong only to the initial group.
*   `-s` defines the path and file name of the user's default login shell. After the boot process is complete, the default login shell is the one specified here. Ensure the chosen shell package is installed if choosing something other than [Bash](/index.php/Bash "Bash").

**Warning:** In order to be able to log in, the login shell must be one of those listed in `/etc/shells`, otherwise the `pam_shell` module will deny the login request. In particular, do not use the `/usr/bin/bash` path instead of `/bin/bash`, unless it is properly configured in `/etc/shells`.

**Note:** The password for the newly created user must then be defined, using _passwd_ as shown in [#Example adding a user](#Example_adding_a_user).

When the login shell is intended to be non-functional, for example when the user account is created for a specific service, `/usr/bin/nologin` may be specified in place of a regular shell to politely refuse a login (see `nologin(8)`).

### Example adding a user

On a typical desktop system, use the following command to add a new user named `archie`, specify Bash as their login shell and add them to the `wheel` group (see the entry in [#User groups](#User_groups) for details):

```
# useradd -m -G wheel -s /bin/bash archie

```

Although it is not required to protect the newly user `archie` with a password, it is highly recommend to do so:

```
# passwd archie

```

**Tip:** Bash is the default value for the shell (as indicated by `useradd -D`), so you can omit the `-s` option except if you want to use something else.

This command will also automatically create a group called `archie` with the same GID as the UID of the user `archie` and makes this the default group for `archie` on login. Making each user have their own group (with group name same as user name and GID same as UID) is the preferred way to add users.

You could also make the default group something else, e.g. `users`:

```
# useradd -m -g users -G wheel archie

```

However, using a single default group (`users` in the example above) is not recommended for multi-user systems. The reason is that typically, the method for facilitating shared write access for specific groups of users is setting user [umask](/index.php/Umask "Umask") value to `002`, which means that the default group will by default always have write access to any file you create. See also [User Private Groups](https://security.ias.edu/how-and-why-user-private-groups-unix).

In the recommended scenario, where the default group has the same name as the user name, all files are by default writeable only for the user who created them. To allow write access to a specific group, shared files/folders can be made writeable by default for everyone in this group and the owning group can be automatically fixed to the group which owns the parent directory by setting the setgid bit on this directory:

```
# chmod g+s _our_shared_directory_

```

Otherwise the file creator's default group (usually the same as the user name) is used.

### Example adding a system user

System users can be used to run processes/daemons under a different user, protecting (e.g. with [chown](/index.php/Chown "Chown")) files and/or directories and more examples of computer hardening.

With the following command a system user without shell access and without a `home` directory is created (optionally append the `-U` parameter to create a group with the same name as the user, and add the user to this group):

```
# useradd -r -s /usr/bin/nologin _username_

```

### Other examples of user management

To change a user's login name:

```
# usermod -l _newname_ _oldname_

```

To change a user's home directory:

```
# usermod -dm /my/new/home _username_

```

The `-m` option also automatically creates the new directory and moves the content there.

**Tip:** You can create a link from the user's former home directory to the new one. Doing this will allow programs to find files that have hardcoded paths.

```
# ln -s /my/new/home/ /my/old/home

```

Make sure there is **no** trailing `/` on `/my/old/home`.

To add a user to other groups use (`_additional_groups_` is a comma-separated list):

```
# usermod -aG _additional_groups_ _username_

```

Alternatively, _gpasswd_ may be used. Though the username can only be added (or removed) from one group at a time.

```
# gpasswd --add _username_ _group_

```

**Warning:** If the `-a` option is omitted in the _usermod_ command above, the user is removed from all groups not listed in `_additional_groups_` (i.e. the user will be member only of those groups listed in `_additional_groups_`).

To enter user information for the [GECOS](#User_database) comment (e.g. the full user name), type:

```
# chfn _username_

```

(this way _chfn_ runs in interactive mode).

Alternatively the GECOS comment can be set more liberally with:

```
# usermod -c "Comment" _username_

```

To mark a user's password as expired, requiring them to create a new password the first time they log in, type:

```
# chage -d 0 _username_

```

User accounts may be deleted with the _userdel_ command.

```
# userdel -r _username_

```

The `-r` option specifies that the user's home directory and mail spool should also be deleted.

**Tip:** The [AUR](/index.php/AUR "AUR") packages [adduser](https://aur.archlinux.org/packages/adduser/)<sup><small>AUR</small></sup>, [adduser-defaults](https://aur.archlinux.org/packages/adduser-defaults/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/adduser-defaults)]</sup> or [adduser-deb](https://aur.archlinux.org/packages/adduser-deb/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/adduser-deb)]</sup> provide an _adduser_ script that allows carrying out the jobs of _useradd_, _chfn_ and _passwd_ interactively. See also [FS#32893](https://bugs.archlinux.org/task/32893).

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
_account:password:UID:GID:GECOS:directory:shell_

```

Where:

*   `_account_` is the user name. This field can not be blank. Standard *NIX naming rules apply.
*   `_password_` is the user password.

    **Warning:** The `passwd` file is world-readable, so storing passwords (hashed or otherwise) in this file is insecure. Instead, Arch Linux uses [shadowed passwords](/index.php/Security#Password_hashes "Security"): the `password` field will contain a placeholder character (`x`) indicating that the hashed password is saved in the access-restricted file `/etc/shadow`. For this reason it is recommended to always change passwords using the **passwd** command.

*   `_UID_` is the numerical user ID. In Arch, the first login name (after root) is UID 1000 by default; subsequent UID entries for users should be greater than 1000.
*   `_GID_` is the numerical primary group ID for the user. Numeric values for GIDs are listed in [/etc/group](#Group_management).
*   `_GECOS_` is an optional field used for informational purposes; usually it contains the full user name, but it can also be used by services such as _finger_ and managed with the [chfn](#Other_examples_of_user_management) command. This field is optional and may be left blank.
*   `_directory_` is used by the login command to set the `$HOME` environment variable. Several services with their own users use `/`, but normal users usually set a folder under `/home`.
*   `_shell_` is the path to the user's default [command shell](/index.php/Command_shell "Command shell"). This field is optional and defaults to `/bin/bash`.

Example:

```
jack:x:1001:100:Jack Smith,some comment here,,:/home/jack:/bin/bash

```

Broken down, this means: user `jack`, whose password is in `/etc/shadow`, whose UID is 1001 and whose primary group is 100\. Jack Smith is his full name and there is a comment associated to his account; his home directory is `/home/jack` and he is using [Bash](/index.php/Bash "Bash").

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** The tools _pwck_ and _pwconv_ should be mentioned. Brief usage example for them best also mentions handling .pacnew files generated by [filesystem](https://www.archlinux.org/packages/?name=filesystem) updates. (Discuss in [ArchWiki:Requests#User_and_group_pacnew_files](https://wiki.archlinux.org/index.php/ArchWiki:Requests#User_and_group_pacnew_files))

## Group management

`/etc/group` is the file that defines the groups on the system (`man group` for details).

Display group membership with the `groups` command:

```
$ groups _user_

```

If `_user_` is omitted, the current user's group names are displayed.

The `id` command provides additional detail, such as the user's UID and associated GIDs:

```
$ id _user_

```

To list all groups on the system:

```
$ cat /etc/group

```

Create new groups with the `groupadd` command:

```
# groupadd _group_

```

Add users to a group with the `gpasswd` command:

```
# gpasswd -a _user_ _group_

```

Modify an existing group with `groupmod`; e.g. to rename `old_group` group to `new_group` whilst preserving gid (all files previously owned by `old_group` will be owned by `new_group`):

```
# groupmod -n _new_group_ _old_group_

```

**Note:** This will change a group name but not the numerical GID of the group.

To delete existing groups:

```
# groupdel _group_

```

To remove users from a group:

```
# gpasswd -d _user_ _group_

```

If the user is currently logged in, he/she must log out and in again for the change to take effect.

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** The tools _grpck_ and _grpconv_ should be mentioned. Brief usage example for them best also mentions handling .pacnew files generated by [filesystem](https://www.archlinux.org/packages/?name=filesystem) updates. (Discuss in [ArchWiki:Requests#User_and_group_pacnew_files](https://wiki.archlinux.org/index.php/ArchWiki:Requests#User_and_group_pacnew_files))

## Group list

### User groups

Workstation/desktop users often add their non-root user to some of following groups to allow access to peripherals and other hardware and facilitate system administration:

<table class="wikitable">

<tbody>

<tr>

<th>Group</th>

<th>Affected files</th>

<th>Purpose</th>

</tr>

<tr>

<td>games</td>

<td>`/var/games`</td>

<td>Access to some game software.</td>

</tr>

<tr>

<td>rfkill</td>

<td>`/dev/rfkill`</td>

<td>Right to control wireless devices power state (used by [rfkill](https://www.archlinux.org/packages/?name=rfkill)).</td>

</tr>

<tr>

<td>users</td>

<td>Standard users group.</td>

</tr>

<tr>

<td>uucp</td>

<td>`/dev/ttyS[0-9]`, `/dev/tts/[0-9]`, `/dev/ttyACM[0-9]`</td>

<td>Serial and USB devices such as modems, handhelds, RS-232/serial ports.</td>

</tr>

<tr>

<td>wheel</td>

<td>Administration group, commonly used to give access to the [sudo](/index.php/Sudo "Sudo") and [su](/index.php/Su "Su") utilities (neither uses it by default, configurable in `/etc/pam.d/su` and `/etc/pam.d/su-l`). It can also be used to gain full read access to [journal](/index.php/Systemd#Journal "Systemd") files.</td>

</tr>

</tbody>

</table>

### System groups

The following groups are used for system purposes and are not likely to be used by novice Arch users:

<table class="wikitable">

<tbody>

<tr>

<th>Group</th>

<th>Affected files</th>

<th>Purpose</th>

</tr>

<tr>

<td>bin</td>

<td>none</td>

<td>Historical</td>

</tr>

<tr>

<td>daemon</td>

</tr>

<tr>

<td>dbus</td>

<td>used internally by [dbus](https://www.archlinux.org/packages/?name=dbus)</td>

</tr>

<tr>

<td>ftp</td>

<td>`/srv/ftp`</td>

<td>used by [FTP](https://en.wikipedia.org/wiki/FTP "wikipedia:FTP") servers like [Proftpd](/index.php/Proftpd "Proftpd")</td>

</tr>

<tr>

<td>fuse</td>

<td>Used by fuse to allow user mounts.</td>

</tr>

<tr>

<td>http</td>

</tr>

<tr>

<td>kmem</td>

<td>`/dev/port`, `/dev/mem`, `/dev/kmem`</td>

</tr>

<tr>

<td>mail</td>

<td>`/usr/bin/mail`</td>

</tr>

<tr>

<td>mem</td>

</tr>

<tr>

<td>nobody</td>

<td>Unprivileged group.</td>

</tr>

<tr>

<td>polkitd</td>

<td>[polkit](/index.php/Polkit "Polkit") group.</td>

</tr>

<tr>

<td>proc</td>

<td>`/proc/_pid_/`</td>

<td>A group authorized to learn processes information otherwise prohibited by `hidepid=` mount option of the [proc filesystem](https://www.kernel.org/doc/Documentation/filesystems/proc.txt). The group must be explicitly set with the `gid=` mount option.</td>

</tr>

<tr>

<td>root</td>

<td>`/*`</td>

<td>Complete system administration and control (root, admin).</td>

</tr>

<tr>

<td>smmsp</td>

<td>[sendmail](https://en.wikipedia.org/wiki/sendmail "wikipedia:sendmail") group.</td>

</tr>

<tr>

<td>systemd-journal</td>

<td>`/var/log/journal/*`</td>

<td>Provides access to the complete systemd logs. Otherwise, only user generated messages are displayed.</td>

</tr>

<tr>

<td>tty</td>

<td>`/dev/tty`, `/dev/vcc`, `/dev/vc`, `/dev/ptmx`</td>

<td>Eg. to acces `/dev/ACMx`</td>

</tr>

</tbody>

</table>

### Software groups

These groups are used by certain non-essential software. Sometimes they are used just internally, in these cases you should not add your user into these groups. See the main page for the software for details.

**Note:** Do **not** create the groups manually, they will be created with [correct GID](/index.php/DeveloperWiki:UID_/_GID_Database "DeveloperWiki:UID / GID Database") when the relevant package is installed. [FS#42182](https://bugs.archlinux.org/task/42182)

<table class="wikitable">

<tbody>

<tr>

<th>Group</th>

<th>Affected files</th>

<th>Purpose</th>

</tr>

<tr>

<td>adbusers</td>

<td>devices nodes under `/dev/`</td>

<td>Right to access [Android](/index.php/Android "Android") Debugging Bridge.</td>

</tr>

<tr>

<td>avahi</td>

</tr>

<tr>

<td>bumblebee</td>

<td>`/run/bumblebee.socket`</td>

<td>Right to launch applications with Bumblebee to utilize NVIDIA Optimus GPUs.</td>

</tr>

<tr>

<td>cdemu</td>

<td>`/dev/vhba_ctl`</td>

<td>Right to use [CDemu](/index.php/CDemu "CDemu") drive emulation.</td>

</tr>

<tr>

<td>clamav</td>

<td>`/var/lib/clamav/*`, `/var/log/clamav/*`</td>

<td>Used by [Clam AntiVirus](/index.php/Clam_AntiVirus "Clam AntiVirus").</td>

</tr>

<tr>

<td>gdm</td>

<td>X server authorization directory (ServAuthDir)</td>

<td>[GDM](/index.php/GDM "GDM") group.</td>

</tr>

<tr>

<td>locate</td>

<td>`/usr/bin/locate`, `/var/lib/locate`, `/var/lib/mlocate`, `/var/lib/slocate`</td>

<td>Right to use [updatedb](https://en.wikipedia.org/wiki/updatedb "wikipedia:updatedb") command.</td>

</tr>

<tr>

<td>mpd</td>

<td>`/var/lib/mpd/*`, `/var/log/mpd/*`, `/var/run/mpd/*`, optionally music directories</td>

<td>[MPD](/index.php/MPD "MPD") group.</td>

</tr>

<tr>

<td>networkmanager</td>

<td>Requirement for your user to connect wirelessly with [NetworkManager](/index.php/NetworkManager "NetworkManager"). This group is not included with Arch by default so it must be added manually.</td>

</tr>

<tr>

<td>ntp</td>

<td>`/var/lib/ntp/*`</td>

<td>[NTPd](/index.php/NTPd "NTPd") group.</td>

</tr>

<tr>

<td>thinkpad</td>

<td>`/dev/misc/nvram`</td>

<td>Used by ThinkPad users for access to tools such as [tpb](/index.php/Tpb "Tpb").</td>

</tr>

<tr>

<td>vboxsf</td>

<td>virtual machines' shared folders</td>

<td>Used by [VirtualBox](/index.php/VirtualBox "VirtualBox").</td>

</tr>

<tr>

<td>vboxusers</td>

<td>`/dev/vboxdrv`</td>

<td>Right to use VirtualBox software.</td>

</tr>

<tr>

<td>vmware</td>

<td>Right to use [VMware](/index.php/VMware "VMware") software.</td>

</tr>

<tr>

<td>wireshark</td>

<td>Right to capture packets with [Wireshark](/index.php/Wireshark "Wireshark").</td>

</tr>

</tbody>

</table>

### Deprecated or unused groups

Following groups are currently of no use for anyone:

<table class="wikitable">

<tbody>

<tr>

<th>Group</th>

<th>Purpose</th>

</tr>

<tr>

<td>log</td>

<td>Access to log files in `/var/log/` created by [syslog-ng](/index.php/Syslog-ng "Syslog-ng").</td>

</tr>

<tr>

<td>ssh</td>

<td><s>[Sshd](/index.php/Sshd "Sshd") can be configured to only allow members of this group to login.</s> This is true for any arbitrary group; the `ssh` group is not created by default, hence non-standard.</td>

</tr>

<tr>

<td>stb-admin</td>

<td>**Unused!** Right to access [system-tools-backends](http://system-tools-backends.freedesktop.org/)</td>

</tr>

<tr>

<td>kvm</td>

<td>Adding a user to the `kvm` group used to be required to allow non-root users to access virtual machines using [KVM](/index.php/KVM "KVM"). This has been deprecated in favor of using [udev](/index.php/Udev "Udev") rules, and this is done automatically.</td>

</tr>

</tbody>

</table>

#### Pre-systemd groups

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Input group introduced with systemd 215 [[1]](http://lists.freedesktop.org/archives/systemd-commits/2014-June/006343.html) (Discuss in [Talk:Users and groups#](https://wiki.archlinux.org/index.php/Talk:Users_and_groups))

These groups used to be needed before arch migrated to [systemd](/index.php/Systemd "Systemd"). That is no longer the case, as long as the _logind_ session is not broken (see [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") to check it). The groups can even cause some functionality to break. See [SysVinit#Migration to systemd](/index.php/SysVinit#Migration_to_systemd "SysVinit") for details.

<table class="wikitable">

<tbody>

<tr>

<th>Group</th>

<th>Affected files</th>

<th>Purpose</th>

</tr>

<tr>

<td>audio</td>

<td>`/dev/audio`, `/dev/snd/*`, `/dev/rtc0`</td>

<td>Direct access to sound hardware, for all sessions (requirement is imposed by both [ALSA](/index.php/ALSA "ALSA") and [OSS](/index.php/OSS "OSS")). Local sessions already have the ability to play sound and access mixer controls.</td>

</tr>

<tr>

<td>camera</td>

<td>Access to [Digital Cameras](/index.php/Digital_Cameras "Digital Cameras").</td>

</tr>

<tr>

<td>disk</td>

<td>`/dev/sda[1-9]`, `/dev/sdb[1-9]`</td>

<td>Access to block devices not affected by other groups such as `optical`, `floppy`, and `storage`.</td>

</tr>

<tr>

<td>floppy</td>

<td>`/dev/fd[0-9]`</td>

<td>Access to floppy drives.</td>

</tr>

<tr>

<td>lp</td>

<td>`/etc/cups`, `/var/log/cups`, `/var/cache/cups`, `/var/spool/cups`, `/dev/parport[0-9]`</td>

<td>Access to printer hardware; enables the user to manage print jobs.</td>

</tr>

<tr>

<td>network</td>

<td>Right to change network settings such as when using [NetworkManager](/index.php/NetworkManager "NetworkManager").</td>

</tr>

<tr>

<td>optical</td>

<td>`/dev/sr[0-9]`, `/dev/sg[0-9]`</td>

<td>Access to optical devices such as CD and DVD drives.</td>

</tr>

<tr>

<td>power</td>

<td>Right to use [Pm-utils](/index.php/Pm-utils "Pm-utils") (suspend, hibernate...) and power management controls.</td>

</tr>

<tr>

<td>scanner</td>

<td>`/var/lock/sane`</td>

<td>Access to scanner hardware.</td>

</tr>

<tr>

<td>storage</td>

<td>Access to removable drives such as USB hard drives, flash/jump drives, MP3 players; enables the user to mount storage devices.</td>

</tr>

<tr>

<td>sys</td>

<td>Right to administer printers in [CUPS](/index.php/CUPS "CUPS").</td>

</tr>

<tr>

<td>video</td>

<td>`/dev/fb/0`, `/dev/misc/agpgart`</td>

<td>Access to video capture devices, 2D/3D hardware acceleration, framebuffer ([X](/index.php/X "X") can be used _without_ belonging to this group). Local sessions already have the ability to use hardware acceleration and video capture.</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=Users_and_groups&oldid=415021](https://wiki.archlinux.org/index.php?title=Users_and_groups&oldid=415021)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Security](/index.php/Category:Security "Category:Security")