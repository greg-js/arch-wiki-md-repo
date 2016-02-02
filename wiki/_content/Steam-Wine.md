# Steam/Wine

Related articles

*   [Steam](/index.php/Steam "Steam")
*   [Steam/Game-specific troubleshooting](/index.php/Steam/Game-specific_troubleshooting "Steam/Game-specific troubleshooting")

This article covers running Steam in Wine, in order to play games not available through the native Linux [Steam](/index.php/Steam "Steam").

## Contents

*   [1 Installation](#Installation)
*   [2 Starting Steam](#Starting_Steam)
*   [3 Tips](#Tips)
    *   [3.1 Performance](#Performance)
    *   [3.2 Source engine launch options](#Source_engine_launch_options)
    *   [3.3 Using a pre-existing Steam installation](#Using_a_pre-existing_Steam_installation)
    *   [3.4 Steam links in Firefox, Chrome, etc](#Steam_links_in_Firefox.2C_Chrome.2C_etc)
    *   [3.5 No text rendered problem](#No_text_rendered_problem)
    *   [3.6 Proxy settings](#Proxy_settings)
*   [4 See also](#See_also)

## Installation

Install Wine as described in [Wine](/index.php/Wine "Wine").

Install the required Microsoft fonts: [ttf-tahoma](https://aur.archlinux.org/packages/ttf-tahoma/)<sup><small>AUR</small></sup> and [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR"). You can also install these fonts through [Winetricks](/index.php/Wine#Winetricks "Wine"): `winetricks corefonts`.

**Note:** If you have access to Windows discs, you may want to install [ttf-ms-win8](https://aur.archlinux.org/packages/ttf-ms-win8/)<sup><small>AUR</small></sup> or [ttf-win7-fonts](https://aur.archlinux.org/packages/ttf-win7-fonts/)<sup><small>AUR</small></sup> instead.

Download and run the Steam installer from [steampowered.com](http://store.steampowered.com/about/). It is a `.msi` file so you have to start it with `msiexec`:

```
$ msiexec /i SteamInstall.msi

```

## Starting Steam

On x86:

```
$ wine ~/.wine/drive_c/Program\ Files/Steam/Steam.exe

```

On x86_64:

```
$ wine ~/.wine/drive_c/Program\ Files\ \(x86\)/Steam/Steam.exe

```

**Note:**

*   If text is not rendered (properly), append `-no-dwrite` to this command. See [#No text rendered problem](#No_text_rendered_problem) for more information.
*   If you are using an Nvidia card through [Bumblebee](/index.php/Bumblebee "Bumblebee"), you should prefix this command with `optirun`.

You should consider making an alias to easily start Steam (and put it in your shell's rc file), example:

```
alias steam-wine='wine ~/.wine/drive_c/Program\ Files\ \(x86\)/Steam/Steam.exe >/dev/null 2>&1 &'

```

## Tips

### Performance

Consider disabling wine debugging output by adding this to your shell rc file:

```
export WINEDEBUG=-all

```

or, just add it to your `steam-wine` alias to only disable it for Steam:

```
alias steam-wine='WINEDEBUG=-all wine ~/.wine/drive_c/Program\ Files\ \(x86\)/Steam/Steam.exe >/dev/null 2>&1 &'

```

Additionally, Source games rely on a paged pool memory size specification for audio, and WINE by default does not have this set. To set it:

```
$ wine reg add "HKLM\\System\\CurrentControlSet\\Control\\Session Manager\\Memory Management\\" /v PagedPoolSize /t REG_DWORD /d 402653184 /f

```

### Source engine launch options

Go to _Properties > Set Launch Options_, e.g.:

```
-console -dxlevel 90 -width 1280 -height 1024

```

*   `console`

	Activate the console in the application to change detailed applications settings.

*   `dxlevel`

	Set the application's DirectX level, e.g. 90 for DirectX Version 9.0\. It is recommended to use the video card's DirectX version to prevent crashes. See the official Valve Software wiki [https://developer.valvesoftware.com/wiki/DirectX_Versions](https://developer.valvesoftware.com/wiki/DirectX_Versions) for details.

*   `width` and `height`

	Set the screen resolution. In some cases the graphic settings are not saved in the application and the applications always starts in the default resolution.

Please refer to [https://developer.valvesoftware.com/wiki/Command_Line_Options](https://developer.valvesoftware.com/wiki/Command_Line_Options) for a complete list of launch options.

### Using a pre-existing Steam installation

If you have a shared drive with Windows, or already have a Steam installation somewhere else, you can simply symlink the Steam directory to `~/.wine/drive_c/Program Files/Steam/` . However, be sure to do **all** the previous steps in this wiki. Confirm Steam launches and logs into your account, _then_ do this:

```
$ cd ~/.wine/drive_c/Program\ Files/ 
$ mv Steam/ Steam.backup/   (or you can just delete the directory)
$ ln -s /mnt/windows_partition/Program\ Files/Steam/

```

**Note:**

*   If you have trouble starting Steam after symlinking the entire Steam folder, try linking only the `steamapps` subdirectory in your existing wine steam folder instead.
*   If you still have trouble starting games, use `# mount --bind /path/to/SteamApps ~/.local/share/Steam/SteamApps -ouser=your-user-name` , this is the only thing that worked with `TF2` for one Arch user.

### Steam links in Firefox, Chrome, etc

To make `steam://` urls in your browser connect with Steam in Wine, there are several things you can do. One involves making steam url-handler keys in gconf, another involves making protocol files for KDE, others involve tinkering with desktop files or the Local State file for Chromium. These seem to only work in Firefox or under certain desktop configurations. One way to do it that works more globally is using mimeo, a tool made by Xyne (an Arch TU) which follows. For another working and less invasive (but Firefox-only) way, see the first post [here](http://ubuntuforums.org/showthread.php?t=433548) .

*   Make `/usr/bin/steam` with your favorite editor and paste:

```
#!/bin/sh
#
# Steam wrapper script
#
exec wine "c:\\program files\\steam\\steam.exe" "$@"

```

*   Make it executable:

```
# chmod +x /usr/bin/steam

```

*   Install [mimeo](https://aur.archlinux.org/packages/mimeo/)<sup><small>AUR</small></sup> and [xdg-utils-mimeo](https://aur.archlinux.org/packages/xdg-utils-mimeo/)<sup><small>AUR</small></sup> from AUR. You will need to replace the existing [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) if installed. In XFCE, you will also need [xorg-utils](https://www.archlinux.org/packages/?name=xorg-utils).

*   Create `~/.config/mimeo/associations.txt` with your favorite editor and paste:

```
/usr/bin/steam %u
  ^steam://

```

*   Lastly, open `/usr/bin/xdg-open` in your favorite editor. Go to the `detectDE()` section and change it to look as follows:

```
detectDE()
{
    #if [ x"$KDE_FULL_SESSION" = x"true" ]; then DE=kde;
    #elif [ x"$GNOME_DESKTOP_SESSION_ID" != x"" ]; then DE=gnome;
    #elif $(dbus-send --print-reply --dest=org.freedesktop.DBus /org/freedesktop/DBus org.freedesktop.DBus.GetNameOwner string:org.gnome.SessionManager > /dev/null 2>&1) ; then DE=gnome;
    #elif xprop -root _DT_SAVE_MODE 2> /dev/null | grep ' = \"xfce4\"$' >/dev/null 2>&1; then DE=xfce;
    #elif [ x"$DESKTOP_SESSION" == x"LXDE" ]; then DE=lxde;
    #else DE=""
    #fi
    DE=""
}

```

*   Restart the browser and you should be good to go. In Chromium, you cannot enter a `steam://` link in the url box like you can with Firefox. The forum link above has a `steam://open/friends` link to try if needed.

**Note:**

*   If you have any problems with file associations after doing this, simply revert to regular xdg-utils and undo your changes to `/usr/bin/xdg-open`.
*   Those on other distributions that stumble upon this page, see the link above for firefox specific instructions. No easy way to get it working on Chromium on other distros exists.

### No text rendered problem

**Note:** This should no longer be an issue with Wine 1.7.50 and up since the implementation of dwrite has progressed sufficiently.

If there is no text/font rendered when starting steam you should try to start steam with the parameter `-no-dwrite`. Read more in [the forum thread about it.](https://bbs.archlinux.org/viewtopic.php?id=146223)

 `wine ~/.wine/drive_c/Program\ Files\ \(x86\)/Steam/Steam.exe -no-dwrite` 

**Note:** Although this method does currently work, It is not persistent if Steam relaunches automatically (i.e. update), or if you follow a URL link.

*   This can be achieved by going through _**winecfg > Libraries**_ and setting the **"dwrite"** override to _"disable"_

**Or**

*   `$ wine reg add 'HKCU\Software\Valve\Steam' /v DWriteEnable /t REG_DWORD /d 00000000`

### Proxy settings

Steam may use environment variables of the form `[protocol]_proxy` to determine the proxy for HTTP/HTTPS.

```
$ export http_proxy=[http://your.proxy.here:port](http://your.proxy.here:port)
$ export https_proxy=$http_proxy

```

However, it seems that it does not support sockv5.

## See also

*   [Wine Application Database](http://appdb.winehq.org/objectManager.php?sClass=version&iId=19444)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Steam/Wine&oldid=416481](https://wiki.archlinux.org/index.php?title=Steam/Wine&oldid=416481)"