From [Wikipedia](https://en.wikipedia.org/wiki/Disk_quota "wikipedia:Disk quota"):

	"*A **disk quota** is a limit set by a system administrator that restricts certain aspects of file system usage on modern operating systems. The function of setting quotas to disks is to allocate limited disk-space in a reasonable way.*"

This article covers the installation and setup of disk quota.

## Contents

*   [1 Installing](#Installing)
*   [2 Enabling](#Enabling)
    *   [2.1 Journaled quota](#Journaled_quota)
*   [3 Configuring](#Configuring)
    *   [3.1 Example configuration](#Example_configuration)
*   [4 Managing](#Managing)
    *   [4.1 Basics](#Basics)
    *   [4.2 Copying quota settings](#Copying_quota_settings)
        *   [4.2.1 To one or several users](#To_one_or_several_users)
        *   [4.2.2 To all users](#To_all_users)
    *   [4.3 Other commands](#Other_commands)
*   [5 More resources](#More_resources)

## Installing

Disk quota only requires one package:

```
# pacman -S quota-tools

```

## Enabling

*For journaled quota, see the notes in [#Journaled quota](#Journaled_quota).*

1\. First, edit `/etc/fstab` to enable the quota mount option(s) on selected file systems:

```
 /dev/sda1 /home ext4 defaults 1 1

```

	edit it as follows;

```
 /dev/sda1 /home ext4 defaults**,usrquota** 1 1

```

	or aditionally enable the group quota mount option;

```
 /dev/sda1 /home ext4 defaults**,usrquota,grpquota** 1 1

```

2\. The next step is to remount:

```
 # mount -vo remount /home

```

3\. Create the quota index:

```
 # quotacheck -vgum /home

```

	or for all partitions with the quota mount options in `/etc/mtab`;

```
 # quotacheck -vguma

```

**Tip:** If you end up with the output "[...]Quotafile $FILE was probably truncated. Cannot save quota settings..." you can try removing the previously created files aquota*

**Tip:** If you get the output "quotacheck: Mountpoint (or device) /home not found or has no quota enabled.
quotacheck: Cannot find filesystem to check or filesystem not mounted with quota option." and you are using a custom kernel, make sure quota support is enabled in your kernel.

**Tip:** In Addition you can try to use "-F vfsold" and "-F vfsv0" afterwards **NOTE:** As of 3.1.6-1, Arch does not support "vfsv1"

4\. Finally, enable quotas:

```
 # quotaon -av

```

Consider adding this command to your start-up, see [Autostarting](/index.php/Autostarting "Autostarting").

### Journaled quota

Enabling journaling for disk quota adds the same benefits journaled file systems do for forced shutdowns, meaning that data is less likely to become corrupt.

Setting up journaled quota is the same as above, except for the mount options:

```
/dev/sda1 /home ext4 defaults**,usrjquota=aquota.user,jqfmt=vfsv0** 1 1

```

or additionally, enable the group quota mount option;

```
/dev/sda1 /home ext4 defaults**,usrjquota=aquota.user,grpjquota=aquota.group,jqfmt=vfsv0** 1 1

```

## Configuring

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

## Managing

*Checking for quota limits and advanced operations*

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
# edquota -p *user1* `awk -F: '$3 > 999 {print $1}' /etc/passwd`

```

### Other commands

There are several useful commands:

```
repquota -a      # Shows the status on disk usage
warnquota        # Can be used to warn the users about their quota, configuration in /etc/warnquota.conf
setquota         # Non-interactive quota setting--useful for scripting

```

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

## More resources

*   [http://tldp.org/HOWTO/Quota.html](http://tldp.org/HOWTO/Quota.html)
*   [http://www.sf.net/projects/linuxquota/](http://www.sf.net/projects/linuxquota/)
*   [http://www.yolinux.com/TUTORIALS/LinuxTutorialQuotas.html](http://www.yolinux.com/TUTORIALS/LinuxTutorialQuotas.html)
*   [http://www.redhat.com/docs/manuals/linux/RHL-8.0-Manual/admin-primer/s1-storage-quotas.html](http://www.redhat.com/docs/manuals/linux/RHL-8.0-Manual/admin-primer/s1-storage-quotas.html)