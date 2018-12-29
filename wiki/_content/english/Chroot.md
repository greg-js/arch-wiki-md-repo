Related articles

*   [PRoot](/index.php/PRoot "PRoot")
*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")
*   [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")

A [chroot](https://en.wikipedia.org/wiki/Chroot "wikipedia:Chroot") is an operation that changes the apparent root directory for the current running process and their children. A program that is run in such a modified environment cannot access files and commands outside that environmental directory tree. This modified environment is called a *chroot jail*.

## Contents

*   [1 Reasoning](#Reasoning)
*   [2 Requirements](#Requirements)
*   [3 Usage](#Usage)
    *   [3.1 Using arch-chroot](#Using_arch-chroot)
        *   [3.1.1 Enter a chroot](#Enter_a_chroot)
        *   [3.1.2 Run a single command and exit](#Run_a_single_command_and_exit)
    *   [3.2 Using chroot](#Using_chroot)
*   [4 Run graphical applications from chroot](#Run_graphical_applications_from_chroot)
*   [5 Without root privileges](#Without_root_privileges)
    *   [5.1 PRoot](#PRoot)
    *   [5.2 Fakechroot](#Fakechroot)
*   [6 See also](#See_also)

## Reasoning

Changing root is commonly done for performing system maintenance on systems where booting and/or logging in is no longer possible. Common examples are:

*   Reinstalling the [bootloader](/index.php/Bootloader "Bootloader").
*   Rebuilding the [initramfs image](/index.php/Mkinitcpio "Mkinitcpio").
*   Upgrading or [downgrading packages](/index.php/Downgrading_packages "Downgrading packages").
*   Resetting a [forgotten password](/index.php/Password_recovery "Password recovery").
*   Building packages in a clean chroot, see [DeveloperWiki:Building in a clean chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot").

See also [Wikipedia:Chroot#Limitations](https://en.wikipedia.org/wiki/Chroot#Limitations "wikipedia:Chroot").

## Requirements

*   Root privilege.
*   Another Linux environment, e.g. a LiveCD or USB flash media, or from another existing Linux distribution.
*   Matching architecture environments; i.e. the chroot from and chroot to. The architecture of the current environment can be discovered with: `uname -m` (e.g. i686 or x86_64).
*   Kernel modules loaded that are needed in the chroot environment.
*   Swap enabled if needed: `# swapon /dev/sd*xY*` 
*   Internet connection established if needed.

## Usage

**Note:**

*   Some [systemd](/index.php/Systemd "Systemd") tools such as *localectl* and *timedatectl* can not be used inside a chroot, as they require an active [dbus](/index.php/Dbus "Dbus") connection. [[1]](https://github.com/systemd/systemd/issues/798#issuecomment-126568596)
*   The file system that will serve as the new root (`/`) of your chroot must be accessible (i.e., decrypted, mounted).

There are two main options for using chroot, described below.

### Using arch-chroot

The bash script `arch-chroot` is part of the [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) package. Before it runs `/usr/bin/chroot`, the script mounts api filesystems like `/proc` and makes `/etc/resolv.conf` available from the chroot.

#### Enter a chroot

Run arch-chroot with the new root directory as first argument:

```
# arch-chroot */location/of/new/root*

```

For example, in the [installation guide](/index.php/Installation_guide "Installation guide") this directory would be `/mnt`:

```
# arch-chroot /mnt

```

To exit the chroot simply use:

```
# exit

```

#### Run a single command and exit

To run a command from the chroot, and exit again append the command to the end of the line:

```
# arch-chroot */location/of/new/root* *mycommand*

```

For example, to run `mkinitcpio -p linux` for a chroot located at `/mnt/arch` do:

```
# arch-chroot /mnt/arch mkinitcpio -p linux

```

### Using chroot

**Warning:** When using `--rbind`, some subdirectories of `dev/` and `sys/` will not be unmountable. Attempting to unmount with `umount -l` in this situation will break your session, requiring a reboot. If possible, use `-o bind` instead.

In the following example `*/location/of/new/root*` is the directory where the new root resides.

First, mount the temporary API filesystems:

```
# cd */location/of/new/root*
# mount -t proc /proc proc/
# mount --rbind /sys sys/
# mount --rbind /dev dev/

```

And optionally:

```
# mount --rbind /run run/

```

Next, in order to use an internet connection in the chroot environment copy over the DNS details:

```
# cp /etc/resolv.conf etc/resolv.conf

```

Finally, to change root into `*/location/of/new/root*` using a bash shell:

```
# chroot */location/of/new/root* /bin/bash

```

**Note:** If you see the error:

*   `chroot: cannot run command '/usr/bin/bash': Exec format error`, it is likely that the architectures of the host environment and chroot environment do not match.
*   `chroot: '/usr/bin/bash': permission denied`, remount with the exec permission: `mount -o remount,exec */location/of/new/root*`.

After chrooting it may be necessary to load the local bash configuration:

```
# source /etc/profile
# source ~/.bashrc

```

**Tip:** Optionally, create a unique prompt to be able to differentiate your chroot environment: `# export PS1="(chroot) $PS1"` 

When finished with the chroot, you can exit it via:

```
# exit

```

Then unmount the temporary file systems:

```
# cd /
# umount --recursive */location/of/new/root*

```

**Note:** If there is an error mentioning something like: `umount: /path: device is busy` this usually means that either: a program (even a shell) was left running in the chroot or that a sub-mount still exists. Quit the program and use `findmnt -R */location/of/new/root*` to find and then `umount` sub-mounts. It may be tricky to `umount` some things and one can hopefully have `umount --force` work, as a last resort use `umount --lazy` which just releases them. In either case to be safe, `reboot` as soon as possible if these are unresolved to avoid possible future conflicts.

## Run graphical applications from chroot

If you have an [X server](/index.php/X_server "X server") running on your system, you can start graphical applications from the chroot environment.

To allow the chroot environment to connect to an X server, open a virtual terminal inside the X server (i.e. inside the desktop of the user that is currently logged in), then run the [xhost](/index.php/Xhost "Xhost") command, which gives permission to anyone to connect to the user's X server:

```
$ xhost +local:

```

Then, to direct the applications to the X server from chroot, set the DISPLAY environment variable inside the chroot to match the DISPLAY variable of the user that owns the X server. So for example, run

```
$ echo $DISPLAY

```

as the user that owns the X server to see the value of DISPLAY. If the value is ":0" (for example), then in the chroot environment run

```
# export DISPLAY=:0

```

## Without root privileges

Chroot requires root privileges, which may not be desirable or possible for the user to obtain in certain situations. There are, however, various ways to simulate chroot-like behavior using alternative implementations.

### PRoot

[PRoot](/index.php/PRoot "PRoot") may be used to change the apparent root directory and use `mount --bind` without root privileges. This is useful for confining applications to a single directory or running programs built for a different CPU architecture, but it has limitations due to the fact that all files are owned by the user on the host system. PRoot provides a `--root-id` argument that can be used as a workaround for some of these limitations in a similar (albeit more limited) manner to *fakeroot*.

### Fakechroot

[fakechroot](https://www.archlinux.org/packages/?name=fakechroot) is a library shim which intercepts the chroot call and fakes the results. It can be used in conjunction with [fakeroot](https://www.archlinux.org/packages/?name=fakeroot) to simulate a chroot as a regular user.

```
# fakechroot fakeroot chroot ~/my-chroot bash

```

## See also

*   [Basic Chroot](https://help.ubuntu.com/community/BasicChroot)