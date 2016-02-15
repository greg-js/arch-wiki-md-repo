| **Summary**  |
| Projekt Enlightenment dostarcza użytecznych bibliotek, środowiska graficznego oraz innych aplikacji, w tym narzędzi developerskich. Artykuł ten zawiera informacje na temat instalacji, konfiguracji oraz problemów jakie możemy napotkać podczas pracy ze środowiskiem. |
| E17 uses the [Elementary](/index.php?title=Elementary&action=edit&redlink=1 "Elementary (page does not exist)") toolkit. |
| **Overview** |
| The [Xorg](/index.php/Xorg "Xorg") project provides an open source implementation of the X Window System – the foundation for a graphical user interface. [Desktop environments](/index.php/Desktop_environment "Desktop environment") such as [Enlightenment](/index.php/Enlightenment "Enlightenment"), [GNOME](/index.php/GNOME "GNOME"), [KDE](/index.php/KDE "KDE"), [LXDE](/index.php/LXDE "LXDE"), and [Xfce](/index.php/Xfce "Xfce") provide a complete graphical environment. Various [window managers](/index.php/Window_manager "Window manager") offer alternative and novel environments, and may be used _standalone_ to conserve system resources. [Display managers](/index.php/Display_manager "Display manager") provide a graphical login prompt. |
| **Related** |
| [Enlightenment](/index.php/Enlightenment "Enlightenment") |

