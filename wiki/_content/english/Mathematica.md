Related articles

*   [Scientific Applications](/index.php/Scientific_Applications "Scientific Applications")
*   [Sage-mathematics](/index.php/Sage-mathematics "Sage-mathematics")
*   [Matlab](/index.php/Matlab "Matlab")

[Mathematica](http://www.wolfram.com/mathematica/) is a commercial program used in scientific, engineering and mathematical fields. Here we explain how to install it.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Mathematica 6](#Mathematica_6)
        *   [1.1.1 Mounting iso](#Mounting_iso)
        *   [1.1.2 Running the Installer](#Running_the_Installer)
        *   [1.1.3 Fonts](#Fonts)
    *   [1.2 Mathematica 7](#Mathematica_7)
    *   [1.3 Mathematica 8](#Mathematica_8)
    *   [1.4 Mathematica 10](#Mathematica_10)
    *   [1.5 Mathematica 11](#Mathematica_11)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Missing symbols](#Missing_symbols)
    *   [2.2 HiDPI / Retina Screens](#HiDPI_.2F_Retina_Screens)
*   [3 See also](#See_also)

## Installation

Since Mathematica is a non-free application and upgrades may incur costs, this section lists instructions for different available versions.

### Mathematica 6

#### Mounting iso

One way to mount the Mathematica `.iso` is to create a `/media/iso` mount directory and add the following line to the [fstab](/index.php/Fstab "Fstab"):

```
/*location/of/mathematica.iso* /media/iso iso9660 exec,ro,user,noauto,loop=/dev/loop0   0 0

```

Now you can mount it with:

```
# mount /media/iso

```

#### Running the Installer

You can start the installer by navigating to:

```
/Unix/Installer

```

Run *MathInstaller* with:

```
sh ./MathInstaller

```

**Note:** If you do not place the "sh" in front, then you will get an error about a bad interpreter.

#### Fonts

Add the directories containing Type1 and BDF fonts to your FontPath.

### Mathematica 7

Mathematica 7 is much easier to install.

```
tar xf Mathematica-7.0.1.tar.gz
cd Unix/Installer
./MathInstaller

```

Follow instructions.

For KDE users, the Mathematica icon may appear in the *Lost & Found* category. To solve this, execute the following as root:

```
# ln -s /etc/xdg/menus/applications-merged /etc/xdg/menus/kde-applications-merged

```

### Mathematica 8

An issue with Mathematica 8 is a reproducible crash when performing WolframAlpha[] functions. By default, Mathematica is configured to detect the system's proxy settings when configuring how to connect to the internet to fetch data. A "bug" exists that will eventually crash Mathematica when the calling library is used. A workaround is to avoid this library call altogether by configuring Mathematica to "directly connect" to the internet. (*Edit > Preferences > Internet Connectivity > Proxy Settings*). This bug has been reported to Wolfram.

### Mathematica 10

[Install](/index.php/Install "Install") [mathematica](https://aur.archlinux.org/packages/mathematica/) (need historical version). The `Mathematica_10.XX.YY_LINUX.sh` installation script is required; you will need to download this separately from Wolfram.com, your university, etc. You will also need an activation key.

### Mathematica 11

[Install](/index.php/Install "Install") [mathematica](https://aur.archlinux.org/packages/mathematica/). Obtain `Mathematica_11.XX.YY_LINUX.sh` from Wolfram Research, along with an activation key. Successful install may throw non-critical errors: xdg-icon-resource, mkdir, xdg-desktop-menu.

Mathematica 11 automatically creates a document folder 'Wolfram Mathematica' in [$UserDocumentsDirectory](https://reference.wolfram.com/language/ref/$UserDocumentsDirectory.html), which is set by Mathematica according to [XDG user directories](/index.php/XDG_user_directories "XDG user directories").

## Troubleshooting

#### Missing symbols

If you have font rendering problems where certain symbols do not show up (i.e. `/` appears as a square), try uninstalling [font-mathematica](https://www.archlinux.org/packages/?name=font-mathematica).

Also, try [this](http://mathematica.stackexchange.com/questions/1158/invisible-conjugate-glyph-in-the-linux-frontend) solution. It also states the issue is fixed with Mathematica version 9.

Try having applications use anti-aliasing. For KDE: *System Settings > Application Appearance > Fonts > Use anti-aliasing (Enabled)*

#### HiDPI / Retina Screens

If you have a [HiDPI](/index.php/HiDPI "HiDPI") screen, such as an Apple Retina display, and the main text in Mathematica looks small when you open it, this can be fixed:

*   Go to *Edit → Preferences*
*   From the *Advanced* tab, click *Open Option Inspector*
*   In the tree on the right, go to *Formatting Options → Font Options → Font Properties*
*   Change the value for *"ScreenResolution"* to double its current setting, e.g. 72 → 144\. You can also use `xdpyinfo | grep resolution` to get a more precise number (which will need to be doubled).

## See also

*   [Official site](http://www.wolfram.com/mathematica/)
*   [Official Support](http://www.wolfram.com/support/)