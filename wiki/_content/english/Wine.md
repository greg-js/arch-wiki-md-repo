Related articles

*   [CrossOver](/index.php/CrossOver "CrossOver")
*   [Wine package guidelines](/index.php/Wine_package_guidelines "Wine package guidelines")

[Wine](https://en.wikipedia.org/wiki/Wine_(software) is a *compatibility layer* capable of running Microsoft Windows applications on Unix-like operating systems. Programs running in Wine act as native programs would, without the performance/memory penalties of an emulator.

**Warning:** If you can access a file or resource with your user account, programs running in Wine can too. See [#Running Wine under a separate user account](#Running_Wine_under_a_separate_user_account) and [Security#Sandboxing applications](/index.php/Security#Sandboxing_applications "Security") for possible precautions.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 WINEPREFIX](#WINEPREFIX)
    *   [2.2 WINEARCH](#WINEARCH)
    *   [2.3 Graphics drivers](#Graphics_drivers)
    *   [2.4 Sound](#Sound)
        *   [2.4.1 MIDI support](#MIDI_support)
    *   [2.5 Other libraries](#Other_libraries)
    *   [2.6 Fonts](#Fonts)
        *   [2.6.1 Enable font smoothing](#Enable_font_smoothing)
    *   [2.7 Desktop launcher menus](#Desktop_launcher_menus)
        *   [2.7.1 Creating menu entries for Wine utilities](#Creating_menu_entries_for_Wine_utilities)
        *   [2.7.2 Removing menu entries](#Removing_menu_entries)
    *   [2.8 Appearance](#Appearance)
    *   [2.9 Printing](#Printing)
*   [3 Usage](#Usage)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Wineconsole](#Wineconsole)
    *   [4.2 Winetricks](#Winetricks)
    *   [4.3 Performance](#Performance)
        *   [4.3.1 CSMT](#CSMT)
        *   [4.3.2 Force OpenGL mode in games](#Force_OpenGL_mode_in_games)
        *   [4.3.3 DXVK](#DXVK)
        *   [4.3.4 Gallium Nine](#Gallium_Nine)
    *   [4.4 Unregister existing Wine file associations](#Unregister_existing_Wine_file_associations)
    *   [4.5 Prevent new Wine file associations](#Prevent_new_Wine_file_associations)
    *   [4.6 Execute Windows binaries with Wine implicitly](#Execute_Windows_binaries_with_Wine_implicitly)
    *   [4.7 Dual Head with different resolutions](#Dual_Head_with_different_resolutions)
    *   [4.8 Burning optical media](#Burning_optical_media)
    *   [4.9 Proper mounting of optical media images](#Proper_mounting_of_optical_media_images)
    *   [4.10 Show FPS overlay in games](#Show_FPS_overlay_in_games)
    *   [4.11 Running Wine under a separate user account](#Running_Wine_under_a_separate_user_account)
    *   [4.12 Temp directory on tmpfs](#Temp_directory_on_tmpfs)
    *   [4.13 Prevent installing Mono/Gecko](#Prevent_installing_Mono/Gecko)
    *   [4.14 Vulkan](#Vulkan)
    *   [4.15 Remove Wine file bindings](#Remove_Wine_file_bindings)
*   [5 Third-party applications](#Third-party_applications)
*   [6 See also](#See_also)

## Installation

Wine can be installed by enabling the [multilib](/index.php/Multilib "Multilib") repository and [installing](/index.php/Install "Install") the [wine](https://www.archlinux.org/packages/?name=wine) (stable) or [wine-staging](https://www.archlinux.org/packages/?name=wine-staging) (testing) package. [Wine Staging](https://wine-staging.com/) is a patched version of [Wine](https://www.winehq.org/), which contains bug fixes and features that have not been integrated into the stable branch yet. See also [#Graphics drivers](#Graphics_drivers) and [#Sound](#Sound).

Consider installing [wine_gecko](https://www.archlinux.org/packages/?name=wine_gecko) and [wine-mono](https://www.archlinux.org/packages/?name=wine-mono) for applications that depend on Internet Explorer and .NET, respectively. These packages are not strictly required as Wine will download the relevant files as needed. However, having the files downloaded in advance allows you to work off-line and makes it so Wine does not download the files for each Wine prefix needing them.

## Configuration

Configuring Wine is typically accomplished using:

*   [winecfg](https://wiki.winehq.org/Winecfg) is a GUI configuration tool for Wine, which can be started by running `winecfg`.
*   [regedit](https://wiki.winehq.org/Regedit) is Wine's registry editing tool, which can be started by running `regedit`. See WineHQ's article on [Useful Registry Keys](https://wiki.winehq.org/Useful_Registry_Keys).
*   [control](https://wiki.winehq.org/Control) is Wine's implementation of the Windows Control Panel, which can be started by running `wine control`.
*   See WineHQ's [List of Commands](https://wiki.winehq.org/List_of_Commands) for the full list.

### WINEPREFIX

By default, Wine stores its configuration files and installed Windows programs in `~/.wine`. This directory is commonly called a "Wine prefix" or "Wine bottle". It is created/updated automatically whenever you run a Windows program or one of Wine's bundled programs such as *winecfg*. The prefix directory also contains a tree which your Windows programs will see as `C:` (the C-drive).

You can override the location Wine uses for a prefix with the `WINEPREFIX` [environment variable](/index.php/Environment_variable "Environment variable"). This is useful if you want to use separate configurations for different Windows programs. The first time a program is run with a new Wine prefix, Wine will automatically create a directory with a bare C-drive and registry.

For example, if you run one program with `$ env WINEPREFIX=~/.win-a wine program-a.exe`, and another with `$ env WINEPREFIX=~/.win-b wine program-b.exe`, the two programs will each have a separate C-drive and separate registries.

**Note:** Wine prefixes are not [sandboxes](https://en.wikipedia.org/wiki/Sandbox_(computer_security) "wikipedia:Sandbox (computer security)")! Programs running under Wine can still access the rest of the system! (for example, `Z:` is mapped to `/`, regardless of the Wine prefix).

To create a default prefix without running a Windows program or other GUI tool you can use:

```
$ env WINEPREFIX=~/.customprefix wineboot -u

```

### WINEARCH

Wine will start an 64-bit environment by default. You can change this behavior using the `WINEARCH` [environment variable](/index.php/Environment_variable "Environment variable"). Rename your `~/.wine` directory and create a new Wine environment by running `$ WINEARCH=win32 winecfg`. This will get you a 32-bit Wine environment. Not setting `WINEARCH` will get you a 64-bit one.

You can combine this with `WINEPREFIX` to make a separate `win32` and `win64` environment:

```
$ WINEARCH=win32 WINEPREFIX=~/win32 winecfg
$ WINEPREFIX=~/win64 winecfg

```

You can also use `WINEARCH` in combination with other Wine programs, such as *winetricks* (using Steam as an example):

```
WINEARCH=win32 WINEPREFIX=~/.local/share/wineprefixes/steam winetricks steam

```

### Graphics drivers

You need to install the 32-bit version of your graphics driver. Please install the package that is listed in the *OpenGL (multilib)* column in the table in [Xorg#Driver installation](/index.php/Xorg#Driver_installation "Xorg").

A good sign that your drivers are inadequate or not properly configured is when Wine reports the following in your terminal window:

```
Direct rendering is disabled, most likely your OpenGL drivers have not been installed correctly

```

**Note:** You might need to restart X after having installed the correct library.

### Sound

By default sound issues may arise when running Wine applications. Ensure only one sound device is selected in *winecfg*.

*   If you want to use the [ALSA](/index.php/ALSA "ALSA") driver in Wine, you will need to install [lib32-alsa-lib](https://www.archlinux.org/packages/?name=lib32-alsa-lib) and [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins).
*   If you want to use the [PulseAudio](/index.php/PulseAudio "PulseAudio") driver in Wine, you will need to install the [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) package.
*   If you want to use the [OSS](/index.php/OSS "OSS") driver in Wine, you will need to install the [lib32-alsa-oss](https://www.archlinux.org/packages/?name=lib32-alsa-oss) package. The OSS driver in the kernel will not suffice.
*   Games that use advanced sound systems (*e.g.* TESV: Skyrim) may additionally require installations of [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal).

If *winecfg* **still** fails to detect the audio driver (Selected driver: (none)), [configure it via the registry](https://www.winehq.org/docs/wineusr-guide/using-regedit#Configuring_Sound). For example, in a case where the microphone was not working in a 32-bit Windows application on a 64-bit stock install of wine-1.9.7, this provided full access to the sound hardware (sound playback and mic): open *regedit*, look for the key HKEY_CURRENT_USER → Software → Wine → Drivers, and add a string called *Audio* and give it the value *alsa*. Also, it may help to [recreate the prefix](#WINEARCH).

#### MIDI support

[MIDI](/index.php/MIDI "MIDI") was a quite popular system for video games music in the 90's. If you are trying out old games, it is not uncommon that the music will not play out of the box. Wine has excellent MIDI support. However you first need to make it work on your host system, as explained in [MIDI](/index.php/MIDI "MIDI"). Last but not least you need to make sure Wine will use the correct MIDI output.

### Other libraries

*   Some applications (e.g. Office 2003/2007) require the MSXML library to parse HTML or XML, in such cases you need to install [lib32-libxml2](https://www.archlinux.org/packages/?name=lib32-libxml2).

*   Some applications that play music may require [lib32-mpg123](https://www.archlinux.org/packages/?name=lib32-mpg123).

*   Some applications that use a color management engine (e.g. pdf viewers, image viewers, etc) may require [lib32-lcms2](https://www.archlinux.org/packages/?name=lib32-lcms2).

*   Some applications that use native image manipulation libraries may require [lib32-giflib](https://www.archlinux.org/packages/?name=lib32-giflib) and [lib32-libpng](https://www.archlinux.org/packages/?name=lib32-libpng).

*   Some applications that require encryption support may require [lib32-gnutls](https://www.archlinux.org/packages/?name=lib32-gnutls).

*   Some applications require 32-bit video codecs or the program crashes. Install [lib32-gst-plugins-base](https://www.archlinux.org/packages/?name=lib32-gst-plugins-base), [lib32-gst-plugins-good](https://www.archlinux.org/packages/?name=lib32-gst-plugins-good), [lib32-gst-plugins-bad](https://aur.archlinux.org/packages/lib32-gst-plugins-bad/) and [lib32-gst-plugins-ugly](https://aur.archlinux.org/packages/lib32-gst-plugins-ugly/).

### Fonts

If Wine applications are not showing easily readable fonts, you may not have any fonts installed. To easily link all of the system fonts so they are accessible from wine:

```
 cd ${WINEPREFIX:-~/.wine}/drive_c/windows/Fonts && for i in /usr/share/fonts/**/*.{ttf,otf}; do ln -s "$i" ; done

```

Wine uses freetype to render fonts, and freetype's defaults changed a few releases ago. Try using this environment setting for wine programs:

```
 FREETYPE_PROPERTIES="truetype:interpreter-version=35"

```

Another possibility is to install Microsoft's Truetype fonts into your wine prefix. See [MS Fonts](/index.php/MS_Fonts "MS Fonts"). If this does not help, try running `winetricks corefonts` first, then `winetricks allfonts` as a last resort.

After running such programs, kill all Wine servers and run `winecfg`. Fonts should be legible now.

If the fonts look somehow smeared, import the following text file into the Wine registry with [regedit](https://wiki.winehq.org/FAQ#How_do_I_edit_the_Wine_registry.3F):

```
Windows Registry Editor Version 5.00
[HKEY_CURRENT_USER\Software\Wine\X11 Driver]
"ClientSideWithRender"="N"

```

For high resolution displays, you can adjust dpi values in winecfg.

See also [Font configuration#Applications without fontconfig support](/index.php/Font_configuration#Applications_without_fontconfig_support "Font configuration").

#### Enable font smoothing

A good way to improve wine font rendering is to enable cleartype font smoothing. To enable "Subpixel smoothing (ClearType) RGB":

```
cat << EOF > /tmp/fontsmoothing
REGEDIT4

[HKEY_CURRENT_USER\Control Panel\Desktop]
"FontSmoothing"="2"
"FontSmoothingOrientation"=dword:00000001
"FontSmoothingType"=dword:00000002
"FontSmoothingGamma"=dword:00000578
EOF

WINE=${WINE:-wine} WINEPREFIX=${WINEPREFIX:-$HOME/.wine} $WINE regedit /tmp/fontsmoothing 2> /dev/null
```

For more information, check [the original answer](https://askubuntu.com/a/219795/514682)

### Desktop launcher menus

When a Windows application installer creates a shortcut Wine creates a `.desktop` file instead. The default locations for those files in Arch Linux are:

*   Desktop shortcuts are put in `~/Desktop`
*   Start menu shortcuts are put in `~/.local/share/applications/wine/Programs/`

**Note:** Wine does not support installing Windows applications for all users, so it will not put `.desktop` files in `/usr/share/applications`. See WineHQ bug [11112](https://bugs.winehq.org/show_bug.cgi?id=11112)

**Tip:** If menu items were *not* created while installing software or have been lost, `wine winemenubuilder` may be of some use.

#### Creating menu entries for Wine utilities

By default, installation of Wine does not create desktop menus/icons for the software which comes with Wine (e.g. for *winecfg*, *winebrowser*, etc). These instructions will add entries for these applications.

First, install a Windows program using Wine to create the base menu. After the base menu is created, you can create the following files in `~/.local/share/applications/wine/`:

 `wine-browsedrive.desktop` 
```
[Desktop Entry]
Name=Browse C: Drive
Comment=Browse your virtual C: drive
Exec=wine winebrowser c:
Terminal=false
Type=Application
Icon=folder-wine
Categories=Wine;
```
 `wine-uninstaller.desktop` 
```
[Desktop Entry]
Name=Uninstall Wine Software
Comment=Uninstall Windows applications for Wine
Exec=wine uninstaller
Terminal=false
Type=Application
Icon=wine-uninstaller
Categories=Wine;
```
 `wine-winecfg.desktop` 
```
[Desktop Entry]
Name=Configure Wine
Comment=Change application-specific and general Wine options
Exec=winecfg
Terminal=false
Icon=wine-winecfg
Type=Application
Categories=Wine;
```

And create the following file in `~/.config/menus/applications-merged/`:

 `wine.menu` 
```
<!DOCTYPE Menu PUBLIC "-//freedesktop//DTD Menu 1.0//EN"
"http://www.freedesktop.org/standards/menu-spec/menu-1.0.dtd">
<Menu>
  <Name>Applications</Name>
  <Menu>
    <Name>wine-wine</Name>
    <Directory>wine-wine.directory</Directory>
    <Include>
      <Category>Wine</Category>
    </Include>
  </Menu>
</Menu>

```

If these settings produce a ugly/non-existent icon, it means that there are no icons for these launchers in the icon set that you have enabled. You should replace the icon settings with the explicit location of the icon that you want. Clicking the icon in the launcher's properties menu will have the same effect. A great icon set that supports these shortcuts is [GNOME-colors](http://www.gnome-look.org/content/show.php/GNOME-colors?content=82562).

#### Removing menu entries

Menu entries created by Wine are located in `~/.local/share/applications/wine/Programs/`. Remove the program's *.desktop* entry to remove the application from the menu.

In addition to remove unwanted extensions binding by Wine, execute the following commands (taken from the Wine website):

```
$ rm ~/.local/share/mime/packages/x-wine*
$ rm ~/.local/share/applications/wine-extension*
$ rm ~/.local/share/icons/hicolor/*/*/application-x-wine-extension*
$ rm ~/.local/share/mime/application/x-wine-extension*

```

### Appearance

A similar to XP looking theme can be downloaded from [here](http://download.microsoft.com/download/e/a/9/ea9af5ae-b48e-473e-85fe-dcde7472e644/ZuneDesktopTheme.msi). To install it see [here](https://wiki.winehq.org/Wine_User%27s_Guide#Running_.msi_files). Lastly use *winecfg* to select it.

### Printing

In order to use your installed printers (both local and network) with wine applications in *win32 prefixes* (e.g. MS Word), install the [lib32-libcups](https://www.archlinux.org/packages/?name=lib32-libcups) package, reboot wine (*wineboot*) and restart your wine application.

## Usage

**Warning:** Do not run or install Wine applications as root! See [Wine FAQ](https://wiki.winehq.org/FAQ#Should_I_run_Wine_as_root.3F) for details.

See [Wine FAQ](https://wiki.winehq.org/FAQ) and [Wine User's Guide](https://wiki.winehq.org/Wine_User%27s_Guide) for general information on Wine usage.

See [Wine Application Database (AppDB)](https://appdb.winehq.org/) for information on running Windows applications in Wine.

## Tips and tricks

### Wineconsole

Often you may need to run *.exe'*s to patch game files, for example a widescreen mod for an old game, and running the *.exe* normally through Wine might yield nothing happening. In this case, you can open a terminal and run the following command:

```
$ wineconsole cmd

```

Then navigate to the directory and run the *.exe* file from there.

### Winetricks

[Winetricks](https://wiki.winehq.org/Winetricks) is a script to allow one to install base requirements needed to run Windows programs. Installable components include DirectX 9.x, MSXML (required by Microsoft Office 2007 and Internet Explorer), Visual Runtime libraries and many more.

[Install](/index.php/Install "Install") the [winetricks](https://www.archlinux.org/packages/?name=winetricks) package (or alternatively [winetricks-git](https://aur.archlinux.org/packages/winetricks-git/)). Then run it with:

```
$ winetricks

```

### Performance

#### CSMT

CSMT is a technology used by Wine to use a separate thread for the OpenGL calls to improve performance noticeably. Since Wine 3.2, CSMT is enabled by default. However, CSMT support needs to be enabled manually for Wine versions lower than 3.2\. For vanilla Wine run `wine regedit` and set the DWORD value for *HKEY_CURRENT_USER -> Software > Wine > Direct3D > csmt* to 0x01 (enabled). For wine-staging run `winecfg` and enable it in the staging tab.

Note that CSMT may actually hurt performance for some applications - if this is the case, disable it by creating/setting the registry value to 0x00 (disabled).

Further information:

*   [Phoronix Forum discussion](http://www.phoronix.com/forums/showthread.php?93967-Wine-s-Big-Command-Stream-D3D-Patch-Set-Updated/page3&s=7775d7c3d4fa698089d5492bb7b1a435) with the CSMT developer Stefan Dösinger

#### Force OpenGL mode in games

Some games might have an OpenGL mode which *may* perform better than their default DirectX mode. While the steps to enable OpenGL rendering is *application specific*, many games accept the `-opengl` parameter.

```
$ wine */path/to/3d_game.exe* -opengl

```

You should of course refer to your application's documentation and Wine's [AppDB](http://appdb.winehq.org) for such application specific information.

#### DXVK

[DXVK](https://github.com/doitsujin/dxvk) is a promising new implementation for DirectX 10 and DirectX 11 over Vulkan. This should allow for greater performance, and in some cases, even better compatibility. Battlefield 1 for example, only runs under DXVK. On the other hand, DXVK does not support all Wine games (yet).

To use it, install [dxvk-bin](https://aur.archlinux.org/packages/dxvk-bin/) for official binaries, or [dxvk-git](https://aur.archlinux.org/packages/dxvk-git/) for the development version. Then run the following command to activate it in your Wineprefix (by default `~/.wine`):

```
$ WINEPREFIX=*your-prefix* setup_dxvk64

```

Use `setup_dxvk32` for 32-bit applications.

**Note:** For Wine versions below 3.5 you need to configure Vulkan support manually, following the instructions at [GitHub](https://github.com/roderickc/wine-vulkan). [wine](https://www.archlinux.org/packages/?name=wine) and [wine-staging](https://www.archlinux.org/packages/?name=wine-staging) work out of the box.

**Warning:** DXVK overrides the DirectX 10 and 11 DLLs, which may be considered cheating in online multiplayer games, and may get your account **banned**. Use at your own risk!

#### Gallium Nine

With the open-source gallium-based drivers (mostly AMD cards) there is a [Gallium Direct3D state tracker](https://wiki.ixit.cz/d3d9) that aims to provide nearly-native performance for DirectX 9\. In most cases it has less visual glitches than the upstream wine and doubles the performances. It consumes much less CPU time than CSMT.

To use it, install [wine-nine](https://www.archlinux.org/packages/?name=wine-nine). This is a standalone package that can be installed with any wine version.

### Unregister existing Wine file associations

By default, Wine takes over as the default application for a lot of formats. Some (e.g. `vbs` or `chm`) are Windows-specific, and opening them with Wine can be a convenience. However, having other formats (e.g. `gif`, `jpeg`, `txt`, `js`) open in Wine's bare-bones simulations of Internet Explorer and Notepad can be annoying.

Wine's file associations are set in `~/.local/share/applications/` as `wine-extension-*extension*.desktop` files. Delete the files corresponding to the extensions you want to unregister. Or, to remove all wine extensions:

```
$ rm -f ~/.local/share/applications/wine-extension*.desktop
$ rm -f ~/.local/share/icons/hicolor/*/*/application-x-wine-extension*

```

Next, remove the old cache:

```
$ rm -f ~/.local/share/applications/mimeinfo.cache
$ rm -f ~/.local/share/mime/packages/x-wine*
$ rm -f ~/.local/share/mime/application/x-wine-extension*

```

And, update the cache:

```
$ update-desktop-database ~/.local/share/applications
$ update-mime-database ~/.local/share/mime/

```

Alternatively you can delete all wine related stuff:

```
$ find ~/.local/share -name "*wine*" | xargs -I '{}' --no-run-if-empty rm -r '{}'

```

And update the cache as above.

Please note Wine will still create new file associations and even recreate the file associations if the application sets the file associations again.

### Prevent new Wine file associations

Prevent wine from creating any file associations by editing the registry:

 `associations.reg` 
```
Windows Registry Editor Version 5.00
[HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServices]
"winemenubuilder"="C:\\windows\\system32\\winemenubuilder.exe -r"
```

Add this to your Wine registry, by running `wine regedit associations.reg`, or alternatively by running `wine regedit` and importing it from the menu in *Registry > Import Registry File*.

This has to be done for each WINEPREFIX which should not update file associations.

You can disable winemenubuilder for all WINEPREFIXes by setting an environment variable:

```
$ export WINEDLLOVERRIDES="winemenubuilder.exe=d"

```

### Execute Windows binaries with Wine implicitly

The [wine](https://www.archlinux.org/packages/?name=wine) package installs a *binfmt* file which will allow you to run Windows programs directly, e.g. `*./myprogram.exe*` will launch as if you had typed `wine *./myprogram.exe*`. All you have to do in order to use this is to [start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") `systemd-binfmt.service`.

**Note:** Make sure the Windows binary is executable, otherwise the binary will not be executed: e.g. run `chmod +x *windows-binary*`.

### Dual Head with different resolutions

If you have issues with dual-head setups and different display resolutions you are probably missing [lib32-libxrandr](https://www.archlinux.org/packages/?name=lib32-libxrandr).

Also installing [lib32-libxinerama](https://www.archlinux.org/packages/?name=lib32-libxinerama) might fix dual-head issues with wine (for example, unclickable buttons and menus of application in the right most or bottom most monitor, not redrawable interface of application in that zone, dragging mouse cursor state stucked after leaving application area).

### Burning optical media

To burn CDs or DVDs, you will need to load the `sg` [kernel module](/index.php/Kernel_module "Kernel module").

### Proper mounting of optical media images

Some applications will check for the optical media to be in drive. They may check for data only, in which case it might be enough to configure the corresponding path as being a CD-ROM drive in *winecfg*. However, other applications will look for a media name and/or a serial number, in which case the image has to be mounted with these special properties.

Some virtual drive tools do not handle these metadata, like fuse-based virtual drives (Acetoneiso for instance). CDEmu will handle it correctly.

### Show FPS overlay in games

Wine features an embedded FPS monitor which works for all graphical applications if the environment variable `WINEDEBUG=fps` is set. This will output the framerate to stdout. You can display the FPS on top of the window thanks to `osd_cat` from the [xosd](https://www.archlinux.org/packages/?name=xosd) package. See [winefps.sh](https://gist.github.com/anonymous/844aefd70bb50bf72b35) for a helper script.

### Running Wine under a separate user account

It may be desirable to run Wine under a specifically created user account in order to reduce concerns about Windows applications having access to your home directory.

First, create a [user account](/index.php/User_account "User account") for Wine:

```
# useradd -m -s /bin/bash wineuser

```

Now switch to another TTY and start your X WM or DE as you normally would or keep reading...

**Note:** The following approach only works when enabling root for Xorg. See [Xorg#Rootless Xorg](/index.php/Xorg#Rootless_Xorg "Xorg") for more information.

Afterwards, in order to open Wine applications using this new user account you need to add the new user to the X server permissions list:

```
$ xhost +SI:localuser:wineuser

```

Finally, you can run Wine via the following command, which uses `env` to launch Wine with the environment variables it expects:

```
$ sudo -u wineuser env HOME=/home/wineuser USER=wineuser USERNAME=wineuser LOGNAME=wineuser wine *arguments*

```

It is possible to automate the process of running Windows applications with Wine via this method by using a shell script as follows:

 `/usr/local/bin/runaswine` 
```
#!/bin/bash
xhost +SI:localuser:wineuser
sudo -u wineuser env HOME=/home/wineuser USER=wineuser USERNAME=wineuser LOGNAME=wineuser wine "$@"
```

Wine applications can then be launched via:

```
$ runaswine *"C:\path\to\application.exe"*

```

In order to not be asked for a password each time Wine is run as another user the following entry can be added to the sudoers file: `*mainuser* ALL=(wineuser) NOPASSWD: ALL`. See [Sudo#Configuration](/index.php/Sudo#Configuration "Sudo") for more information.

It is recommended to run `winecfg` as the Wine user and remove all bindings for directories outside the home directory of the Wine user in the "Desktop Integration" section of the configuration window so no program run with Wine has read access to any file outside the special user's home directory.

Keep in mind that audio will probably be non-functional in Wine programs which are run this way if [PulseAudio](/index.php/PulseAudio "PulseAudio") is used. See [PulseAudio/Examples#Allowing multiple users to use PulseAudio at the same time](/index.php/PulseAudio/Examples#Allowing_multiple_users_to_use_PulseAudio_at_the_same_time "PulseAudio/Examples") for information about allowing the Wine user to access the PulseAudio daemon of the principal user.

### Temp directory on tmpfs

To prevent Wine from writing its temporary files to a physical disk, one can define an alternative location, like *tmpfs*. Remove Wine's default directory for temporary files and creating a symlink:

```
$ rm -r ~/.wine/drive_c/users/$USER/Temp
$ ln -s /tmp/ ~/.wine/drive_c/users/$USER/Temp

```

### Prevent installing Mono/Gecko

If Gecko and/or Mono are not present on the system nor in the Wine prefix, Wine will prompt to download them from the internet. If you do not need Gecko and/or Mono, you might want to disable this dialog, by setting the `WINEDLLOVERRIDES` [environment variable](/index.php/Environment_variable "Environment variable") to `mscoree=d;mshtml=d`.

### Vulkan

Vulkan support is included, since Wine 3.3\. The default Wine Vulkan ICD loader works fine for most applications, but does not support advanced features, like Vulkan layers. To use these features, you have to install the official Vulkan SDK, see step 2-4 on the original Vulkan patches author's [GitHub page](https://github.com/roderickc/wine-vulkan).

**Note:** The Wine ICD loader was added in Wine 3.5, you need to install the official Vulkan SDK to use Vulkan in Wine 3.3 and 3.4

### Remove Wine file bindings

For security reasons it may be useful to remove the preinstalled Wine bindings so Windows applications can't be launched directly from a file manager or from the browser (Firefox offers to open EXE files directly with Wine!). If you want to do this, you may add the following to the `[options]` section in `/etc/pacman.conf`

```
NoExtract = usr/lib/binfmt.d/wine.conf
NoExtract = usr/share/applications/wine.desktop

```

## Third-party applications

These have their own communities and websites, and are **not supported** by greater Wine community. See [Wine Wiki](https://wiki.winehq.org/Third_Party_Applications) for more details.

*   **[CrossOver](/index.php/CrossOver "CrossOver")** — Paid, commercialized version of Wine which provides more comprehensive end-user support.

	[crossover](https://aur.archlinux.org/packages/crossover/) || [https://www.codeweavers.com/](https://www.codeweavers.com/)

*   **exe-thumbnailer** — Generates thumbnails for Windows executable files (.exe, .lnk, .msi, and .dll).

	[exe-thumbnailer](https://aur.archlinux.org/packages/exe-thumbnailer/) || [https://github.com/exe-thumbnailer/exe-thumbnailer](https://github.com/exe-thumbnailer/exe-thumbnailer)

*   **Lutris** — Gaming launcher for all types of games, including Wine games (with prefix management), native Linux games and emulators.

	[lutris](https://www.archlinux.org/packages/?name=lutris) || [https://lutris.net/](https://lutris.net/)

*   **PlayOnLinux** — Graphical prefix manager for Wine. Contains scripts to assist with program installation and configuration.

	[playonlinux](https://www.archlinux.org/packages/?name=playonlinux) || [https://www.playonlinux.com/](https://www.playonlinux.com/)

*   **PyWinery** — Simple graphical prefix manager for Wine.

	[pywinery](https://aur.archlinux.org/packages/pywinery/) || [https://github.com/ergoithz/pywinery](https://github.com/ergoithz/pywinery)

*   **Q4Wine** — Graphical prefix manager for Wine. Can export [Qt](/index.php/Qt "Qt") themes into the Wine configuration for better integration.

	[q4wine](https://aur.archlinux.org/packages/q4wine/) || [https://sourceforge.net/projects/q4wine/](https://sourceforge.net/projects/q4wine/)

## See also

*   [Wine Homepage](https://www.winehq.org/)
*   [Wine Wiki](https://wiki.winehq.org/)
*   [Wine Application Database (AppDB)](https://appdb.winehq.org/) - Information about running specific Windows applications (Known issues, ratings, guides, etc tailored to specific applications)
*   [Wine Forums](https://forum.winehq.org/) - A great place to ask questions *after* you have looked through the FAQ and AppDB
*   [Wine - Gentoo Wiki](https://wiki.gentoo.org/wiki/Wine)