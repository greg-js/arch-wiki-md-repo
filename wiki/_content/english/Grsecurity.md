[Grsecurity](https://grsecurity.net/) is an extensive security enhancement to the Linux kernel that defends against a wide range of security threats. The [PaX](/index.php/PaX "PaX") project is included, hardening both userspace applications and the kernel against memory corruption-based exploits. Grsecurity includes a powerful Mandatory Access Control system with an effortless automatic learning mode and a host of other miscellaneous hardening features.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Custom kernel](#Custom_kernel)
*   [2 Compatibility](#Compatibility)
*   [3 PaX](#PaX)
*   [4 Configuration](#Configuration)
*   [5 Trusted path execution](#Trusted_path_execution)
    *   [5.1 Using the tpe group as a whitelist or blacklist](#Using_the_tpe_group_as_a_whitelist_or_blacklist)
    *   [5.2 Compatibility](#Compatibility_2)
    *   [5.3 Partially restrict all non-root users](#Partially_restrict_all_non-root_users)
*   [6 chroot hardening](#chroot_hardening)
*   [7 Socket restrictions](#Socket_restrictions)
*   [8 Auditing](#Auditing)
*   [9 Hide information from /proc](#Hide_information_from_.2Fproc)
*   [10 RBAC](#RBAC)
    *   [10.1 Working with gradm](#Working_with_gradm)
    *   [10.2 Generating a policy](#Generating_a_policy)
    *   [10.3 Tweaking your policy](#Tweaking_your_policy)
    *   [10.4 Tweaking /etc/grsec/policy directly](#Tweaking_.2Fetc.2Fgrsec.2Fpolicy_directly)
    *   [10.5 Using Wine; Changes needed to /etc/grsec/policy](#Using_Wine.3B_Changes_needed_to_.2Fetc.2Fgrsec.2Fpolicy)
*   [11 Troubleshooting](#Troubleshooting)
    *   [11.1 Out-of-tree kernel module compilation failure](#Out-of-tree_kernel_module_compilation_failure)

## Installation

The [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec) package in the [official repositories](/index.php/Official_repositories "Official repositories") provides the grsecurity hardened kernel. In most cases, grsecurity is a drop-in replacement for the vanilla kernel and will not cause any issues. By default, many of the user-facing features are disabled, but there is significant hardening of the kernel itself against exploitation.

**Note:** The linux-grsec-lts package used to provide the 3.14 stable branch but it is [no longer available](https://grsecurity.net/announce.php).

After installing the [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec) package, you need to edit your [bootloader](/index.php/Bootloader "Bootloader") settings to load `vmlinuz-linux-grsec` and `initramfs-linux-grsec.img`.

Installing the optional [paxd](https://www.archlinux.org/packages/?name=paxd) package causes the PaX exploit mitigations to be enabled, protecting userspace processes. It automatically applies the necessary exceptions for packages in the repositories. See [PaX#PaX exceptions](/index.php/PaX#PaX_exceptions "PaX") for more details.

Also included are [checksec](https://www.archlinux.org/packages/?name=checksec), [pax-utils](https://www.archlinux.org/packages/?name=pax-utils) and [paxtest](https://www.archlinux.org/packages/?name=paxtest) packages providing useful tooling for working with PaX and verifying that the exploit mitigation techniques are active.

The optional [gradm](https://www.archlinux.org/packages/?name=gradm) package provides the userspace tooling for managing RBAC policies. RBAC is disabled by default, and the sample policy is not usable without significant configuration (likely via heavy use of the learning mode).

### Custom kernel

Compiling a custom kernel based on the official package with [ABS](/index.php/ABS "ABS") is worth considering. There are several important compromises to make between performance and security, so while the official configuration is solid it is not perfect for every use case. See [PaX#Performance](/index.php/PaX#Performance "PaX") for coverage of the PaX options with a significant performance impact. The official package prioritizes security over performance.

The /proc and /sys restrictions are unacceptable for a general purpose package due to breaking too much software, but can be worth enabling to plug potential information leaks.

Some features like the RANDSTRUCT plugin and hiding symbol addresses are only truly useful with a custom kernel, since the pre-built kernel is available for analysis by any attacker. The [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec) package enables `CONFIG_RANDOMIZE_BASE`, but a custom build can provide unique symbol offsets in addition to the randomized base, making `CONFIG_GRKERNSEC_HIDESYM` valuable.

[linux-libre-grsec](https://aur.archlinux.org/packages/linux-libre-grsec/) and [linux-zen-grsec](https://aur.archlinux.org/packages/linux-zen-grsec/) are also available.

## Compatibility

**Note:** An incompatibility between [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec) and another package should not be reported as a bug in that package. It should be filed against the [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec) package and will either be fixed or documented as a compatibility issue here.

The following incompatibilities require building a custom kernel with fewer features enabled:

*   hibernation is not supported (conflicts with `CONFIG_GRKERNSEC_KMEM`, `CONFIG_PAX_MEMORY_SANITIZE` and `CONFIG_RANDOMIZE_BASE`)
*   Xen and [virtualbox](https://www.archlinux.org/packages/?name=virtualbox) are not supported (conflicts with `CONFIG_PAX_KERNEXEC` and `CONFIG_PAX_MEMORY_UDEREF`)
*   `CONFIG_GRKERNSEC_KMEM` is incompatible with software altering the CPU MSR, such as power saving configuration tools like [cpupower](https://www.archlinux.org/packages/?name=cpupower), [powertop](https://www.archlinux.org/packages/?name=powertop) and [x86_energy_perf_policy](https://www.archlinux.org/packages/?name=x86_energy_perf_policy) (optionally used by [tlp](https://www.archlinux.org/packages/?name=tlp)). Rather than disabling the option, you could recompile the kernel with your desired defaults.

Known incompatibilities with other packages:

*   [pkgstats](https://www.archlinux.org/packages/?name=pkgstats) - tries to list the loaded modules as non-root and treats it as a fatal error when it fails
*   [broadcom-wl-dkms](https://aur.archlinux.org/packages/broadcom-wl-dkms/) - fails to be compiled with [linux-grsec-headers](https://www.archlinux.org/packages/?name=linux-grsec-headers) due to illegal memory access

Out-of-tree modules may require patches for compatibility with kernel hardening features like `CONFIG_PAX_SIZE_OVERFLOW`:

*   the [nvidia-grsec](https://aur.archlinux.org/packages/nvidia-grsec/) package in the [AUR](/index.php/AUR "AUR") patches the proprietary [NVIDIA](/index.php/NVIDIA "NVIDIA") driver for compatibility with the `CONFIG_PAX_USERCOPY` and `CONFIG_PAX_CONSTIFY_PLUGIN` features

## PaX

The [PaX](https://en.wikipedia.org/wiki/PaX "wikipedia:PaX") project provides many of the exploit mitigations offered by grsecurity. See [the documentation on PaX](/index.php/PaX "PaX") for more information.

## Configuration

The user-facing features are configurable at runtime via [sysctl](/index.php/Sysctl "Sysctl") settings. Sane defaults are set in the `/etc/sysctl.d/05-grsecurity.conf` configuration file and it can be modified as desired.

## Trusted path execution

Trusted path execution (TPE) is an opt-in feature restricting file execution. It can be enabled by setting the `kernel.grsecurity.tpe` [sysctl](/index.php/Sysctl "Sysctl") switch to `1`. TPE prevents users from executing any file writeable by a non-root user. By tightening up the rules for executing files, some exploits (such as upload + CGI exploits on a web server) and persistent backdoors will be prevented.

### Using the `tpe` group as a whitelist or blacklist

By default, `kernel.grsecurity.tpe_invert` is set to `1`, causing TPE to operate with a whitelist-based model. It will be applied to every user that is not a member of the `tpe` group. If `kernel.grsecurity.tpe_invert` is set to `0`, the `tpe` group will instead function as a blacklist of users with the restriction, with users not in the group unaffected.

The whitelist model is recommended, and adding non-system users to the whitelist is usually enough. It will slightly improve the isolation of services running as non-root while not getting in anyone's way.

### Compatibility

[Containers](/index.php/Linux_Containers "Linux Containers") or plain [chroots](/index.php/Chroot "Chroot") can throw a wrench into the ease of using TPE, as each one has a local `/etc/group`. A group with the same id in the container will still work as a whitelist, but this will be broken if the container makes use of user namespaces (not yet supported by Arch kernels).

### Partially restrict all non-root users

Setting the `kernel.grsecurity.tpe_restrict_all` [sysctl](/index.php/Sysctl "Sysctl") switch to `1` will prevent non-root users from executing files writeable by a user other than themselves or root. This feature is enabled by the default `/etc/sysctl.d/05-grsecurity.conf`.

## chroot hardening

A [chroot](/index.php/Chroot "Chroot") is a common isolation mechanism for services. Grsecurity includes features for eliminating many common escape routes from chroots and can lock them down to the point where the confinement is equivalent to a container. These features can all be toggled on and off via sysctl switches. For a detailed explanantion of these features, see the [configuration documentation](https://en.wikibooks.org/wiki/Grsecurity/Appendix/Grsecurity_and_PaX_Configuration_Options#Chroot_jail_restrictions).

The following features are enabled in `/etc/sysctl.d/05-grsecurity.conf` by default and are unlikely to cause any compatibility issues:

```
kernel.grsecurity.chroot_deny_fchdir = 1
kernel.grsecurity.chroot_deny_shmat = 1
kernel.grsecurity.chroot_deny_sysctl = 1
kernel.grsecurity.chroot_deny_unix = 1
kernel.grsecurity.chroot_enforce_chdir = 1
kernel.grsecurity.chroot_findtask = 1

```

The remaining features are left off by default, to remain compatible with containers:

```
#kernel.grsecurity.chroot_caps = 1
#kernel.grsecurity.chroot_deny_chmod = 1
#kernel.grsecurity.chroot_deny_chroot = 1
#kernel.grsecurity.chroot_deny_mknod = 1
#kernel.grsecurity.chroot_deny_mount = 1
#kernel.grsecurity.chroot_deny_pivot = 1
#kernel.grsecurity.chroot_restrict_nice = 1

```

## Socket restrictions

There are 3 groups for restricting access to sockets. Users in the `socket-deny-client` group are forbidden from connecting to other hosts. Users in the `socket-deny-server` group are unable to listen on a port. The `socket-deny-all` group includes both of the restrictions.

## Auditing

There are a few security-related logging features added to the kernel.

By default, only `kernel.grsecurity.rwxmap_logging` is enabled. It logs an error whenever an application has an `mprotect` or `mmap` system call rejected due to the PaX MPROTECT feature along with some other edge cases. In most cases, the application is intentionally doing dynamic machine code generation and just needs an exception. However, it may indicate a compiler / linker bug or a bug in application / library code and the errors will also be logged when an exploit attempt is prevented by the MPROTECT feature. See [PaX](/index.php/PaX "PaX") for more information about exceptions.

The remaining audit features are currently disabled by default due to the high number of false positives, but can be enabled via [sysctl](/index.php/Sysctl "Sysctl"). The `kernel.grsecurity.audit_group` switch can be set to `1` to limit `kernel.grsecurity.audit_chdir` and `kernel.grsecurity.exec_logging` to users in the `audit` group as they will generate a LOT of log messages.

## Hide information from /proc

The [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec) package does not enable the strict `/proc` restrictions (`CONFIG_GRKERNSEC_PROC`). Instead, the `hidepid=2` mount option can be set on `/proc` to hide processes of other users and the `gid` option can be used to make a group with an exception from the restrictions. The `hidepid` mount option is less invasive because it's local to each process namespace so it can be set per [container](/index.php/Systemd-nspawn "Systemd-nspawn"). However, it's missing the additional miscellaneous information hiding so compiling a custom kernel may be desired.

The [hidepid](https://www.archlinux.org/packages/?name=hidepid) package can be installed to set up the necessary `systemd-logind` exception and enable `hidepid=2`. It will also work with `CONFIG_GRKERNSEC_PROC` in a custom kernel configured to use the correct proc group gid.

## RBAC

Role Based Access Control

There are two basic types of access control mechanisms used to prevent unauthorized access to files (or information in general): DAC (Discretionary Access Control) and MAC (Mandatory Access Control). By default, Linux uses a DAC mechanism: the creator of the file can define who has access to the file. A MAC system however forces everyone to follow rules set by the administrator.

The MAC implementation grsecurity supports is called Role Based Access Control. RBAC associates roles with each user. Each role defines what operations can be performed on certain objects. Given a well-written collection of roles and operations your users will be restricted to perform only those tasks that you tell them they can do. The default "deny-all" ensures you that a user cannot perform an action you have not thought of.

### Working with gradm

[gradm](https://www.archlinux.org/packages/?name=gradm) is a tool which allows you to administer and maintain a policy for your system. With it, you can enable or disable the RBAC system, reload the RBAC roles, change your role, set a password for admin mode, etc.

When you install gradm a default policy will be installed in /etc/grsec/policy.

By default, the RBAC policies are not activated. It is the sysadmin's job to determine when the system should have an RBAC policy enforced. Before activating the RBAC system you should set an admin password.

```
# gradm -P admin
Setting up grsecurity RBAC password
Password: (Enter a well-chosen password)
Re-enter Password: (Enter the same password for confirmation)
Password written in /etc/grsec/pw
# gradm -E

```

To disable the RBAC system, run gradm -D. If you are not allowed to, you first need to switch to the admin role:

```
# gradm -a admin
Password: (Enter your admin role password)
# gradm -D

```

If you want to leave the admin role, run gradm -u admin:

```
# gradm -u admin

```

### Generating a policy

The RBAC system comes with a great feature called "learning mode". The learning mode can generate an anticipatory least privilege policy for your system. This allows for time and money savings by being able to rapidly deploy multiple secure servers.

To use the learning mode, activate it using gradm:

```
# gradm -F -L /etc/grsec/learning.log

```

Now use your system, do the things you would normally do. Try to avoid rsyncing, running locate or any other heavy file i/o operation as this can really slow down the processing time.

When you believe you have used your system sufficiently to obtain a good policy, let gradm process them and propose roles under `/etc/grsec/learning.roles`:

```
# gradm -D
# gradm -F -L /etc/grsec/learning.log -O /etc/grsec/learning.roles

```

Audit the `/etc/grsec/learning.roles` and save it as `/etc/grsec/policy` (mode `0600`) when you are finished.

```
# mv /etc/grsec/learning.roles /etc/grsec/policy
# chmod 0600 /etc/grsec/policy

```

You will now be able to enable the RBAC system with your new learned policy.

```
# gradm -E

```

**Tip:** If you receive the error **Viewing access is allowed by role <insert user> to /etc/grsec, the directory which stores RBAC policies and RBAC password information.**, add the following to your **subject /** under **# Role: <insert user>**:
```
/etc/grsec h

```

Example:

```
# Role: root
subject /  {
       /                               h
       /etc                            rx
       /etc/grsec                      h

```

The reasoning for this can be found [here](https://forums.grsecurity.net/viewtopic.php?f=5&t=1607)

### Tweaking your policy

An interesting feature of grsecurity 2.x is Set Operation Support for the configuration file. Currently it supports unions, intersections and differences of sets (of objects in this case).

```
define objset1 {
/root/blah rw
/root/blah2 r
/root/blah3 x
}

define somename2 {
/root/test1 rw
/root/blah2 rw
/root/test3 h
}

```

Here is an example of its use, and the resulting objects that will be added to your subject:

```
subject /somebinary o
$objset1 & $somename2

```

The above would expand to:

```
subject /somebinary o
/root/blah2 r

```

This is the result of the & operator which takes both sets and returns the files that exist in both sets and the permission for those files that exist in both sets.

```
subject /somebinary o
$objset1 | $somename2

```

This example would expand to:

```
subject /somebinary o
/root/blah rw
/root/blah2 rw
/root/blah3 x
/root/test1 rw
/root/test3 h

```

This is the result of the | operator which takes both sets and returns the files that exist in either set. If a file exists in both sets, it is returned as well and the mode contains the flags that exist in either set.

```
subject /somebinary o
$objset1 - $somename2

```

This example would expand to:

```
subject /somebinary o
/root/blah rw
/root/blah2 h
/root/blah3 x

```

This is the result of the - operator which takes both sets and returns the files that exist in the set on the left but not in the match of the file in set on the right. If a file exists on the left and a match is found on the right (either the filenames are the same, or a parent directory exists in the right set), the file is returned and the mode of the second set is removed from the first set, and that file is returned.

In some obscure pseudo-language you could see this as:

```
if ( ($objset1 contained /tmp/blah rw) and
     ($objset2 contained /tmp/blah r) )
then
  $objset1 - $objset2 would contain /tmp/blah w

if ( ($objset1 contained /tmp/blah rw) and
     ($objset2 contained / rwx) )
then 
  $objset1 - $objset2 would contain /tmp/blah h

```

As for order of precedence (from highest to lowest): "-, & |".

If you do not want to bother remembering precedence, parenthesis support is also included, so you can do things like:

```
(($set1 - $set2) | $set3) & $set4

```

### Tweaking /etc/grsec/policy directly

Sometimes, full learning mode doesnt work for a particular program and direct revisions to the policy file will need to be made. One might simply want to tweak the policy file to add or remove access to directories without requiring one to reinitiate learning mode or recreating a policy file. The file itself is composed of Roles and Subjects. A Role determines what user the ruleset applies to, while the Subject could be seen as what process/program the ruleset applies to.

Consider a situation where the role is "username", while the subject is /usr/lib/firefox/firefox. Within the curly braces of this role/subject rule, directories will be listed, along with flags that dictate what capacities (read, write, execute, etc) you wish to give that subject (firefox for example) under that role (username, when firefox is ran under the user "username" for example). Here is a list of flags and what they do:

```
  a 	This object can be opened for appending.
  c 	Allow creation of the file/directory.
  d 	Allow deletion of the file/directory.
  f 	Needed to mark the pipe used for communication with init to transfer the privilege of the 		persistent role; only valid within a persistent role. Transfer only occurs when the file is opened for writing.
  h 	This object is hidden.
  i 	This mode only applies to binaries. When the object is executed, it inherits the ACL of the     subject in which it was contained.
  l 	Lowercase L. Allow a hardlink at this path. Hardlinking requires a minimum of c and l modes, and the target link cannot have any greater permission than the source file.
  m 	Allow creation of setuid/setgid files/directories and modification of files/directories to be setuid/setgid.
  p 	Reject all ptraces to this object.
  r 	This object can be opened for reading.
  t 	This object can be ptraced, but cannot modify the running task. This is referred to as a 'read-only ptrace'.
  w 	This object can be opened for writing or appending.
  x 	This object can be executed (or mmap'd with PROT_EXEC into a task).

```

So for example, if you want firefox to have read access to the home folder of the user username, be able to do everything (read, write, create and destroy files, execute) in /home/username/Downloads, but not be able to see /home/username/secretstuff or anything in /, your ruleset might look like this:

```
  # Role: username
  subject /usr/lib/firefox/firefox o {
      /                                               h
      /home/username                       r
      /home/username/Downloads     rwxcd
      /home/username/secretstuff      h
  }

```

Of course, a Firefox ruleset will need more than just the above (like access to directories it needs to run in /usr for example); compare the above with what is generated by full-learning-mode and you quickly see the pattern. The idea is that you want to limit each process as much as possible to limit the changes it can make to the filesystem in the event it is compromised. Much more info is available on the [GRsecurity RBAC wiki page.](http://en.wikibooks.org/wiki/Grsecurity/The_RBAC_System)

### Using Wine; Changes needed to /etc/grsec/policy

In the event you use wine, your executables for wine apps are on an NTFS partition, and you want it to work while RBAC is enabled, you will need to append "O" to the Subject mode of /usr/bin/wine-preloader for the Role (user) using this subject. I am unsure if this applies to executables in .wine as I do not have the free space to test it. I put my system into full-learning mode and ran wine, and after generating a /etc/grsec/policy from this session RBAC still prevented my wine program from running with:

```
grsec: (username:U:/usr/bin/wine-preloader) denied load of writable library /mnt/winblows/Program Files (x86)/Diablo II/Game.exe by /usr/bin/wine-preloader[Game.exe:7518] uid...

```

Appending "O" to the end of the Subject mode will fix this problem. An example of a working ruleset (notice the capital O after subject /usr/bin/wine-preloader):

```
# Role: username
subject /usr/bin/wine-preloader O {
 /					r
 <other listed files generated by full-learning mode>   rwcdx
}

```

"O" is one of a number of flags you might append to the Subject mode. Others include:

```
A 	Protect the shared memory of this subject. No other processes but processes contained within this subject may access the shared memory of this subject.
C 	Auto-kill all processes belonging to the attacker's IP address upon violation of security policy.
K 	When processes belonging to this subject generate an alert, kill the process.
O 	Allow loading of writable libraries.
T 	Deny execution of binaries or scripts that are writable by any other subject in the policy. This flag is evaluated at policy enable time. All binaries with execute permission that are writable by another subject (ignoring special roles) will be reported and the RBAC system will not allow itself to be enabled until the changes are made.

```

See [this link.](http://en.wikibooks.org/wiki/Grsecurity/Appendix/Subject_Modes)

## Troubleshooting

### Out-of-tree kernel module compilation failure

PaX and grsecurity implement some hardening features via GCC plugins. The compiler configuration / version used to build the plugins provided in the package needs to be the same when building a kernel module. For example, the compiler provided in the [gcc-multilib](https://www.archlinux.org/packages/?name=gcc-multilib) package will not work - one should use the same compiler toolchain that was used to build the kernel. This also means [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec) needs to be rebuilt after even minor GCC upgrades before modules built with the new compiler can work with it. Rebuilding a kernel can be accomplished with the [Arch Build System](/index.php/Kernels/Arch_Build_System "Kernels/Arch Build System"). See bug [FS#43057](https://bugs.archlinux.org/task/43057).