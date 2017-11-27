Related articles

*   [Laptop/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo")

Business laptops manufactured by Lenovo and IBM under the ThinkPad brand have a proprietary connector at the bottom of the laptop that is used in junction with docking stations that enable the ThinkPad to be used as a desktop PC.

These docking stations can function in two ways:

*   Passive port replicators (no active components)
*   Active docks (active components such as USB hubs or USB 3.0 controllers)

Both of them are supported out-the-box by [GNOME](/index.php/GNOME "GNOME") and [KDE](/index.php/KDE "KDE") and should not require additional software. Otherwise use can use dockd.

## Using dockd

To handle docks outside [KDE](/index.php/KDE "KDE") and [GNOME](/index.php/GNOME "GNOME") you will need to install a dock daemon that will auto-switch the monitors. [dockd](https://aur.archlinux.org/packages/dockd/) is a dock daemon that was developed for light desktops and will auto switch the monitor configuration.

[Install](/index.php/Install "Install") the [dockd](https://aur.archlinux.org/packages/dockd/) package.

**Note:** If your current desktop environment switches the displays automatically you do *not* need this program.

**Warning:** A dependency of dockd called [libthinkpad](https://aur.archlinux.org/packages/libthinkpad/) requires [acpid](/index.php/Acpid "Acpid") to be running, so after the install of dockd do not forget to [enable](/index.php/Enable "Enable") and start acpid.

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

*   Log out and log back it

The daemon should now be configured and ready to use. Insert the ThinkPad into the dock and observe if the daemon switches to your external display automatically.

**Note:** If it does not switch output modes automatically, that means your system or configuration is not supported. Please, open an issue on [GitHub](https://github.com/libthinkpad/dockd) with your ThinkPad and dock model, as well as the [journalctl](/index.php/Journalctl "Journalctl") output.

**Warning:** If you change your monitor setup or resolution, you **MUST** configure the daemon again.

## See also

*   [dockd Documentation - ThinkPads.org](http://thinkpads.org/projects/dockd/)
*   [Docking Port - ThinkWiki](http://www.thinkwiki.org/wiki/Docking_Port)