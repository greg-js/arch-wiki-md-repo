Related articles

*   [Laptop/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo")

Business laptops manufactured by Lenovo and IBM under the ThinkPad brand have a proprietary connector at the bottom of the laptop that is used in junction with docking stations that enable the ThinkPad to be used as a desktop PC.

These docking stations can function in two ways:

*   Passive port replicators (no active components)
*   Active docks (active components such as USB hubs or USB 3.0 controllers)

Both of them are supported out-the-box by [GNOME](/index.php/GNOME "GNOME") and [KDE](/index.php/KDE "KDE") and should not require additional software. Otherwise you can use dockd.

**Note:** Some modern ThinkPads with exotic [NVIDIA](/index.php/NVIDIA "NVIDIA") graphics like the Quadro M2200 might not work with dockd because the [NVIDIA](/index.php/NVIDIA "NVIDIA") driver is buggy and causes a kernel crash. See [Issue #3](https://github.com/libthinkpad/dockd/issues/3) on Github

## Contents

*   [1 Using dockd](#Using_dockd)
*   [2 Installing](#Installing)
*   [3 Dock and undock hooks](#Dock_and_undock_hooks)
*   [4 See also](#See_also)

## Using dockd

To handle docks outside [KDE](/index.php/KDE "KDE") and [GNOME](/index.php/GNOME "GNOME") you will need to install a dock daemon that will auto-switch the monitors. [dockd](https://aur.archlinux.org/packages/dockd/) is a dock daemon that was developed for light desktops and will auto switch the monitor configuration.

**Warning:** dockd is not Coreboot/Libreboot compatible.

## Installing

[Install](/index.php/Install "Install") the [dockd](https://aur.archlinux.org/packages/dockd/) package.

**Note:** If your current desktop environment switches the displays automatically you do *not* need this program.

The daemon needs to know your current display configuration when the laptop is docked and undocked, so we need to configure the daemon first before using it.

*   Insert your ThinkPad into the dock
*   Configure the display layouts and resolutions using your desktop environments interface or [xrandr](/index.php/Xrandr "Xrandr")
*   Write the profile when the ThinkPad is docked

```
# dockd --config docked

```

*   Remove the ThinkPad from the dock
*   Configure the internal panel resolution and refresh rates using your desktop environments interface or [xrandr](/index.php/Xrandr "Xrandr")
*   Write the profile when the ThinkPad is undocked

```
# dockd --config undocked

```

*   [Enable](/index.php/Enable "Enable") and start [acpid](/index.php/Acpid "Acpid")

```
# systemctl enable acpid
# systemctl start acpid

```

*   If you are using [i3](/index.php/I3 "I3"), you need to manuall autostart dockd as [i3](/index.php/I3 "I3") is not XDG Autostart compatible

 `~/.config/i3/config`  ` exec --no-startup-id dockd --daemon` 

*   Log out and log back it

The daemon should now be configured and ready to use. Insert the ThinkPad into the dock and observe if the daemon switches to your external display automatically.

**Note:** If it does not switch output modes automatically, that means your system or configuration is not supported. Please, open an issue on [GitHub](https://github.com/libthinkpad/dockd) with your ThinkPad and dock model, as well as the [journalctl](/index.php/Journalctl "Journalctl") output.

**Warning:** If you change your monitor setup or resolution, you **MUST** configure the daemon again.

## Dock and undock hooks

As of dockd 1.21, you can define some hooks that run when the ThinkPad is docked and undocked.

For example, to disable WiFi when docking and enable it when undocking:

 `/etc/dockd/dock.hook`  `nmcli radio wifi off`  `/etc/dockd/undock.hook`  `nmcli radio wifi on` 

## See also

*   [dockd Documentation - ThinkPads.org](http://thinkpads.org/projects/dockd/)
*   [Docking Port - ThinkWiki](http://www.thinkwiki.org/wiki/Docking_Port)