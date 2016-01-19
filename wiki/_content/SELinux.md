# SELinux

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Security](/index.php/Security "Security")
*   [AppArmor](/index.php/AppArmor "AppArmor")

Security-Enhanced Linux (SELinux) is a Linux feature that provides a variety of security policies, including U.S. Department of Defense style mandatory access controls (MAC), through the use of Linux Security Modules (LSM) in the Linux kernel. It is not a Linux distribution, but rather a set of modifications that can be applied to Unix-like operating systems, such as Linux and BSD.

Running SELinux under a Linux distribution requires three things: An SELinux enabled kernel, SELinux Userspace tools and libraries, and SELinux Policies (mostly based on the Reference Policy). Some common Linux programs will also need to be patched/compiled with SELinux features.

## Contents

*   [1 Current status in Arch Linux](#Current_status_in_Arch_Linux)
*   [2 Concepts: Mandatory Access Controls](#Concepts:_Mandatory_Access_Controls)
*   [3 Installing SELinux](#Installing_SELinux)
    *   [3.1 Package description](#Package_description)
        *   [3.1.1 SELinux aware system utilities](#SELinux_aware_system_utilities)
        *   [3.1.2 SELinux userspace utilities](#SELinux_userspace_utilities)
        *   [3.1.3 SELinux policy packages](#SELinux_policy_packages)
        *   [3.1.4 Other SELinux tools](#Other_SELinux_tools)
    *   [3.2 Installation](#Installation)
        *   [3.2.1 Via Unofficial Repository](#Via_Unofficial_Repository)
        *   [3.2.2 Via AUR](#Via_AUR)
    *   [3.3 Changing boot loader configuration](#Changing_boot_loader_configuration)
        *   [3.3.1 GRUB](#GRUB)
        *   [3.3.2 Syslinux](#Syslinux)
        *   [3.3.3 Gummiboot](#Gummiboot)
    *   [3.4 Checking PAM](#Checking_PAM)
    *   [3.5 Installing a policy](#Installing_a_policy)
*   [4 Post-installation steps](#Post-installation_steps)
    *   [4.1 Swapfiles](#Swapfiles)
*   [5 Working with SELinux](#Working_with_SELinux)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Useful tools](#Useful_tools)
    *   [6.2 Reporting issues](#Reporting_issues)
*   [7 See also](#See_also)

## Current status in Arch Linux

Current status of those elements in Arch Linux:

<table class="wikitable">

<tbody>

<tr>

<th>Name</th>

<th>Status</th>

<th>Available at</th>

</tr>

<tr>

<td>SELinux enabled kernel</td>

<td>Implemented</td>

<td>Removed since the 3.14 official Arch kernel: The main complaint was the lack of Kconfig option to disable audit by default. Available in the AUR.</td>

</tr>

<tr>

<td>SELinux Userspace tools and libraries</td>

<td>Work in progress: [https://aur.archlinux.org/packages/?O=0&K=selinux](https://aur.archlinux.org/packages/?O=0&K=selinux)</td>

<td>Work is done at [https://github.com/archlinuxhardened/selinux](https://github.com/archlinuxhardened/selinux)</td>

</tr>

<tr>

<td>SELinux Policy</td>

<td>Work in progress, will probably be named selinux-policy-arch</td>

<td>No working repository for now.</td>

</tr>

</tbody>

</table>

Summary of changes in AUR as compared to official core packages:

<table class="wikitable">

<tbody>

<tr>

<th>Name</th>

<th>Status and comments</th>

</tr>

<tr>

<td>linux</td>

<td>Need a rebuild with some KConfig options enabled</td>

</tr>

<tr>

<td>coreutils</td>

<td>Need a rebuild to link with libselinux</td>

</tr>

<tr>

<td>cronie</td>

<td>Need a rebuild with `--with-selinux` flag</td>

</tr>

<tr>

<td>findutils</td>

<td>Need SELinux patch, already upstream</td>

</tr>

<tr>

<td>openssh</td>

<td>Need a rebuild with `--with-selinux` flag</td>

</tr>

<tr>

<td>pam</td>

<td>Need a rebuild with `--enable-selinux` flag for Linux-PAM ; Need a patch for pam_unix2, which only removes a function already implemented in a library elsewhere</td>

</tr>

<tr>

<td>pambase</td>

<td>Configuration changes to add pam_selinux.so</td>

</tr>

<tr>

<td>psmisc</td>

<td>Need a patch, already upstream. Will be in version 22.21</td>

</tr>

<tr>

<td>shadow</td>

<td>Need a rebuild with `-lselinux` and `--with-selinux` flags</td>

</tr>

<tr>

<td>sudo</td>

<td>Need a rebuild with `--enable-selinux` flag</td>

</tr>

<tr>

<td>systemd</td>

<td>Need a rebuild with `--enable-selinux` flag</td>

</tr>

<tr>

<td>util-linux</td>

<td>Need a rebuild with `--enable-selinux` flag</td>

</tr>

</tbody>

</table>

All of the other SELinux-related packages may be included without changes nor risks.

## Concepts: Mandatory Access Controls

**Note:** This section is meant for beginners. If you know what SELinux does and how it works, feel free to skip ahead to the installation.

Before you enable SELinux, it is worth understanding what it does. Simply and succinctly, SELinux enforces _Mandatory Access Controls (MACs)_ on Linux. In contrast to SELinux, the traditional user/group/rwx permissions are a form of _Discretionary Access Control (DAC)_. MACs are different from DACs because security policy and its execution are completely separated.

An example would be the use of the _sudo_ command. When DACs are enforced, sudo allows temporary privilege escalation to root, giving the process so spawned unrestricted systemwide access. However, when using MACs, if the security administrator deems the process to have access only to a certain set of files, then no matter what the kind of privilege escalation used, unless the security policy itself is changed, the process will remain constrained to simply that set of files. So if _sudo_ is tried on a machine with SELinux running in order for a process to gain access to files its policy does not allow, it will fail.

Another set of examples are the traditional (-rwxr-xr-x) type permissions given to files. When under DAC, these are user-modifiable. However, under MAC, a security administrator can choose to freeze the permissions of a certain file by which it would become impossible for any user to change these permissions until the policy regarding that file is changed.

As you may imagine, this is particularly useful for processes which have the potential to be compromised, i.e. web servers and the like. If DACs are used, then there is a particularly good chance of havoc being wreaked by a compromised program which has access to privilege escalation.

For further information, do visit the [MAC Wikipedia page](https://en.wikipedia.org/wiki/Mandatory_access_control).

## Installing SELinux

### Package description

All SELinux related packages belong to the _selinux_ group in the AUR as well as in [Siosm's unofficial repository](/index.php/Unofficial_user_repositories#siosm-selinux "Unofficial user repositories").

#### SELinux aware system utilities

[coreutils-selinux](https://aur.archlinux.org/packages/coreutils-selinux/)<sup><small>AUR</small></sup>

Modified coreutils package compiled with SELinux support enabled. It replaces the [coreutils](https://www.archlinux.org/packages/?name=coreutils) package

[selinux-flex](https://aur.archlinux.org/packages/selinux-flex/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-flex)]</sup>

Flex version needed only to build checkpolicy. The normal flex package causes a failure in the checkmodule command. It replaces the [flex](https://www.archlinux.org/packages/?name=flex) package.

[pam-selinux](https://aur.archlinux.org/packages/pam-selinux/)<sup><small>AUR</small></sup> and [pambase-selinux](https://aur.archlinux.org/packages/pambase-selinux/)<sup><small>AUR</small></sup>

PAM package with pam_selinux.so. and the underlying base package. They replace the [pam](https://www.archlinux.org/packages/?name=pam) and [pambase](https://www.archlinux.org/packages/?name=pambase) packages respectively.

[systemd-selinux](https://aur.archlinux.org/packages/systemd-selinux/)<sup><small>AUR</small></sup>

An SELinux aware version of Systemd. It replaces the [systemd](https://www.archlinux.org/packages/?name=systemd) package.

[util-linux-selinux](https://aur.archlinux.org/packages/util-linux-selinux/)<sup><small>AUR</small></sup>

Modified util-linux package compiled with SELinux support enabled. It replaces the [util-linux](https://www.archlinux.org/packages/?name=util-linux) package.

[findutils-selinux](https://aur.archlinux.org/packages/findutils-selinux/)<sup><small>AUR</small></sup>

Patched findutils package compiled with SELinux support to make searching of files with specified security context possible. It replaces the [findutils](https://www.archlinux.org/packages/?name=findutils) package.

[sudo-selinux](https://aur.archlinux.org/packages/sudo-selinux/)<sup><small>AUR</small></sup>

Modified [sudo](/index.php/Sudo "Sudo") package compiled with SELinux support which sets the security context correctly. It replaces the [sudo](https://www.archlinux.org/packages/?name=sudo) package.

[psmisc-selinux](https://aur.archlinux.org/packages/psmisc-selinux/)<sup><small>AUR</small></sup>

Psmisc package compiled with SELinux support; for example, it adds the `-Z` option to `killall`. It replaces the [psmisc](https://www.archlinux.org/packages/?name=psmisc) package.

[shadow-selinux](https://aur.archlinux.org/packages/shadow-selinux/)<sup><small>AUR</small></sup>

Shadow package compiled with SELinux support; contains a modified `/etc/pam.d/login` file to set correct security context for user after login. It replaces the [shadow](https://www.archlinux.org/packages/?name=shadow) package.

[cronie-selinux](https://aur.archlinux.org/packages/cronie-selinux/)<sup><small>AUR</small></sup>

Fedora fork of Vixie cron with SELinux enabled. It replaces the [cronie](https://www.archlinux.org/packages/?name=cronie) package.

[logrotate-selinux](https://aur.archlinux.org/packages/logrotate-selinux/)<sup><small>AUR</small></sup>

Logrotate package compiled with SELinux support. It replaces the [logrotate](https://www.archlinux.org/packages/?name=logrotate) package.

[openssh-selinux](https://aur.archlinux.org/packages/openssh-selinux/)<sup><small>AUR</small></sup>

OpenSSH package compiled with SELinux support to set security context for user sessions. It replaces the [openssh](https://www.archlinux.org/packages/?name=openssh) package.

#### SELinux userspace utilities

[checkpolicy](https://aur.archlinux.org/packages/checkpolicy/)<sup><small>AUR</small></sup>

Tools to build SELinux policy

[libselinux](https://aur.archlinux.org/packages/libselinux/)<sup><small>AUR</small></sup>

Library for security-aware applications. Python bindings needed for _semanage_ and _setools_ now included.

[libsemanage](https://aur.archlinux.org/packages/libsemanage/)<sup><small>AUR</small></sup>

Library for policy management. Python bindings needed for _semanage_ and _setools_ now included.

[libsepol](https://aur.archlinux.org/packages/libsepol/)<sup><small>AUR</small></sup>

Library for binary policy manipulation.

[policycoreutils](https://aur.archlinux.org/packages/policycoreutils/)<sup><small>AUR</small></sup>

SELinux core utils such as newrole, setfiles, etc.

[sepolgen](https://aur.archlinux.org/packages/sepolgen/)<sup><small>AUR</small></sup>

A Python library for parsing and modifying policy source.

#### SELinux policy packages

[selinux-refpolicy](https://aur.archlinux.org/packages/selinux-refpolicy/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-refpolicy)]</sup>

Precompiled modular-otherways-vanilla Reference policy with headers and documentation but without sources.

[selinux-refpolicy-src](https://aur.archlinux.org/packages/selinux-refpolicy-src/)<sup><small>AUR</small></sup>

Reference policy sources

[selinux-refpolicy-arch](https://aur.archlinux.org/packages/selinux-refpolicy-arch/)<sup><small>AUR</small></sup>

Precompiled modular Reference policy with headers and documentation but without sources. Development Arch Linux Refpolicy patch included, but for now [February 2011] it only fixes some issues with `/etc/rc.d/*` labeling.

**Note:** The _selinux-refpolicy-arch_ package was last updated in 2011, hence it seems doubtful that it is useful any longer.

#### Other SELinux tools

[setools](https://aur.archlinux.org/packages/setools/)<sup><small>AUR</small></sup>

CLI and GUI tools to manage SELinux

### Installation

Only ext2, ext3, ext4, JFS, XFS and BtrFS filesystems are supported to use SELinux. Since the 3.13 kernel update, the options required for SELinux to work on any system are enabled in the default kernel configuration, hence there should be no problems by default. If you are using a custom kernel, please do make sure that Xattr (Extended Attributes), `CONFIG_AUDIT` and `CONFIG_SECURITY_SELINUX` are enabled in your config. (Source: [Debian Wiki](http://wiki.debian.org/SELinux/Setup#kernel))

**Note:** If using proprietary drivers, such as [NVIDIA](/index.php/NVIDIA "NVIDIA") graphics drivers, you may need to [rebuild them](/index.php/NVIDIA#Alternate_install:_custom_kernel "NVIDIA") for custom kernels.

There are two methods to install the requisite SELinux packages.

#### Via Unofficial Repository

Add the [siosm-selinux](/index.php/Unofficial_user_repositories#siosm-selinux "Unofficial user repositories") repository into `pacman.conf` and [add](/index.php/Pacman-key#Adding_unofficial_keys "Pacman-key") Siosm's key.

Then install the following packages by either using the `su -` command or by logging in as root:

*   _pambase-selinux_
*   _pam-selinux_
*   _coreutils-selinux_
*   _libsemanage_
*   _shadow-selinux_
*   _libcgroup_
*   _policycoreutils_
*   _cronie-selinux_
*   _findutils-selinux_
*   _selinux-flex_
*   _selinux-logrotate_
*   _openssh-selinux_
*   _psmisc-selinux_
*   _python2-ipy_
*   _setools_
*   _systemd-selinux_

**Warning:** Do not use the _sudo_ command to install these packages. This is because [pam](https://www.archlinux.org/packages/?name=pam), which is used for _sudo_ authentication, is being replaced.

#### Via AUR

The first install needs to be of [pambase-selinux](https://aur.archlinux.org/packages/pambase-selinux/)<sup><small>AUR</small></sup> and [pam-selinux](https://aur.archlinux.org/packages/pam-selinux/)<sup><small>AUR</small></sup>.

Next, you need to build and install [coreutils-selinux](https://aur.archlinux.org/packages/coreutils-selinux/)<sup><small>AUR</small></sup>, [libsemanage](https://aur.archlinux.org/packages/libsemanage/)<sup><small>AUR</small></sup>, [shadow-selinux](https://aur.archlinux.org/packages/shadow-selinux/)<sup><small>AUR</small></sup>, [libcgroup](https://aur.archlinux.org/packages/libcgroup/)<sup><small>AUR</small></sup>, [policycoreutils](https://aur.archlinux.org/packages/policycoreutils/)<sup><small>AUR</small></sup>, [cronie-selinux](https://aur.archlinux.org/packages/cronie-selinux/)<sup><small>AUR</small></sup>, [findutils-selinux](https://aur.archlinux.org/packages/findutils-selinux/)<sup><small>AUR</small></sup>, [selinux-flex](https://aur.archlinux.org/packages/selinux-flex/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/selinux-flex)]</sup>, [logrotate-selinux](https://aur.archlinux.org/packages/logrotate-selinux/)<sup><small>AUR</small></sup>, [openssh-selinux](https://aur.archlinux.org/packages/openssh-selinux/)<sup><small>AUR</small></sup> and [psmisc-selinux](https://aur.archlinux.org/packages/psmisc-selinux/)<sup><small>AUR</small></sup> from the AUR and [python2-ipy](https://www.archlinux.org/packages/?name=python2-ipy) from the _community_ repository.

Now comes the [setools](https://aur.archlinux.org/packages/setools/)<sup><small>AUR</small></sup> package. For this, do make sure that you have the [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) package installed, in order for the `JAVA_HOME` variable to be set properly. If it still is not even after installing the package, run:

```
$ export JAVA_HOME=/usr/lib/jvm/java-7-openjdk

```

Next, backup your `/etc/sudoers` file. Install [sudo-selinux](https://aur.archlinux.org/packages/sudo-selinux/)<sup><small>AUR</small></sup>, [dbus-selinux](https://aur.archlinux.org/packages/dbus-selinux/)<sup><small>AUR</small></sup> and [checkpolicy](https://aur.archlinux.org/packages/checkpolicy/)<sup><small>AUR</small></sup>. Finally, install [util-linux-selinux](https://aur.archlinux.org/packages/util-linux-selinux/)<sup><small>AUR</small></sup> and [systemd-selinux](https://aur.archlinux.org/packages/systemd-selinux/)<sup><small>AUR</small></sup>. Because of cyclic makedepends between these two packages which will not be fixed ([FS#39767](https://bugs.archlinux.org/task/39767)), you need to build the source package [systemd-selinux](https://aur.archlinux.org/packages/systemd-selinux/)<sup><small>AUR</small></sup>, install [libsystemd-selinux](https://aur.archlinux.org/packages/libsystemd-selinux/)<sup><small>AUR</small></sup>, build and install [util-linux-selinux](https://aur.archlinux.org/packages/util-linux-selinux/)<sup><small>AUR</small></sup> (with [libutil-linux-selinux](https://aur.archlinux.org/packages/libutil-linux-selinux/)<sup><small>AUR</small></sup>) and rebuild and install the source package [systemd-selinux](https://aur.archlinux.org/packages/systemd-selinux/)<sup><small>AUR</small></sup>.

### Changing boot loader configuration

If you have installed a new kernel, make sure that you update your bootloader accordingly to boot on it. Moreover you may need to add "security=selinux selinux=1" to the kernel command line. More precisely, if the kernel configuration does not set CONFIG_DEFAULT_SECURITY_SELINUX, "security=selinux" is needed, and if it contains CONFIG_SECURITY_SELINUX_BOOTPARAM=y CONFIG_SECURITY_SELINUX_BOOTPARAM_VALUE=0, "selinux=1" is needed.

#### GRUB

Add "security=selinux selinux=1" GRUB_CMDLINE_LINUX_DEFAULT variable in /etc/default/grub Run the following command:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

#### Syslinux

Change your syslinux.cfg file by adding:

 `/boot/syslinux/syslinux.cfg` 

```
LABEL arch-selinux
         LINUX ../vmlinuz-linux-selinux
         APPEND root=/dev/sda2 ro selinux selinux=1
         INITRD ../initramfs-linux-selinux.img
```

at the end. Change "linux-selinux" to whatever kernel you are using.

#### Gummiboot

Create a new loader entry, for example in /boot/loader/entries/arch-selinux.conf:

 `/boot/loader/entries/arch-selinux.conf` 

```
title Arch Linux SELinux
linux /vmlinuz-linux-selinux
initrd /initramfs-linux-selinux.img
options root=/dev/sda2 ro selinux=1 security=selinux
```

### Checking PAM

A correctly set-up PAM is important to get the proper security context after login. Check for the presence of the following lines in `/etc/pam.d/system-login`:

```
# pam_selinux.so close should be the first session rule
session         required        pam_selinux.so close
```

```
# pam_selinux.so open should only be followed by sessions to be executed in the user context
session         required        pam_selinux.so open
```

### Installing a policy

**Warning:** The reference policy as given by [Tresys](http://oss.tresys.com/projects/refpolicy) is not very good for Arch Linux, as almost no file is labelled correctly. However, as of writing, Archers have no other choice. If anyone has made any significant strides in addressing this problem, they are encouraged to share it, preferably on the [AUR](/index.php/AUR "AUR"). The major problems are:

*   `/lib` and `/usr/lib` are considered different (and also `/bin`, `/sbin`, `/usr/bin` and `/usr/sbin`). This introduces some instability when applying labels to the whole system, as files in these folders may be seen with 2 (or 4) different labels.
*   systemd is not yet supported (C. PeBenito, main developer of the refpolicy, announced its willingness to work on it in its github repository in October 2014, [http://oss.tresys.com/pipermail/refpolicy/2014-October/007430.html](http://oss.tresys.com/pipermail/refpolicy/2014-October/007430.html))

Policies are the mainstay of SELinux. They are what govern its behaviour. The only policy currently available in the AUR is the Reference Policy. In order to install it, you should use the source files, which may be got from the package [selinux-refpolicy-src](https://aur.archlinux.org/packages/selinux-refpolicy-src/)<sup><small>AUR</small></sup> or by downloading the latest release on [https://github.com/TresysTechnology/refpolicy/wiki/DownloadRelease#current-release](https://github.com/TresysTechnology/refpolicy/wiki/DownloadRelease#current-release). When using the AUR package, navigate to `/etc/selinux/refpolicy/src/policy` and run the following commands:

```
# make bare
# make conf
# make install
```

to install the reference policy as it is. Those who know how to write SELinux policies can tweak them to their heart's content before running the commands written above. The command takes a while to do its job and taxes one core of your system completely, so do not worry. Just sit back and let the command run for as long as it takes.

To load the reference policy run:

 `# make load` 

Then, make the file `/etc/selinux/config` with the following contents (Only works if you used the defaults as mentioned above. If you decided to change the name of the policy, you need to tweak the file):

 `/etc/selinux/config` 

```
# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#       enforcing - SELinux security policy is enforced.
#                   Set this value once you know for sure that SELinux is configured the way you like it and that your system is ready for deployment
#       permissive - SELinux prints warnings instead of enforcing.
#                    Use this to customise your SELinux policies and booleans prior to deployment. Recommended during policy development.
#       disabled - No SELinux policy is loaded.
#                  This is not a recommended setting, for it may cause problems with file labelling
SELINUX=permissive
# SELINUXTYPE= takes the name of SELinux policy to
# be used. Current options are:
#       refpolicy (vanilla reference policy)
#       <custompolicy> - Substitute <custompolicy> with the name of any custom policy you choose to load
SELINUXTYPE=refpolicy
```

Now, you may reboot. After rebooting, run:

```
# restorecon -r /

```

to label your filesystem.

Now, make a file `requiredmod.te` with the contents:

 `requiredmod.te` 

```
module requiredmod 1.0;

require {
        type devpts_t;
        type kernel_t;
        type device_t;
        type var_run_t;
        type udev_t;
        type hugetlbfs_t;
        type udev_tbl_t;
        type tmpfs_t;
        class sock_file write;
        class unix_stream_socket { read write ioctl };
        class capability2 block_suspend;
        class dir { write add_name };
        class filesystem associate;
}

#============= devpts_t ==============
allow devpts_t device_t:filesystem associate;

#============= hugetlbfs_t ==============
allow hugetlbfs_t device_t:filesystem associate;

#============= kernel_t ==============
allow kernel_t self:capability2 block_suspend;

#============= tmpfs_t ==============
allow tmpfs_t device_t:filesystem associate;

#============= udev_t ==============
allow udev_t kernel_t:unix_stream_socket { read write ioctl };
allow udev_t udev_tbl_t:dir { write add_name };
allow udev_t var_run_t:sock_file write;
```

and run the following commands:

```
# checkmodule -m -o requiredmod.mod requiredmod.te
# semodule_package -o requiredmod.pp -m requiredmod.mod
# semodule -i requiredmod.pp
```

This is required to remove a few messages from `/var/log/audit/audit.log` which are a nuisance to deal with in the reference policy. This is an ugly hack and it should be made very clear that the policy so installed simply patches the reference policy in order to hide the effects of incorrect labelling.

## Post-installation steps

You can check that SELinux is working with `sestatus`. You should get something like:

```
SELinux status:                 enabled
SELinuxfs mount:                /sys/fs/selinux
SELinux root directory:         /etc/selinux
Loaded policy name:             refpolicy
Current mode:                   permissive
Mode from config file:          permissive
Policy MLS status:              disabled
Policy deny_unknown status:     allowed
Max kernel policy version:      28
```

To maintain correct context, you can use _restorecond_:

```
# systemctl enable restorecond

```

To switch to enforcing mode without rebooting, you can use:

```
# echo 1 > /sys/fs/selinux/enforce

```

### Swapfiles

If you have a swap file instead of a swap partition, issue the following commands in order to set the appropriate security context:

```
# semanage fcontext -a -t swapfile_t "/path/to/swapfile"
# restorecon /path/to/swapfile
```

## Working with SELinux

SELinux defines security using a different mechanism than traditional Unix access controls. The best way to understand it is by example. For example, the SELinux security context of the apache homepage looks like the following:

```
$ls -lZ /var/www/html/index.html
-rw-r--r--  username username system_u:object_r:httpd_sys_content_t /var/www/html/index.html

```

The first three and the last columns should be familiar to any (Arch) Linux user. The fourth column is new and has the format:

```
user:role:type[:level]

```

To explain:

1.  **User:** The SELinux user identity. This can be associated to one or more roles that the SELinux user is allowed to use.
2.  **Role:** The SELinux role. This can be associated to one or more types the SELinux user is allowed to access.
3.  **Type:** When a type is associated with a process, it defines what processes (or domains) the SELinux user (the subject) can access. When a type is associated with an object, it defines what access permissions the SELinux user has to that object.
4.  **Level:** This optional field can also be know as a range and is only present if the policy supports MCS or MLS.

This is important in case you wish to understand how to build your own policies, for these are the basic building blocks of SELinux. However, for most purposes, there is no need to, for the reference policy is sufficiently mature. However, if you are a power user or someone with very specific needs, then it might be ideal for you to learn how to make your own SELinux policies.

[This](http://www.fosteringlinux.com/tag/selinux/) is a great series of articles for someone seeking to understand how to work with SELinux.

## Troubleshooting

The place to look for SELinux errors is the systemd journal. In order to see SELinux messages related to the label `system_u:system_r:policykit_t:s0` (for example), you would need to run:

```
# journalctl _SELINUX_CONTEXT=system_u:system_r:policykit_t:s0

```

### Useful tools

There are some tools/commands that can greatly help with SELinux.

restorecon

Restores the context of a file/directory (or recursively with `-R`) based on any policy rules

chcon

Change the context on a specific file

### Reporting issues

Please report issues on GitHub: [https://github.com/archlinuxhardened/selinux/issues](https://github.com/archlinuxhardened/selinux/issues)

## See also

*   [Security Enhanced Linux](http://en.wikipedia.org/wiki/Security-Enhanced_Linux)
*   [Gentoo SELinux Handbook](http://www.gentoo.org/proj/en/hardened/selinux/selinux-handbook.xml)
*   [Fedora Project's SELinux Wiki](http://fedoraproject.org/wiki/SELinux)
*   [NSA's Official SELinux Homepage](http://www.nsa.gov/research/selinux/index.shtml)
*   [Reference Policy Homepage](http://oss.tresys.com/projects/refpolicy)
*   [SELinux Userspace Homepage](http://userspace.selinuxproject.org/trac/)
*   [SETools Homepage](http://oss.tresys.com/projects/setools)
*   [ArchLinux, SELinux and You (archived)](https://web.archive.org/web/20140816115906/http://jamesthebard.net/archlinux-selinux-and-you-a-trip-down-the-rabbit-hole/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=SELinux&oldid=415682](https://wiki.archlinux.org/index.php?title=SELinux&oldid=415682)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Security](/index.php/Category:Security "Category:Security")
*   [Kernel](/index.php/Category:Kernel "Category:Kernel")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")