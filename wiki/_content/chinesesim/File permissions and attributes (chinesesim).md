Related articles

*   [Users and groups (简体中文)](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Users and groups (简体中文)")
*   [umask (简体中文)](/index.php?title=Umask_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "Umask (简体中文) (page does not exist)")
*   [Access Control Lists (简体中文)](/index.php?title=Access_Control_Lists_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "Access Control Lists (简体中文) (page does not exist)")
*   [Capabilities (简体中文)](/index.php/Capabilities_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Capabilities (简体中文)")

**翻译状态：** 本文是英文页面 [File permissions and attributes](/index.php/File_permissions_and_attributes "File permissions and attributes") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-07-30，点击[这里](https://wiki.archlinux.org/index.php?title=File+permissions+and+attributes&diff=0&oldid=562573)可以查看翻译后英文页面的改动。

[文件系统](/index.php/%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F "文件系统") 用 [权限](https://en.wikipedia.org/wiki/File_system_permissions "w:File system permissions") 和 [属性](https://en.wikipedia.org/wiki/File_attribute "w:File attribute")来规范系统进程与文件和目录之间的交互。

**警告:** 权限和属性设置只能防范来自已经启动了的当前系统的攻击。为了防止数据被能物理访问该机器的人的接触，必须同时使用[磁盘加密](/index.php/%E7%A3%81%E7%9B%98%E5%8A%A0%E5%AF%86 "磁盘加密").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 查看权限](#查看权限)
    *   [1.1 Examples](#Examples)
*   [2 Changing permissions](#Changing_permissions)
    *   [2.1 Text method](#Text_method)
        *   [2.1.1 Text method shortcuts](#Text_method_shortcuts)
        *   [2.1.2 Copying permissions](#Copying_permissions)
    *   [2.2 Numeric method](#Numeric_method)
    *   [2.3 Bulk chmod](#Bulk_chmod)
*   [3 Changing ownership](#Changing_ownership)
*   [4 Access Control Lists](#Access_Control_Lists)
*   [5 Umask](#Umask)
*   [6 File attributes](#File_attributes)
    *   [6.1 chattr and lsattr](#chattr_and_lsattr)
*   [7 Extended attributes](#Extended_attributes)
    *   [7.1 User extended attributes](#User_extended_attributes)
    *   [7.2 Preserving extended attributes](#Preserving_extended_attributes)
*   [8 Tips and tricks](#Tips_and_tricks)
    *   [8.1 Preserve root](#Preserve_root)
*   [9 See also](#See_also)

## 查看权限

使用[ls](/index.php/Ls "Ls")命令的 `-l`选项查看为目录内容设置的权限（或**文件模式**），例如：

 `$ ls -l /path/to/directory` 
```
total 128
drwxr-xr-x 2 archie users  4096 Jul  5 21:03 Desktop
drwxr-xr-x 6 archie users  4096 Jul  5 17:37 Documents
drwxr-xr-x 2 archie users  4096 Jul  5 13:45 Downloads
-rw-rw-r-- 1 archie users  5120 Jun 27 08:28 customers.ods
-rw-r--r-- 1 archie users  3339 Jun 27 08:28 todo
-rwxr-xr-x 1 archie users  2048 Jul  6 12:56 myscript.sh

```

第一栏是我们必须关注的内容。 以 `drwxrwxrwx +`为例，每个字符的含义在下表中说明：

| `d` | `rwx` | `rwx` | `rwx` | `+` |
| 文件类型，技术上不属于其权限。 有关可能值的说明，请参阅 `info ls -n "What information is listed"`。 | 所有者对文件的权限，如下所述。 | 该组对该文件的权限，如下所述。 | 所有其他用户对该文件的权限，如下所述。 | 一个字符，指定备用访问方法是否适用于该文件。 当此字符是空格时，没有替代访问方法。 `.`字符表示具有安全上下文的文件，但没有其他备用访问方法。 具有备用访问方法的任何其他组合的文件用 `+`字符标记，例如在[Access Control Lists](/index.php/Access_Control_Lists "Access Control Lists")的情况下. |

Each of the three permission triads (`rwx` in the example above) can be made up of the following characters:

 Character | Effect on files | Effect on directories |
| Read permission (first character) | `-` | The file cannot be read. | The directory's contents cannot be shown. |
| `r` | The file can be read. | The directory's contents can be shown. |
| Write permission (second character) | `-` | The file cannot be modified. | The directory's contents cannot be modified. |
| `w` | The file can be modified. | The directory's contents can be modified (create new files or folders; rename or delete existing files or folders); requires the execute permission to be also set, otherwise this permission has no effect. |
| Execute permission (third character) | `-` | The file cannot be executed. | The directory cannot be accessed with [cd](/index.php/Cd "Cd"). |
| `x` | The file can be executed. | The directory can be accessed with [cd](/index.php/Cd "Cd"); this is the only permission bit that in practice can be considered to be "inherited" from the ancestor directories, in fact if *any* folder in the path does not have the `x` bit set, the final file or folder cannot be accessed either, regardless of its permissions; see [path_resolution(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/path_resolution.7) for more information. |
| `s` | The [setuid](https://en.wikipedia.org/wiki/setuid "w:setuid") bit when found in the **u**ser triad; the **setgid** bit when found in the **g**roup triad; it is not found in the **o**thers triad; it also implies that `x` is set. |
| `S` | Same as `s`, but `x` is not set; rare on regular files, and useless on folders. |
| `t` | The [sticky](https://en.wikipedia.org/wiki/sticky_bit "w:sticky bit") bit; it can only be found in the **o**thers triad; it also implies that `x` is set. |
| `T` | Same as `t`, but `x` is not set; rare on regular files, and useless on folders. |

See `info Coreutils -n "Mode Structure"` and [chmod(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chmod.1) for more details.

**Tip:** You can view permissions along a path with `namei -l *path*`.

### Examples

Let us see some examples to clarify:

```
**drwx------** 6 archie users  4096 Jul  5 17:37 Documents

```

Archie has full access to the Documents directory. He can list, create files and rename, delete any file in Documents, regardless of file permissions. His ability to access a file depends on the file's permission.

```
**dr-x------** 6 archie users  4096 Jul  5 17:37 Documents

```

Archie has full access except he can not create, rename, delete any file. He can list the files and (if file's permission empowers) may access an existing file in Documents.

```
**d-wx------** 6 archie users  4096 Jul  5 17:37 Documents

```

Archie can not do 'ls' in Documents but if he knows the name of an existing file then he may list, rename, delete or (if file's permission empowers him) access it. Also, he is able to create new files.

```
**d--x------** 6 archie users  4096 Jul  5 17:37 Documents

```

Archie is only capable of (if file's permission empowers him) access those files in Documents which he knows of. He can not list already existing files or create, rename, delete any of them.

You should keep in mind that we elaborate on directory permissions and it has nothing to do with the individual file permissions. When you create a new file it is the directory that changes. That is why you need write permission to the directory.

Let us look at another example, this time of a file, not a directory:

```
**-rw-r--r--** 1 archie users  5120 Jun 27 08:28 foobar

```

Here we can see the first letter is not `d` but `-`. So we know it is a file, not a directory. Next the owner's permissions are `rw-` so the owner has the ability to read and write but not execute. This may seem odd that the owner does not have all three permissions, but the `x` permission is not needed as it is a text/data file, to be read by a text editor such as Gedit, EMACS, or software like R, and not an executable in its own right (if it contained something like python programming code then it very well could be). The group's permissions are set to `r--`, so the group has the ability to read the file but not write/edit it in any way — it is essentially like setting something to read-only. We can see that the same permissions apply to everyone else as well.

## Changing permissions

[chmod](https://en.wikipedia.org/wiki/chmod "wikipedia:chmod") is a command in Linux and other Unix-like operating systems that allows to *ch*ange the permissions (or access *mod*e) of a file or directory.

### Text method

To change the permissions — or *access mode* — of a file, use the *chmod* command in a terminal. Below is the command's general structure:

```
chmod *who*=*permissions* *filename*

```

Where `*who*` is any from a range of letters, each signifying who is being given the permission. They are as follows:

*   `u`: the [user](/index.php/User "User") that owns the file.
*   `g`: the [user group](/index.php/User_group "User group") that the file belongs to.
*   `o`: the **o**ther users, i.e. everyone else.
*   `a`: **a**ll of the above; use this instead of typing `ugo`.

The permissions are the same as discussed in [#Viewing permissions](#Viewing_permissions) (`r`, `w` and `x`).

Now have a look at some examples using this command. Suppose you became very protective of the Documents directory and wanted to deny everybody but yourself, permissions to read, write, and execute (or in this case search/look) in it:

Before: `drwxr-xr-x 6 archie users 4096 Jul 5 17:37 Documents`

```
$ chmod g= Documents
$ chmod o= Documents

```

After: `drwx------ 6 archie users 4096 Jul 6 17:32 Documents`

Here, because you want to deny permissions, you do not put any letters after the `=` where permissions would be entered. Now you can see that only the owner's permissions are `rwx` and all other permissions are `-`.

This can be reverted with:

Before: `drwx------ 6 archie users 4096 Jul 6 17:32 Documents`

```
$ chmod g=rx Documents
$ chmod o=rx Documents

```

After: `drwxr-xr-x 6 archie users 4096 Jul 6 17:32 Documents`

In the next example, you want to grant read and execute permissions to the group, and other users, so you put the letters for the permissions (`r` and `x`) after the `=`, with no spaces.

You can simplify this to put more than one `*who*` letter in the same command, e.g:

```
$ chmod go=rx Documents

```

**Note:** It does not matter in which order you put the `*who*` letters or the permission letters in a `chmod` command: you could have `chmod go=rx file` or `chmod og=xr file`. It is all the same.

Now let us consider a second example, suppose you want to change a `foobar` file so that you have read and write permissions, and fellow users in the group `users` who may be colleagues working on `foobar`, can also read and write to it, but other users can only read it:

Before: `-rw-r--r-- 1 archie users 5120 Jun 27 08:28 foobar`

```
$ chmod g=rw foobar

```

After: `-rw-rw-r-- 1 archie users 5120 Jun 27 08:28 foobar`

This is exactly like the first example, but with a file, not a directory, and you grant write permission (just so as to give an example of granting every permission).

#### Text method shortcuts

The *chmod* command lets add and subtract permissions from an existing set using `+` or `-` instead of `=`. This is different from the above commands, which essentially re-write the permissions (e.g. to change a permission from `r--` to `rw-`, you still need to include `r` as well as `w` after the `=` in the *chmod* command invocation. If you missed out `r`, it would take away the `r` permission as they are being re-written with the `=`. Using `+` and `-` avoids this by adding or taking away from the *current* set of permissions).

Let us try this `+` and `-` method with the previous example of adding write permissions to the group:

Before: `-rw-r--r-- 1 archie users 5120 Jun 27 08:28 foobar`

```
$ chmod g+w foobar

```

After: `-rw-rw-r-- 1 archie users 5120 Jun 27 08:28 foobar`

Another example, denying write permissions to all (**a**):

Before: `-rw-rw-r-- 1 archie users 5120 Jun 27 08:28 foobar`

```
$ chmod a-w foobar

```

After: `-r--r--r-- 1 archie users 5120 Jun 27 08:28 foobar`

A different shortcut is the special `X` mode: this is not an actual file mode, but it is often used in conjunction with the `-R` option to set the executable bit only for directories, and leave it unchanged for regular files, for example:

```
$ chmod -R a+rX ./data/

```

#### Copying permissions

It is possible to tell *chmod* to copy the permissions from one class, say the owner, and give those same permissions to group or even all. To do this, instead of putting `r`, `w`, or `x` after the `=`, put another *who* letter. e.g:

Before: `-rw-r--r-- 1 archie users 5120 Jun 27 08:28 foobar`

```
$ chmod g=u foobar

```

After: `-rw-rw-r-- 1 archie users 5120 Jun 27 08:28 foobar`

This command essentially translates to "change the permissions of group (`g=`), to be the same as the owning user (`=u`). Note that you cannot copy a set of permissions as well as grant new ones e.g.:

```
$ chmod g=wu foobar

```

In that case *chmod* throw an error.

### Numeric method

*chmod* can also set permissions using numbers.

Using numbers is another method which allows you to edit the permissions for all three owner, group, and others at the same time, as well as the setuid, setgid, and sticky bits. This basic structure of the code is this:

```
$ chmod *xxx* *filename*

```

Where `**xxx**` is a 3-digit number where each digit can be anything from 0 to 7\. The first digit applies to permissions for owner, the second digit applies to permissions for group, and the third digit applies to permissions for all others.

In this number notation, the values `r`, `w`, and `x` have their own number value:

```
r=4
w=2
x=1

```

To come up with a 3-digit number you need to consider what permissions you want owner, group, and user to have, and then total their values up. For example, if you want to grant the owner of a directory read write and execution permissions, and you want group and everyone else to have just read and execute permissions, you would come up with the numerical values like so:

*   Owner: `rwx`=4+2+1=7
*   Group: `r-x`=4+0+1=5
*   Other: `r-x`=4+0+1=5

```
$ chmod 755 *filename*

```

This is the equivalent of using the following:

```
$ chmod u=rwx *filename*
$ chmod go=rx *filename*

```

To view the existing permissions of a file or directory in numeric form, use the [stat(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/stat.1) command:

```
$ stat -c %a *filename*

```

Where the %a option specifies output in numeric form.

Most folders and directories are set to `755` to allow reading, writing and execution to the owner, but deny writing to everyone else, and files are normally `644` to allow reading and writing for the owner but just reading for everyone else; refer to the last note on the lack of `x` permissions with non executable files: it is the same thing here.

To see this in action with examples consider the previous example that has been used but with this numerical method applied instead:

Before: `-rw-r--r-- 1 archie users 5120 Jun 27 08:28 foobar`

```
$ chmod 664 foobar

```

After: `-rw-rw-r-- 1 archie users 5120 Jun 27 08:28 foobar`

If this were an executable the number would be `774` if you wanted to grant executable permission to the owner and group. Alternatively if you wanted everyone to only have read permission the number would be `444`. Treating `r` as 4, `w` as 2, and `x` as 1 is probably the easiest way to work out the numerical values for using `chmod *xxx* *filename*`, but there is also a binary method, where each permission has a binary number, and then that is in turn converted to a number. It is a bit more convoluted, but here included for completeness.

Consider this permission set:

```
-rwxr-xr--

```

If you put a 1 under each permission granted, and a 0 for every one not granted, the result would be something like this:

```
-rwxrwxr-x
 111111101

```

You can then convert these binary numbers:

```
000=0	    100=4
001=1	    101=5
010=2	    110=6
011=3	    111=7

```

The value of the above would therefore be 775\.

Consider we wanted to remove the writable permission from group:

```
-rwxr-xr-x
 111101101

```

The value would therefore be 755 and you would use `chmod 755 *filename*` to remove the writable permission. You will notice you get the same three digit number no matter which method you use. Whether you use text or numbers will depend on personal preference and typing speed. When you want to restore a directory or file to default permissions e.g. read and write (and execute) permission to the owner but deny write permission to everyone else, it may be faster to use `chmod 755/644 *filename*`. However if you are changing the permissions to something out of the norm, it may be simpler and quicker to use the text method as opposed to trying to convert it to numbers, which may lead to a mistake. It could be argued that there is not any real significant difference in the speed of either method for a user that only needs to use *chmod* on occasion.

You can also use the numeric method to set the `setuid`, `setgid`, and `sticky` bits by using four digits.

```
setuid=4
setgid=2
sticky=1

```

For example, `chmod 2777 *filename*` will set read/write/executable bits for everyone and also enable the `setgid` bit.

### Bulk chmod

Generally directories and files should not have the same permissions. If it is necessary to bulk modify a directory tree, use [find](/index.php/Find "Find") to selectively modify one or the other.

To *chmod* only directories to 755:

```
$ find *directory* -type d -exec chmod 755 {} +

```

To *chmod* only files to 644:

```
$ find *directory* -type f -exec chmod 644 {} +

```

## Changing ownership

[chown](https://en.wikipedia.org/wiki/chown "wikipedia:chown") changes the owner of a file or directory, which is quicker and easier than altering the permissions in some cases.

Consider the following example, making a new partition with [GParted](/index.php/GParted "GParted") for backup data. Gparted does this all as root so everything belongs to root by default. This is all well and good but when it comes to writing data to the mounted partition, permission is denied for regular users.

```
brw-rw---- 1 root disk 8,    9 Jul  6 16:02 sda9
drwxr-xr-x 5 root root    4096 Jul  6 16:01 Backup

```

As you can see the device in `/dev` is owned by root, as is the mount location (`/media/Backup`). To change the owner of the mount location one can do the following:

Before: `drwxr-xr-x 5 root root 4096 Jul 6 16:01 Backup`

```
# chown archie /media/Backup

```

After: `drwxr-xr-x 5 archie root 4096 Jul 6 16:01 Backup`

Now the partition can have data written to it by the new owner, archie, without altering the permissions (as the owner triad already had `rwx` permissions).

**Note:**

*   `chown` always clears the setuid and setgid bits.
*   Non-root users cannot use `chown` to "give away" files they own to another user.

## Access Control Lists

[Access Control Lists](/index.php/Access_Control_Lists "Access Control Lists") provides an additional, more flexible permission mechanism for file systems by allowing to set permissions for any user or group to any file.

## Umask

The [umask](/index.php/Umask "Umask") utility is used to control the file-creation mode mask, which determines the initial value of file permission bits for newly created files.

## File attributes

Apart from the file mode bits that control [user and group](/index.php/Users_and_groups "Users and groups") read, write and execute permissions, several [file systems](/index.php/File_systems "File systems") support file attributes that enable further customization of allowable file operations. This section describes some of these attributes and how to work with them.

**Warning:** By default, file attributes are not preserved by [cp](/index.php/Cp "Cp"), [rsync](/index.php/Rsync "Rsync"), and other similar programs.

### chattr and lsattr

For ext2 and [ext3](/index.php/Ext3 "Ext3") file systems, the [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) package contains the programs [lsattr](https://en.wikipedia.org/wiki/lsattr "wikipedia:lsattr") and [chattr](https://en.wikipedia.org/wiki/chattr "wikipedia:chattr") that list and change a file's attributes, respectively. Though some are not honored by all file systems, the available attributes are:

*   `a`: append only
*   `c`: compressed
*   `d`: no dump
*   `e`: extent format
*   `i`: immutable
*   `j`: data journalling
*   `s`: secure deletion
*   `t`: no tail-merging
*   `u`: undeletable
*   `A`: no atime updates
*   `C`: no copy on write
*   `D`: synchronous directory updates
*   `S`: synchronous updates
*   `T`: top of directory hierarchy

For example, if you want to set the immutable bit on some file, use the following command:

```
# chattr +i */path/to/file*

```

To remove an attribute on a file just change `+` to `-`.

## Extended attributes

From [xattr(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xattr.7): "Extended attributes are name:value pairs associated permanently with files and directories". There are four extended attribute classes: security, system, trusted and user.

**Warning:** By default, extended attributes are not preserved by [cp](/index.php/Cp "Cp"), [rsync](/index.php/Rsync "Rsync"), and other similar programs, see [#Preserving extended attributes](#Preserving_extended_attributes).

Extended attributes are also used to set [Capabilities](/index.php/Capabilities "Capabilities").

### User extended attributes

User extended attributes can be used to store arbitrary information about a file. To create one:

```
$ setfattr -n user.checksum -v "3baf9ebce4c664ca8d9e5f6314fb47fb" foo.txt

```

Use getfattr to display extended attributes:

 `$ getfattr -d foo.txt` 
```
# file: foo.txt
user.checksum="3baf9ebce4c664ca8d9e5f6314fb47fb"
```

### Preserving extended attributes

| Command | Required flag |
| `cp` | `--preserve=mode,ownership,timestamps,xattr` |
| `mv` | preserves by default |
| `tar` | `--xattrs` for creation and extraction |
| `bsdtar` | `-p` for extraction |
| [rsync](/index.php/Rsync "Rsync") | `--xattrs` |

1.  mv silently discards extended attributes when the target file system does not support them.

To preserve extended attributes with [text editors](/index.php/Text_editor "Text editor") you need to configure them to truncate files on saving instead of using [rename(2)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rename.2).[[1]](https://unix.stackexchange.com/questions/45407)

## Tips and tricks

### Preserve root

Use the `--preserve-root` flag to prevent `chmod` from acting recursively on `/`. This can, for example, prevent one from removing the executable bit systemwide and thus breaking the system. To use this flag every time, set it within an [alias](/index.php/Alias "Alias"). See also [[2]](https://www.reddit.com/r/linux/comments/4ni3xe/tifu_sudo_chmod_644/).

## See also

*   [wikipedia:Chattr](https://en.wikipedia.org/wiki/Chattr "wikipedia:Chattr")
*   [Linux File Permission Confusion](http://www.hackinglinuxexposed.com/articles/20030417.html)
*   [Linux File Permission Confusion part 2](http://www.hackinglinuxexposed.com/articles/20030424.html)
*   [wikipedia:Extended file attributes#Linux](https://en.wikipedia.org/wiki/Extended_file_attributes#Linux "wikipedia:Extended file attributes")
*   [Extended attributes: the good, the not so good, the bad.](http://www.lesbonscomptes.com/pages/extattrs.html)
*   [Backup and restore file permissions in Linux](http://www.concrete5.org/documentation/how-tos/designers/backup-and-restore-file-permissions-in-linux/)
*   [Why is “chmod -R 777 /” destructive?](https://serverfault.com/questions/364677/why-is-chmod-r-777-destructive)