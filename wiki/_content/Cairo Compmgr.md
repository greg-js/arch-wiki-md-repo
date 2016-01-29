# Cairo Compmgr

Related articles

*   [Xcompmgr](/index.php/Xcompmgr "Xcompmgr")
*   [Xorg](/index.php/Xorg "Xorg")

Cairo Composite Manager is a versatile and extensible [composite manager](http://en.wikipedia.org/wiki/Compositing_window_manager) which uses cairo for rendering. Plugins can be used to add some cool effects to your desktop. It's capable of, but not limited to, rendering of drop shadows, setting window transparency, menu and window animations, and applying decorations.

Like [Xcompmgr](/index.php/Xcompmgr "Xcompmgr"), it does not replace an existing window manager, which makes it ideal for users of lightweight window managers, like [Openbox](/index.php/Openbox "Openbox") and [Fluxbox](/index.php/Fluxbox "Fluxbox"), who seek a more elegant desktop.

## Installation

Install either [cairo-compmgr](https://aur.archlinux.org/packages/cairo-compmgr/)<sup><small>AUR</small></sup> or [cairo-compmgr-git](https://aur.archlinux.org/packages/cairo-compmgr-git/)<sup><small>AUR</small></sup> (for the development version).

Note that the dependency on [gconf](https://www.archlinux.org/packages/?name=gconf) can be safely removed however the dependency on [vala](https://www.archlinux.org/packages/?name=vala) cannot be removed. If you do remove the [gconf](https://www.archlinux.org/packages/?name=gconf) dependency, you also need to remove the last three lines from the `package()` function in the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

## Configuration

To start Cairo Composite Manager, simply run:

```
$ cairo-compmgr 

```

If it runs for a few seconds and then crashes taking the terminal with it, open the Cairo Composite Manager and disable the 'Freeze' plugin:

```
$ cairo-compmgr --configure

```

If it does not start at all disable the 'Clone' plugin.

To have it load every time you start X, you can add it to your `~/.xinitrc` :

```
cairo-compmgr &

```

Once started, Cairo Composite Manager installs itself in your systray and you can configure it by by right-clicking the systray icon.

If you just want Xcompmgr's behaviour, you can disable a lot of the plugins straightaway. Be patient while Cairo Composite Manager unloads a plugin, it might stall your screen for a moment.

## Additional Resources

*   [Xcompmgr](/index.php/Xcompmgr "Xcompmgr") -- A simple composite manager capable of drop shadows and primitive transparency
*   [Compiz](/index.php/Compiz "Compiz") -- A composite and window manager offering a rich 3D accelerated desktop environment
*   [Wikipedia:Compositing window manager](https://en.wikipedia.org/wiki/Compositing_window_manager "wikipedia:Compositing window manager")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Cairo_Compmgr&oldid=387949](https://wiki.archlinux.org/index.php?title=Cairo_Compmgr&oldid=387949)"