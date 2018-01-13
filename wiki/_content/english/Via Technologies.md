The proprietary VIA drivers are no longer available as they are considered unstable and insecure.

## Contents

*   [1 The OpenChrome driver](#The_OpenChrome_driver)
    *   [1.1 Troubleshooting](#Troubleshooting)
        *   [1.1.1 Black screen when booting from LiveCD](#Black_screen_when_booting_from_LiveCD)
*   [2 Unichrome and OpenGL](#Unichrome_and_OpenGL)
*   [3 DPMS problems](#DPMS_problems)
*   [4 Hangup on exit](#Hangup_on_exit)
*   [5 See also](#See_also)

## The OpenChrome driver

The most advanced and developed driver for Unichromes. Supports CLE266, KM400/KN400/KM400A/P4M800, CN400/PM800/PN800/PM880, K8M800, CN700/VM800/P4M800Pro, CX700, P4M890, K8M890 and P4M900/VN896 chipsets. Accelerates 2D, 3D, Xvideo and mpeg2 decoding using [XvMC](/index.php/XvMC "XvMC"). This driver is the only way to go if you want to be on the bleeding edge.

To get the OpenChrome driver, [install](/index.php/Install "Install") the [xf86-video-openchrome](https://www.archlinux.org/packages/?name=xf86-video-openchrome) package.

The `xorg.conf` driver name is `openchrome`.

### Troubleshooting

To enable any of the following options to fix issues, first create a new file `10-openchrome.conf` in `/etc/X11/xorg.conf.d/`:

```
Section "Device"
    Identifier "*My Device Name*"
    Driver "openchrome"
EndSection

```

If your X Server shows artifacts and fails to redraw some windows, try disabling the `EnableAGPDMA` option:

```
Option     "EnableAGPDMA"               "false"

```

If your machine freeze at startup ([GDM](/index.php/GDM "GDM")) or after login ([SLiM](/index.php/SLiM "SLiM")), try adding the XAA option `XaaNoImageWriteRect`. Note that this only applies if you are using the XAA acceleration method (configured by the `AccelMethod` option). Since 0.2.906, the default acceleration method is EXA.

```
Option "XaaNoImageWriteRect"

```

If you experience significant CPU usage and low UI framerate, try adding:

```
Option "AccelMethod" "XAA"

```

#### Black screen when booting from LiveCD

If you experience a black screen when booting from Live-CD, add `modprobe.blacklist=viafb` on the [kernel command line](/index.php/Kernel_command_line "Kernel command line").

**Note:** The `nomodeset` option will probably not work here.

After installing the system you will need to [blacklist](/index.php/Blacklist "Blacklist") the `viafb` module.

## Unichrome and OpenGL

OpenGL support for Via's graphic chipsets is seriously outdated. At the moment you will not be able to run more fancy applications, games or compositing desktops like Compiz Fusion that rely on OpenGL as a backend, because the more recent OpenGL extensions are not yet supported in Unichrome 3D driver. You will be able to run simple OpenGL-applications though. The 3D driver for Unichrome is provided by the the DRI project.

Install [unichrome-dri](https://www.archlinux.org/packages/?name=unichrome-dri) and [mesa](https://www.archlinux.org/packages/?name=mesa) packages to get OpenGL to work.

## DPMS problems

If you experience problems with DPMS not turning off laptop's backlight, try adding:

```
Option "VBEModes" "true"

```

to the device section of `xorg.conf`.

## Hangup on exit

If your computer crashes when closing X, you may try not using vesa driver for kernel console. Just delete the vga stuff from kernel line on grub or append line on lilo.

## See also

*   [OpenChrome-project](http://www.freedesktop.org/wiki/Openchrome/)
*   [Unichrome-project](http://unichrome.sourceforge.net/)