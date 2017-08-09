يحتوي ملف [/etc/fstab](https://en.wikipedia.org/wiki/Fstab "wikipedia:Fstab") على معلومات عن نظم الملفات الثابتة .وهو يعرفنا بكيفية وصل أقراص التخزين ونظم الملفات وكيفية دمجا في النظام بشكل كلي. ويتم قراءته من خلال الأمر `mount` لتحديد أي خيار سيستخدم عند وصل قسم أو قرص معين.

## Contents

*   [1 مثال للملف](#.D9.85.D8.AB.D8.A7.D9.84_.D9.84.D9.84.D9.85.D9.84.D9.81)
*   [2 تعريفات الحقول](#.D8.AA.D8.B9.D8.B1.D9.8A.D9.81.D8.A7.D8.AA_.D8.A7.D9.84.D8.AD.D9.82.D9.88.D9.84)
*   [3 تعريف نظم الملفات](#.D8.AA.D8.B9.D8.B1.D9.8A.D9.81_.D9.86.D8.B8.D9.85_.D8.A7.D9.84.D9.85.D9.84.D9.81.D8.A7.D8.AA)
    *   [3.1 تسمية النواة](#.D8.AA.D8.B3.D9.85.D9.8A.D8.A9_.D8.A7.D9.84.D9.86.D9.88.D8.A7.D8.A9)
    *   [3.2 العنوان Label](#.D8.A7.D9.84.D8.B9.D9.86.D9.88.D8.A7.D9.86_Label)
    *   [3.3 معرف UUID](#.D9.85.D8.B9.D8.B1.D9.81_UUID)
*   [4 تلميحات و حيل](#.D8.AA.D9.84.D9.85.D9.8A.D8.AD.D8.A7.D8.AA_.D9.88_.D8.AD.D9.8A.D9.84)
    *   [4.1 معرف قسم التبديل Swap UUID](#.D9.85.D8.B9.D8.B1.D9.81_.D9.82.D8.B3.D9.85_.D8.A7.D9.84.D8.AA.D8.A8.D8.AF.D9.8A.D9.84_Swap_UUID)
    *   [4.2 Filepath spaces](#Filepath_spaces)
    *   [4.3 اﻷقراص الخارجية](#.D8.A7.EF.BB.B7.D9.82.D8.B1.D8.A7.D8.B5_.D8.A7.D9.84.D8.AE.D8.A7.D8.B1.D8.AC.D9.8A.D8.A9)
    *   [4.4 خيارات atime](#.D8.AE.D9.8A.D8.A7.D8.B1.D8.A7.D8.AA_atime)
    *   [4.5 نظام ملفات tmpfs](#.D9.86.D8.B8.D8.A7.D9.85_.D9.85.D9.84.D9.81.D8.A7.D8.AA_tmpfs)
        *   [4.5.1 طرق الاستخدام](#.D8.B7.D8.B1.D9.82_.D8.A7.D9.84.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85)
            *   [4.5.1.1 Improving compile times](#Improving_compile_times)
    *   [4.6 الكتابة على قسم FAT32 كمستخدم عادي](#.D8.A7.D9.84.D9.83.D8.AA.D8.A7.D8.A8.D8.A9_.D8.B9.D9.84.D9.89_.D9.82.D8.B3.D9.85_FAT32_.D9.83.D9.85.D8.B3.D8.AA.D8.AE.D8.AF.D9.85_.D8.B9.D8.A7.D8.AF.D9.8A)
    *   [4.7 إعادة وصل قسم نظام ملفات الجذر](#.D8.A5.D8.B9.D8.A7.D8.AF.D8.A9_.D9.88.D8.B5.D9.84_.D9.82.D8.B3.D9.85_.D9.86.D8.B8.D8.A7.D9.85_.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D8.A7.D9.84.D8.AC.D8.B0.D8.B1)
*   [5 انظر أيضا](#.D8.A7.D9.86.D8.B8.D8.B1_.D8.A3.D9.8A.D8.B6.D8.A7)

## مثال للملف

هذا مثال مبسط لملف `/etc/fstab` يستخدم طريقة معرفات النواة:

 `/etc/fstab` 
```
# <file system>        <dir>         <type>    <options>             <dump> <pass>
/dev/sda1              /             ext4      defaults,noatime      0      1
/dev/sda2              none          swap      defaults              0      0
/dev/sda3              /home         ext4      defaults,noatime      0      2
```

## تعريفات الحقول

يحتوي ملف `/etc/fstab` على الحقول التالية مفصولة بمسافة أو تبويب:

```
 <file system>        <dir>         <type>    <options>             <dump> <pass>

```

*   **<file system>** - القسم أو قرص التخزين الذي سيتم وصله.
*   **<dir>** - نقطة الوصل التي يربط بها نظام الملفات <file system> .
*   **<type>** - نوع نظام الملفات للقسم أو قرص التخزين الذي سيتم وصله. يوجد العديد من نظم الملفات المدعومة مثل: `ext2`, `ext3`, `ext4`, `reiserfs`, `xfs`, `jfs`, `smbfs`, `iso9660`, `vfat`, `ntfs`, `swap` and `auto`.

الخيار `auto` يدع البريمج mount يخمن نوع نظام الملفات المستخدم. وذلك يكون بشكل افتراضي مع وسائط التخزين الضوئية (CD/DVD).

*   **<options>** - خيارات وصل نظام الملفات المستخدمة. لا حظ أن [خيارات التوصيل](http://linux.die.net/man/8/بعض) هي لنظم ملفات معينة.

بعض الخيارات المستخدمة بكثرة هي:

*   `auto` - التوصيل تلقائيا عند الإقلاع، أو عند تغيل الأمر `mount -a` .
*   `noauto` - التوصيل فقط عندما تأمر بذلك.
*   `exec` - السماح بتنفيذ الملفات الثنائية على نظم الملفات.
*   `noexec` - عدم السماح بتنفيذ الملفات الثنائية على نظم الملفات.
*   `ro` - توصيل نظام الملفات على وضعية القراءة فقط.
*   `rw` - توصيل نظام الملفات على وضعية القراءة-الكتابة.
*   `user` - السماح للمستخدم العادي بتوصيل نظام الملفات. وذلك يتضمن تلقائيا الخيارات `noexec`, `nosuid`, `nodev`, إلى يتم إبطالها.
*   `users` - السماح لأي مستخدم في المجموعة بتوصيل نظام الملفات.
*   `nouser` - السماح للمستخدم المدير (الجذر) فقط بتوصيل نظام الملفات.
*   `owner` - السماح للمستخدم مالك القرص فقط بتوصيل نظام الملفات.
*   `sync` - I/O should be done synchronously.
*   `async` - I/O دخل/خرج ينبغي أن يتم بشكل غير متزامن .
*   `dev` - Interpret block special devices on the filesystem.
*   `nodev` - Don't interpret block special devices on the filesystem.
*   `suid` - Allow the operation of suid, and sgid bits. They are mostly used to allow users on a computer system to execute binary executables with temporarily elevated privileges in order to perform a specific task.
*   `nosuid` - Block the operation of suid, and sgid bits.
*   `noatime` - Don't update inode access times on the filesystem. Can help performance (see [atime options](#atime_options)).
*   `nodiratime` - Do not update directory inode access times on the filesystem. Can help performance (see [atime options](#.D8.AE.D9.8A.D8.A7.D8.B1.D8.A7.D8.AA_atime)).
*   `relatime` - Update inode access times relative to modify or change time. Access time is only updated if the previous access time was earlier than the current modify or change time. (Similar to noatime, but doesn't break mutt or other applications that need to know if a file has been read since the last time it was modified.) Can help performance (see [atime options](/index.php/Fstab#atime_options "Fstab")).
*   `flush` - The `vfat` option to flush data more often, thus making copy dialogs or progress bars to stay up until all data is written.
*   `defaults` - the default mount options for the filesystem to be used. The default options for `ext4` are: `rw`, `suid`, `dev`, `exec`, `auto`, `nouser`, `async`.

*   **<dump>** - تستخدم من قِبَل used لتقرير أين ستوضع النسخة الاحتياطية . يقوم Dump بفحص امدخلة ويستخدم الرقم المحدد إذا كان يجب عمل نسخة احتياطية لنظام الملفات. المدخلات المتاحة هي و . إذا كن الرقم هو 0 سيتجاهل Dump نظام الملفات ، وإذا كان الرقم 1 سيقوم Dump بعمل نسخة احتياطية. أغلب المستخدمين لا يكون عندهم Dump مثبتا لذا عليهم أن يضعوا الرقم 0 للمدخلة <dump>.

*   **<pass>** - تستخدم من قِبَل اﻷمر [fsck](/index.php/Fsck "Fsck") لتحديد أي نظام ملفات سيتم فحصه. المدخلات المتاحة هي 0 و 1 و 2 ،. نظام الملفات الجذر يجب أن يحمل اﻷسبقية اﻷعلى بالرقم 1 ، وكل نظم الملفات اﻷخرى التي تريد فحصها يجب أن تحمل الرقم 2 . نظم الملفات المحددة بالرقم 0 لن يتم فحصها بالأداة fsck.

## تعريف نظم الملفات

يوجد ثلاث طرق لتعريف اﻷقسام أو أقراص التخزين في ملف `/etc/fstab`: : من خلال تسمية النواة ، والعنوان label أو المعرف UUID. ميزة استخدام المعرفات UUIDs أو العناوين labels تكمن في أنها لا تعتمد على ما هي اﻷقراص الموصلة فيزيائيا بالجهاز. وذلك مفيد في حالة ما تم تغيير وضعية أقراص التخزين من داخل نظام بيوس ، أو تم تبديل كوابل التوصيل الخاصة بأقراص التخزين. على الرغم من أن بيوس ربما يقوم من آن ﻵخر بتغيير وضعية أقراص التخزين. اقرأ المزيد عن ذلك الأمر في المقال التالي [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming").

لعرض قائمة بالمعلومات اﻷساسية عن الأقسام نفذ اﻷمر:

 `$ lsblk -f` 
```
NAME   FSTYPE LABEL      UUID                                 MOUNTPOINT
sda                                                           
├─sda1 ext4   Arch_Linux 978e3e81-8048-4ae1-8a06-aa727458e8ff /
├─sda2 ntfs   Windows    6C1093E61093B594                     
└─sda3 ext4   Storage    f838b24e-3a66-4d02-86f4-a2e73e454336 /media/Storage
sdb                                                           
├─sdb1 ntfs   Games      9E68F00568EFD9D3                     
└─sdb2 ext4   Backup     14d50a6c-e083-42f2-b9c4-bc8bae38d274 /media/Backup
sdc                                                           
└─sdc1 vfat   Camera     47FA-4071                            /media/Camera
```

### تسمية النواة

نفذ اﻷمر `lsblk -f` لعرض قائمة أقسام القرص ، مع تصديرها بالبادئة `/dev`.

انظر [مثال](#.D9.85.D8.AB.D8.A7.D9.84_.D9.84.D9.84.D9.85.D9.84.D9.81).

### العنوان Label

**ملاحظة:** كل عنوان label لا بد أن يكون فريدا ، وذلك لتجنب اي تعارض ممكن .

لمزيد من المعلومات عن كيفية تسمة الأقسام أو الأقراص ا نظر [Persistent block device naming#by-label](/index.php/Persistent_block_device_naming#by-label "Persistent block device naming"). إعادة تسمية قسم الجذر يجب عمله من خلال إسطوانة توزيعة لينكس **حية** حيث إنه لابد من إلغاء توصيل بارتيشن الروت أولا.

نفذ اﻷمر `lsblk -f` لعرض قائمة أقسام القرص مع تصديرها بالبادئة `LABEL=` :

 `/etc/fstab` 
```
# <file system>        <dir>         <type>    <options>             <dump> <pass> 
LABEL=Arch_Linux       /             ext4      defaults,noatime      0      1
LABEL=Arch_Swap        none          swap      defaults              0      0
```

### معرف UUID

All partitions and devices have a unique UUID. They are generated by filesystem utilities (e.g. `mkfs.*`) when you create or format a partition.

Run `lsblk -f` to list the partitions, and prefix them with `UUID=` :

**Tip:** If you would like to return just the UUID of a specific partition:
```
$ lsblk -no UUID /dev/sda2

```

 `/etc/fstab` 
```
# <file system>                            <dir>     <type>    <options>             <dump> <pass>
UUID=24f28fc6-717e-4bcd-a5f7-32b959024e26  /         ext4      defaults,noatime      0      1
UUID=03ec5dd3-45c0-4f95-a363-61ff321a09ff  /home     ext4      defaults,noatime      0      2
UUID=4209c845-f495-4c43-8a03-5363dd433153  none      swap      defaults              0      0
```

## تلميحات و حيل

### معرف قسم التبديل Swap UUID

In case your swap partition doesn't have an UUID, you can add it manually. This happens when the UUID of the swap is not shown with the `lsblk -f` command. Here are some steps to assign a UUID to your swap:

Identify the swap partition:

```
# swapon -s

```

Disable the swap:

```
# swapoff /dev/sda7

```

Recreate the swap with a new UUID assigned to it:

```
# mkswap -U random /dev/sda7

```

Activate the swap:

```
# swapon /dev/sda7

```

### Filepath spaces

If any mountpoint contains spaces, use the escape character `\` followed by the 3 digit octal code `040` to emulate them:

 `/etc/fstab` 
```
UUID=47FA-4071     /home/username/Camera<font color="grey">\040</font>Pictures   vfat  defaults,noatime       0  0
/dev/sda7          /media/100<font color="grey">\040</font>GB<font color="grey">\040</font>(Storage)       ext4  defaults,noatime,user  0  2
```

### اﻷقراص الخارجية

External devices that are to be mounted when present but ignored if absent may require the `nofail` option. This prevents errors being reported at boot.

 `/etc/fstab`  `/dev/sdg1        /media/backup    jfs    defaults,nofail    0  2` 

### خيارات atime

The use of `noatime`, `nodiratime` or `relatime` can improve drive performance. Linux by default uses `atime`, which keeps a record (writes to the drive) every time it reads anything. This is more purposeful when Linux is used for servers; it doesn't have much value for desktop use. The worst thing about the default `atime` option is that even reading a file from the page cache (reading from memory instead of the drive) will still result in a write! Using the `noatime` option fully disables writing file access times to the drive every time you read a file. This works well for almost all applications, except for a rare few like [Mutt](/index.php/Mutt "Mutt") that need the such information. For mutt, you should only use the `relatime` option. Using the `relatime` option enables the writing of file access times only when the file is being modified (unlike `noatime` where the file access time will never be changed and will be older than the modification time). The `nodiratime` option disables the writing of file access times only for directories while other files still get access times written. The best compromise might be the use of `relatime` in which case programs like [Mutt](/index.php/Mutt "Mutt") will continue to work, but you'll still have a performance boost because files will not get access times updated unless they are modified.

**Note:** `noatime` already includes `nodiratime`. You do not need to specify both.[[1]](http://lwn.net/Articles/244941/)

### نظام ملفات tmpfs

[tmpfs](https://en.wikipedia.org/wiki/Tmpfs "wikipedia:Tmpfs") is a temporary filesystem that resides in memory and/or your swap partition(s), depending on how much you fill it up. Mounting directories as tmpfs can be an effective way of speeding up accesses to their files, or to ensure that their contents are automatically cleared upon reboot.

Some directories where tmpfs is commonly used are [/tmp](http://www.pathname.com/fhs/2.2/fhs-3.15.html), [/var/lock](http://www.pathname.com/fhs/2.2/fhs-5.9.html) and [/var/run](http://www.pathname.com/fhs/2.2/fhs-5.13.html). Do NOT use it on [/var/tmp](http://www.pathname.com/fhs/2.2/fhs-5.15.html), because that folder is meant for temporary files that are preserved across reboots. Arch uses a tmpfs `/run` directory, with `/var/run` and `/var/lock` simply existing as symlinks for compatibility. It is also used for `/tmp` in the default `/etc/fstab`.

**Note:** When using [systemd](/index.php/Systemd "Systemd"), temporary files in tmpfs directories can be recreated at boot by using [tmpfiles.d](/index.php/Systemd#Temporary_files "Systemd").

By default, a tmpfs partition has its maximum size set to half your total RAM, but this can be customized. Note that the actual memory/swap consumption depends on how much you fill it up, as tmpfs partitions do not consume any memory until it is actually needed.

To use tmpfs for `/tmp`, add this line to `/etc/fstab`:

 `/etc/fstab`  `tmpfs   /tmp         tmpfs   nodev,nosuid                  0  0` 

You may or may not want to specify the size here, but you should leave the `mode` option alone in these cases to ensure that they have the correct permissions (1777). In the example above, `/tmp` will be set to use up to half of your total RAM. To explicitly set a maximum size, use the `size` mount option:

 `/etc/fstab`  `tmpfs   /tmp         tmpfs   nodev,nosuid,size=2G          0  0` 

Here is a more advanced example showing how to add tmpfs mounts for users. This is useful for websites, mysql tmp files, `~/.vim/`, and more. It's important to try and get the ideal mount options for what you are trying to accomplish. The goal is to have as secure settings as possible to prevent abuse. Limiting the size, and specifying uid and gid + mode is very secure. For more information on this subject, follow the links listed in the [#See also](#See_also) section.

 `/etc/fstab`  `tmpfs   /www/cache    tmpfs  rw,size=1G,nr_inodes=5k,noexec,nodev,nosuid,uid=648,gid=648,mode=1700   0  0` 

See the `mount` command man page for more information. One useful mount option in the man page is the `default` option. At least understand that.

Reboot for the changes to take effect. Note that although it may be tempting to simply run `mount -a` to make the changes effective immediately, this will make any files currently residing in these directories inaccessible (this is especially problematic for running programs with lockfiles, for example). However, if all of them are empty, it should be safe to run `mount -a` instead of rebooting (or mount them individually).

After applying changes, you may want to verify that they took effect by looking at `/proc/mounts` and using `findmnt`:

 `$ findmnt --target /tmp` 
```
TARGET SOURCE FSTYPE OPTIONS
/tmp   tmpfs  tmpfs  rw,nosuid,nodev,relatime
```

#### طرق الاستخدام

Generally, I/O intensive tasks and programs that run frequent read/write operations can benefit from using a tmpfs folder. Some applications can even receive a substantial gain by offloading some (or all) of their data onto the shared memory. For example, [relocating the Firefox profile into RAM](/index.php/Firefox_Ramdisk "Firefox Ramdisk") shows a significant improvement in performance.

##### Improving compile times

**Note:** The tmpfs folder (`/tmp`, in this case) needs to be mounted without `noexec`, else it will prevent build scripts or utilities from being executed. Also, as stated [above](#tmpfs), the default size is half of the available RAM so you may run out of space.

You can run [makepkg](/index.php/Makepkg "Makepkg") with a tmpfs folder for the build directory (which is also a setting in `/etc/makepkg.conf`):

```
$ BUILDDIR=/tmp/makepkg makepkg

```

### الكتابة على قسم FAT32 كمستخدم عادي

To write on a FAT32 partition, you must make a few changes to your `/etc/fstab` file.

 `/etc/fstab`  `/dev/sdxY    /mnt/some_folder  vfat   user,rw,umask=000              0  0` 

The `user` flag means that any user (even non-root) can mount and unmount the partition `/dev/sdX`. `rw` gives read-write access; `umask` option removes selected rights - for example `umask=111` remove executable rights. The problem is that this entry removes executable rights from directories too, so we must correct it by `dmask=000`. See also [Umask](/index.php/Umask "Umask").

Without these options, all files will be executable. You can use the option `showexec` instead of the umask and dmask options, which shows all Windows executables (com, exe, bat) in executable colours.

For example, if your FAT32 partition is on `/dev/sda9`, and you wish to mount it to `/mnt/fat32`, then you would use:

 `/etc/fstab`  `/dev/sda9    /mnt/fat32        vfat   user,rw,umask=111,dmask=000    0  0` 

### إعادة وصل قسم نظام ملفات الجذر

لسبب ما وفي حالة ما تم توصيل قسم الجذر بوضعية القراءة فقط ، قم بإعادة التوصيل بوضعية read-write من خلال تنفيذ اﻷمر التالي:

```
# mount -o remount,rw /

```

## انظر أيضا

*   [Full device listing including block device](http://www.kernel.org/pub/linux/docs/lanana/device-list/devices-2.6.txt)
*   [Filesystem Hierarchy Standard](http://www.pathname.com/fhs/2.2/index.html)
*   [30x Faster Web-Site Speed](http://www.askapache.com/web-hosting/super-speed-secrets.html) (Detailed tmpfs)