From the [Enlightenment wiki](http://trac.enlightenment.org/e/wiki/Enlightenment):

	_Enlightenment (ang. oświecenie, nazywany też często e) - menedżer okien dla środowiska X Window System, który może być używany samodzielnie lub wraz ze środowiskami graficznymi takimi jak GNOME (swego czasu był to domyślny menedżer okien tego środowiska) czy KDE. Jego głównym autorem jest programista i grafik Carsten Haitzler (Rasterman). Wydany na licencji BSD._

Enlightenment znany jest z dużych możliwości konfiguracji oraz atrakcyjnej grafiki i efektów specjalnych. Dostępne są (na stronie domowej projektu) niezwykle dopracowane pod względem graficznym tematy pulpitu (themes) oraz statyczne i animowane tła pulpitu.

Menedżer dostępny jest w dwóch liniach – wydanej w 2000 roku, stabilnej DR16 oraz rozwojowej DR17\. Kod następnej serii, DR17 (lub inaczej E17), jest napisany od początku i bazuje na silnie zmodularyzowanych bibliotekach EFL (Enlightenment Foundation Libraries). DR17 ma być samodzielną powłoką graficzną, przeznaczoną dla szerokiej gamy urządzeń od urządzeń wbudowanych do stacji roboczych.

## Contents

*   [1 Instalacja E17](#Instalacja_E17)
    *   [1.1 From the community repository (SVN snapshots)](#From_the_community_repository_.28SVN_snapshots.29)
    *   [1.2 Compiling and packaging with ArchE17 script](#Compiling_and_packaging_with_ArchE17_script)
    *   [1.3 Compiling with easy_e17.sh](#Compiling_with_easy_e17.sh)
        *   [1.3.1 Update_e17.sh](#Update_e17.sh)
*   [2 Starting E17](#Starting_E17)
    *   [2.1 startx](#startx)
    *   [2.2 Elsa](#Elsa)
    *   [2.3 Other](#Other)
*   [3 Configuring the Network](#Configuring_the_Network)
    *   [3.1 NetworkManager](#NetworkManager)
    *   [3.2 connman](#connman)
*   [4 Installing Themes](#Installing_Themes)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Cursors](#Cursors)
    *   [5.2 Screen unlocking does not work](#Screen_unlocking_does_not_work)
    *   [5.3 Unreadable fonts](#Unreadable_fonts)
    *   [5.4 Modules and gadgets](#Modules_and_gadgets)
    *   [5.5 udisks vs. HAL](#udisks_vs._HAL)
    *   [5.6 What is Places?](#What_is_Places.3F)
        *   [5.6.1 Why doesn't the Places work?](#Why_doesn.27t_the_Places_work.3F)
        *   [5.6.2 A workaround that gets Places working](#A_workaround_that_gets_Places_working)
*   [6 External Links](#External_Links)

## Instalacja E17

### From the community repository (SVN snapshots)

**Note:** Make sure the [community repository](/index.php/Community_repository "Community repository") is enabled in your `/etc/pacman.conf`.

To install e17:

```
pacman -S e-svn

```

To install additional e17 modules and applications:

```
pacman -S e17-extra-svn

```

You might also want to install additional [Fonts](/index.php/Fonts "Fonts"). You need at least 1 True Type Font.

If you need/want an e17 package which is not (yet) available in [community], see if it is available in the [AUR](/index.php/AUR "AUR").

**Warning:** As e17 is still beta software you are encouraged to keep packages of the previous version on your computer, allowing you to [downgrade](/index.php/Downgrade "Downgrade") if needed.

### Compiling and packaging with ArchE17 script

You can build your own Arch Linux e17 packages with a small python script called [ArchE17](https://dev.archlinux.org/~ronald/e17.html).

### Compiling with easy_e17.sh

`easy_e17.sh` compiles E17 from source and installs it in `/opt/e17`. It does not create packages and therefore does not install dependencies automatically.

1.  Get it from the [AUR](/index.php/AUR "AUR"): [easy-e17](https://aur.archlinux.org/packages/easy-e17/).
2.  Edit `/etc/easy_e17.conf` if you want.
3.  Run it as user, so it downloads to ~/e17_src and builds as user, to install E17 (the script will immediately ask for your password so it can install in the end): `# easy_e17.sh -i` 
    **Warning:** This will install the latest svn version. For a stable result add the --srcrev= parameter with the latest stable revision. For beta 3 use 55246 as argument. For the revision with the 1.0 release of the core libraries, use 56361, and for the 1.1 release use 65800 ([2 Dec. 2011](http://enlightenment.org/p.php?p=news/show&l=en&news_id=37)).

4.  Put `/opt/e17/bin` in your `PATH` by editing `/etc/profile`. For example, you can add this line at the end of the file: `PATH="$PATH:/opt/e17/bin"` 
5.  If, after completing the install, xinitrc complains that it cannot find enlightenment upon starting, you may need to add these lines to the end of /etc/profile as well: `PYTHONPATH=":$PYTHONPATH"`  `LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/opt/e17/lib"` 

If you encounter any errors while trying to install E17, first check to make sure it is not a dependency problem. If it is, install the dependency and continue installing e17.

To update E17 without using the program mentioned below, run this command as root:

```
# easy_e17.sh -u

```

#### Update_e17.sh

`update_e17.sh` is a zenity script which is made to accompany `easy_e17.sh`. It makes several aspects of updating e17 easier as it can backup and restore your E17 svn tree (in case there is breakage), as well as roll it back to a specific revision (again, in case of breakage) or even let you know when a new revision has come around on E17's svn tree. See [this page](http://cafelinux.org/OzOs/content/how-administer-your-ozos-e17-desktop) for more information on this optional component. You can get it from the [AUR](/index.php/AUR "AUR"): [oz-e17-tools](https://aur.archlinux.org/packages/oz-e17-tools/).

## Starting E17

### startx

If you use `startx` or a simple [Display manager](/index.php/Display_manager "Display manager") like XDM or [SLiM](/index.php/SLiM "SLiM"), add or uncomment the following command in [xinitrc](/index.php/Xinitrc "Xinitrc"):

```
exec enlightenment_start

```

### Elsa

Nowadays E17 has a new display manager called Elsa, you can download it from AUR [elsa-svn-arch](https://aur.archlinux.org/packages/elsa-svn-arch/). Elsa is quite sophisticated and its configuration is controlled by `/etc/elsa.conf`. To start Elsa add the following line to your `/etc/inittab`

```
x:5:respawn:/usr/sbin/elsa

```

and change your default runlevel to 5.

### Other

More advanced display managers like [GDM](/index.php/GDM "GDM") and [KDM](/index.php/KDM "KDM") will automatically detect E17 thanks to the `/usr/share/xsessions/enlightenment.desktop` file provided by the `e-svn` package.

## Configuring the Network

### NetworkManager

You can use [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) to manage your network connections.

```
pacman -S networkmanager

```

Then you need to follow the instructions on [NetworkManager](/index.php/NetworkManager "NetworkManager") to do the configuration. You may also need [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) to help with your settings.

```
pacman -S network-manager-applet

```

You may want to add it to the start up programs so every time your E17 starts it appears on systray.

```
Settings -> Settings Panel -> Apps -> Startup Applications -> System -> Network

```

### connman

Another available network manager is [Connman](/index.php/Connman "Connman"), you can download it from AUR [connman](https://www.archlinux.org/packages/?name=connman). You do not need to follow any of the other instructions on the [Connman wiki page](/index.php/Connman "Connman"). The current build of ConnMan already includes network policy group section (although with only one statement, not three).

Next, edit your `/etc/rc.conf`. Remove **network** from your DAEMONS line. Add **connmand** (do not forget the **d**) _after_ **dbus** and **hal**.

ConnMan loads very quickly and appears to handle DHCP quite nicely. If you have installed [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant"), ConnMan latches onto that shows all available wireless connections.

## Installing Themes

More themes to customize the look of e17 are available from:

*   [exchange.enlightenment.org](http://exchange.enlightenment.org/), for which you can use the [e17-themes](https://aur.archlinux.org/packages/e17-themes/) [AUR](/index.php/AUR "AUR") package
*   [e17-stuff.org](http://www.e17-stuff.org)

You can install the themes (coming in .edj format) from the configuration dialog. During 2010 there was a change in how themes work, so for older themes you may need to do the following:

```
edje_convert <theme>.edj

```

**Note:** The edje_convert binary has been "dropped" by upstream developers... see: [trac.enlightenment.org](http://trac.enlightenment.org/e/changeset/56156)

You can also change the theme for the etk toolkit (the one which is used by exhibit). You can start the dialog to change the etk toolkit by starting `etk_prefs`.

## Troubleshooting

If you find some unexpected behavior, there are a few things you can do:

1.  try to see if the same behavior exists with the default theme
2.  backup `~/.e` and remove it (e.g. `mv ~/.e ~/.e.back`).

If you are sure you found a bug please report it directly upstream. [http://trac.enlightenment.org/e/report](http://trac.enlightenment.org/e/report)

### Cursors

If X complains about X cursors not being available, install the [libxcursor](https://www.archlinux.org/packages/?name=libxcursor) package.

### Screen unlocking does not work

If screenlock does not accept your password add the following to `/etc/pam.d/enlightenment`:

```
auth required pam_unix_auth.so

```

### Unreadable fonts

If fonts are too small and your screen is unreadable, be sure the right font packages are installed:

```
pacman -S ttf-dejavu ttf-bitstream-vera

```

### Modules and gadgets

	Module

	a name used in enlightenment to refer to the "backing" code for a gadget.

	Gadget

	a front-end or user interface that should help the end users of [E17](/index.php/E17 "E17") do something.

### udisks vs. HAL

Often a gadget with the name "Places", for example, will use a corresponding module also named "Places". Also modules may need to use underlying libraries or daemons to interact with various devices connected to your computer. Currently there are at least two choices for these underlying libraries or daemons to interact with connected devices. The two that will be considered here are udisks and HAL. At the time of this entry the [HAL](/index.php/HAL "HAL") page says:

	_HAL (Hardware Abstraction Layer) is a daemon that allows desktop applications to readily access hardware information, to locate and use such hardware regardless of bus or device type. In this way a desktop GUI can present all resources to its user in a seamless and uniform manner. HAL has become deprecated in favor of udev, udisks, upower, etc. and is no longer developed. Currently, a small number of programs still rely on and use HAL, though development is heading toward utilizing udev as a replacement._

So, apparently [E17](/index.php/E17 "E17") now tries to use udisks instead of [HAL](/index.php/HAL "HAL"). But some of the modules and gadgets, such as Places, have not been updated to use udisks yet.

### What is Places?

From the current source code [README](http://trac.enlightenment.org/e/browser/trunk/E-MODULES-EXTRA/places/README) for Places:

	Places module

	_This module manage the volumes device attached to the system._

In [other words](http://www.urbandictionary.com/define.php?term=engrish), Places is a gadget that will help you browse files on various devices you might plug into your computer, like phones, cameras, or other various storage devices you might plug into the usb port.

#### Why doesn't the Places work?

So, if you load the "Places" module, and then add the Places gadget to, say, your bottom shelf in enlightenment, it may look something like a blank grey area with no Gadget in it because the Places module and Gadget are still trying to use [HAL](/index.php/HAL "HAL"). Not to mention that if you plug a usb device in, the Places module will not detect it. So in order to fix this, here is a "solution":

#### A workaround that gets Places working

This procedure will attempt to help you get the HAL daemon running and the Places gadget working on your e17 desktop.

Install [hal-info](https://aur.archlinux.org/packages/hal-info/) and [hal-git](https://aur.archlinux.org/packages/hal-git/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). Note that [hal-info](https://aur.archlinux.org/packages/hal-info/) is a dependency for [hal-git](https://aur.archlinux.org/packages/hal-git/), so you may want to install it with [pacman](/index.php/Pacman "Pacman")'s `--asdeps` flag.

Start the hal daemon

 `# rc.d start hal` 

Now you must remove the "Places" gadget from my shelf, and unload the Places module from menu `settings -> modules -> Places -> unload`

Restart enlightenment, reload the Places module and add the Places gadget to my shelf

Try connecting a USB camera and watch it appear as a new device on the gadget bar in "places". If necessary, move it to the desktop, right click on the gadget `Gadget Places -> Move to -> Desktop`.

The Places gadget on the desktop should now look like an icon with a camera plugged into a usb port, and when you click on it, it opens a file manager, and shows you the files on your camera.

## External Links

*   [exchange.enlightenment.org](http://exchange.enlightenment.org/)
*   [e17-stuff.org](http://e17-stuff.org/)