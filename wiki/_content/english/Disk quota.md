From [Wikipedia](https://en.wikipedia.org/wiki/Disk_quota "wikipedia:Disk quota"):

	"*A **disk quota** is a limit set by a system administrator that restricts certain aspects of file system usage on modern operating systems. The function of setting quotas to disks is to allocate limited disk-space in a reasonable way.*"

This article covers the installation and setup of disk quota.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Journaled quota](#Journaled_quota)
*   [3 Configuration](#Configuration)
    *   [3.1 Example configuration](#Example_configuration)
*   [4 Managing](#Managing)
    *   [4.1 Basics](#Basics)
    *   [4.2 Copying quota settings](#Copying_quota_settings)
        *   [4.2.1 To one or several users](#To_one_or_several_users)
        *   [4.2.2 To all users](#To_all_users)
    *   [4.3 Other commands](#Other_commands)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [quota-tools](https://www.archlinux.org/packages/?name=quota-tools) package.

## Usage

First, edit `/etc/fstab` to enable the quota mount option(s) on selected file systems. For example, edit an entry

```
/dev/sda1 /home ext4 defaults 1 1

```

as follows:

```
/dev/sda1 /home ext4 defaults**,usrquota** 1 1

```

or, to additionally enable the group quota mount option:

```
/dev/sda1 /home ext4 defaults**,usrquota,grpquota** 1 1

```

Note: these quota options are possibly obsolete. See [#Journaled quota](#Journaled_quota).

After adding the options remount

```
 # mount -vo remount /home

```

and create the quota index:

```
 # quotacheck -vgum /home

```

If you added quota options for more partitions, you may also use `quotacheck -vguma` as root.

**Tip:**

If the command returns with

*   `[...]Quotafile $FILE was probably truncated. Cannot save quota settings...`, you can try removing the previously created files `aquota*`.
*   `quotacheck: Mountpoint (or device) /home not found or has no quota enabled. quotacheck: Cannot find filesystem to check or filesystem not mounted with quota option.` and you are using a custom kernel, make sure quota support is enabled in your kernel.

If it continues to throw an error, you can additionally try to use options `"-F vfsold` or `-F vfsv0` afterwards. Note that as of kernel 3.1.6-1, Arch does not support `vfsv1` anymore.

If trying to remount the filesystem returns with

*   `mount: /home not mounted already, or bad option` you might have enabled quotas already, run `quotaoff /home` as root and the remount again.

Finally, enable quotas:

```
# quotaon -av

```

After this configuration the systemd units `quotaon.service` and `systemd-quotacheck.service` will perform the disk quota check without further configuration at least each boot.[[1]](https://bugs.archlinux.org/task/31391) Both are started automatically, if `/etc/fstab` quota mount options are parsed.

### Journaled quota

Enabling journaling for disk quota adds the same benefits journalled file systems do for forced shutdowns, meaning that data is less likely to become corrupt.

Setting up journaled quota is the same as above, except for the mount options:

```
/dev/sda1 /home ext4 defaults**,usrjquota=aquota.user,jqfmt=vfsv1** 1 1

```

or additionally, enable the group quota mount option;

```
/dev/sda1 /home ext4 defaults**,usrjquota=aquota.user,grpjquota=aquota.group,jqfmt=vfsv1** 1 1

```

The vfsv1 format is necessary for supporting quotas more than 4TB. You need at least kernel 2.6.33 for quota_v2 support. If your kernel is older, you have to use vfsv0.

## Configuration

**Tip:** To find out how many 1K blocks are there for a partition use `df`

Replace `$USER` as appropriate:

 `# edquota *$USER*` 
```
Disk quotas for user **$USER** (uid 1000):
  Filesystem                   blocks       soft       hard     inodes     soft     hard
  /dev/sda1                      1944          0          0        120        0        0

```

**Note:** to edit group quotas, use `edquota -g $GROUP`.

	blocks

	Number of 1k blocks currently used by `$USER`.

**Note:** Block size is statically set to 1k regardless of filesystem block size. [Explanation](http://stackoverflow.com/questions/2506288/detect-block-size-for-quota-in-linux/2506311#2506311)

	inodes

	Number of entries by `$USER` in directory file.

	soft

	Max number of blocks/inodes `$USER` may have on partition before warning is issued and grace period countdown begins. If set to "0" (zero) then no limit is enforced.

	hard

	Max number of blocks/inodes `$USER` may have on partition. If set to "0" (zero) then no limit is enforced.

Configure the `soft` limit grace period:

```
# edquota -t

```

### Example configuration

Consider the following configuration for *user1*:

 `# edquota *user1*` 
```
Disk quotas for user *user1* (uid *1000*):
Filesystem      blocks      soft      hard      inodes      soft      hard
*/dev/sda1*       695879      10000     15000     6741        0         0

```

The `soft` limit means that once *user1* uses over 10MB of space a warning gets issues, and after the time set by `edquota -t` the soft limit gets enforced.

The `hard` limit is stricter, so to speak; a user can never write more data once this limit is reached.

**Warning:** The `hard` limit applies to all files written by and for the respective user/group, including temporary files by started applications, which may crash at this point.

**Tip:** If a problem is encountered with the defined quotas, you should first try to correct them with `edquota *user1*` from a root console. Alternatively, `quotaoff -a` as root disables all quotas at runtime and the `quotacheck.mode=skip` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") can be used at boot to temporarily disable the `systemd-quotacheck.service`.

## Managing

Check for quota limits and advanced operations.

### Basics

Use this command to check for quotas on a specific partition:

```
# repquota /home

```

Use this command to check for all quotas that apply to a user:

```
# quota -u $USER

```

for groups;

```
# quota -g $GROUP

```

### Copying quota settings

#### To one or several users

To copy quota settings from `*user1*` to `*user2*`, use this:

```
# edquota -p *user1* *user2*

```

To copy quota settings to several other users, append `*user3*`, `*user4*`, and so on, to the command.

Use `edquota -g -p *group1* *group2* ...` to copy settings for groups.

#### To all users

The idea is to modify the quota settings for one user and copy the setting to all other users. Set the quota for `*user1*` and apply the quota to users with a UID greater than 999.

```
# edquota -p *user1* $(awk -F: '$3 > 999 {print $1}' /etc/passwd)

```

### Other commands

There are several useful commands:

*   `repquota -a` shows the status on disk usage
*   `warnquota` can be used to warn the users about their quota, configuration in `/etc/warnquota.conf`
*   `setquota` is a non-interactive quota setting - useful for scripting.

Lasty, `quotastats` is used to give thorough information about the quota system:

 `$ quotastats` 
```
Number of dquot lookups: 101289
Number of dquot drops: 101271
Number of still active inodes with quota : 18
Number of dquot reads: 93
Number of dquot writes: 2077
Number of quotafile syncs: 134518740
Number of dquot cache hits: 7391
Number of allocated dquots: 90
Number of free dquots: 2036
Number of in use dquot entries (user/group): -1946

```

## See also

*   [http://tldp.org/HOWTO/Quota.html](http://tldp.org/HOWTO/Quota.html)
*   [http://www.sf.net/projects/linuxquota/](http://www.sf.net/projects/linuxquota/)
*   [http://www.yolinux.com/TUTORIALS/LinuxTutorialQuotas.html](http://www.yolinux.com/TUTORIALS/LinuxTutorialQuotas.html)
*   [RHEL7: Disk Quotas](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/ch-disk-quotas.html)