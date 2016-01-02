# XScreenSaver

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

XScreenSaver is a screen saver and locker for the X Window System.

## Contents

*   [1 Installing XScreenSaver](#Installing_XScreenSaver)
*   [2 Configuring XScreenSaver](#Configuring_XScreenSaver)
    *   [2.1 DPMS and blanking settings](#DPMS_and_blanking_settings)
    *   [2.2 Xresources](#Xresources)
*   [3 Starting XScreenSaver](#Starting_XScreenSaver)
*   [4 Lock Screen](#Lock_Screen)
    *   [4.1 Automatically lock when suspending/sleeping/hibernating](#Automatically_lock_when_suspending.2Fsleeping.2Fhibernating)
*   [5 Disabling XScreenSaver for Media Applications](#Disabling_XScreenSaver_for_Media_Applications)
    *   [5.1 MPlayer](#MPlayer)
    *   [5.2 Kodi](#Kodi)
    *   [5.3 Adobe Flash/MPlayer/VLC](#Adobe_Flash.2FMPlayer.2FVLC)
*   [6 Using XScreenSaver as animated wallpaper](#Using_XScreenSaver_as_animated_wallpaper)
    *   [6.1 XScreenSaver as wallpaper under xcompmgr](#XScreenSaver_as_wallpaper_under_xcompmgr)
*   [7 Theming](#Theming)
*   [8 User switching from the lock screen](#User_switching_from_the_lock_screen)
    *   [8.1 LXDM](#LXDM)
    *   [8.2 LightDM](#LightDM)
    *   [8.3 KDM](#KDM)
*   [9 Debugging](#Debugging)
*   [10 See Also](#See_Also)

## Installing XScreenSaver

[Install](/index.php/Install "Install") the [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver) package.

For an Arch Linux branded experience, install the [xscreensaver-arch-logo](https://aur.archlinux.org/packages/xscreensaver-arch-logo/)<sup><small>AUR</small></sup> package.

## Configuring XScreenSaver

Global options are defined in `/usr/share/X11/app-defaults/XScreenSaver`. Under a standard setup, there is likely no need to edit this file. Instead most options are configured on a user-by-user basis simply by running _xscreensaver-demo_.

_xscreensaver-demo_ writes the chosen configuration in `~/.xscreensaver`, discarding any manual modification to the file.

Fortunately, since at least XScreenSaver 5.22, there is another way to edit XScreenSaver's user configuration, using `~/.Xresources`; see [Xdefaults#XScreenSaver resources](/index.php/Xdefaults#XScreenSaver_resources "Xdefaults") for some examples.

### DPMS and blanking settings

XScreenSaver manages screen blanking and display energy saving ([DPMS](/index.php/DPMS "DPMS")) independently of X itself and overrides it. To configure the timings for blanking, standby, display poweroff and such, use _xscreensaver-demo_ or edit the configuration file manually, e.g. `~/.xscreensaver`,

```
timeout:	1:00:00
cycle:		0:05:00
lock:		False
lockTimeout:	0:00:00
passwdTimeout:	0:00:30
fade:		True
unfade:		False
fadeSeconds:	0:00:03
fadeTicks:	20
dpmsEnabled:	True
dpmsStandby:	2:00:00
dpmsSuspend:	2:00:00
dpmsOff:	4:00:00

```

Note that if _Lock Screen After_ in _xscreensaver-demo_ is ticked and set to 0 minutes, the screen will be locked immediately upon blanking. Also note that if _Power Manager Enabled_ is unticked, this will have the effect of disabling DPMS - it does not mean that XScreenSaver will relinquish control of DPMS settings.

DPMS and screen blanking can be disabled by starting _xscreensaver-demo_ and, for the _Mode_ setting, choosing _Disable Screen Saver_.

### Xresources

Control many settings by using `~/.Xresources`. Defaults are located in `/usr/share/X11/app-defaults/XScreenSaver`.

Below are all the valid Xresources for version 5.22.

 `from: driver/XScreenSaver.ad` 

```
xscreensaver.mode: random
xscreensaver.timeout: 0:10:00
xscreensaver.cycle: 0:10:00
xscreensaver.lockTimeout: 0:00:00
xscreensaver.passwdTimeout: 0:00:30
xscreensaver.dpmsEnabled: False
xscreensaver.dpmsQuickoffEnabled: False
xscreensaver.dpmsStandby: 2:00:00
xscreensaver.dpmsSuspend: 2:00:00
xscreensaver.dpmsOff: 4:00:00
xscreensaver.grabDesktopImages: True
xscreensaver.grabVideoFrames: False
xscreensaver.chooseRandomImages: True

! This can be a local directory name, or the URL of an RSS or Atom feed.
xscreensaver.imageDirectory: /usr/share/wallpapers/
xscreensaver.nice: 10
xscreensaver.memoryLimit: 0
xscreensaver.lock: False
xscreensaver.verbose: False
xscreensaver.timestamp: True
xscreensaver.fade: True
xscreensaver.unfade: False
xscreensaver.fadeSeconds: 0:00:03
xscreensaver.fadeTicks: 20
xscreensaver.splash: True
xscreensaver.splashDuration: 0:00:05
xscreensaver.visualID: default
xscreensaver.captureStderr: True
xscreensaver.ignoreUninstalledPrograms: False

xscreensaver.textMode: file
xscreensaver.textLiteral: XScreenSaver
xscreensaver.textFile:
xscreensaver.textProgram: fortune
xscreensaver.textURL: http://en.wikipedia.org/w/index.php?title=Special:NewPages&feed=rss

xscreensaver.overlayTextForeground: #FFFF00
xscreensaver.overlayTextBackground: #000000
xscreensaver.overlayStderr: True
xscreensaver.font: *-medium-r-*-140-*-m-*

! The default is to use these extensions if available (as noted.)
xscreensaver.sgiSaverExtension: True
xscreensaver.xidleExtension: True
xscreensaver.procInterrupts: True

! Turning this on makes pointerHysteresis not work.
xscreensaver.xinputExtensionDev: False

! Set this to True if you are experiencing longstanding XFree86 bug #421
! (xscreensaver not covering the whole screen)
xscreensaver.GetViewPortIsFullOfLies: False

! This is what the "Demo" button on the splash screen runs (/bin/sh syntax.)
xscreensaver.demoCommand: xscreensaver-demo

! This is what the "Prefs" button on the splash screen runs (/bin/sh syntax.)
xscreensaver.prefsCommand: xscreensaver-demo -prefs

! This is the URL loaded by the "Help" button on the splash screen,
! and by the "Documentation" menu item in xscreensaver-demo.
xscreensaver.helpURL: http://www.jwz.org/xscreensaver/man.html

! loadURL       -- how the "Help" buttons load the helpURL (/bin/sh syntax.)
xscreensaver.loadURL: firefox '%s' || mozilla '%s' || netscape '%s'

! manualCommand -- how the "Documentation" buttons display man pages.
xscreensaver.manualCommand: xterm -sb -fg black -bg gray75 -T '%s manual' -e /bin/sh -c 'man "%s" ; read foo'

! The format used for printing the date and time in the password dialog box
! To show the time only:  %I:%M %p
! For 24 hour time: %H:%M
xscreensaver.dateFormat: %d-%b-%y (%a); %I:%M %p

! This command is executed by the "New Login" button on the lock dialog.
! (That button does not appear on the dialog if this program does not exist.)
! For Gnome: probably "gdmflexiserver -ls".  KDE, probably "kdmctl reserve".
! Or maybe yet another wheel-reinvention, "lxdm -c USER_SWITCH".
xscreensaver.newLoginCommand: kdmctl reserve
xscreensaver.installColormap: True
xscreensaver.pointerPollTime: 0:00:05
xscreensaver.pointerHysteresis: 10
xscreensaver.initialDelay: 0:00:00
xscreensaver.windowCreationTimeout: 0:00:30
xscreensaver.bourneShell: /bin/sh

! Resources for the password and splash-screen dialog boxes of
! the "xscreensaver" daemon.
xscreensaver.Dialog.headingFont: *-helvetica-bold-r-*-*-*-180-*-*-*-iso8859-1
xscreensaver.Dialog.bodyFont: *-helvetica-bold-r-*-*-*-140-*-*-*-iso8859-1
xscreensaver.Dialog.labelFont: *-helvetica-bold-r-*-*-*-140-*-*-*-iso8859-1
xscreensaver.Dialog.unameFont: *-helvetica-bold-r-*-*-*-120-*-*-*-iso8859-1
xscreensaver.Dialog.buttonFont: *-helvetica-bold-r-*-*-*-140-*-*-*-iso8859-1
xscreensaver.Dialog.dateFont: *-helvetica-medium-r-*-*-*-80-*-*-*-iso8859-1

! Helvetica asterisks look terrible.
xscreensaver.passwd.passwdFont: *-courier-medium-r-*-*-*-140-*-*-*-iso8859-1

xscreensaver.Dialog.foreground: #000000
xscreensaver.Dialog.background: #E6E6E6
xscreensaver.Dialog.Button.foreground: #000000
xscreensaver.Dialog.Button.background: #F5F5F5

!*Dialog.Button.pointBackground: #EAEAEA
!*Dialog.Button.clickBackground: #C3C3C3
xscreensaver.Dialog.text.foreground: #000000
xscreensaver.Dialog.text.background: #FFFFFF
xscreensaver.passwd.thermometer.foreground: #4464AC
xscreensaver.passwd.thermometer.background: #FFFFFF
xscreensaver.Dialog.topShadowColor: #FFFFFF
xscreensaver.Dialog.bottomShadowColor: #CECECE
xscreensaver.Dialog.logo.width: 210
xscreensaver.Dialog.logo.height: 210
xscreensaver.Dialog.internalBorderWidth: 24
xscreensaver.Dialog.borderWidth: 1
xscreensaver.Dialog.shadowThickness: 2

xscreensaver.passwd.heading.label: XScreenSaver %s
xscreensaver.passwd.body.label: This screen is locked.
xscreensaver.passwd.unlock.label: OK
xscreensaver.passwd.login.label: New Login
xscreensaver.passwd.user.label: Username:
xscreensaver.passwd.thermometer.width: 8
xscreensaver.passwd.asterisks: True
xscreensaver.passwd.uname: True

xscreensaver.splash.heading.label: XScreenSaver %s
xscreensaver.splash.body.label: Copyright © 1991-2013 by
xscreensaver.splash.body2.label: Jamie Zawinski <jwz@jwz.org>
xscreensaver.splash.demo.label: Settings
xscreensaver.splash.help.label: Help
```

## Starting XScreenSaver

**Tip:** To start XScreenSaver without the splash screen, use the `-no-splash` switch. See `man xscreensaver` for a full list of options.

In the [Xfce](/index.php/Xfce "Xfce"), [LXDE](/index.php/LXDE "LXDE") and [LXQt](/index.php/LXQt "LXQt") environments, XScreenSaver is autostarted automatically if it is available - no further action is required. For other environments, see [Autostarting](/index.php/Autostarting "Autostarting").

## Lock Screen

To immediately trigger `xscreensaver`, if it is running, and lock the screen, execute the following command:

```
$ xscreensaver-command --lock

```

### Automatically lock when suspending/sleeping/hibernating

The best option is to install [xss-lock](https://aur.archlinux.org/packages/xss-lock/)<sup><small>AUR</small></sup> from [AUR](/index.php/AUR "AUR"), and run this command from the X session autostart script:

```
xscreensaver & xss-lock -- xscreensaver-command -lock &

```

Another option is to install [xuserrun-git](https://aur.archlinux.org/packages/xuserrun-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/xuserrun-git)]</sup> from [AUR](/index.php/AUR "AUR"), and create the following file:

 `/etc/systemd/system/xscreensaver.service` 

```
[Unit]
Description=Lock X session using xscreensaver
Before=sleep.target

[Service]
Type=oneshot
ExecStart=/usr/bin/xuserrun /usr/bin/xscreensaver-command -lock

[Install]
WantedBy=sleep.target

```

and enable it with `systemctl enable xscreensaver`.

You may want to set XScreenSaver's fade out time to 0.

Other service configuration without xuserrun and for one user from [this thread](https://bbs.archlinux.org/viewtopic.php?id=163281), replace the previous [Service] section by this one :

 `/etc/systemd/system/xscreensaver.service` 

```
[Service]
User=yourusername
Type=oneshot
Environment=DISPLAY=:0
ExecStart=/usr/bin/xscreensaver-command -lock

```

## Disabling XScreenSaver for Media Applications

### MPlayer

Add the following to `~/.mplayer/config`

```
heartbeat-cmd="xscreensaver-command -deactivate >&- 2>&- &"

```

### Kodi

There is no native support within [Kodi](/index.php/Kodi "Kodi") to disable XScreenSaver (although it comes with its own screensaver). The [AUR](/index.php/AUR "AUR") contains a tiny app called [kodi-prevent-xscreensaver](https://aur.archlinux.org/packages/kodi-prevent-xscreensaver/)<sup><small>AUR</small></sup> that does just this.

### Adobe Flash/MPlayer/VLC

There is no native way to disable XScreenSaver for flash, but there is script named [lightsOn](https://github.com/iye/lightsOn) that works great and has support for Firefox's Flash plugin, Chromium's Flash plugin, MPlayer, and VLC.

Another approach would be to [disable DPMS](/index.php/DPMS#Setting_up_DPMS_in_X "DPMS") completely.

## Using XScreenSaver as animated wallpaper

One can run `xscreensaver` in the background, just like a wallpaper. First, kill any process that is controlling the background (the root window). Locate the desired XScreenSaver executable (they are usually on `/usr/lib/xscreensaver/`) and run it with the `-root` flag, like this

```
$ /usr/lib/xscreensaver/glslideshow -root &

```

### XScreenSaver as wallpaper under xcompmgr

xcompmgr may cause problems. One recommended solution is to use xwinwrap to run it in order to use it as wallpaper. Find it as [shantz-xwinwrap-bzr](https://aur.archlinux.org/packages/shantz-xwinwrap-bzr/)<sup><small>AUR</small></sup> in the [AUR](/index.php/AUR "AUR").

Run it with the following command:

```
$ xwinwrap -b -fs -sp -fs -nf -ov  -- /usr/lib/xscreensaver/glslideshow -root -window-id WID &

```

## Theming

XScreenSaver's unlock screen can be themed with [X resources](/index.php/X_resources "X resources") (see: [XScreenSaver resources](/index.php/X_resources#XScreenSaver_resources "X resources")).

## User switching from the lock screen

**Warning:** When switching users using a display manager such as GDM or LightDM, XScreenSaver will not lock the original session - it can be accessed without a password simply by switching TTY's to the session in question. If you are using LightDM, as a workaround, install [light-locker](https://www.archlinux.org/packages/?name=light-locker) and run it alongside XscreenSaver. Alternatively, use a different screen locking program altogether - see [List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security").

By default, XScreenSaver's "New Login" button in the lock screen will call `/usr/bin/gdmflexiserver` to switch users. This is fine if [GDM](/index.php/GDM "GDM") or [KDM](/index.php/KDM "KDM") are being used however for other [display managers](/index.php/Display_manager "Display manager") that support user switching (such as [LightDM](/index.php/LightDM "LightDM")), an alternative command will need to be specified.

**Note:** As mentioned in [#Configuring XScreenSaver](#Configuring_XScreenSaver), modifications made in `~/.xscreensaver` are discarded by _xscreensaver-demo_. Therefore, use `~/.Xresources` instead.

### LXDM

Paste the following into `~/.Xresources` to use LXDM's switching mode:

```
xscreensaver.newLoginCommand: lxdm -c USER_SWITCH

```

### LightDM

Paste the following into `~/.Xresources` to use LightDM's switching mode:

```
xscreensaver.newLoginCommand: dm-tool switch-to-greeter

```

**Note:** If you use this to switch to an already-logged-in user, you might have to enter the password twice (once for LightDM, and once for the XScreenSaver dialog of the user you logged in to).

### KDM

Paste the following into `~/.Xresources` to use kdm's switching mode:

```
xscreensaver.newLoginCommand: kdmctl reserve

```

## Debugging

You can configure xscreensaver to write to a log file by creating the logfile `# touch /var/log/xscreensaver.log` and then specifying its X resource _logFile_.

 `~/.Xresources`  `xscreensaver.logFile:/var/log/xscreensaver.log` 

To log verbose debugging information to the logFile as well start xscreensaver with the `-verbose` command line option, or add this to `~/.Xresources`

 `~/.Xresources` 

```
xscreensaver.logFile:/var/log/xscreensaver.log
xscreensaver.verbose:true
```

## See Also

*   [Homepage for XScreenSaver](http://www.jwz.org/xscreensaver/)
*   [Display Power Management Signaling](/index.php/Display_Power_Management_Signaling "Display Power Management Signaling")
*   [xinitrc](/index.php/Xinitrc "Xinitrc")
*   [List of applications#Screen lockers](/index.php/List_of_applications#Screen_lockers "List of applications")

Retrieved from "[https://wiki.archlinux.org/index.php?title=XScreenSaver&oldid=414066](https://wiki.archlinux.org/index.php?title=XScreenSaver&oldid=414066)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [X server](/index.php/Category:X_server "Category:X server")