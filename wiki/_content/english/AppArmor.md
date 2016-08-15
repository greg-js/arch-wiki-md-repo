[AppArmor](https://en.wikipedia.org/wiki/AppArmor "wikipedia:AppArmor") is a [Mandatory Access Control](https://en.wikipedia.org/wiki/Mandatory_access_control "wikipedia:Mandatory access control") (MAC) system, implemented upon the [Linux Security Modules](https://en.wikipedia.org/wiki/Linux_Security_Modules "wikipedia:Linux Security Modules") (LSM).

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Kernel](#Kernel)
    *   [1.2 Userspace Tools](#Userspace_Tools)
    *   [1.3 Testing](#Testing)
*   [2 Disabling](#Disabling)
*   [3 Creating new profiles](#Creating_new_profiles)
*   [4 Security considerations](#Security_considerations)
    *   [4.1 Preventing circumvention of path-based MAC via links](#Preventing_circumvention_of_path-based_MAC_via_links)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Get desktop notification on DENIED actions](#Get_desktop_notification_on_DENIED_actions)
*   [6 More Info](#More_Info)
*   [7 Links](#Links)
*   [8 See also](#See_also)

## Installation

### Kernel

When compiling the kernel, it needs the following options:

```
 CONFIG_SECURITY_APPARMOR=y
 CONFIG_SECURITY_APPARMOR_BOOTPARAM_VALUE=1
 CONFIG_DEFAULT_SECURITY_APPARMOR=y
 CONFIG_AUDIT=y

```

Instead of setting `CONFIG_SECURITY_APPARMOR_BOOTPARAM_VALUE` and `CONFIG_DEFAULT_SECURITY_APPARMOR`, you can also set [kernel boot parameters](/index.php/Kernel_parameters "Kernel parameters"): `apparmor=1 security=apparmor`.

There also is a stock kernel with AppArmor: [linux-apparmor](https://aur.archlinux.org/packages/linux-apparmor/). However, as of May 2015, the kernel is outdated.

### Userspace Tools

The userspace tools and libraries to control AppArmor are supplied by the [apparmor](https://aur.archlinux.org/packages/apparmor/) package.

The package is a split package which consists of following sub-packages:

*   apparmor (meta package)
*   apparmor-libapparmor
*   apparmor-utils
*   apparmor-parser
*   apparmor-profiles
*   apparmor-pam
*   apparmor-vim

To load all AppArmor profiles on startup, the [apparmor](https://aur.archlinux.org/packages/apparmor/) package includes a systemd unit:

 `# systemctl enable apparmor` 

### Testing

After reboot you can test if AppArmor is really enabled using this command as root:

```
 # cat /sys/module/apparmor/parameters/enabled 
 Y

```

(Y=enabled, N=disabled, no such file = module not in kernel)

**Note:** Since AppArmor builds and installs a kernel module it must be rebuilt against the current kernel on each update

## Disabling

To disable AppArmor temporarily, you can add `apparmor=0 security=""` to the [kernel boot parameters](/index.php/Kernel_parameters "Kernel parameters").

Alternatively run

```
# systemctl stop apparmor.service

```

to disable it for the current session.

## Creating new profiles

To create new profiles using `aa-genprof`, `auditd.service` from the package [audit](https://www.archlinux.org/packages/?name=audit) must be running. This is because Arch Linux adopted systemd and doesn't do kernel logging to file by default. Apparmor can grab kernel audit logs from the userspace auditd daemon, allowing you to build a profile. To get kernel audit logs, you'll need to have create rules. See this section: [Audit framework#Adding rules](/index.php/Audit_framework#Adding_rules "Audit framework").

Be sure to stop the service afterwards (and maybe clear `/var/log/audit/audit.log`) because it causes overhead.

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

To get a notification on your desktop whenever AppArmor enters a "DENIED" log entry start the notify daemon by

```
# aa-notify -p --display $DISPLAY

```

This daemon must be started at each boot.

## More Info

AppArmor, like most other LSMs, supplements rather than replaces the default Discretionary access control. As such it's impossible to grant a process more privileges than it had in the first place.

Ubuntu, SUSE and a number of other distributions use it by default. RHEL (and it's variants) use SELinux which requires good userspace integration to work properly. People tend to agree that it is also much much harder to configure correctly.

Taking a common example - A new Flash vulnerability: If you were to browse to a malicious website AppArmor can prevent the exploited plugin from accessing anything that may contain private information. In almost all browsers, plugins run out of process which makes isolating them much easier.

AppArmor profiles (usually) get stored in easy to read text files in `/etc/apparmor.d`

Every breach of policy triggers a message in the system log, and many distributions also integrate it into DBUS so that you get real-time violation warnings popping up on your desktop.

## Links

*   Official pages
    *   Kernel: [https://apparmor.wiki.kernel.org/](https://apparmor.wiki.kernel.org/) [http://wiki.apparmor.net/](http://wiki.apparmor.net/)
    *   Userspace: [https://launchpad.net/apparmor](https://launchpad.net/apparmor)

*   [http://www.kernel.org/pub/linux/security/apparmor/AppArmor-2.6/](http://www.kernel.org/pub/linux/security/apparmor/AppArmor-2.6/)
*   [http://wiki.apparmor.net/index.php/AppArmor_Core_Policy_Reference](http://wiki.apparmor.net/index.php/AppArmor_Core_Policy_Reference)

*   [http://ubuntuforums.org/showthread.php?t=1008906](http://ubuntuforums.org/showthread.php?t=1008906) (Tutorial)
*   [https://help.ubuntu.com/community/AppArmor](https://help.ubuntu.com/community/AppArmor)
*   [FS#21406](https://bugs.archlinux.org/task/21406)
*   [http://stuff.mit.edu/afs/sipb/contrib/linux/Documentation/apparmor.txt](http://stuff.mit.edu/afs/sipb/contrib/linux/Documentation/apparmor.txt)
*   [http://wiki.apparmor.net/index.php/Kernel_interfaces](http://wiki.apparmor.net/index.php/Kernel_interfaces)
*   [http://wiki.apparmor.net/index.php/AppArmor_versions](http://wiki.apparmor.net/index.php/AppArmor_versions)
*   [http://manpages.ubuntu.com/manpages/oneiric/man5/apparmor.d.5.html](http://manpages.ubuntu.com/manpages/oneiric/man5/apparmor.d.5.html)
*   [http://manpages.ubuntu.com/manpages/oneiric/man8/apparmor_parser.8.html](http://manpages.ubuntu.com/manpages/oneiric/man8/apparmor_parser.8.html)
*   [http://wiki.apparmor.net/index.php/Distro_CentOS](http://wiki.apparmor.net/index.php/Distro_CentOS)
*   [http://bodhizazen.net/aa-profiles/](http://bodhizazen.net/aa-profiles/)
*   [https://wiki.ubuntu.com/ApparmorProfileMigration](https://wiki.ubuntu.com/ApparmorProfileMigration)
*   [wikipedia:Linux Security Modules](https://en.wikipedia.org/wiki/Linux_Security_Modules "wikipedia:Linux Security Modules")
*   [http://wiki.apparmor.net/index.php/Gittutorial](http://wiki.apparmor.net/index.php/Gittutorial)

## See also

*   [TOMOYO Linux](/index.php/TOMOYO_Linux "TOMOYO Linux")
*   [SELinux](/index.php/SELinux "SELinux")