Related articles

*   [Security](/index.php/Security "Security")
*   [SELinux](/index.php/SELinux "SELinux")
*   [TOMOYO Linux](/index.php/TOMOYO_Linux "TOMOYO Linux")

[AppArmor](https://en.wikipedia.org/wiki/AppArmor "wikipedia:AppArmor") is a [Mandatory Access Control](/index.php/Mandatory_Access_Control "Mandatory Access Control") (MAC) system, implemented upon the [Linux Security Modules](https://en.wikipedia.org/wiki/Linux_Security_Modules "wikipedia:Linux Security Modules") (LSM).

AppArmor, like most other LSMs, supplements rather than replaces the default Discretionary Access Control (DAC). As such it's impossible to grant a process more privileges than it had in the first place.

Ubuntu, SUSE and a number of other distributions use it by default. RHEL (and its variants) use SELinux which requires good userspace integration to work properly. SELinux attaches labels to all files, processes and objects and is therefore very flexible. However configuring SELinux is considered to be very complicated and requires a supported filesystem. AppArmor on the other hand works using file paths and its configuration can be easily adapted.

AppArmor proactively protects the operating system and applications from external or internal threats and even zero-day attacks by enforcing a specific rule set on a per application basis. Security policies completely define what system resources individual applications can access, and with what privileges. Access is denied by default if no profile says otherwise. A few default policies are included with AppArmor and using a combination of advanced static analysis and learning-based tools, AppArmor policies for even very complex applications can be deployed successfully in a matter of hours.

Every breach of policy triggers a message in the system log, and AppArmor can be configured to notify users with real-time violation warnings popping up on the desktop.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Kernel](#Kernel)
        *   [1.1.1 Custom kernel](#Custom_kernel)
    *   [1.2 Userspace Tools](#Userspace_Tools)
    *   [1.3 Testing](#Testing)
*   [2 Disabling](#Disabling)
*   [3 Configuration](#Configuration)
    *   [3.1 Auditing and generating profiles](#Auditing_and_generating_profiles)
    *   [3.2 Understanding profiles](#Understanding_profiles)
    *   [3.3 Parsing profiles](#Parsing_profiles)
*   [4 Security considerations](#Security_considerations)
    *   [4.1 Preventing circumvention of path-based MAC via links](#Preventing_circumvention_of_path-based_MAC_via_links)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Get desktop notification on DENIED actions](#Get_desktop_notification_on_DENIED_actions)
    *   [5.2 Cache profiles](#Cache_profiles)
*   [6 See also](#See_also)

## Installation

### Kernel

[Install](/index.php/Install "Install") either [linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened) (4.17.4 or later) or [linux-apparmor](https://aur.archlinux.org/packages/linux-apparmor/). A third option is to compile a [#Custom kernel](#Custom_kernel).

To enable AppArmor as default security model on every boot, set the following [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"): `apparmor=1 security=apparmor`

**Note:** [linux-apparmor](https://aur.archlinux.org/packages/linux-apparmor/) should already use AppArmor as default security model (`CONFIG_DEFAULT_SECURITY_APPARMOR=y`).

#### Custom kernel

When [compiling the kernel](/index.php/Kernels#Compilation "Kernels"), it is required to set at least the following options:

```
CONFIG_SECURITY_APPARMOR=y
CONFIG_AUDIT=y

```

To use AppArmor as the default Linux security model and omitting the need of setting kernel parameters, also set the following options:

```
CONFIG_SECURITY_APPARMOR_BOOTPARAM_VALUE=1
CONFIG_DEFAULT_SECURITY_APPARMOR=y

```

### Userspace Tools

The userspace tools and libraries to control AppArmor are supplied by the [apparmor](https://aur.archlinux.org/packages/apparmor/) package.

The package is a split package which consists of following sub-packages:

*   [apparmor](https://aur.archlinux.org/packages/apparmor/) (meta package)
*   [apparmor-libapparmor](https://aur.archlinux.org/packages/apparmor-libapparmor/)
*   [apparmor-utils](https://aur.archlinux.org/packages/apparmor-utils/)
*   [apparmor-parser](https://aur.archlinux.org/packages/apparmor-parser/)
*   [apparmor-profiles](https://aur.archlinux.org/packages/apparmor-profiles/)
*   [apparmor-pam](https://aur.archlinux.org/packages/apparmor-pam/)
*   [apparmor-vim](https://aur.archlinux.org/packages/apparmor-vim/)

To load all AppArmor profiles on startup, [enable](/index.php/Enable "Enable") `apparmor.service`.

### Testing

To test if AppArmor has been enabled:

 `# cat /sys/module/apparmor/parameters/enabled` 
```
Y

```

(Y=enabled, N=disabled, no such file = module not in kernel)

To display the current loaded status use `apparmor_status`:

 `# apparmor_status` 
```
apparmor module is loaded.
44 profiles are loaded.
44 profiles are in enforce mode.
 ...
0 profiles are in complain mode.
0 processes have profiles defined.
0 processes are in enforce mode.
0 processes are in complain mode.
0 processes are unconfined but have a profile defined.

```

## Disabling

To disable AppArmor for the current session, [stop](/index.php/Stop "Stop") `apparmor.service`, or [disable](/index.php/Disable "Disable") it to prevent it from starting at the next boot.

Alternatively you may choose to disable the kernel modules required by AppArmor by appending `apparmor=0 security=""` to the [kernel boot parameters](/index.php/Kernel_parameters "Kernel parameters").

## Configuration

### Auditing and generating profiles

To create new profiles the [Audit framework](/index.php/Audit_framework "Audit framework") should be running. This is because Arch Linux adopted [systemd](/index.php/Systemd "Systemd") and doesn't do kernel logging to file by default. AppArmor can grab kernel audit logs from the userspace auditd daemon, allowing you to build a profile.

To get kernel audit logs, you'll need to have rules in place to monitor the desired application. Most often a basic rule configured with [auditctl(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/auditctl.8) will suffice:

```
# auditctl -a exit,always -F arch=b64 -S all -F path=/usr/bin/chromium -F key=MonitorChromium

```

Be sure to read [Audit framework#Adding rules](/index.php/Audit_framework#Adding_rules "Audit framework") if this is unfamiliar to you.

**Note:** Remember to stop the service afterwards (and maybe clear `/var/log/audit/audit.log`) because it may cause overhead depending on your rules.

### Understanding profiles

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

Strings preceded by a '@' symbol are variables defined by abstractions (`/etc/apparmor.d/abstractions/`), tunables (`/etc/apparmor.d/tunables/`) or by the profile itself. `#include` includes other profile-files directly. Paths followed by a set of characters are [access permissions](http://wiki.apparmor.net/index.php/AppArmor_Core_Policy_Reference#File_access_rules). Pattern matching is done using [AppArmor's globbing syntax](http://wiki.apparmor.net/index.php/AppArmor_Core_Policy_Reference#AppArmor_globbing_syntax).

Most common use cases are covered by the following statements:

*   `r` — read: read data
*   `w` — write: create, delete, write to a file and extend it
*   `m` — memory map executable: memory map a file executable
*   `x` — execute: execute file; needs to be preceded by a [qualifier](http://wiki.apparmor.net/index.php/AppArmor_Core_Policy_Reference#Execute_rules)

Remember that those permission do not allow binaries to exceed the permission dictated by the Discretionary Access Control (DAC).

This is merely a short overview, for a more detailed guide be sure to have a look at the [documentation](http://wiki.apparmor.net/index.php/AppArmor_Core_Policy_Reference).

### Parsing profiles

To load (enforce or complain), unload, reload, cache and stat profiles use `apparmor_parser`. The default action (`-a`) is to load a new profile in enforce mode, loading it in complain mode is possible using the `-C` switch, in order to overwrite an existing profile use the `-r` option and to remove a profile use `-R`. Each action may also apply to multiple profiles. Refer to [apparmor_parser(8)](http://man.cx/apparmor_parser(8)) man page for more information.

## Security considerations

### Preventing circumvention of path-based MAC via links

Previously AppArmor can be circumvented via hardlinks in the standard POSIX security model. However, the kernel [included](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=800179c9b8a1e796e441674776d11cd4c05d61d7) the ability to prevent this vulnerability via the following settings:

 `/usr/lib/sysctl.d/50-default.conf` 
```
...
fs.protected_hardlinks = 1
fs.protected_symlinks = 1
```

Kernel patches distributed by Ubuntu as workarounds are not needed.

## Tips and tricks

### Get desktop notification on DENIED actions

The notify daemon displays desktop notifications whenever AppArmor denies a program access. The script must be started at each boot and needs a few additional parameters:

```
# aa-notify -p -f /var/log/audit/audit.log --display $DISPLAY

```

The daemon relies on the auditing events being logged to a text file which can be specified using `-f`. To circumvent [systemd](/index.php/Systemd "Systemd") not logging to a file it is necessary to [enable](/index.php/Enable "Enable") `auditd.service` and pass its log file to `aa-notify`. No special auditing rules are necessary for this to work, therefore the overhead is not as significant as it was when [#Auditing and generating profiles](#Auditing_and_generating_profiles).

### Cache profiles

Since AppArmor has to translate the configured profiles into a binary format it may take some time to load them. Besides being bothersome for the user, it may also increases the boot time significantly!

To circumvent some of those problems AppArmor can cache profiles in `/etc/apparmor.d/cache/`. However this behaviour is disabled by default therefore it must be done manually with `apparmor_parser`. In order to write to the cache use `-W` (overwrite existing profiles with `-T`) and reload the profiles using `-r`. Refer to [#Parsing profiles](#Parsing_profiles) for a brief overview of additional arguments.

## See also

*   [AppArmor wiki](http://wiki.apparmor.net/)
*   [AppArmor Core Policy Reference](http://wiki.apparmor.net/index.php/AppArmor_Core_Policy_Reference) — Detailed description of available options in a profile
*   [Ubuntu Tutorial](http://ubuntuforums.org/showthread.php?t=1008906) — General overview of available utilities and profile creation
*   [Ubuntu Wiki](https://help.ubuntu.com/community/AppArmor) — Basic command overview
*   [AppArmor Versions](http://wiki.apparmor.net/index.php/AppArmor_versions) — Version overview and links to the respective release notes
*   [apparmor.d(5)](http://manpages.ubuntu.com/manpages/artful/man5/apparmor.d.5.html) — Structure of the AppArmor configuration directory
*   [apparmor_parse(8)](http://manpages.ubuntu.com/manpages/artful/man8/apparmor_parser.8.html) — The most fundamental AppArmor utility to load, unload, cache and stat profiles
*   [Kernel Interfaces](http://wiki.apparmor.net/index.php/Kernel_interfaces) — Low level interfaces to the AppArmor kernel module
*   [Apparmor Profile Migration](https://wiki.ubuntu.com/ApparmorProfileMigration) — Emergence of profiles
*   [wikipedia:Linux Security Modules](https://en.wikipedia.org/wiki/Linux_Security_Modules "wikipedia:Linux Security Modules") — Linux kernel module on which basis AppArmor is build upon
*   [Launchpad Project Page](https://launchpad.net/apparmor)
*   [FS#21406](https://bugs.archlinux.org/task/21406) — Initial discussion about the introduction of AppArmor