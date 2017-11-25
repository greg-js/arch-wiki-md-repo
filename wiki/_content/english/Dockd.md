On Windows, when a user places their ThinkPad into a dock, Windows automatically recognizes that the ThinkPad has been docked and switches to the connected external monitor. On some desktops like [KDE](/index.php/KDE "KDE") this is handled automatically, but on some desktops like [Xfce](/index.php/Xfce "Xfce") or [LXDE](/index.php/LXDE "LXDE") or on lightweight window managers like [awesome](/index.php/Awesome "Awesome") or [i3](/index.php/I3 "I3") that is not the case, and usually when docking the ThinkPad nothing happens.

For this reason, [dockd](https://aur.archlinux.org/packages/dockd/) was developed.

# Installing

Install the [dockd](https://aur.archlinux.org/packages/dockd/) package.

**Note:** If your current desktop environment switches the displays automatically you do *not* need this program.

# Configuring

The daemon needs to know your current display configuration when the laptop is docked and undocked, so we need to configure the daemon first before using it.

1\. Insert your ThinkPad into the dock

2\. Configure the display layouts and resolutions using your desktop environments interface (or [xrandr](/index.php/Xrandr "Xrandr") if you use something like [i3](/index.php/I3 "I3"))

3\. Write the profile when the ThinkPad is docked

```
# sudo dockd --config docked

```

4\. Remove the ThinkPad from the dock

5\. Configure the internal panel resolution and refresh rates using your desktop environments interface (or [xrandr](/index.php/Xrandr "Xrandr") if you use something like [i3](/index.php/I3 "I3").)

6\. Write the profile when the ThinkPad is undocked

```
# sudo dockd --config undocked

```

7\. Enable [acpid](/index.php/Acpid "Acpid")

```
# sudo systemctl enable acpid
# sudo systemctl start acpid

```

8\. Log out and log back it

The daemon should now be configured and ready to use. Insert the ThinkPad into the dock and observe if the daemon switches to your external display automatically.

**Note:** If it does not switch output modes automatically, that means your system or configuration is not supported. Please, open an issue on [GitHub](https://github.com/libthinkpad/dockd) with your ThinkPad and dock model, as well as the [journalctl](/index.php/Journalctl "Journalctl") output.

**Warning:** If you change your monitor setup or resolution, you **MUST** configure the daemon again.

## See also

*   [ThinkPads.org homepage](http://thinkpads.org/)
*   [Documentation on ThinkPads.org](http://thinkpads.org/projects/dockd/)