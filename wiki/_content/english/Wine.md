[Wine](https://en.wikipedia.org/wiki/Wine_(software) is a *compatibility layer* capable of running Microsoft Windows applications on Unix-like operating systems. Programs running in Wine act as native programs would, without the performance/memory penalties of an emulator. See the [official project home](http://www.winehq.org/) and [wiki](https://wiki.winehq.org/) pages for longer introduction.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 WINEPREFIX](#WINEPREFIX)
    *   [2.2 WINEARCH](#WINEARCH)
    *   [2.3 Graphics drivers](#Graphics_drivers)
    *   [2.4 Sound](#Sound)
        *   [2.4.1 MIDI support](#MIDI_support)
    *   [2.5 Other libraries](#Other_libraries)
    *   [2.6 Fonts](#Fonts)
    *   [2.7 Desktop launcher menus](#Desktop_launcher_menus)
        *   [2.7.1 Creating menu entries for Wine utilities](#Creating_menu_entries_for_Wine_utilities)
        *   [2.7.2 Removing menu entries](#Removing_menu_entries)
*   [3 Using Windows applications](#Using_Windows_applications)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Wineconsole](#Wineconsole)
    *   [4.2 Winetricks](#Winetricks)
    *   [4.3 CSMT patch](#CSMT_patch)
    *   [4.4 Unregister Wine file associations](#Unregister_Wine_file_associations)
    *   [4.5 Dual Head with different resolutions](#Dual_Head_with_different_resolutions)
    *   [4.6 exe-thumbnailer](#exe-thumbnailer)
    *   [4.7 Changing the language](#Changing_the_language)
    *   [4.8 Using Wine as an interpreter for Win16/Win32 binaries](#Using_Wine_as_an_interpreter_for_Win16.2FWin32_binaries)
    *   [4.9 16-bit programs](#16-bit_programs)
    *   [4.10 Burning optical media](#Burning_optical_media)
    *   [4.11 Proper mounting of optical media images](#Proper_mounting_of_optical_media_images)
    *   [4.12 Force OpenGL mode in games](#Force_OpenGL_mode_in_games)
    *   [4.13 Show FPS overlay in games](#Show_FPS_overlay_in_games)
    *   [4.14 Installing .NET Framework 4.0](#Installing_.NET_Framework_4.0)
    *   [4.15 Installing Microsoft Office](#Installing_Microsoft_Office)
        *   [4.15.1 Office 2010](#Office_2010)
        *   [4.15.2 Office 2013](#Office_2013)
        *   [4.15.3 Office 2016](#Office_2016)
*   [5 Third-party interfaces](#Third-party_interfaces)
    *   [5.1 CrossOver](#CrossOver)
    *   [5.2 PlayOnLinux/PlayOnMac](#PlayOnLinux.2FPlayOnMac)
    *   [5.3 PyWinery](#PyWinery)
    *   [5.4 Q4wine](#Q4wine)
    *   [5.5 Wine-staging](#Wine-staging)
*   [6 See also](#See_also)

## Installation

**Warning:** If you can access a file or resource with your user account, programs running in Wine can too. Wine prefixes are **not** [sandboxes](https://en.wikipedia.org/wiki/Sandbox_(computer_security) "wikipedia:Sandbox (computer security)"). Consider using [virtualization](https://en.wikipedia.org/wiki/Virtualization "wikipedia:Virtualization") if security is important.

Wine can be [installed](/index.php/Pacman "Pacman") with the package [wine](https://www.archlinux.org/packages/?name=wine), available in the [official repositories](/index.php/Official_repositories "Official repositories"). If you are running a 64-bit system, you will need to enable the [Multilib](/index.php/Multilib "Multilib") repository first. See also [#Sound](#Sound).

You may also want to install [wine_gecko](https://www.archlinux.org/packages/?name=wine_gecko) and [wine-mono](https://www.archlinux.org/packages/?name=wine-mono) for applications that need support for Internet Explorer and .NET, respectively. These packages are not strictly required as Wine will download the relevant files as needed. However, having the files downloaded in advance allows you to work off-line and makes it so Wine does not download the files for each Wine prefix needing them.

**Architectural differences**

Wine by default is 32-bit, as is the i686 Arch package. As such, it is unable to execute any 64-bit Windows applications.

The x86_64 Arch package, however, is built with `--enable-win64`. This activates the Wine version of [WoW64](https://en.wikipedia.org/wiki/WoW64 "wikipedia:WoW64").

*   In Windows, this complicated subsystem allows the user to use 32-bit and 64-bit Windows programs concurrently and even in the same directory.
*   In Wine, some 32-bit programs do not work properly in a 64-bit prefix. In that case the user will have to make separate directories/prefixes. See the [Wine FAQ](https://wiki.winehq.org/FAQ#How_do_I_create_a_32_bit_wineprefix_on_a_64_bit_system.3F) for specific information on this.

If you run into problems with `winetricks` or programs with a 64-bit environment, try creating a new 32-bit `WINEPREFIX`. See below: [#WINEARCH](#WINEARCH). Using the x86_64 Wine package with `WINEARCH=win32` should have the same behaviour as using the i686 Wine package.

## Configuration

Configuring Wine is typically accomplished using:

*   [winecfg](https://wiki.winehq.org/Winecfg) is a GUI configuration tool for Wine. You can run it from a console window with: `$ wine winecfg`, or `$ WINEPREFIX=~/.some_prefix wine winecfg`.
*   `control.exe` is Wine's implementation of Windows' Control Panel which can be accessed with: `$ wine control`.
*   [regedit](https://wiki.winehq.org/FAQ#How_do_I_edit_the_Wine_registry.3F) is Wine's registry editing tool. If *winecfg* and the Control Panel are not enough, see WineHQ's article on [Useful Registry Keys](https://wiki.winehq.org/Useful_Registry_Keys).
*   See WineHQ's [List of Commands](https://wiki.winehq.org/List_of_Commands) for the full list.

### WINEPREFIX

By default, Wine stores its configuration files and installed Windows programs in `~/.wine`. This directory is commonly called a "Wine prefix" or "Wine bottle". It is created/updated automatically whenever you run a Windows program or one of Wine's bundled programs such as *winecfg*. The prefix directory also contains a tree which your Windows programs will see as `C:` (the C-drive).

You can override the location Wine uses for a prefix with the `WINEPREFIX` environment variable. This is useful if you want to use separate configurations for different Windows programs. The first time a program is run with a new Wine prefix, Wine will automatically create a directory with a bare C-drive and registry.

For example, if you run one program with `$ env WINEPREFIX=~/.win-a wine program-a.exe`, and another with `$ env WINEPREFIX=~/.win-b wine program-b.exe`, the two programs will each have a separate C-drive and separate registries.

**Note:** Wine prefixes are not [sandboxes](https://en.wikipedia.org/wiki/Sandbox_(computer_security) "wikipedia:Sandbox (computer security)")! Programs running under Wine can still access the rest of the system! (for example, `Z:` is mapped to `/`, regardless of the Wine prefix).

To create a default prefix without running a Windows program or other GUI tool you can use:

```
$ env WINEPREFIX=~/.customprefix wineboot -u

```

### WINEARCH

If you have a 64-bit system, Wine will start an 64-bit environment by default. You can change this behavior using the `WINEARCH` environment variable. Rename your `~/.wine` directory and create a new Wine environment by running `$ WINEARCH=win32 winecfg`. This will get you a 32-bit Wine environment. Not setting `WINEARCH` will get you a 64-bit one.

You can combine this with `WINEPREFIX` to make a separate `win32` and `win64` environment:

```
$ WINEARCH=win32 WINEPREFIX=~/win32 winecfg
$ WINEPREFIX=~/win64 winecfg

```

**Note:** During prefix creation, the 64-bit version of Wine treats all folders as 64-bit prefixes and will not create a 32-bit in any existing folder. To create a 32-bit prefix you have to let Wine create the folder specified in `WINEPREFIX`. See WineHQ bug [29661](https://bugs.winehq.org/show_bug.cgi?id=29661)

You can also use `WINEARCH` in combination with other Wine programs, such as *winetricks* (using Steam as an example):

```
WINEARCH=win32 WINEPREFIX=~/.local/share/wineprefixes/steam winetricks steam

```

To have them permanently defined for [bash configuration ~/.bashrc](/index.php/Bash#Shell_and_environment_variables "Bash") do:

```
export WINEPREFIX=$HOME/.config/wine/
export WINEARCH=win32

```

### Graphics drivers

For most games, Wine requires high performance accelerated graphics drivers. This likely means using proprietary [NVIDIA](/index.php/NVIDIA "NVIDIA") or [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") drivers, although the open source [ATI](/index.php/ATI "ATI") driver is increasingly become proficient for use with Wine. [Intel](/index.php/Intel "Intel") drivers should mostly work as well as they are going to out of the box.

A good sign that your drivers are inadequate or not properly configured is when Wine reports the following in your terminal window:

```
Direct rendering is disabled, most likely your OpenGL drivers have not been installed correctly

```

For 64-bit systems, additional [multilib](/index.php/Multilib "Multilib") packages are required. Please install the one that is listed in the *Multilib Package* column in the table in [Xorg#Driver installation](/index.php/Xorg#Driver_installation "Xorg").

**Note:** You might need to restart X after having installed the correct library.

### Sound

By default sound issues may arise when running Wine applications. Ensure only one sound device is selected in *winecfg*. Currently, the [Alsa](/index.php/Alsa "Alsa") driver is the best supported.

*   If you want to use the [ALSA](/index.php/ALSA "ALSA") driver in Wine on a 64-bit system, you will need to install [lib32-alsa-lib](https://www.archlinux.org/packages/?name=lib32-alsa-lib) and [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins).
*   If you want to use the [PulseAudio](/index.php/PulseAudio "PulseAudio") driver in Wine, you will need to install the [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) package.
*   If you want to use the [OSS](/index.php/OSS "OSS") driver in Wine, you will need to install the [lib32-alsa-oss](https://www.archlinux.org/packages/?name=lib32-alsa-oss) package. The OSS driver in the kernel will not suffice.

If *winecfg* **still** fails to detect the audio driver (Selected driver: (none)), [configure it via the registry](http://wine-wiki.org/index.php/Wine_Registry#Configuring_Sound). Also, if you are using a 64-bit Arch, it may help to [recreate the prefix](/index.php/Wine#WINEARCH "Wine")

Games that use advanced sound systems may require installations of [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal).

#### MIDI support

[MIDI](/index.php/MIDI "MIDI") was a quite popular system for video games music in the 90's. If you are trying out old games, it is not uncommon that the music will not play out of the box. Wine has excellent MIDI support. However you first need to make it work on your host system, as explained in [MIDI](/index.php/MIDI "MIDI"). Last but not least you need to make sure Wine will use the correct MIDI output.

### Other libraries

*   Some applications (e.g. Office 2003/2007) require the MSXML library to parse HTML or XML, in such cases you need to install [lib32-libxml2](https://www.archlinux.org/packages/?name=lib32-libxml2).

*   Some applications that play music may require [lib32-mpg123](https://www.archlinux.org/packages/?name=lib32-mpg123).

*   Some applications that use a color management engine (e.g. pdf viewers, image viewers, etc) may require [lib32-lcms2](https://www.archlinux.org/packages/?name=lib32-lcms2).

*   Some applications that use native image manipulation libraries may require [lib32-giflib](https://www.archlinux.org/packages/?name=lib32-giflib) and [lib32-libpng](https://www.archlinux.org/packages/?name=lib32-libpng).

*   Some applications that require encryption support may require [lib32-gnutls](https://www.archlinux.org/packages/?name=lib32-gnutls).

### Fonts

If Wine applications are not showing easily readable fonts, you may not have Microsoft's Truetype fonts installed. See [MS Fonts](/index.php/MS_Fonts "MS Fonts"). If this does not help, try running `winetricks corefonts` first, then `winetricks allfonts` as a last resort.

After running such programs, kill all Wine servers and run `winecfg`. Fonts should be legible now.

If the fonts look somehow smeared, import the following text file into the Wine registry with [regedit](https://wiki.winehq.org/FAQ#How_do_I_edit_the_Wine_registry.3F):

```
[HKEY_CURRENT_USER\Software\Wine\X11 Driver]
"ClientSideWithRender"="N"

```

See also [Font configuration#Applications without fontconfig support](/index.php/Font_configuration#Applications_without_fontconfig_support "Font configuration").

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

## Using Windows applications

**Warning:** Do not run or install Wine applications as root! See [Running Wine as root](https://wiki.winehq.org/FAQ#run_as_root) for the official statement.

See [Installing Windows Applications](https://wiki.winehq.org/FAQ#Installing_Windows_Applications) at WineHQ. See [#Desktop launcher menus](#Desktop_launcher_menus) for information on where the shortcuts were created.

See [Running applications](https://wiki.winehq.org/FAQ#Running_applications) at WineHQ. The `.desktop` files created by the installer should automatically appear as entries in any X menu or file manager applications. They can also be examined to determine what command to use to run the application from a terminal.

See [How do I uninstall Windows applications?](https://wiki.winehq.org/FAQ#How_do_I_uninstall_Windows_applications.3F) at WineHQ.

## Tips and tricks

**Tip:** In addition to the links provided in the beginning of the article the following may be of interest:

*   [The Wine Application Database (AppDB)](http://appdb.winehq.org/) - Information about running specific Windows applications (Known issues, ratings, guides, etc tailored to specific applications)
*   [The WineHQ Forums](http://forum.winehq.org/) - A great place to ask questions *after* you have looked through the FAQ and AppDB

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

### CSMT patch

Since 2013 Wine developers have been experimenting with [stream/worker thread optimizations](http://www.winehq.org/pipermail/wine-devel/2013-September/101106.html). You may experience an enormous performance improvement by using this experimental patched Wine versions. Many games may run as fast as on Windows or even faster. This Wine patch is known as CSMT patch and works with NVidia and AMD graphics cards.

[Wine-staging](http://www.wine-staging.com/) includes CSMT support, and can be installed with the [wine-staging](https://www.archlinux.org/packages/?name=wine-staging) package.

CSMT support needs to be enabled before it can be used, instructions can be found [here](https://github.com/wine-compholio/wine-staging/wiki/CSMT#enabledisable-csmt), no further configuration is needed.

Further information:

*   [Phoronix Forum discussion](http://www.phoronix.com/forums/showthread.php?93967-Wine-s-Big-Command-Stream-D3D-Patch-Set-Updated/page3&s=7775d7c3d4fa698089d5492bb7b1a435) with the CSMT developer Stefan Dösinger
*   [Here](https://www.youtube.com/playlist?list=PL0P2a_sII2eTd8uq-azTNpQjiFLqBhDjg) you find some game videos running with CSMT enabled

### Unregister Wine file associations

By default, Wine takes over as the default application for a lot of formats. Some (e.g. `vbs` or `chm`) are Windows-specific, and opening them with Wine can be a convenience. However, having other formats (e.g. `gif`, `jpeg`, `txt`, `js`) open in Wine's bare-bones simulations of Internet Explorer and Notepad can be annoying.

Wine's file associations are set in `~/.local/share/applications/` as `wine-extension-{extension}.desktop` files. Delete the files corresponding to the extensions you want to unregister. Or, to remove all wine extensions:

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
$ find ~/.local/share | grep wine | xargs rm

```

And update the cache as above.

Please note Wine will still create new file associations and even recreate the file associations if the application sets the file associations again.

To prevent this, edit your `$WINEPREFIX/system.reg` file, Search for `winemenubuilder` and remove `-a`, so you'll get:

 `$WINEPREFIX/system.reg` 
```
[Software\\Microsoft\\Windows\\CurrentVersion\\RunServices]
"winemenubuilder"="C:\\windows\\system32\\winemenubuilder.exe -r"
```

This has to be done for each WINEPREFIX which should not update file associations.

You can disable winemenubuilder for all WINEPREFIXes by setting an environment variable:

```
$ export WINEDLLOVERRIDES="winemenubuilder.exe=d"

```

### Dual Head with different resolutions

If you have issues with dual-head setups and different display resolutions you are probably missing [lib32-libxrandr](https://www.archlinux.org/packages/?name=lib32-libxrandr).

Also installing [lib32-libxinerama](https://www.archlinux.org/packages/?name=lib32-libxinerama) might fix dual-head issues with wine.

### exe-thumbnailer

This is a small piece of UI code meant to be installed with (or even before) Wine. It provides thumbnails for executable files that show the embedded icons when available, and also gives the user a hint that Wine will be used to open it. Install it with the [gnome-exe-thumbnailer](https://aur.archlinux.org/packages/gnome-exe-thumbnailer/) package.

### Changing the language

Some programs may not offer a language selection, they will guess the desired language upon the sytem locales. Wine will transfer the current environment (including the locales) to the application, so it should work out of the box. If you want to force a program to run in a specific locale (which is fully [generated](/index.php/Locale "Locale") on your system), you can call Wine with the following setting:

```
$ LC_ALL=*xx_XX.encoding* wine */path/to/program*

```

For instance

```
$ LC_ALL=it_IT.UTF-8 wine */path/to/program*

```

### Using Wine as an interpreter for Win16/Win32 binaries

It is also possible to tell the kernel to use Wine as an interpreter for all Win16/Win32 binaries:

```
# echo ':DOSWin:M::MZ::/usr/bin/wine:' > /proc/sys/fs/binfmt_misc/register

```

To make the setting permanent, create the `/etc/binfmt.d/wine.conf` file with the following content:

 `/etc/binfmt.d/wine.conf` 
```
# Start WINE on Windows executables
:DOSWin:M::MZ::/usr/bin/wine:
```

[systemd](/index.php/Systemd "Systemd") automatically mounts the `/proc/sys/fs/binfmt_misc` filesystem using `proc-sys-fs-binfmt_misc.mount` (and automount) and runs the `systemd-binfmt.service` to load your settings.

Try it out by running a Windows program:

```
$ chmod +x *exefile.exe*
$ ./*exefile.exe*

```

If all went well, *exefile.exe* should run.

### 16-bit programs

Upon running older Windows 9x programs, the following error may be encountered:

```
modify_ldt: Invalid argument
err:winediag:build_module Failed to create module for "krnl386.exe",
16-bit LDT support may be missing.
err:module:attach_process_dlls "krnl386.exe16" failed to initialize,
aborting

```

In this case, running the following may fix it:

```
# echo 1 > /proc/sys/abi/ldt16

```

Source: [Fedora Mailing List](http://www.spinics.net/linux/fedora/fedora-users/msg450821.html)

### Burning optical media

To burn CDs or DVDs, you will need to load the `sg` [kernel module](/index.php/Kernel_module "Kernel module").

### Proper mounting of optical media images

Some applications will check for the optical media to be in drive. They may check for data only, in which case it might be enough to configure the corresponding path as being a CD-ROM drive in *winecfg*. However, other applications will look for a media name and/or a serial number, in which case the image has to be mounted with these special properties.

Some virtual drive tools do not handle these metadata, like fuse-based virtual drives (Acetoneiso for instance). CDEmu will handle it correctly.

### Force OpenGL mode in games

Many games have an OpenGL mode which *may* perform better than their default DirectX mode. While the steps to enable OpenGL rendering is *application specific*, many games accept the `-opengl` parameter.

```
$ wine /path/to/3d_game.exe -opengl

```

You should of course refer to your application's documentation and Wine's [AppDB](http://appdb.winehq.org) for such application specific information.

### Show FPS overlay in games

Wine features an embedded FPS monitor which works for all graphical applications if the environment variable `WINEDEBUG=fps` is set. This will output the framerate to stdout. You can display the FPS on top of the window thanks to `osd_cat` from the [xosd](https://www.archlinux.org/packages/?name=xosd) package. See [winefps.sh](https://gist.github.com/anonymous/844aefd70bb50bf72b35) for a helper script.

### Installing .NET Framework 4.0

First create a new 32-bit Wine prefix if you are on a 64-bit system.

```
$ WINEARCH=win32 WINEPREFIX=~/win32 winecfg

```

Then install the following packages using winetricks

```
$ WINEARCH=win32 WINEPREFIX=~/win32 winetricks -q msxml3 dotnet40 corefonts

```

### Installing Microsoft Office

#### Office 2010

Microsoft Office 2010 works without any problems (tested with Microsoft Office Home and Student 2010, Wine 1.7.5; Microsoft Office Professional Plus 2010, Wine 1.7.51). Activation over Internet also works.

Start by installing [wine-mono](https://www.archlinux.org/packages/?name=wine-mono), [wine_gecko](https://www.archlinux.org/packages/?name=wine_gecko), [samba](https://www.archlinux.org/packages/?name=samba), [lib32-libxslt](https://www.archlinux.org/packages/?name=lib32-libxslt) and [lib32-libxml2](https://www.archlinux.org/packages/?name=lib32-libxml2).

Proceed with launching the installer:

```
$ export WINEPREFIX=~/.wine # Wine prefix to use
$ export WINEARCH=win32
$ wine /path/to/office_cd/setup.exe

```

If you do not want to setup Office in the default Wine prefix (`~/.wine`), create new one as described in [#WINEPREFIX](#WINEPREFIX) section. You could also put the above exports into your shell initialization script as also noted there.

Once installation has completed, open Word or Excel to activate over the Internet. After activation run *winecfg* and set `riched20` (under libraries) to `(native,builtin)`. This will enable PowerPoint to work and makes the drop-down list of countries visible for phone activation.

For OneNote to work, run `winetricks wininet` and then make sure that `wininet` is set to `(native,builtin)`

For additional info, see the [WineHQ](http://appdb.winehq.org/appview.php?iVersionId=4992) article.

As an alternative to the above method, [playonlinux](https://www.archlinux.org/packages/?name=playonlinux) provides custom installer scripts that make the installation of Office 2003, 2007 and 2010 an ease. You just have to provide the *setup.exe* or ISO and the installer will guide you seamlessly through the installation procedure. You do not have to deal with the underlying Wine at all. The playonlinux installation for Office 2010 improves on the minimum installation instructions provided above by enabling xml conversions for Word documents created with certain earlier versions of Word.

#### Office 2013

[CodeWeawers](https://www.codeweavers.com/) managed to install and run Microsoft Office 2013 with many bugs. It is still pretty unusable. You can read more [here](https://www.codeweavers.com/about/blogs/caron/2015/07/13/two-weeks-in-crossover-microsoft-office-2013-installs-and-launches).

#### Office 2016

Doesn't work.

## Third-party interfaces

These have their own sites, and are *not supported* in the official Wine forums/bugzilla.

### CrossOver

[CrossOver](http://www.codeweavers.com/about/) Has its own [wiki page](/index.php/CrossOver "CrossOver").

### PlayOnLinux/PlayOnMac

[PlayOnLinux](http://www.playonlinux.com/) is a graphical Windows and DOS program manager. It contains scripts to assist the configuration and running of programs, it can manage multiple Wine versions and even use a specific version for each executable (e.g. because of regressions). If you need to know which Wine version works best for a certain game, try the [Wine Application Database](http://appdb.winehq.org/). You can find the [playonlinux](https://www.archlinux.org/packages/?name=playonlinux) package in [community](/index.php/Community "Community").

**Tip:** PlayOnLinux supports Bumblebee. Open POL console, type this command `POL_Config_Write PRE_WINE **optirun**` and hit enter. **optirun** command will used and each application will be run using **optirun**. You can even use **primusrun** instead!

### PyWinery

[PyWinery](https://github.com/ergoithz/pywinery) is a graphical and simple wine-prefix manager which allows you to launch apps and manage configuration of separate prefixes, also have a button to open winetricks in the same prefix, to open prefix dir, *winecfg*, application uninstaller and wineDOS. You can install You can install PyWinery with the [pywinery](https://aur.archlinux.org/packages/pywinery/) package. It is especially useful for having differents settings like DirectX games, office, programming, etc, and choose which prefix to use before you open an application or file.

It is recommended using winetricks by default to open *.exe* files, so you can choose between any Wine configuration you have.

### Q4wine

[Q4Wine](http://sourceforge.net/projects/q4wine/) is a graphical wine-prefix manager which allows you to manage configuration of prefixes. Notably it allows exporting [Qt](/index.php/Qt "Qt") themes into the Wine configuration so that they can integrate nicely. You can find the [q4wine](https://www.archlinux.org/packages/?name=q4wine) package in [multilib](/index.php/Multilib "Multilib").

### Wine-staging

[Wine-Staging](http://www.wine-staging.com/) (formerly wine-compholio) is a special wine version containing bug fixes and features, which are not yet available in regular wine versions. The idea of Wine Staging is to provide new features faster to end users and to give developers the possibility to discuss and improve their patches before they are sent upstream. Available via the [wine-staging](https://www.archlinux.org/packages/?name=wine-staging) package or directly via the wine-staging [Arch Linux repo](https://github.com/wine-compholio/wine-staging/wiki/Installation#-arch-linux).

## See also

*   [Official Wine website](http://www.winehq.com/)
*   [Wine application database](http://appdb.winehq.org/)
*   [Advanced configuring of video card and OpenGL in Wine; Speed up Wine](http://linuxgamingtoday.wordpress.com/2008/02/16/quick-tips-to-speed-up-your-gaming-in-wine/)
*   [FileInfo](http://wiki.gotux.net/code:perl:fileinfo) - Find Win32 PE/COFF headers in exe/dll/ocx files under Linux/Unix environment.
*   [Gentoo's Wine Wiki Page](https://wiki.gentoo.org/wiki/Wine)