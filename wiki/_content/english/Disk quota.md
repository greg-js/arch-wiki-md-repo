From [Wikipedia](https://en.wikipedia.org/wiki/Disk_quota "wikipedia:Disk quota"):

	"*A **disk quota** is a limit set by a system administrator that restricts certain aspects of file system usage on modern operating systems. The function of setting quotas to disks is to allocate limited disk-space in a reasonable way.*"

This article covers the installation and setup of disk quota.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Setup the filesystem](#Setup_the_filesystem)
    *   [2.2 Create quota index](#Create_quota_index)
*   [3 Usage](#Usage)
    *   [3.1 Enable quota for user/group](#Enable_quota_for_user/group)
    *   [3.2 Specify a grace period](#Specify_a_grace_period)
    *   [3.3 Reports](#Reports)
    *   [3.4 Copy quota settings](#Copy_quota_settings)
        *   [3.4.1 To one or several users](#To_one_or_several_users)
        *   [3.4.2 To groups](#To_groups)
        *   [3.4.3 To all users](#To_all_users)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Quota warnings](#Quota_warnings)
    *   [4.2 Stats](#Stats)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [quota-tools](https://www.archlinux.org/packages/?name=quota-tools) package.

## Configuration

### Setup the filesystem

Edit [fstab](/index.php/Fstab "Fstab") to enable the quota mount option(s) on selected file systems, e.g.:

 `/etc/fstab`  `/dev/sda3 /home ext4 defaults**,usrquota** 0 2` 

To additionally enable the group quota mount option:

 `/etc/fstab`  `/dev/sda3 /home ext4 defaults**,usrquota,grpquota** 0 2` 

If supported by the [kernel](/index.php/Kernel "Kernel") and [file system](/index.php/File_systems#Journaling "File systems") it is recommended to use journaled quota instead:

 `/etc/fstab`  `/dev/sda3 /home ext4 defaults**,usrjquota=aquota.user,jqfmt=vfsv1** 0 2` 

Append `grpjquota=aquota.group` to enable group quota.

Remount the partition to apply the change:

```
 # mount -vo remount /home

```

### Create quota index

To create the quota index for `/home`:

```
 # quotacheck -cum /home

```

Append the `-g` parameter to also create a group index.

To enable disk quotas for the desired file system:

```
# quotaon -v /home

```

To disable disk quotas for the file system:

```
# quotaoff -v /home

```

## Usage

### Enable quota for user/group

**Tip:**

*   To find out how many 1 kilobyte blocks are there for a partition use `$ df`.
*   You may use a online bytes converter to calculate the correct amount of blocks [[1]](http://whatsabyte.com/P1/byteconverter.htm).
*   The command `# setquota` may be used as an alternative of `# edquota` [[2]](https://gehrcke.de/2013/05/setting-up-quotas-on-a-local-linux-file-system/).

**Note:** Block size is statically set to 1k regardless of filesystem block size [[3]](http://stackoverflow.com/questions/2506288/detect-block-size-for-quota-in-linux/2506311#2506311).

Quotas are configured using `# edquota` that will be opened in the default configured text editor:

 `# edquota *user*` 
```
Disk quotas for user *user* (uid 1000):
  Filesystem                   blocks       soft       hard     inodes     soft     hard
  /dev/sda3                        24          0          0          6        0        0

```

	blocks

	Indicates number of 1k blocks currently used by the user/group.

	soft

	Indicates max number of blocks for the user/group before a warning is issued and grace period countdown begins. If set to "0" (zero) then no limit is enforced.

	hard

	Indicates max number of blocks for the user/group can use. If maximum amount has been reached, no further disk space can be used. If set to "0" (zero) then no limit is enforced.

	inodes

	Indicates the current inodes amount used by the user/group.

	soft

	Indicates the soft inode limit for the user/group.

	hard

	Indicates the hard inode limit for the user/group.

Consider the following configuration for *ftpuser1*:

 `# edquota *ftpuser1*` 
```
Disk quotas for user ftpuser1 (uid *1000*):
  Filesystem                   blocks       soft       hard     inodes     soft     hard
  /dev/sda3                        24    1000000    1048576          6        0        0

```

In this case if *ftpuser1* uses over 976MB of space a warning will be issued. If the hard limit of 1GB has been reached the user will be unable to write any more data.

See [#Specify a grace period](#Specify_a_grace_period) to give users a specific amount of time to reduce storage usage when they hit their soft limit.

**Warning:** The `hard` limit applies to all files written by and for the respective user/group, including temporary files by started applications, which may crash at this point.

### Specify a grace period

To give current users some time to reduce their file usage, a grace period can be configured. This specifies the allowed time a user/group can exceed their soft limit and while under their hard limit:

 `# edquota -t` 
```
Grace period before enforcing soft limits for users:
Time units may be: days, hours, minutes, or seconds
  Filesystem             Block grace period     Inode grace period
  /dev/sda3              7days                  7days

```

The grace period can be set in seconds, minutes, hours, days, weeks or months.

### Reports

Shows all configured quotas:

```
# repquota -a

```

Shows quotas on a specific partition:

```
# repquota */home*

```

Show quotas that apply to a [user](/index.php/User "User")/[user group](/index.php/User_group "User group"):

```
# quota -u *user*

```

```
# quota -g *group*

```

### Copy quota settings

#### To one or several users

To copy quota settings from `*user1*` to `*user2*`:

```
# edquota -p *user1* *user2*

```

To copy quota settings to several other users, append `*user3*` `*user4*` ...

#### To groups

To copy quota settings from `*group1*` to `*group2*`:

```
# edquota -g -p *group1* *group2*

```

#### To all users

The idea is to modify the quota settings for one user and copy the setting to all other users. Set the quota for `*user1*` and apply the quota to users with a UID greater than 999:

```
# edquota -p *user1* $(awk -F: '$3 > 999 {print $1}' /etc/passwd)

```

## Tips and tricks

### Quota warnings

The command `warnquota` can be used to warn the users about their quota. Configuration is available in `/etc/warnquota.conf`.

### Stats

The command `quotastats` can be used to give more information about the current quota usage:

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
*   [https://www.digitalocean.com/community/tutorials/how-to-enable-user-and-group-quotas](https://www.digitalocean.com/community/tutorials/how-to-enable-user-and-group-quotas)