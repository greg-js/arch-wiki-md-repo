# ConsoleKit

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [PolicyKit](/index.php/PolicyKit "PolicyKit")
*   [init](/index.php/Init "Init")

**Warning:** Arch Linux only has official support for _logind_ [[1]](https://www.archlinux.org/news/consolekit-replaced-by-logind/) and [systemd](/index.php/Systemd "Systemd"). When using _ConsoleKit_, please mention so in support requests.

**Note:** While Consolekit is no longer maintained upstream, the fork ConsoleKit2 is under development. [[2]](https://github.com/ConsoleKit2/ConsoleKit2)

**ConsoleKit2** is a framework for defining and tracking users, login sessions, and seats. Its function is to support multiuser setups. It also works for a single user, but offers no benefits compared to existing methods. [[3]](http://wiki.gentoo.org/wiki/ConsoleKit#Description)

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 ck-launch-session](#ck-launch-session)
    *   [2.2 No display manager](#No_display_manager)
    *   [2.3 Desktop environments](#Desktop_environments)
        *   [2.3.1 Xfce](#Xfce)
        *   [2.3.2 Mate](#Mate)
        *   [2.3.3 KDE](#KDE)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Use D-Bus for power operations](#Use_D-Bus_for_power_operations)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Running several applications from ~/.xinitrc](#Running_several_applications_from_.7E.2F.xinitrc)
    *   [4.2 Consolekit blocks active TTY](#Consolekit_blocks_active_TTY)
    *   [4.3 Inactive session when launching X on same TTY](#Inactive_session_when_launching_X_on_same_TTY)
*   [5 Replacing ConsoleKit with systemd-logind](#Replacing_ConsoleKit_with_systemd-logind)
*   [6 See also](#See_also)

## Installation

Install [consolekit](https://aur.archlinux.org/packages/consolekit/)<sup><small>AUR</small></sup> and [polkit-consolekit](https://aur.archlinux.org/packages/polkit-consolekit/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR").

## Configuration

### ck-launch-session

To launch an X session with ConsoleKit, append the following to the `exec` statement in `~/.xinitrc` e.g.:

```
exec ck-launch-session dbus-launch --sh-syntax --exit-with-session openbox-session

```

This starts [Openbox](/index.php/Openbox "Openbox") with proper environment variables so it and its children are able to use ConsoleKit.

[Display managers](/index.php/Display_manager "Display manager") like [KDM](/index.php/KDM "KDM"), [GDM](/index.php/GDM "GDM"), [LXDM](/index.php/LXDM "LXDM") and [SLiM](/index.php/SLiM "SLiM") start ConsoleKit automatically with each X session.

**Note:**

*   Do not nest ConsoleKit sessions by calling one from another, or you will break ConsoleKit.
*   In particular, since [SLiM](/index.php/SLiM "SLiM") reads `~/.xinitrc`, you should make sure _not_ to run `ck-launch-session` there.

### No display manager

If you are not using a display manager, but starting your window manager via the `startx` command, or from [inittab](/index.php/Inittab "Inittab").

If ConsoleKit is not working (`ck-list-sessions` command showing active = FALSE), you should start your window manager using the bash_profile method: [Start X at login#bash profile](/index.php/Start_X_at_login#bash_profile "Start X at login").

### Desktop environments

#### Xfce

For a login manager, [lxdm-consolekit](https://aur.archlinux.org/packages/lxdm-consolekit/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR") or [LightDM](/index.php/LightDM "LightDM") could be used.

#### Mate

[Install](/index.php/Install "Install") [mate-session-manager-upower](https://aur.archlinux.org/packages/mate-session-manager-upower/)<sup><small>AUR</small></sup> and [mate-power-manager-upower](https://aur.archlinux.org/packages/mate-power-manager-upower/)<sup><small>AUR</small></sup>.

If you use [mdm-display-manager](https://aur.archlinux.org/packages/mdm-display-manager/)<sup><small>AUR</small></sup> as a login manager and have trouble logging in, edit `/etc/pam.d/mdm`, comment out `session required pam_systemd.so` and restart `mdm`. Additionally append `session optional pam_ck_connector.so nox11` if you have [consolekit](https://aur.archlinux.org/packages/consolekit/)<sup><small>AUR</small></sup> installed.

#### KDE

The kdebase-workspace package needs to be recompiled for use with consolekit ([kdebase-workspace-consolekit](https://aur.archlinux.org/packages/kdebase-workspace-consolekit/)<sup><small>AUR</small></sup> is available from the AUR).

## Tips and tricks

### Use D-Bus for power operations

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** Content must be revised for `ConsoleKit2` and other developments (Discuss in [Talk:ConsoleKit#](https://wiki.archlinux.org/index.php/Talk:ConsoleKit))

**Note:** Using ConsoleKit2's D-Bus methods for suspend, hibernate, and hybrid sleep requires [pm-utils](https://www.archlinux.org/packages/?name=pm-utils).

Shut down:

 `dbus-send --system --print-reply --dest="org.freedesktop.ConsoleKit" /org/freedesktop/ConsoleKit/Manager org.freedesktop.ConsoleKit.Manager.Stop` 

Restart:

 `dbus-send --system --print-reply --dest="org.freedesktop.ConsoleKit" /org/freedesktop/ConsoleKit/Manager org.freedesktop.ConsoleKit.Manager.Restart` 

Suspend:

 `dbus-send --system --print-reply --dest="org.freedesktop.ConsoleKit" /org/freedesktop/ConsoleKit/Manager org.freedesktop.ConsoleKit.Manager.Suspend  boolean:true` 

Hibernate (suspend to disk):

 `dbus-send --system --print-reply --dest="org.freedesktop.ConsoleKit" /org/freedesktop/ConsoleKit/Manager org.freedesktop.ConsoleKit.Manager.Hibernate  boolean:true` 

Hybrid Sleep (suspend + hibernate):

 `dbus-send --system --print-reply --dest="org.freedesktop.ConsoleKit" /org/freedesktop/ConsoleKit/Manager org.freedesktop.ConsoleKit.Manager.HybridSleep  boolean:true` 

This method assumes that you are given permission to shut the system down via PolicyKit. The default group for this is `wheel`. To change this, edit `/etc/polkit-1/localauthority.conf.d/50-localauthority.conf` as root.

## Troubleshooting

### Running several applications from ~/.xinitrc

If several applications are to be executed from `~/.xinitrc`, not all of these will have ConsoleKit environment variables set. In the following example, only children of Compiz will be able to properly use ConsoleKit, but children of xterm will not.

 `~/.xinitrc` 

```
xterm &
exec ck-launch-session compiz ccp

```

Typically, this can be an issue when for example using Compiz standalone and some other application launchers, (gnome-do, kupfer, gmrun, xbindkeys, etc.) since children of the application launcher will not be able to use ConsoleKit. A dirty workaround is to have the entire session started by a second script, e.g. `~/.xstart`. Do not forget dbus-launch, it is likely that you will need it too:

 `~/.xinitrc` 

```
exec ck-launch-session dbus-launch ~/.xstart

```

 `~/.xstart` 

```
xterm &
thunar &
compiz ccp

```

Do not forget to make `~/.xstart` executable:

```
$ chmod +x ~/.xstart

```

To see whether everything is started correctly:

```
$ ck-list-sessions

```

It should show at least one session like this one:

```
Session18:
       unix-user = '1000'
       realname = 'Your Name'
       seat = 'Seat1'
       session-type = 
       active = TRUE
       x11-display = ':0'
       x11-display-device = '/dev/tty2'
       display-device = '/dev/tty1'
       remote-host-name = 
       is-local = TRUE
       on-since = '2011-11-16T12:01:50.104764Z'
       login-session-id = '7'

```

### Consolekit blocks active TTY

Configure [init](/index.php/Init "Init") to start ConsoleKit on an unused TTY, for example:

```
/usr/bin/openvt -c 63 -f -- /usr/sbin/console-kit-daemon --no-daemon &

```

See [[4]](https://bugs.freedesktop.org/show_bug.cgi?id=29920) for details.

### Inactive session when launching X on same TTY

Specify the `keeptty` flag to _startx_ or _xinit_ [[5]](http://www.linuxquestions.org/questions/slackware-14/starting-xorg-on-same-vt-as-login-vt-while-keeping-active-consolekit-session-4175533711/), for example:

```
startx -- -keeptty

```

See also [Xorg#Broken redirection](/index.php/Xorg#Broken_redirection "Xorg").

## Replacing ConsoleKit with systemd-logind

**Note:** _systemd-logind_ requires booting with [systemd](/index.php/Systemd "Systemd") to be functional.

Remove references to `ck-launch-session` from `~/.xinitrc`.

See [Session](/index.php/Session "Session") to check the status of your user session.

## See also

*   [ck-launch-session, Compiz, and mounting in Thunar/udisks](https://bbs.archlinux.org/viewtopic.php?id=116853)
*   [Gentoo wiki](http://wiki.gentoo.org/wiki/ConsoleKit)

Retrieved from "[https://wiki.archlinux.org/index.php?title=ConsoleKit&oldid=389660](https://wiki.archlinux.org/index.php?title=ConsoleKit&oldid=389660)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Security](/index.php/Category:Security "Category:Security")

Hidden category:

*   [Pages or sections flagged with Template:Accuracy](/index.php/Category:Pages_or_sections_flagged_with_Template:Accuracy "Category:Pages or sections flagged with Template:Accuracy")