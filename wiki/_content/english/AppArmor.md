Related articles

*   [Security](/index.php/Security "Security")
*   [SELinux](/index.php/SELinux "SELinux")
*   [TOMOYO Linux](/index.php/TOMOYO_Linux "TOMOYO Linux")

[AppArmor](https://gitlab.com/apparmor) is a [Mandatory Access Control](/index.php/Mandatory_Access_Control "Mandatory Access Control") (MAC) system, implemented upon the [Linux Security Modules](https://en.wikipedia.org/wiki/Linux_Security_Modules "wikipedia:Linux Security Modules") (LSM).

AppArmor, like most other LSMs, supplements rather than replaces the default Discretionary Access Control (DAC). As such it's impossible to grant a process more privileges than it had in the first place.

Ubuntu, SUSE and a number of other distributions use it by default. RHEL (and its variants) use SELinux which requires good userspace integration to work properly. SELinux attaches labels to all files, processes and objects and is therefore very flexible. However configuring SELinux is considered to be very complicated and requires a supported filesystem. AppArmor on the other hand works using file paths and its configuration can be easily adapted.

AppArmor proactively protects the operating system and applications from external or internal threats and even zero-day attacks by enforcing a specific rule set on a per application basis. Security policies completely define what system resources individual applications can access, and with what privileges. Access is denied by default if no profile says otherwise. A few default policies are included with AppArmor and using a combination of advanced static analysis and learning-based tools, AppArmor policies for even very complex applications can be deployed successfully in a matter of hours.

Every breach of policy triggers a message in the system log, and AppArmor can be configured to notify users with real-time violation warnings popping up on the desktop.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Custom kernel](#Custom_kernel)
*   [2 Usage](#Usage)
    *   [2.1 Display current status](#Display_current_status)
    *   [2.2 Parsing profiles](#Parsing_profiles)
    *   [2.3 Disabling loading](#Disabling_loading)
*   [3 Configuration](#Configuration)
    *   [3.1 Auditing and generating profiles](#Auditing_and_generating_profiles)
    *   [3.2 Understanding profiles](#Understanding_profiles)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Get desktop notification on DENIED actions](#Get_desktop_notification_on_DENIED_actions)
    *   [4.2 Speed-up AppArmor start by caching profiles](#Speed-up_AppArmor_start_by_caching_profiles)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Failing to start Samba SMB/CIFS server](#Failing_to_start_Samba_SMB.2FCIFS_server)
*   [6 See also](#See_also)

## Installation

AppArmor is available in [linux](https://www.archlinux.org/packages/?name=linux) ([since 4.18.8.arch1-1](https://git.archlinux.org/svntogit/packages.git/commit/?id=c46609a4b0325c363455264844091b71de01eddc)), [linux-zen](https://www.archlinux.org/packages/?name=linux-zen) ([since 4.18.8.zen1-1](https://git.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/linux-zen&id=3ab708208c8e13d5de08dabebc442d2d0be7a585)) and [linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened) ([since 4.17.4.a-1](https://git.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/linux-hardened&id=14eccc6c604d37fa3001146f5bd4ca32ffa15c4f)).

To enable AppArmor as default security model on every boot, set the following [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"):

```
apparmor=1 security=apparmor

```

[Install](/index.php/Install "Install") [apparmor](https://www.archlinux.org/packages/?name=apparmor) for userspace tools and libraries to control AppArmor. To load all AppArmor profiles on startup, [enable](/index.php/Enable "Enable") `apparmor.service`.

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

## Usage

### Display current status

To test if AppArmor has been correctly enabled:

 `$ aa-enabled` 
```
Yes

```

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

### Parsing profiles

To load (enforce or complain), unload, reload, cache and stat profiles use `apparmor_parser`. The default action (`-a`) is to load a new profile in enforce mode, loading it in complain mode is possible using the `-C` switch, in order to overwrite an existing profile use the `-r` option and to remove a profile use `-R`. Each action may also apply to multiple profiles. Refer to [apparmor_parser(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/apparmor_parser.8) man page for more information.

### Disabling loading

Disable AppArmor by unloading all profiles for the current session:

```
# aa-teardown 

```

To prevent from loading AppArmor profiles at the next boot [disable](/index.php/Disable "Disable") `apparmor.service`. To prevent the kernel from loading AppArmor, remove `apparmor=1 security=apparmor` from the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

## Configuration

### Auditing and generating profiles

To create new profiles the [Audit framework](/index.php/Audit_framework "Audit framework") should be running. This is because Arch Linux adopted [systemd](/index.php/Systemd "Systemd") and doesn't do kernel logging to file by default. AppArmor can grab kernel audit logs from the userspace auditd daemon, allowing you to build a profile.

New AppArmor profiles can be created by utilizing [aa-genprof(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/aa-genprof.8) and [aa-logprof(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/aa-logprof.8) tools available in [apparmor](https://www.archlinux.org/packages/?name=apparmor) package. Detailed guide about using those tools is available at [AppArmor wiki - Profiling with tools](https://gitlab.com/apparmor/apparmor/wikis/Profiling_with_tools).

Alternatively profiles may be also created manually, see guide available at [AppArmor wiki - Profiling by hand](https://gitlab.com/apparmor/apparmor/wikis/Profiling_by_hand).

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

Strings preceded by a `@` symbol are variables defined by abstractions (`/etc/apparmor.d/abstractions/`), tunables (`/etc/apparmor.d/tunables/`) or by the profile itself. `#include` includes other profile-files directly. Paths followed by a set of characters are [access permissions](https://gitlab.com/apparmor/apparmor/wikis/AppArmor_Core_Policy_Reference#file-access-rules). Pattern matching is done using [AppArmor's globbing syntax](https://gitlab.com/apparmor/apparmor/wikis/AppArmor_Core_Policy_Reference#apparmor-globbing-syntax).

Most common use cases are covered by the following statements:

*   `r` — read: read data
*   `w` — write: create, delete, write to a file and extend it
*   `m` — memory map executable: memory map a file executable
*   `x` — execute: execute file; needs to be preceded by a [qualifier](https://gitlab.com/apparmor/apparmor/wikis/AppArmor_Core_Policy_Reference#execute-rules)

Remember that those permission do not allow binaries to exceed the permission dictated by the Discretionary Access Control (DAC).

This is merely a short overview, for a more detailed guide be sure to have a look at the [apparmor.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/apparmor.d.5) man page and [documentation](https://gitlab.com/apparmor/apparmor/wikis/AppArmor_Core_Policy_Reference).

## Tips and tricks

### Get desktop notification on DENIED actions

The notification daemon displays desktop notifications whenever AppArmor denies a program access. To automatically start `aa-notify` daemon on login follow below steps:

Install and enable [Audit framework](/index.php/Audit_framework "Audit framework"). Allow your desktop user to read audit logs in `/var/log/audit` by adding it to `audit` [user group](/index.php/User_group "User group"):

```
# groupadd -r audit
# gpasswd -a <username> audit

```

Add `audit` group to `auditd.conf`:

 `/etc/audit/auditd.conf`  `log_group = audit` 
**Tip:** You may use other already existing system groups like `wheel` or `adm`.

Create [desktop launcher](/index.php/Desktop_launcher "Desktop launcher") with the below content:

 `~/.config/autostart/apparmor-notify.desktop` 
```
[Desktop Entry]
Type=Application
Name=AppArmor Notify
Comment=Receive on screen notifications of AppArmor denials
TryExec=/usr/bin/aa-notify
Exec=/usr/bin/aa-notify -p -s 1 -w 60 -f /var/log/audit/audit.log
StartupNotify=false
NoDisplay=true
```

Reboot and check if `aa-notify` daemon is running:

```
$ ps aux | grep aa-notify

```

**Note:** Depending on your specific system configuration there could be A LOT of notifications displayed.

For more information, see [aa-notify(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/aa-notify.8).

### Speed-up AppArmor start by caching profiles

Since AppArmor has to translate the configured profiles into a binary format it may significantly increase the boot time. You can check current AppArmor startup time with:

```
$ systemd-analyze blame | grep apparmor

```

To enable caching AppArmor profiles, uncomment:

 `/etc/apparmor/parser.conf` 
```
## Turn creating/updating of the cache on by default
write-cache
```

To change default cache location add:

 `/etc/apparmor/parser.conf`  `cache-loc=/path/to/location` 
**Note:** Since 2.13.1 default cache location is `/var/cache/apparmor/`, previously it was `/etc/apparmor.d/cache.d/`.

Reboot and check AppArmor startup time again to see improvement:

```
$ systemd-analyze blame | grep apparmor

```

## Troubleshooting

### Failing to start Samba SMB/CIFS server

See [Samba#Permission issues on AppArmor](/index.php/Samba#Permission_issues_on_AppArmor "Samba").

## See also

*   [Wikipedia:AppArmor](https://en.wikipedia.org/wiki/AppArmor "wikipedia:AppArmor")
*   [AppArmor wiki](https://gitlab.com/apparmor/apparmor/wikis/home)
*   [AppArmor Core Policy Reference](https://gitlab.com/apparmor/apparmor/wikis/AppArmor_Core_Policy_Reference) — Detailed description of available options in a profile
*   [Ubuntu Tutorial](https://ubuntuforums.org/showthread.php?t=1008906) — General overview of available utilities and profile creation
*   [Ubuntu Wiki](https://help.ubuntu.com/community/AppArmor) — Basic command overview
*   [AppArmor Versions](https://gitlab.com/apparmor/apparmor/wikis/AppArmor_versions) — Version overview and links to the respective release notes
*   [Kernel Interfaces](https://gitlab.com/apparmor/apparmor/wikis/Kernel_interfaces) — Low level interfaces to the AppArmor kernel module
*   [wikipedia:Linux Security Modules](https://en.wikipedia.org/wiki/Linux_Security_Modules "wikipedia:Linux Security Modules") — Linux kernel module on which basis AppArmor is build upon
*   [AppArmor in openSUSE Security Guide](https://doc.opensuse.org/documentation/leap/security/single-html/book.security/index.html#part.apparmor)