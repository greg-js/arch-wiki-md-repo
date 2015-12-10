# Access Control Lists

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**A**ccess **C**ontrol **L**ist (ACL) provides an additional, more flexible permission mechanism for file systems. It is designed to assist with `UNIX` file permissions. ACL allows you to give permissions for any user or group to any disc resource.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Enabling ACL](#Enabling_ACL)
    *   [2.2 Set ACL](#Set_ACL)
*   [3 Examples](#Examples)
    *   [3.1 Output of ls command](#Output_of_ls_command)
*   [4 Granting execution permissions for private files to a Web Server](#Granting_execution_permissions_for_private_files_to_a_Web_Server)
*   [5 See also](#See_also)

## Installation

The required package [acl](https://www.archlinux.org/packages/?name=acl) is a dependency of [systemd](/index.php/Systemd "Systemd"), it should already be installed.

## Configuration

### Enabling ACL

To enable ACL, the filesystem must be mounted with the `acl` option. You can use [fstab](/index.php/Fstab "Fstab") to make it permanent on your system.

There is a possibility that the `acl` option is already active as default mount option on the filesystem. [Btrfs](/index.php/Btrfs "Btrfs") does and possibly ext filesystems do too. Use the following command to check ext* formatted partitions for the option:

 `# tune2fs -l /dev/sd_XY_ | grep "Default mount options:"` 

```
Default mount options:    user_xattr acl

```

Also check that the default mount option is not overridden, in such case you will see `noacl` in `/proc/mounts` in the relevant line.

You can set the default mount options of a filesystem using the `tune2fs -o _option_ _partition_` command, for example:

```
# tune2fs -o acl /dev/sd_XY_

```

Using the default mount options instead of an entry in `/etc/fstab` is very useful for external drives, such partition will be mounted with `acl` option also on other Linux machines. There is no need to edit `/etc/fstab` on every machine.

**Note:**

*   `acl` is specified as default mount option when creating an ext2/3/4 filesystem. This is configured in `/etc/mke2fs.conf`.
*   The default mount options are not listed in `/proc/mounts`.

### Set ACL

To modify ACL use `setfacl` command. To add permissions use `setfacl -m`.

Add permissions to some user:

```
# setfacl -m "u:username:permissions"

```

or

```
# setfacl -m "u:uid:permissions"

```

Add permissions to some group:

```
# setfacl -m "g:groupname:permissions"

```

or

```
# setfacl -m "g:gid:permissions"

```

Remove all permissions:

```
# setfacl -b

```

Remove each entry:

```
# setfacl -x "entry"

```

To check permissions use:

```
# getfacl filename

```

## Examples

Set all permissions for user johny to file named "abc":

```
# setfacl -m "u:johny:rwx" abc

```

Check permissions

 `# getfacl abc` 

```
# file: abc
# owner: someone
# group: someone
user::rw-
user:johny:rwx
group::r--
mask::rwx
other::r--

```

Change permissions for user johny:

```
# setfacl -m "u:johny:r-x" abc

```

Check permissions

 `# getfacl abc` 

```
# file: abc
# owner: someone
# group: someone
user::rw-
user:johny:r-x
group::r--
mask::r-x
other::r--

```

Remove all extended ACL entries:

```
# setfacl -b abc

```

Check permissions

 `# getfacl abc` 

```
# file: abc
# owner: someone
# group: someone
user::rw-
group::r--
other::r--

```

### Output of ls command

You will notice that there is an ACL for a given file because it will exhibit a `**+**` (plus sign) after its Unix permissions in the output of `ls -l`.

 `$ ls -l /dev/audio` 

```
crw-rw----+ 1 root audio 14, 4 nov.   9 12:49 /dev/audio

```

 `$ getfacl /dev/audio` 

```
getfacl: Removing leading '/' from absolute path names
# file: dev/audio
# owner: root
# group: audio
user::rw-
user:solstice:rw-
group::rw-
mask::rw-
other::---

```

## Granting execution permissions for private files to a Web Server

The following technique describes how a process like a web server can be granted access to files that reside in a user's home directory, without compromising security by giving the whole world access.

In the following we assume that the web server runs as the user `webserver` and grant it access to `geoffrey`'s home directory `/home/geoffrey`.

The first step is granting execution permission to `webserver` so it can access `geoffrey`'s home:

```
# setfacl -m "u:webserver:--x" /home/geoffrey

```

_Remeber_: Execution permissions to a directory are necessary for a process to list the directories content.

Since `webserver` is now able to access files in `/home/geoffrey`, `other`s do no longer need access:

```
# chmod o-rx /home/geoffrey

```

`getfacl` can be used to verify the changes:

```
$ getfacl /home/geoffrey
getfacl: Removing leading '/' from absolute path names
# file: home/geoffrey
# owner: geoffrey
# group: geoffrey
user::rwx
user:webserver:--x
group::r-x
mask::r-x
other::---

```

As the above output shows, `other`s no longer have any permissions, but `webserver` still is able to access the files, thus security might be considered increased.

## See also

*   Man Page - `man getfacl`
*   Man Page - `man setfacl`
*   An old but still relevant (and thorough) [guide](http://www.vanemery.com/Linux/ACL/linux-acl.html) to ACL

Retrieved from "[https://wiki.archlinux.org/index.php?title=Access_Control_Lists&oldid=369541](https://wiki.archlinux.org/index.php?title=Access_Control_Lists&oldid=369541)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Security](/index.php/Category:Security "Category:Security")