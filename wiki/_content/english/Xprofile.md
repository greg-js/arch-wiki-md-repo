An xprofile file, `~/.xprofile` and `/etc/xprofile`, allows you to execute commands at the beginning of the X user session - before the [window manager](/index.php/Window_manager "Window manager") is started.

The xprofile file is similar in style to [xinitrc](/index.php/Xinitrc "Xinitrc").

## Compatibility

The xprofile files are natively sourced by the following display managers:

*   [GDM](/index.php/GDM "GDM") - `/etc/gdm/Xsession`
*   [KDM](/index.php/KDM "KDM") - `/usr/share/config/kdm/Xsession`
*   [LightDM](/index.php/LightDM "LightDM") - `/etc/lightdm/Xsession`
*   [LXDM](/index.php/LXDM "LXDM") - `/etc/lxdm/Xsession`
*   [SDDM](/index.php/SDDM "SDDM") - `/usr/share/sddm/scripts/Xsession`

### Sourcing xprofile from a session started with xinit

It is possible to source xprofile from a session started with one of the following programs:

*   `startx`
*   `xinit`
*   [XDM](/index.php/XDM "XDM")
*   [SLiM](/index.php/SLiM "SLiM")
*   Any other [Display manager](/index.php/Display_manager "Display manager") which uses `~/.xsession` or `~/.xinitrc`

All of these execute, directly or indirectly, `~/.xinitrc` or `/etc/X11/xinit/xinitrc` if it does not exist. That is why xprofile has to be sourced from these files.

 `~/.xinitrc and /etc/X11/xinit/xinitrc` 
```
#!/bin/sh

# Make sure this is before the 'exec' command or it won't be sourced.
[ -f /etc/xprofile ] && source /etc/xprofile
[ -f ~/.xprofile ] && source ~/.xprofile

...

```

## Configuration

Firstly, create the file `~/.xprofile` if it does not exist already. Then, simply add the commands for the programs you wish to start with the session. See below:

 `~/.xprofile` 
```
tint2 &
nm-applet &

```