[AppArmor](https://en.wikipedia.org/wiki/AppArmor "wikipedia:AppArmor") is a [Mandatory Access Control](https://en.wikipedia.org/wiki/Mandatory_access_control "wikipedia:Mandatory access control") (MAC) system, implemented upon the [Linux Security Modules](https://en.wikipedia.org/wiki/Linux_Security_Modules "wikipedia:Linux Security Modules") (LSM).

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Kernel](#Kernel)
    *   [1.2 Userspace Tools](#Userspace_Tools)
    *   [1.3 Testing](#Testing)
*   [2 Disabling](#Disabling)
*   [3 Configuration](#Configuration)
    *   [3.1 Auditing and generating profiles](#Auditing_and_generating_profiles)
    *   [3.2 Editing and understanding profiles](#Editing_and_understanding_profiles)
    *   [3.3 Parsing profiles](#Parsing_profiles)
*   [4 Security considerations](#Security_considerations)
    *   [4.1 Preventing circumvention of path-based MAC via links](#Preventing_circumvention_of_path-based_MAC_via_links)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Get desktop notification on DENIED actions](#Get_desktop_notification_on_DENIED_actions)
    *   [5.2 Cache profiles](#Cache_profiles)
*   [6 More Info](#More_Info)
*   [7 Links](#Links)
*   [8 See also](#See_also)

## Installation

### Kernel

**Note:** The highly disputed user namespace (`CONFIG_USER_NS=Y`) isn't set in the [kernel](/index.php/Kernel "Kernel") configuration, but may bring additional functionality to AppArmor. See [FS#36969](https://bugs.archlinux.org/task/36969) for details on user namespaces.

When compiling the kernel, it is required to at least set the following options:

```
 CONFIG_SECURITY_APPARMOR=y
 CONFIG_SECURITY_APPARMOR_BOOTPARAM_VALUE=1
 CONFIG_DEFAULT_SECURITY_APPARMOR=y
 CONFIG_AUDIT=y

```

For those new or altered variables to not get overridden, place them at the bottom of the config file or adjust the previous invocations accordingly.

Instead of setting `CONFIG_SECURITY_APPARMOR_BOOTPARAM_VALUE` and `CONFIG_DEFAULT_SECURITY_APPARMOR`, you can also set [kernel boot parameters](/index.php/Kernel_parameters "Kernel parameters"): `apparmor=1 security=apparmor`.

### Userspace Tools

**Note:** Since AppArmor builds and installs a kernel module it must be rebuilt against the current kernel on each update

The userspace tools and libraries to control AppArmor are supplied by the [apparmor](https://aur.archlinux.org/packages/apparmor/) package.

The package is a split package which consists of following sub-packages:

*   apparmor (meta package)
*   apparmor-libapparmor
*   apparmor-utils
*   apparmor-parser
*   apparmor-profiles
*   apparmor-pam
*   apparmor-vim

To load all AppArmor profiles on startup, [enable](/index.php/Enable "Enable") `apparmor.service`.

### Testing

After reboot you can test if AppArmor is really enabled using this command as root:

```
 # cat /sys/module/apparmor/parameters/enabled 
 Y

```

(Y=enabled, N=disabled, no such file = module not in kernel)

## Disabling

To disable AppArmor for the current session, [stop](/index.php/Stop "Stop") `apparmor.service`, or disable it to prevent it from starting at the next boot.

Alternatively you may choose to disable the kernel modules required by AppArmor by appending `apparmor=0 security=""` to the [kernel boot parameters](/index.php/Kernel_parameters "Kernel parameters").

## Configuration

### Auditing and generating profiles

To create new profiles using `aa-genprof`, `auditd.service` from the package [audit](https://www.archlinux.org/packages/?name=audit) must be running. This is because Arch Linux adopted systemd and doesn't do kernel logging to file by default. Apparmor can grab kernel audit logs from the userspace auditd daemon, allowing you to build a profile. To get kernel audit logs, you'll need to have rules in place to monitor the desired application. Most often a basic rule configured with [auditctl(8)](http://linux.die.net/man/8/auditctl) will suffice:

```
# auditctl -a exit,always -F arch=b64 -S all -F path=/usr/bin/chromium -F key=MonitorChromium

```

but be sure to read [Audit framework#Adding rules](/index.php/Audit_framework#Adding_rules "Audit framework") if this is unfamiliar to you.

**Note:** Remember to stop the service afterwards (and maybe clear `/var/log/audit/audit.log`) because it may cause overhead depending on your rules.

### Editing and understanding profiles

Profiles are human readable text files residing under `/etc/apparmor.d/` describing how binaries should be treated when executed. A basic profile looks similar to this:

 `/etc/apparmor.d/usr.bin.test` 
```
#include <tunables/global>

profile test /usr/lib/test/test_binary {
    #include <abstractions/base>

    # Main libraries and plugins
    /usr/share/TEST/** r,
    /usr/lib/TEST/** rm,

    # Configuration files and logs
    @{HOME}/.config/ r,
    @{HOME}/.config/TEST/** rw,
}

```

Text preceded by a `@` symbol are variables defined by abstractions (`/etc/apparmor.d/abstractions/`), tunables (`/etc/apparmor.d/tunables/`) or by the profile itself. `#include` includes other profile-files directly. Paths followed by a set of characters are [access permissions](http://wiki.apparmor.net/index.php/AppArmor_Core_Policy_Reference#File_access_rules). Pattern matching is done using [AppArmor's globbing syntax](http://wiki.apparmor.net/index.php/AppArmor_Core_Policy_Reference#AppArmor_globbing_syntax). Most common use cases are covered by the following statements:

*   `r` — read: read data
*   `w` — write: create, delete, write to a file and extend it
*   `m` — memory map executable: memory map a file executable
*   `x` — execute: execute file; needs to be preceded by a [qualifier](http://wiki.apparmor.net/index.php/AppArmor_Core_Policy_Reference#Execute_rules)

Remember that those permission do not allow binaries to exceed the permission dictated by the Discretionary Access Control (DAC).

This is merely a short overview, for a more detailed guide be sure to have a look at the [documentation](http://wiki.apparmor.net/index.php/AppArmor_Core_Policy_Reference).

### Parsing profiles

To load, unload, reload, cache and stat profiles use `apparmor_parser`. The default action (`-a`) is to load a new profile, in order to overwrite an existing profile use the `-r` option and to remove a profile use `-R`. Each action may also apply to multiple profiles. Refer to [apparmor_parser(8)](http://man.cx/apparmor_parser(8)) man page for more information.

## Security considerations

### Preventing circumvention of path-based MAC via links

AppArmor can be circumvented via hardlinks in the standard POSIX security model. However, the kernel [included](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=800179c9b8a1e796e441674776d11cd4c05d61d7) the ability to prevent this vulnerability via the following settings:

 `/usr/lib/sysctl.d/50-default.conf` 
```
...
fs.protected_hardlinks = 1
fs.protected_symlinks = 1
```

Patches distributions like Ubuntu have applied to their kernels as workarounds as not needed anymore.

## Tips and tricks

### Get desktop notification on DENIED actions

The notify daemon displays desktop notifications whenever AppArmor denies a program access. The script must be started at each boot and needs a few additional parameters:

```
# aa-notify -p -f /var/log/audit/audit.log --display $DISPLAY

```

The daemon relies on the auditing events being logged to a text file which can be specified using `-f`. To circumvent [systemd](/index.php/Systemd "Systemd") not logging to a file it is necessary to [enable](/index.php/Enable "Enable") `auditd.service` and pass its log file to `aa-notify`. No special auditing rules are necessary for this to work, therefore the overhead is not as significant as it was when [#Creating new profiles](#Creating_new_profiles).

### Cache profiles

Since AppArmor has to translate the configured profiles into a binary format it may take some time to load them. Besides being bothersome for the user, it may also increases the boot time significantly!

To circumvent some of those problems AppArmor can cache profiles in `/etc/apparmor.d/cache/`. However this behaviour is disabled by default therefore it must be done manually with `apparmor_parser`. In order to write to the cache use `-W` (overwrite existing profiles with `-T`) and reload the profiles using `-r`. Refer to [#Parsing profiles](#Parsing_profiles) for a brief overview of additional arguments.

## More Info

AppArmor, like most other LSMs, supplements rather than replaces the default Discretionary Access Control (DAC). As such it's impossible to grant a process more privileges than it had in the first place.

Ubuntu, SUSE and a number of other distributions use it by default. RHEL (and it's variants) use SELinux which requires good userspace integration to work properly. People tend to agree that it is also much much harder to configure correctly.

Taking a common example - A new Flash vulnerability: If you were to browse to a malicious website AppArmor can prevent the exploited plugin from accessing anything that may contain private information. In almost all browsers, plugins run out of process which makes isolating them much easier.

AppArmor profiles (usually) get stored in easy to read text files in `/etc/apparmor.d`

Every breach of policy triggers a message in the system log, and many distributions also integrate it into DBUS so that you get real-time violation warnings popping up on your desktop.

## Links

*   [Home Page](http://wiki.apparmor.net/index.php/Main_Page)
*   [AppArmor Core Policy Reference](http://wiki.apparmor.net/index.php/AppArmor_Core_Policy_Reference) — Detailed description of available options in a profile
*   [Ubuntu Tutorial](http://ubuntuforums.org/showthread.php?t=1008906) — General overview of available utilities and profile creation
*   [Ubuntu Wiki](https://help.ubuntu.com/community/AppArmor) — Basic command overview
*   [AppArmor Verions](http://wiki.apparmor.net/index.php/AppArmor_versions) — Version overview and links to the respective release notes
*   [apparmor.d(5)](http://manpages.ubuntu.com/manpages/oneiric/man5/apparmor.d.5.html) — Structure of the AppArmor configuration directory
*   [apparmor_parse(8)](http://manpages.ubuntu.com/manpages/oneiric/man8/apparmor_parser.8.html) — The most fundamental AppArmor utility to load, unload, cache and stat profiles
*   [Kernel Interfaces](http://wiki.apparmor.net/index.php/Kernel_interfaces) — Low level interfaces to the AppArmor kernel module
*   [Apparmor Profile Migration](https://wiki.ubuntu.com/ApparmorProfileMigration) — Emergence of profiles
*   [Build Instructions for CentOS](http://wiki.apparmor.net/index.php/Distro_CentOS)
*   [wikipedia:Linux Security Modules](https://en.wikipedia.org/wiki/Linux_Security_Modules "wikipedia:Linux Security Modules") — Linux kernel module on which basis AppArmor is build upon
*   [Launchpad Project Page](https://launchpad.net/apparmor)
*   [Contributing](http://wiki.apparmor.net/index.php/Gittutorial) — Introduction to git mechanics and on how to contribute
*   [FS#21406](https://bugs.archlinux.org/task/21406) — Initial discussion about the introduction of AppArmor

## See also

*   [TOMOYO Linux](/index.php/TOMOYO_Linux "TOMOYO Linux")
*   [SELinux](/index.php/SELinux "SELinux")