# DirectFB

[DirectFB](http://directfb.org/) stands for Direct Frame Buffer. It is a software library for GNU/Linux/Unix-based operating systems with a small memory footprint that provides graphics acceleration, input device handling and abstraction layer, and integrated windowing system with support for translucent windows and multiple display layers on top of the Linux framebuffer without requiring any kernel modifications.[2] DirectFB is free software licensed under the terms of the GNU Lesser General Public License (LGPL).

## Installation

[Install](/index.php/Install "Install") the [directfb](https://www.archlinux.org/packages/?name=directfb) package. You can now also build and install DirectFB-examples which contain some example applications and some benchmarks.

### Directfb with shared application enabled

The directfb package does not enable running multiply applications on the same display. This is of cause necessary for running different windows on this display. For testing install [directfb-multi](https://aur.archlinux.org/packages/directfb-multi/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/directfb-multi)]</sup> and [linux-fusion](https://aur.archlinux.org/packages/linux-fusion/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/linux-fusion)]</sup>.

DirectFB includes an internal window manager. To move a window in the internal window manager, press the `Super` key. Sawman was the original WM but in archlinux [Sawman](https://aur.archlinux.org/packages/Sawman/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/sawman)]</sup> is now out of date for quite a long time.

## See also

*   [TLDP: Framebuffer HOWTO](http://www.tldp.org/HOWTO/Framebuffer-HOWTO/x168.html#AEN170)

Retrieved from "[https://wiki.archlinux.org/index.php?title=DirectFB&oldid=392062](https://wiki.archlinux.org/index.php?title=DirectFB&oldid=392062)"