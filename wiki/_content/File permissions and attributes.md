# File permissions and attributes

Related articles

*   [Users and groups](/index.php/Users_and_groups "Users and groups")
*   [umask](/index.php/Umask "Umask")
*   [Access Control Lists](/index.php/Access_Control_Lists "Access Control Lists")
*   [Capabilities](/index.php/Capabilities "Capabilities")

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Missing description of the three additional bits for SUID, SGID and Sticky. (Discuss in [Talk:File permissions and attributes#](https://wiki.archlinux.org/index.php/Talk:File_permissions_and_attributes))

## Contents

*   [1 Viewing permissions](#Viewing_permissions)
    *   [1.1 What the columns mean](#What_the_columns_mean)
    *   [1.2 What the permissions mean](#What_the_permissions_mean)
        *   [1.2.1 Folders](#Folders)
        *   [1.2.2 Files](#Files)
*   [2 Changing permissions using the chmod command](#Changing_permissions_using_the_chmod_command)
    *   [2.1 Text method](#Text_method)
        *   [2.1.1 Text method shortcuts](#Text_method_shortcuts)
        *   [2.1.2 Copying permissions](#Copying_permissions)
    *   [2.2 Numeric method](#Numeric_method)
    *   [2.3 Bulk chmod](#Bulk_chmod)
*   [3 Changing ownership using the chown command](#Changing_ownership_using_the_chown_command)
*   [4 Access Control Lists](#Access_Control_Lists)
*   [5 File attributes](#File_attributes)
    *   [5.1 chattr and lsattr](#chattr_and_lsattr)
*   [6 Extended attributes](#Extended_attributes)
    *   [6.1 User extended attributes](#User_extended_attributes)
*   [7 See also](#See_also)

## Viewing permissions

In order to use chmod to change permissions of a file or directory, you will first need to know what the current mode of access is. You can view the contents of a directory in the terminal by "cd" to that directory and then using:

```
$ ls -l 

```

The `-l` switch is important because using _ls_ without it will only display the names of files or folders in the directory.

Below is an example of using `ls -l` on my home directory:

 `$ ls -l` 

```
total 128
-rw-r--r-- 1 ben users   832 Jul  6 17:22 #chmodwiki#
drwxr-xr-x 2 ben users  4096 Jul  5 21:03 Desktop
drwxr-xr-x 6 ben users  4096 Jul  5 17:37 Documents
drwxr-xr-x 2 ben users  4096 Jul  5 13:45 Downloads
drwxr-xr-x 2 ben users  4096 Jun 24 03:36 Movies
drwxr-xr-x 2 ben users  4096 Jun 24 03:38 Music
-rw-r--r-- 1 ben users 57047 Jun 24 13:57 Namoroka_wallpaper.png
drwxr-xr-x 2 ben users  4096 Jun 26 00:09 Pictures
drwxr-xr-x 3 ben users  4096 Jun 24 05:03 R
-rw-r--r-- 1 ben users   354 Jul  6 17:15 chmodwiki
-rw-r--r-- 1 ben users  5120 Jun 27 08:28 data
-rw-r--r-- 1 ben users  3339 Jun 27 08:28 datadesign
-rw-r--r-- 1 ben users  2048 Jul  6 12:56 dustprac
-rw-r--r-- 1 ben users  1568 Jun 27 14:11 dustpracdesign
-rw-r--r-- 1 ben users  1532 Jun 27 14:07 dustpracdesign~
-rw-r--r-- 1 ben users   229 Jun 27 14:01 ireland.R
-rw-r--r-- 1 ben users   570 Jun 27 17:02 noattach.R
-rw-r--r-- 1 ben users   588 Jun  5 15:35 noattach.R~

```

### What the columns mean

The first column is the type of each file:

*   **-** denotes a normal file.
*   **d** denotes a directory, i.e. a folder containing other files or folders.
*   **p** denotes a named pipe (aka FIFO).
*   **l** denotes a symbolic link.

The letters after that are the permissions, this first column is what we will be most interested in. The second one is how many links there are in a file, we can safely ignore it. The third column has two values/names: The first one (in my example 'ben') is the name of the user that owns the file. The second value ('users' in the example) is the **group** that the owner belongs to (Read more about [groups](/index.php/Groups "Groups")).

The next column is the size of the file or directory in bytes and information after that are the dates and times the file or directory was last modified, and of course the name of the file or directory.

### What the permissions mean

The first three letters, after the first **-** or **d**, are the permissions the owner has. The next three letters are permissions that apply to the group. The final three letters are the permissions that apply to everyone else. Each set of three letters is made up of **r w** and **x**. **r** is always in the first position, **w** is always in the second position, and **x** is always in the third position. **r** is the read permission, **w** is the write permission, and **x** is the execute permission. If there is a hyphen (**-**) in the place of one of these letters it means the permission is not granted, and if the letter is present then it is granted.

#### Folders

In case of folders the mode bits can be interpreted as follows:

*   **r** (read) stands for the ability to read the table of contents of the given directory,
*   **w** (write) stands for the ability to write the table of contents of the given directory (create new files, folders; rename, delete existing files, folders) **if and only if** execute bit is set. Otherwise this permission is meaningless.
*   **x** (execute) stands for the ability to enter the given directory with command `cd` and access files, folders in that directory.

Let's see some examples to clarify, taking one directory from above:

```
# Ben has full access to the Documents directory.
# He can list, create files and rename, delete any file in Documents,
# regardless of file permissions.
# His ability to access a file depends on the file's permission. 
**drwx------ 6** ben users  4096 Jul  5 17:37 Documents

# Ben has full access except he can not create, rename, delete
# any file.
# He can list the files and (if file's permission empowers) 
# may access an existing file in Documents.
**dr-x------ 6** ben users  4096 Jul  5 17:37 Documents

# Ben can not do 'ls' in Documents but if he knows
# the name of an existing file then he may list, rename, delete or
# (if file's permission empowers him) access it.
# Also, he is able to create new files.
**d-wx------ 6** ben users  4096 Jul  5 17:37 Documents

# Ben is only capable of (if file's permission empowers him) 
# access those files in Documents which he knows of.
# He can not list already existing files or create, rename,
# delete any of them.
**d--x------ 6** ben users  4096 Jul  5 17:37 Documents

```

You should keep in mind that we elaborate on directory permissions and it has nothing to do with the individual file permissions. When you create a new file it is the directory that changes. That is why you need write permission to the directory.

**Note:** To keep out graphical file managers, you ought to remove **r**, not **x**.

#### Files

Let's look at another example, this time of a file, not a directory:

```
**-rw-r--r--** 1 ben users  5120 Jun 27 08:28 data

**- rw- r-- r--** 1 ben users 5120 Jun 27 08:28 data (Split the permissions coloumn again for easier interpretation)

```

Here we can see the first letter is not **d** but **-**. So we know it is a file, not a directory. Next the owners permissions are **rw-** so the owner has the ability to read and write but not execute. This may seem odd that the owner does not have all three permissions, but the x permission is not needed as it is a text/data file, to be read by a text editor such as Gedit, EMACS, or software like R, and not an executable in it's own right (if it contained something like python programming code then it very well could be). The group's permssions are set to **r--**, so the group has the ability to read the file but not write/edit it in any way - it is essentially like setting something to Read-Only. We can see that the same permissions apply to everyone else as well.

## Changing permissions using the chmod command

[chmod](https://en.wikipedia.org/wiki/chmod "wikipedia:chmod") is a command in Linux and other Unix-like operating systems. It allows you to _ch_ange the permissions (or access _mod_e) of a file or directory.

### Text method

To change the permissions-or _access mode_-of a file, we use the `chmod` command in a terminal. Below is the command's general structure:

```
chmod _who_=_permissions_ _filename_

```

Where _Who_ is any from a range of letters, and each signifies who you are going to give the permission to. They are as follows:

```
u - The **u**ser that own the file.
g - The **g**roup the file belongs to.
o - The **o**ther users i.e. everyone else.
a - **a**ll of the above - use this instead of having to type **ugo**.

```

The permissions are the same as already discussed (**r, w,** and **x**).

Let's have a look at some examples now using this command. Suppose we became very protective of the Documents directory and wanted to deny everybody but ourselves, permissions to read, write, and execute (or in this case search/look) in it:

```
Before: drwxr-xr-x 6 ben users  4096 Jul  5 17:37 Documents

```

```
Command 1: chmod g= Documents
Command 2: chmod o= Documents

```

```
After: drwx------ 6 ben users  4096 Jul  6 17:32 Documents

```

Here, because we want to deny permissions, we do not put any letter after the **=** where permissions would be entered. Now you can see that only the owner's permissions are **rwx** and all other permissions are **-'**s.

This can be reverted with:

```
Before: drwx------ 6 ben users  4096 Jul  6 17:32 Documents

```

```
Command 1: chmod g=rx Documents
Command 2: chmod o=rx Documents

```

```
After: drwxr-xr-x 6 ben users  4096 Jul  6 17:32 Documents

```

In the next example, we want to grant read and execute permissions to the group, and other users, so we put the letters for the permissions (**r** and **x**) after the **=**, with no spaces.

You can simplify this to put more than one **who** letter in the same command e.g:

```
chmod go=rx Documents

```

**Note:** It does not matter which order you put the who letters or the permission letters in a `chmod` command: you could have `chmod go=rx File` or `chmod og=xr File`. It is all the same.

Now let's consider a second example, say we want to change our data file so that we have read and write permissions, and fellow users in our group **users** who may be colleagues working with us on **data**, can also read and write to it, but other users can only read it:

```
Before: -rw-r--r-- 1 ben users  5120 Jun 27 08:28 data

```

```
Command1: chmod g=rw data

```

```
After: -rw-rw-r-- 1 ben users  5120 Jun 27 08:28 data

```

This is exactly like the first example, but with a data file, not a directory, and we grant a write permission (just so as to give an example of granting every permission).

#### Text method shortcuts

The `chmod` command lets us add and subtract permissions from an existing set using **+** or **-** instead of **=**. This is different to the above commands, which essentially re-write the permissions (i.e. to change a permission from **r--** to **rw-**, you still need to include **r** as well as **w** after the **=** in the `chmod` command. If you missed out **r**, it would take away the **r** permission as they are being re-written with the **=**. Using **+** and **-** avoid this by adding or taking away from the _current_ set of permissions).

Let's try this **+** and **-** method with the previous example of adding write permissions to the group:

```
Before: -rw-r--r-- 1 ben users 5120 Jun 27 08:28 data

Command: chmod g+w data

```

```
After: -rw-rw-r-- 1 ben users  5120 Jun 27 08:28 data

```

Another example, denying write permissions to all (**a**):

```
Before: -rw-rw-r-- 1 ben users  5120 Jun 27 08:28 data

Command: chmod a-w data

```

```
After: -r--r--r-- 1 ben users  5120 Jun 27 08:28 data

```

#### Copying permissions

It is possible to tell `chmod` to copy the permissions from one class, say the owner, and give those same permissions to group or even all. To do this, instead of putting **r**, **w**, or **x** after the **=**, we put another **who** letter. e.g:

```
Before: -rw-r--r-- 1 ben users 5120 Jun 27 08:28 data

```

```
Command: chmod g=u data

```

```
After: -rw-rw-r-- 1 ben users 5120 Jun 27 08:28 data

```

This command essentially translates to "change the permissions of group (**g=**), to be the same as the owning user (**=u**). Note that you cannot copy a set of permissions as well as grant new ones e.g.:

```
chmod g=wu data

```

In that case, `chmod` will have a small fit and throw you an error.

### Numeric method

chmod can also set permissions using numbers.

Using numbers is another method which allows you to edit the permissions for all three owner, group, and others at the same time. This basic structure of the code is this:

```
_chmod xxx file/directory_

```

Where **xxx** is a 3 digit number where each digit can be anything from 1 to 7\. The first digit applies to permissions for owner, the second digit applies to permissions for group, and the third digit applies to permissions for all others.

In this number notation, the values r, w, and x have their own number value:

```
r=4
w=2
x=1

```

To come up with a three digit number you need to consider what permissions you want owner, group, and user to have, and then total their values up. For example, say I wanted to grant the owner of a directory read write and execution permissions, and I wanted group and everyone else to have just read and execute permissions. I would come up with the numerical values like so:

```
Owner: rwx = 4+2+1=7
Group: r-x = 4+0+1=5 (or just 4+1=5)
Other: r-x = 4+0+1=5 (or just 4+1=5)

```

```
Final number = 755

```

```
Command: _chmod 755 filename_

```

This is the equivalent of using the following:

```
chmod u=rwx filename
chmod go=rx filename

```

Most folders/directories are set to **755** to allow reading and writing and execution to the owner, but deny writing to everyone else, and files are normally **644** to allow reading and writing for the owner but just reading for everyone else, refer to the last note on the lack of **x** permissions with non executable files - its the same deal here.

To see this in action with examples consider the previous example I've been using but with this numerical method applied instead:

```
Before: -rw-r--r-- 1 ben users  5120 Jun 27 08:28 data

```

```
Command: chmod 664 data

```

```
After: -rw-rw-r-- 1 ben users  5120 Jun 27 08:28 data

```

If this were an executable the number would be **774** if I wanted to grant executable permission to the owner and group. Alternatively if I wanted everyone to only have read permission the number would be **444**. Treating **r** as **4**, **w** as **2**, and **x** as **1** is probably the easiest way to work out the numerical values for using **chmod xxx filename**, but there is also a binary method, where each permission has a binary number, and then that is in turn converted to a number. It is a bit more convoluted, but I include it for completeness.

Consider this permission set:

**- rwx r-x r--**

If you put a 1 under each permission granted, and a 0 for every one not granted, the result would be something like this:

```
**- rwx rwx r-x**
 **111 111 101**  

```

You can then convert these binary numbers:

```
000=0	    100=4
001=1	    101=5
010=2	    110=6
011=3	    111=7

```

The value of the above would therefore be **775**.

Consider we wanted to remove the writable permission from group:

```
**- rwz r-x r-x**
 **111 101 101**

```

The value would therefore be **755** and you would use **chmod 755 filename** to remove the writable permission. You will notice you get the same three digit number no matter which method you use. Whether you use text or numbers will depend on personal preference and typing speed. When you want to restore a directory or file to default permissions i.e. read and write (and execute) permission to the owner but deny write permission to everyone else, it may be faster to use **chmod 755/644 directory/filename**. But if you are changing the permissions to something out of the norm, it may be simpler and quicker to use the text method as opposed to trying to convert it to numbers, which may lead to a mistake. It could be argued that there isn't any real significant difference in the speed of either method for a user that only needs to use chmod on occasion.

### Bulk chmod

Generally directories and files should not have the same permissions. If it is necessary to bulk modify a directory tree, use _find_ to selectively modify one or the other.

To chmod only directories to 755:

```
$ find _directory_ -type d -exec chmod 755 {} +

```

To chmod only files to 644:

```
$ find _directory_ -type f -exec chmod 644 {} +

```

## Changing ownership using the chown command

Whilst this is an article dedicated to chmod, [chown](https://en.wikipedia.org/wiki/chown "wikipedia:chown") deserves mention as well. Where chmod changes the access mode of a file or directory, chown changes the owner of a file or directory, which is quicker and easier than altering the permissions in some cases, but do be careful when you do so.

Consider the following example, making a new partition with GParted for backup data. Gparted does this all as root so everything belongs to root. This is all well and good but when it came to writing data to the mounted partition, permission was denied.

```
brw-rw----  1 root disk      8,   9 Jul  6 16:02 sda9
drwxr-xr-x 5 root  root 4096 Jul  6 16:01 Backup

```

As you can see the device in **/dev** is owned by **root**, as is where it is mounted (**/media/Backup**). To change the owner of where it is mounted one can do the following:

```
Before: drwxr-xr-x 5 root  root 4096 Jul  6 16:01 Backup

```

```
Command: chown ben Backup  (cd'd to /media first)

```

```
After drwxr-xr-x 5 ben  root 4096 Jul  6 16:01 Backup

```

Now the partition can have backup data written to it as instead of altering the permissions, as the owner already has **rwx** permissions, the owner has been altered to the user ben. Alternatives would be to alter the permissions for everyone else (undesirable as it's a backup permission) or adding the user to the group **root**.

## Access Control Lists

[Access Control Lists](/index.php/Access_Control_Lists "Access Control Lists") provides an additional, more flexible permission mechanism for file systems by allowing to set permissions for any user or group to any file.

The presence of ACLs can be identified by a plus (`+`) sign in the [output of ls command](/index.php/Access_Control_Lists#Output_of_ls_command "Access Control Lists").

## File attributes

Apart from the file mode bits that control [user and group](/index.php/Users_and_groups "Users and groups") read, write and execute permissions, several [file systems](/index.php/File_systems "File systems") support file attributes that enable further customization of allowable file operations. This section describes some of these attributes and how to work with them.

**Warning:** By default, file attributes are not preserved by cp, rsync, and probably others.

### chattr and lsattr

For ext2 and [ext3](/index.php/Ext3 "Ext3") file systems, the [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) package contains the programs [lsattr](https://en.wikipedia.org/wiki/lsattr "wikipedia:lsattr") and [chattr](https://en.wikipedia.org/wiki/chattr "wikipedia:chattr") that list and change a file's attributes, respectively. Though some are not honored by all file systems, the available attributes are:

*   a : append only
*   c : compressed
*   d : no dump
*   e : extent format
*   i : immutable
*   j : data journalling
*   s : secure deletion
*   t : no tail-merging
*   u : undeletable
*   A : no atime updates
*   C : no copy on write
*   D : synchronous directory updates
*   S : synchronous updates
*   T : top of directory hierarchy

For example, if you want to set the immutable bit on some file, use the following command:

```
# chattr +i _/path/to/file_

```

To remove an attribute on a file just change `+` to `-`.

## Extended attributes

From `attr(5)`: "Extended attributes are name:value pairs associated permanently with files and directories". There are four extended attribute classes: security, system, trusted and user.

**Warning:** By default, extended attributes are not preserved by cp, rsync, and probably others.

### User extended attributes

User extended attributes can be used to store arbitrary information about a file. To create one:

```
$ setfattr -n user.checksum -v "3baf9ebce4c664ca8d9e5f6314fb47fb" foo.bar

```

Use getfattr to display extended attributes:

```
$ getfattr -d foo.bar
# file: foo.bar
user.checksum="3baf9ebce4c664ca8d9e5f6314fb47fb"

```

## See also

*   [wikipedia:Chattr](https://en.wikipedia.org/wiki/Chattr "wikipedia:Chattr")
*   [Linux File Permission Confusion](http://www.hackinglinuxexposed.com/articles/20030417.html)
*   [Linux File Permission Confusion part 2](http://www.hackinglinuxexposed.com/articles/20030424.html)
*   [wikipedia:Extended file attributes#Linux](https://en.wikipedia.org/wiki/Extended_file_attributes#Linux "wikipedia:Extended file attributes")
*   [Extended attributes: the good, the not so good, the bad.](http://www.lesbonscomptes.com/pages/extattrs.html)
*   [Backup and restore file permissions in Linux](http://www.concrete5.org/documentation/how-tos/designers/backup-and-restore-file-permissions-in-linux/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=File_permissions_and_attributes&oldid=406729](https://wiki.archlinux.org/index.php?title=File_permissions_and_attributes&oldid=406729)"