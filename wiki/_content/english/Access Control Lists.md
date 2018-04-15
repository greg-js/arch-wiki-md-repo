[Access control list](https://en.wikipedia.org/wiki/Access_Control_List "wikipedia:Access Control List") (ACL) provides an additional, more flexible permission mechanism for [file systems](/index.php/File_systems "File systems"). It is designed to assist with UNIX file permissions. ACL allows you to give permissions for any user or group to any disc resource.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Enabling ACL](#Enabling_ACL)
    *   [2.2 Set ACL](#Set_ACL)
    *   [2.3 Show ACL](#Show_ACL)
*   [3 Examples](#Examples)
    *   [3.1 Output of ls command](#Output_of_ls_command)
*   [4 Granting execution permissions for private files to a Web Server](#Granting_execution_permissions_for_private_files_to_a_Web_Server)
*   [5 See also](#See_also)

## Installation

The [acl](https://www.archlinux.org/packages/?name=acl) package is a dependency of [systemd](/index.php/Systemd "Systemd"), it should already be installed.

## Configuration

### Enabling ACL

To enable ACL, the filesystem must be mounted with the `acl` option. You can use [fstab](/index.php/Fstab "Fstab") to make it permanent on your system.

There is a possibility that the `acl` option is already active as default mount option on the filesystem. [Btrfs](/index.php/Btrfs "Btrfs") does and Ext2/[3](/index.php/Ext3 "Ext3")/[4](/index.php/Ext4 "Ext4") filesystems do too. Use the following command to check ext* formatted partitions for the option:

 `# tune2fs -l /dev/sd*XY* | grep "Default mount options:"` 
```
Default mount options:    user_xattr acl

```

Also check that the default mount option is not overridden, in such case you will see `noacl` in `/proc/mounts` in the relevant line.

You can set the default mount options of a filesystem using the `tune2fs -o *option* *partition*` command, for example:

```
# tune2fs -o acl /dev/sd*XY*

```

Using the default mount options instead of an entry in `/etc/fstab` is very useful for external drives, such partition will be mounted with `acl` option also on other Linux machines. There is no need to edit `/etc/fstab` on every machine.

**Note:**

*   `acl` is specified as default mount option when creating an ext2/3/4 filesystem. This is configured in `/etc/mke2fs.conf`.
*   The default mount options are not listed in `/proc/mounts`.

### Set ACL

The ACL can be modified using the *setfacl* command.

To add permissions for a user (`*user*` is either the user name or ID):

```
# setfacl -m "u:*user:permissions*" <file/dir>

```

To add permissions for a group (`*group*` is either the group name or ID):

```
# setfacl -m "g:*group:permissions*" <file/dir>

```

To allow all files or directories to inherit ACL entries from the directory it is within:

```
# setfacl -dm "*entry*" <dir>

```

To remove a specific entry:

```
# setfacl -x "*entry*" <file/dir>

```

To remove all entries:

```
# setfacl -b <file/dir>

```

### Show ACL

To show permissions, use:

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

The following technique describes how a process like a web server (e.g. [nginx](/index.php/Nginx "Nginx"), [apache](/index.php/Apache "Apache")) can be granted access to files that reside in a user's home directory, without compromising security by giving the whole world access.

In the following we assume that the web server runs as the user `http` and grant it access to `geoffrey`'s home directory `/home/geoffrey`.

The first step is granting execution permission to `http` so it can access `geoffrey`'s home:

```
# setfacl -m "u:http:--x" /home/geoffrey

```

*Remember*: Execution permissions to a directory are necessary for a process to list the directory's content.

Since `http` is now able to access files in `/home/geoffrey`, `other` no longer needs access, so it can be safely removed:

```
# chmod o-rx /home/geoffrey

```

Use `getfacl` to verify the changes:

 `$ getfacl /home/geoffrey` 
```
getfacl: Removing leading '/' from absolute path names
# file: home/geoffrey
# owner: geoffrey
# group: geoffrey
user::rwx
user:http:--x
group::r-x
mask::r-x
other::---

```

As the above output shows, `other`'s no longer have any permissions, but `http` still is able to access the files, thus security might be considered increased.

## See also

*   [getfacl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/getfacl.1)
*   [setfacl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfacl.1)
*   An old but still relevant (and thorough) [guide](http://vanemery.net/Linux/ACL/linux-acl.html) to ACL
*   [How to set default file permissions for all folders/files in a directory?](http://unix.stackexchange.com/questions/1314/how-to-set-default-file-permissions-for-all-folders-files-in-a-directory)