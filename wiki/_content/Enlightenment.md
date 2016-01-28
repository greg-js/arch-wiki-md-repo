# Enlightenment

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Display manager](/index.php/Display_manager "Display manager")
*   [Window manager](/index.php/Window_manager "Window manager")

## Contents

*   [1 Enlightenment](#Enlightenment)
    *   [1.1 Installation](#Installation)
        *   [1.1.1 From the AUR](#From_the_AUR)
    *   [1.2 Starting Enlightenment](#Starting_Enlightenment)
        *   [1.2.1 Entrance](#Entrance)
        *   [1.2.2 Starting Enlightenment manually](#Starting_Enlightenment_manually)
    *   [1.3 Configuration](#Configuration)
        *   [1.3.1 Network](#Network)
        *   [1.3.2 Polkit agent](#Polkit_agent)
        *   [1.3.3 GNOME Keyring integration](#GNOME_Keyring_integration)
        *   [1.3.4 Enabling the system tray](#Enabling_the_system_tray)
        *   [1.3.5 Notifications](#Notifications)
    *   [1.4 Themes](#Themes)
        *   [1.4.1 GTK+](#GTK.2B)
    *   [1.5 Modules and Gadgets](#Modules_and_Gadgets)
        *   [1.5.1 "Extra" modules](#.22Extra.22_modules)
    *   [1.6 Troubleshooting](#Troubleshooting)
        *   [1.6.1 Compositing](#Compositing)
        *   [1.6.2 Unreadable fonts](#Unreadable_fonts)
        *   [1.6.3 Backlight always dimmed](#Backlight_always_dimmed)
        *   [1.6.4 Inconsistent cursor theme](#Inconsistent_cursor_theme)
*   [2 Enlightenment DR16](#Enlightenment_DR16)
    *   [2.1 To install E16](#To_install_E16)
    *   [2.2 Basic Configuration](#Basic_Configuration)
        *   [2.2.1 Background images](#Background_images)
        *   [2.2.2 Start/Restart/Stop Scripts](#Start.2FRestart.2FStop_Scripts)
        *   [2.2.3 Compositor](#Compositor)
*   [3 See also](#See_also)

## Enlightenment

This comprises both the [Enlightenment](https://www.enlightenment.org/) [window manager](/index.php/Window_manager "Window manager") and Enlightenment Foundation Libraries (EFL), which provide additional desktop environment features such as a toolkit, object canvas, and abstracted objects. It has been under development since 2005, but in February 2011 the core EFLs saw their first stable 1.0 release.

### Installation

Enlightenment can be [installed](/index.php/Installed "Installed") with the package [enlightenment](https://www.archlinux.org/packages/?name=enlightenment).

You might also want to install [terminology](https://www.archlinux.org/packages/?name=terminology), which is an EFL-based terminal emulator that integrates well with Enlightenment.

#### From the AUR

**Warning:** Some of these PKGBUILDs use unstable development code. Use them at your own risk.

Development PKGBUILDs which download and install the very latest development code are available as [enlightenment-git](https://aur.archlinux.org/packages/enlightenment-git/)<sup><small>AUR</small></sup> and its dependencies.

The following are EFL-based applications, most in an early stage of development and not yet released:

*   [econcentration-git](https://aur.archlinux.org/packages/econcentration-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/econcentration-git)]</sup> – Econcentration card game
*   [ecrire-git](https://aur.archlinux.org/packages/ecrire-git/)<sup><small>AUR</small></sup> – Ecrire text editor
*   [elbow-git](https://aur.archlinux.org/packages/elbow-git/)<sup><small>AUR</small></sup> – Elbow web browser
*   [eluminance-git](https://aur.archlinux.org/packages/eluminance-git/)<sup><small>AUR</small></sup> – Eluminance photo browser
*   [emprint-git](https://aur.archlinux.org/packages/emprint-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/emprint-git)]</sup> – Emprint screenshot tool
*   [enjoy-git](https://aur.archlinux.org/packages/enjoy-git/)<sup><small>AUR</small></sup> – [Enjoy](https://trac.enlightenment.org/e/wiki/Enjoy) music player
*   [epad](https://aur.archlinux.org/packages/epad/)<sup><small>AUR</small></sup> – ePad text editor
*   [eperiodique](https://aur.archlinux.org/packages/eperiodique/)<sup><small>AUR</small></sup> – [Eperiodique](http://eperiodique.sourceforge.net/) periodic table viewer
*   [ephoto-git](https://aur.archlinux.org/packages/ephoto-git/)<sup><small>AUR</small></sup> – [Ephoto](https://trac.enlightenment.org/e/wiki/Ephoto) picture viewer
*   [epour](https://aur.archlinux.org/packages/epour/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/epour)]</sup> and [epour-git](https://aur.archlinux.org/packages/epour-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/epour-git)]</sup> – Epour Bittorrent client
*   [epymc-git](https://aur.archlinux.org/packages/epymc-git/)<sup><small>AUR</small></sup> – E Python Media Center
*   [equate-git](https://aur.archlinux.org/packages/equate-git/)<sup><small>AUR</small></sup> – Equate calculator
*   [eruler-git](https://aur.archlinux.org/packages/eruler-git/)<sup><small>AUR</small></sup> – Eruler on-screen ruler and measurement tools
*   [efbb-git](https://aur.archlinux.org/packages/efbb-git/)<sup><small>AUR</small></sup> – Escape from Booty Bay angry birds style game
*   [elemines-git](https://aur.archlinux.org/packages/elemines-git/)<sup><small>AUR</small></sup> – [Elemines](http://elemines.sourceforge.net/) minesweeper style game
*   [espionage-git](https://aur.archlinux.org/packages/espionage-git/)<sup><small>AUR</small></sup> – Espionage D-Bus inspector
*   [ev-git](https://aur.archlinux.org/packages/ev-git/)<sup><small>AUR</small></sup> – ev simple picture viewer
*   [e_cho-git](https://aur.archlinux.org/packages/e_cho-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/e_cho-git)]</sup> – E_Cho simon style game
*   [e_jeweled-git](https://aur.archlinux.org/packages/e_jeweled-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/e_jeweled-git)]</sup> – E_Jeweled bejeweled style game
*   [rage](https://aur.archlinux.org/packages/rage/)<sup><small>AUR</small></sup> and [rage-git](https://aur.archlinux.org/packages/rage-git/)<sup><small>AUR</small></sup> – Rage video player

### Starting Enlightenment

Simply choose _Enlightenment_ session from your favourite [display manager](/index.php/Display_manager "Display manager") or configure [xinitrc](/index.php/Xinitrc "Xinitrc") to start it from the console.

#### Entrance

**Warning:** Entrance is highly experimental, and does not have proper systemd support. Use it at your own risk.

Enlightenment has a new display manager called Entrance, which is provided by the [entrance-git](https://aur.archlinux.org/packages/entrance-git/)<sup><small>AUR</small></sup> package. Entrance is quite sophisticated and its configuration is controlled by `/etc/entrance.conf`. It can be used by enabling `entrance.service` [using systemd](/index.php/Systemd#Using_units "Systemd").

#### Starting Enlightenment manually

If you prefer to start Enlightenment manually from the console, add the following line to your `~/.xinitrc` file:

 `~/.xinitrc` 

```
exec enlightenment_start

```

After that Enlightenment can be launched by typing `startx`. See [xinitrc](/index.php/Xinitrc "Xinitrc") for details.

### Configuration

Enlightenment has a sophisticated configuration system that can be accessed from the Main menu's Settings submenu.

#### Network

**ConnMan**

Enlightenment's preferred network manager is [ConnMan](/index.php/Connman "Connman") which can be installed from the [connman](https://www.archlinux.org/packages/?name=connman) package. Follow the instructions on [Connman](/index.php/Connman "Connman") to do the configuration.

For extended configuration, you may also install EConnman (available in AUR as [econnman](https://aur.archlinux.org/packages/econnman/)<sup><small>AUR</small></sup> or [econnman-git](https://aur.archlinux.org/packages/econnman-git/)<sup><small>AUR</small></sup>) and its associated dependencies.

**NetworkManager**

You can also use [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) to manage your network connections. Follow the instructions on [NetworkManager](/index.php/NetworkManager "NetworkManager") to do the configuration.

You probably also need [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) to help with your settings. You may want to add it to the start up programs so every time Enlightenment starts it appears on systray. For that you should go to _Settings Panel > Apps > Startup Applications > System_ and activate _Network_.

Whilst network connectivity will work, the applet itself will not be visible unless you have enabled the system tray, see [#Enabling the system tray](#Enabling_the_system_tray).

#### Polkit agent

Enlightenment does not ship with a [graphical polkit authentication agent](/index.php/Polkit#Authentication_agents "Polkit"). If you want to access some privileged actions (e.g. mount a filesystem on a system device), you have to install one and autostart it. For that you should go to _Settings Panel > Apps > Startup Applications > System_ and activate it. There is an EFL based authentication agent available in the AUR, [polkit-efl-git](https://aur.archlinux.org/packages/polkit-efl-git/)<sup><small>AUR</small></sup>.

#### GNOME Keyring integration

It is possible to use gnome-keyring in Enlightenment. However, at the time of writing, you need a small hack to make it work in full. First, you must tell Enlightenment to autostart gnome-keyring. For that you should go to _Settings Panel > Apps > Startup Applications > System_ and activate _Certificate and Key Storage_, _GPG Password Agent_, _SSH Key Agent_ and "Secret Storage Service". After this, you should edit your `~/.profile` and add the following:

```
       #Set gnome-keyring as the ssh authentication agent
       export SSH_AUTH_SOCK=/run/user/${UID}/keyring/ssh

```

This "hack" is used to override the automatic setting of the variable by "enlightenment-start" from "ssh-agent" to gnome-keyring.

More information on this topic in the [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring") article.

#### Enabling the system tray

**Note:** Since Enlightenment 20, Xembed support has been removed [[1]](https://twitter.com/_enlightenment_/status/538000507315314688) meaning that many 'legacy' applets can no longer be displayed in the Systray. To use these applets, you will need to use a standalone system tray application such as [stalonetray](https://www.archlinux.org/packages/?name=stalonetray) instead.

Enlightenment has support for a system tray but it is disabled by default. To enable the system tray, open the Enlightenment main menu, navigate to the _Settings_ submenu and click on the _Modules_ option. Scroll down until you see the _Systray_ option. Highlight that option and click the _Load_ button. Now that the module has been loaded, it can be added to the shelf. Right click on the shelf you wish to add the Systray to, hightlight the _Shelf_ submenu and click on the _Contents_ option. Scroll down until you see _Systray_. Highlight that option and click the _Add_ button.

#### Notifications

Enlightenment provides a notification server through its Notification extension.

*   Notifications may be displayed in any corner of the "screen" as defined below
*   Available screen policies are Primary Screen, Current Screen, All Screens, and Xinerama
*   Notifications may be filtered based on urgency (Low, Normal, or Critical in any combination)
*   A default notification timeout may be set and optionally enforced for all notifications
*   The notification server may also optionally ignore replace ID requests

### Themes

More themes to customize the look of Enlightenment are available from:

*   [exchange.enlightenment.org](http://exchange.enlightenment.org/theme)
*   [e17-stuff.org](http://e17-stuff.org/index.php?xcontentmode=7000)
*   [relighted.c0n.de](http://relighted.c0n.de/#100) for the default theme in 200 different colors
*   [git.enlightenment.org](http://git.enlightenment.org/themes) (git clone the theme you like, run 'make' and you end up with a .edj theme file)
*   [packages.bodhilinux.com](http://packages.bodhilinux.com/bodhi/pool/stable/b/) has a good collection (you will need to extract the .edj file from the .deb; bsdtar will do this and is part of the base ArchLinux install). A nice catalog can be seen at [their wiki](https://web.archive.org/web/20140120083020/http://art.bodhilinux.com/doku.php?id=bodhi_e17_themes_v3).

You can install the themes (coming in .edj format) using the theme configuration dialog or by moving them to `~/.e/e/themes`.

**Note:** Enlightenment does not provide a stable theme API, and there have been numerous theme API changes over the years, even after E17 was released. Themes that have not been updated regularly are unlikely to work.

**Tip:** To make GTK and Qt applications match the default theme of Enlightenment you can download a theme like the [E17 GTK theme](http://gnome-look.org/content/show.php/?content=163472), place it in `~/.themes/` and select application themes from Enlightenments settings, and set it to that, this will make all GTK2 and GTK3 applications match the default Enlightenment theme, you can then configure Qt applications (or configure Qt's default settings) to use the Gtk+ theme so it will mimic the theme your GTK applications are using, this way you can make sure most applications will blend in perfectly with your default enlightenment theme. See also [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications").

#### GTK+

To alter the GTK+ theme, go to _Settings > All > Look > Application Theme_.

### Modules and Gadgets

Module

Name used in enlightenment to refer to the "backing" code for a gadget.

Gadget

Front-end or user interface that should help the end users of Enlightenment do something.

Many Modules provide Gadgets that can be added to your desktop or on a shelf. Some Modules (such as CPUFreq) only provide a single Gadget while others (such as Composite) provide additional features without any gadgets. Note that certain gadgets such as Systray can only be added to a shelf while others such as Moon can only be loaded on the desktop.

#### "Extra" modules

**Warning:** These are 3rd party modules and not officially supported by the Enlightenment developers. They are also pulled directly from git, so they are development code that may or may not work at any time. Use at your own risk.

Beyond the modules described here, more "extra" modules are available from [e-modules-extra-git](https://aur.archlinux.org/packages/e-modules-extra-git/)<sup><small>AUR</small></sup>.

**Places**

Places is a gadget that will help you browse files on various devices you might plug into your computer, like phones, cameras, or other various storage devices you might plug into the usb port.

Available from [places-git](https://aur.archlinux.org/packages/places-git/)<sup><small>AUR</small></sup>.

**Note:** This module is no longer required for auto-mounting external devices in Enlightenment

**Scale Windows**

The _Scale Windows_ module, which requires compositing to be enabled, adds several features. The scale windows effect shrinks all open windows and brings them all into view. This is known in Mac OS X as "Exposé". The scale pager effect zooms out and shows all desktops as a wall, like the compiz expo plugin. Both can be added to the desktop as a gadget or bound to a key binding, mouse binding or screen edge binding.

Some people like to change the standard window selection key binding `ALT + Tab` to use Scale Windows to select windows. To change this setting, you navigate to _Menu > Settings > Settings Panel > Input > Keys_. From here, you can set any key binding you would like.

To replace the window selection key binding functionality with Scale Windows, scroll through the left panel until you find the _ALT_ section and then find and select `ALT + Tab`. Then, scroll through the right panel looking for the "Scale Windows" section and choose either _Select Next_ or _Select Next (All)_ depending on whether you would like to see windows from only the current desktop or from all desktops and click _Apply_ to save the binding.

Available from [comp-scale-git](https://aur.archlinux.org/packages/comp-scale-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/comp-scale-git)]</sup>.

### Troubleshooting

If you find some unexpected behavior, there are a few things you can do:

1.  try to see if the same behavior exists with the default theme
2.  disable any 3rd party modules you may have installed
3.  backup `~/.e` and remove it (e.g. `mv ~/.e ~/.e.back`)

If you are sure you found a bug please report it [directly upstream](https://phab.enlightenment.org/maniphest/task/create/).

#### Compositing

When the configuration is messed up and the settings windows can no longer be approached, configuration for the compositor can be reset by the hardcoded keybinding `Ctrl + Alt + Shift + Home`.

#### Unreadable fonts

If fonts are too small and your screen is unreadable, be sure the right font packages are installed. [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) and [ttf-bitstream-vera](https://www.archlinux.org/packages/?name=ttf-bitstream-vera) are valid candidates.

You can set scaling under _Settings > Settings Panel > Look > Scaling_.

#### Backlight always dimmed

You may find that Enlightenment routinely dims the backlight to 30% on logout and will only restore it to 100% when you log into another Enlightenment session. This is especially problematic when using another desktop environment alongside Enlightenment as the backlight will not automatically be restored to its normal level when using that desktop environment. To fix this issue, open the Enlightenment _Settings Panel_ and, under the _Look_ tab, click on the _Composite_ option. Tick the _Don't fade backlight_ box and click _OK_.

#### Inconsistent cursor theme

You may find that the cursor theme for the desktop is different to the one used in applications such as [Firefox](/index.php/Firefox "Firefox"). This is because desktop applications are using X cursor themes whilst Enlightenment has its own set of cursor themes. For consistency, you can set Enlightenment to always use the X cursor theme. To do this, open the Enlightenment _Settings Panel_ and click on the _Input_ tab. Click on the _Mouse_ option. Change the theme from _Enlightenment_ to _X_ and click _OK_. You should now find that the same cursor theme is used everywhere. If the X cursor theme itself is not always consistent, see [Cursor themes#XDG specification](/index.php/Cursor_themes#XDG_specification "Cursor themes").

## Enlightenment DR16

Enlightenment, Development Release 16 was first released in 2000, and reached version 1.0 in 2009\. Originally, the DR16 stood for the 0.16 version of the Enlightenment project. You'll find it as "Enlightenment16" now in the Arch repositories, it is still under development today, regularly updated by its maintainer Kim 'kwo' Woelders. With compositing, shadows and transparencies, E16 kept all of the speed that presided over its foundation by original author Carsten "Rasterman" Haitzler but with up to date refinement.

### To install E16

Install [enlightenment16](https://www.archlinux.org/packages/?name=enlightenment16).

E16 can be quite different from the other WM's out there, read `/usr/share/doc/e16/e16.html` after installation to learn more. The man page is at `man e16`, not `man enlightenment`, and only gives startup options.

### Basic Configuration

Most everything in E16 resides in `~/.e16` and is text-based, editable at will. That includes the Menus too.

Shortcut keys can be either modified by hand, or with the e16keyedit software provided as source on the [sourceforge](http://sourceforge.net/projects/enlightenment/) page of the e16 project, or from the [e16keyedit](https://aur.archlinux.org/packages/e16keyedit/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/e16keyedit)]</sup> package.

#### Background images

You have to copy the desired wallpapers into `~/.e16/backgrounds/`

MMB or RMB anywhere on the desktop will give access to the settings, select `/Desktop/Backgrounds/`

Any new image copied in the `~/.e16/backgrounds/` folder will get the list of available backgrounds auto-updated. Select desired wallpaper from drop-down menu. Inside the appropriate tabs in the global e16 settings, you can adjust things like tiling of the background image, filling screen and such.

#### Start/Restart/Stop Scripts

Create an Init, a Start and a Stop folder in your `~/.e16` folder: any .sh script found there will either be executed at Startup (from Init folder), at each Restart (from Start folder), or at Shutdown (from Stop folder); provided you allowed it trough the MMB / settings / session / <enable scripts> button and made them executable with `chmod +x **yourscript.sh**`. Typical examples involves starting pulseaudio or your favorite network manager applet.

#### Compositor

Shadows, Transparent effects _et all_ can be found in MMB or RMB /Settings, under Composite .

## See also

*   [Enlightenment Homepage](http://www.enlightenment.org/)
*   [Enlightenment Exchange](http://exchange.enlightenment.org/)
*   [Enlightenment Developer Documentation](http://docs.enlightenment.org/)
*   [Bodhi Guide to Enlightenment](http://www.bodhilinux.com/e17guide/e17guideEN/)
*   [E17-Stuff](http://www.e17-stuff.org/)
*   [DR16 download resource](http://sourceforge.net/projects/enlightenment/)
*   [Enlightenment users mail list](https://lists.sourceforge.net/lists/listinfo/enlightenment-users)
*   [Enlightenment developer mail list](https://lists.sourceforge.net/lists/listinfo/enlightenment-devel)
*   [irc://irc.freenode.net#e](irc://irc.freenode.net#e)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Enlightenment&oldid=412390](https://wiki.archlinux.org/index.php?title=Enlightenment&oldid=412390)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Desktop environments](/index.php/Category:Desktop_environments "Category:Desktop environments")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")