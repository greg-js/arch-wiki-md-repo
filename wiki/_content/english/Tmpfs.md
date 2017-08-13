[tmpfs](https://en.wikipedia.org/wiki/Tmpfs "wikipedia:Tmpfs") is a temporary filesystem that resides in memory and/or your swap partition(s), depending on how much you fill it up. Mounting directories as tmpfs can be an effective way of speeding up accesses to their files, or to ensure that their contents are automatically cleared upon reboot.

**Note:** When using [systemd](/index.php/Systemd "Systemd"), temporary files in tmpfs directories can be recreated at boot by using [tmpfiles.d](/index.php/Systemd#Temporary_files "Systemd").

## Contents

*   [1 Usage](#Usage)
*   [2 Examples](#Examples)
*   [3 Disable automatic mount](#Disable_automatic_mount)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Opening symlinks in tmpfs as root fails](#Opening_symlinks_in_tmpfs_as_root_fails)
*   [5 See also](#See_also)

## Usage

Some directories where tmpfs is commonly used are [/tmp](http://www.pathname.com/fhs/2.2/fhs-3.15.html), [/var/lock](http://www.pathname.com/fhs/2.2/fhs-5.9.html) and [/var/run](http://www.pathname.com/fhs/2.2/fhs-5.13.html). Do **not** use it on [/var/tmp](http://www.pathname.com/fhs/2.2/fhs-5.15.html), because that folder is meant for temporary files that are preserved across reboots.

Arch uses a tmpfs `/run` directory, with `/var/run` and `/var/lock` simply existing as symlinks for compatibility. It is also used for `/tmp` by the default systemd setup and does not require an entry in [fstab](/index.php/Fstab "Fstab") unless a specific configuration is needed.

[glibc](https://www.archlinux.org/packages/?name=glibc) 2.2 and above expects tmpfs to be mounted at `/dev/shm` for [POSIX shared memory](https://en.wikipedia.org/wiki/Shared_memory#Support_on_Unix-like_systems "wikipedia:Shared memory"). Mounting tmpfs at `/dev/shm` is handled automatically by [systemd](/index.php/Systemd "Systemd"), so manual configuration in [fstab](/index.php/Fstab "Fstab") is no longer necessary.

Generally, I/O intensive tasks and programs that run frequent read/write operations can benefit from using a tmpfs folder. Some applications can even receive a substantial gain by offloading some (or all) of their data onto the shared memory. For example, [relocating the Firefox profile into RAM](/index.php/Firefox_on_RAM "Firefox on RAM") shows a significant improvement in performance.

## Examples

By default, a tmpfs partition has its maximum size set to half your total RAM, but this can be customized. Note that the actual memory/swap consumption depends on how much you fill it up, as tmpfs partitions do not consume any memory until it is actually needed.

To explicitly set a maximum size, in this example to override the default `/tmp` mount, use the `size` mount option:

 `/etc/fstab`  `tmpfs   /tmp         tmpfs   rw,nodev,nosuid,size=2G          0  0` 

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

The tmpfs can also be temporarily resized without the need to reboot, for example when a large compile job needs to run soon. In this case, you can run:

```
# mount -o remount,size=4G,noatime /tmp

```

## Disable automatic mount

Under [systemd](/index.php/Systemd "Systemd"), `/tmp` may be automatically mounted as a tmpfs even though you have no entry for that in your `/etc/fstab`.

To disable the automatic mount, run:

```
# systemctl mask tmp.mount

```

Files will no longer be stored in a tmpfs, but your block device instead. The `/tmp` contents will now be preserved between reboots, which you might not want. To regain the previous behavior and clean the `/tmp` folder automatically when restarting your machine, consider using `tmpfiles.d(5)`:

 `/etc/tmpfiles.d/tmp.conf` 
```
# see tmpfiles.d(5)
# always enable /tmp folder cleaning
D! /tmp 1777 root root 0

# remove files in /var/tmp older than 10 days
D /var/tmp 1777 root root 10d

# namespace mountpoints (PrivateTmp=yes) are excluded from removal
x /tmp/systemd-private-*
x /var/tmp/systemd-private-*
X /tmp/systemd-private-*/tmp
X /var/tmp/systemd-private-*/tmp
```

## Troubleshooting

### Opening symlinks in tmpfs as root fails

Considering `/tmp` is using tmpfs, change the current directory to `/tmp`, then create a file and create a symlink to that file in the same `/tmp` directory. If you try to open the file you created via the symlink, you will get a permission denied error. This is expected as `/tmp` [has the sticky bit set](https://wiki.ubuntu.com/Security/Features#Symlink_restrictions).

This behaviour can be controlled via `/proc/sys/fs/protected_symlinks` or simply via sysctl: `sysctl -w fs.protected_symlinks=0`. See [Sysctl#Configuration](/index.php/Sysctl#Configuration "Sysctl") to make this permanent.

**Warning:** Changing this behaviour can lead to security issues! Disable it only if you know what you are doing.

## See also

*   [Linux kernel documentation](https://www.kernel.org/doc/Documentation/filesystems/tmpfs.txt)