# Mathematica

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:Mathematica#](https://wiki.archlinux.org/index.php/Talk:Mathematica))

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Mathematica#](https://wiki.archlinux.org/index.php/Talk:Mathematica))

Related articles

*   [Scientific Applications](/index.php/Scientific_Applications "Scientific Applications")
*   [Sage-mathematics](/index.php/Sage-mathematics "Sage-mathematics")
*   [Matlab](/index.php/Matlab "Matlab")

Mathematica is a commercial program used in scientific, engineering and mathematical fields. Here we explain how to install it.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Mathematica 6](#Mathematica_6)
        *   [1.1.1 Mounting iso](#Mounting_iso)
        *   [1.1.2 Running the Installer](#Running_the_Installer)
        *   [1.1.3 Fonts](#Fonts)
        *   [1.1.4 Troubleshooting](#Troubleshooting)
    *   [1.2 Mathematica 7](#Mathematica_7)
    *   [1.3 Mathematica 8.0.4.0](#Mathematica_8.0.4.0)
    *   [1.4 Mathematica 10](#Mathematica_10)
        *   [1.4.1 HiDPI / Retina Screens](#HiDPI_.2F_Retina_Screens)
*   [2 See also](#See_also)

## Installation

### Mathematica 6

#### Mounting iso

One way to mount the Mathematica .iso is to create _/media/iso_ and add the following line to the fstab:

```
/_location/of/mathematica.iso_ /media/iso iso9660 exec,ro,user,noauto,loop=/dev/loop0   0 0

```

Now you can mount it with:

```
mount /media/iso

```

#### Running the Installer

You can start the installer by navigating to:

```
/Unix/Installer

```

Run _MathInstaller_ with:

```
sh ./MathInstaller

```

**Note:** If you do not place the "sh" in front, then you will get an error about a bad interpreter.

#### Fonts

Add the directories containing Type1 and BDF fonts to your FontPath.

#### Troubleshooting

If you have font rendering problems where certain symbols do not show up (i.e. "/" appears as a square), try uninstalling [font-mathematica](https://www.archlinux.org/packages/?name=font-mathematica).

Also, try [this](http://mathematica.stackexchange.com/questions/1158/invisible-conjugate-glyph-in-the-linux-frontend) solution.

Try having applications use anti-aliasing. For KDE: System Settings > Application Appearance > Fonts > Use anti-aliasing (Enabled)

### Mathematica 7

Mathematica 7 is much easier to install.

```
tar xf Mathematica-7.0.1.tar.gz
cd Unix/Installer
./MathInstaller

```

Follow instructions.

For KDE users, the Mathematica icon may appear in the _Lost & Found_ category. To solve this, execute the following as root:

```
# ln -s /etc/xdg/menus/applications-merged /etc/xdg/menus/kde-applications-merged

```

### Mathematica 8.0.4.0

On 64-bit machines, two known issues are present; but solutions are provided. The second issue is present on 64-bit installs: but not yet confirmed on a 32-bit arch setup.

The first issue assumes you are trying to use nVidia, CUDA and OpenCL libraries within Mathematica.

The 64-bit archlinux nVidia and opencl driver packages install libraries in `/usr/lib`, not in `/usr/lib64` as does nVidia's binary installer. This is not a problem: `/usr/lib` is the correct location for 64-bit libraries on a 64-bit arch system. However, a 64-bit install of Mathematica will assume the drivers are installed in `/usr/lib64`; other distributions that Mathematica has been tested on have their drivers in that location. The easiest method to overcome this is to make a symlink from `/usr/lib64` to `/usr/lib`. Mathematica will be able to find nVidia, CUDA, and OpenCL libraries this way without further tweaking.

A second, separate but partial solution, is to set the following environment variables:

```
export NVIDIA_DRIVER_LIBRARY_PATH=/usr/lib/libnvidia-tls.so

```

```
export CUDA_LIBRARY_PATH=/usr/lib/libcuda.so

```

This second method, however, still will not permit Mathematica to find the OpenCL libraries in `/usr/local` as Mathematica seems hardwired to find them in `/usr/lib64`.

The second issue with Mathematica 8 in 64-bit archlinux (may also affect 32-bit environments; but not tested) is a reproducible crash when performing WolframAlpha[] functions. By default, Mathematica is configured to detect the system's proxy settings when configuring how to connect to the internet to fetch data. A "bug" exists that will eventually crash Mathematica when the calling library is used. A workaround is to avoid this library call altogether by configuring Mathematica to "directly connect" to the internet. (_Edit > Preferences > Internet Connectivity > Proxy Settings_). This bug has been reported to Wolfram.

### Mathematica 10

[Install](/index.php/Install "Install") [mathematica](https://aur.archlinux.org/packages/mathematica/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR"). The _Mathematica_10.XX.YY_LINUX.sh_ installation script is required; you will need to download this separately from Wolfram.com, your university, etc. You will also need an activation key.

#### HiDPI / Retina Screens

If you have a [HiDPI](/index.php/HiDPI "HiDPI") screen, such as an Apple Retina display, and the main text in Mathematica looks small when you open it, this can be fixed:

*   Go to _Edit → Preferences_
*   From the _Advanced_ tab, click _Open Option Inspector_
*   In the tree on the right, go to _Formatting Options → Font Options → Font Properties_
*   Change the value for _"ScreenResolution"_ to double its current setting, e.g. 72 → 144\. You can also use `xdpyinfo | grep resolution` to get a more precise number (which will need to be doubled).

## See also

*   [Official site](http://www.wolfram.com/mathematica/)
*   [Official Support](http://www.wolfram.com/support/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Mathematica&oldid=412130](https://wiki.archlinux.org/index.php?title=Mathematica&oldid=412130)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Mathematics and science](/index.php/Category:Mathematics_and_science "Category:Mathematics and science")

Hidden categories:

*   [Pages flagged with Template:Stub](/index.php/Category:Pages_flagged_with_Template:Stub "Category:Pages flagged with Template:Stub")
*   [Pages or sections flagged with Template:Out of date](/index.php/Category:Pages_or_sections_flagged_with_Template:Out_of_date "Category:Pages or sections flagged with Template:Out of date")