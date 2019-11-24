[Access control list](https://en.wikipedia.org/wiki/Access_Control_List "wikipedia:Access Control List") (ACL) provides an additional, more flexible permission mechanism for [file systems](/index.php/File_systems "File systems"). It is designed to assist with UNIX file permissions. ACL allows you to give permissions for any user or group to any disk resource.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Enabling ACL](#Enabling_ACL)
    *   [2.2 Set ACL](#Set_ACL)
    *   [2.3 Show ACL](#Show_ACL)
*   [3 Examples](#Examples)
    *   [3.1 Output of ls command](#Output_of_ls_command)
*   [4 Granting execution permissions for private files to a web server](#Granting_execution_permissions_for_private_files_to_a_web_server)
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

**Tip:** You can list file/directory permission changes without modifying the permissions (i.e. dry-run) by appending the `--test` flag.

To set permissions for a user (`*user*` is either the user name or ID):

```
# setfacl -m "u:*user:permissions*" <file/dir>

```

To set permissions for a group (`*group*` is either the group name or ID):

```
# setfacl -m "g:*group:permissions*" <file/dir>

```

To set permissions for others:

```
# setfacl -m "other:*permissions*" <file/dir>

```

To allow all *newly created* files or directories to inherit entries from the parent directory (this will not affect files which will be *copied* into the directory):

```
# setfacl -dm "*entry*" <dir>

```

To remove a specific entry:

```
# setfacl -x "*entry*" <file/dir>

```

To remove the default entries:

```
# setfacl -k <file/dir>

```

To remove all entries (entries of the owner, group and others are retained):

```
# setfacl -b <file/dir>

```

**Note:** The default behavior of *setfacl* is to recalculate the ACL mask entry, unless a `--mask` entry was explicitly given. The mask entry is set to the union of all permissions of the owning group, and all named user and group entries (These are exactly the entries affected by the mask entry).

**Tip:** To apply operations to all files and directories recursively, append the `-R` argument.

### Show ACL

To show permissions, use:

```
# getfacl <file/dir>

```

## Examples

Set all permissions for user `johnny` to file named `abc`:

```
# setfacl -m "u:johnny:rwx" abc

```

Check permissions:

 `# getfacl abc` 
```
# file: abc
# owner: someone
# group: someone
user::rw-
user:johnny:rwx
group::r--
mask::rwx
other::r--

```

Change permissions for user `johnny`:

```
# setfacl -m "u:johnny:r-x" abc

```

Check permissions:

 `# getfacl abc` 
```
# file: abc
# owner: someone
# group: someone
user::rw-
user:johnny:r-x
group::r--
mask::r-x
other::r--

```

Remove all extended ACL entries:

```
# setfacl -b abc

```

Check permissions:

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

## Granting execution permissions for private files to a web server

The following technique describes how a process like a [web server](/index.php/Web_server "Web server") can be granted access to files that reside in a user's home directory, without compromising security by giving the whole world access.

In the following we assume that the web server runs as the user `http` and grant it access to `geoffrey`'s home directory `/home/geoffrey`.

The first step is granting execution permissions for the user `http`:

```
# setfacl -m "u:http:--x" /home/geoffrey

```

**Note:** Execution permissions to a directory are necessary for a process to list the directory's content.

Since the user `http` is now able to access files in `/home/geoffrey`, others no longer need access:

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

As the above output shows, `other`'s no longer have any permissions, but the user `http` is still able to access the files, thus security might be considered increased.

**Note:** One may need to give write access for the user `http` on specific directories and/or files:
```
# setfacl -dm "u:http:rwx" /home/geoffrey/project1/cache

```

## See also

*   [getfacl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/getfacl.1)
*   [setfacl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfacl.1)
*   An old but still relevant (and thorough) [guide](http://vanemery.net/Linux/ACL/linux-acl.html) to ACL
*   [How to set default file permissions for all folders/files in a directory?](http://unix.stackexchange.com/questions/1314/how-to-set-default-file-permissions-for-all-folders-files-in-a-directory)