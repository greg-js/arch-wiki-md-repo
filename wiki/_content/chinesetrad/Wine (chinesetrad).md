[Wine](https://en.wikipedia.org/wiki/Wine_(software) is a compatibility layer capable of running Microsoft Windows applications on Unix-like operating systems. Windows programs running in Wine act as native programs would, running without the performance or memory usage penalties of an emulator, with a similar look and feel to other applications on your desktop environment.

## Contents

*   [1 安裝](#.E5.AE.89.E8.A3.9D)
    *   [1.1 開啟multilib](#.E9.96.8B.E5.95.9Fmultilib)
    *   [1.2 安裝 wine](#.E5.AE.89.E8.A3.9D_wine)
    *   [1.3 Architectural differences](#Architectural_differences)
*   [2 Configuration](#Configuration)
    *   [2.1 Using WINEARCH](#Using_WINEARCH)
    *   [2.2 Graphics Drivers](#Graphics_Drivers)
    *   [2.3 Sound](#Sound)
    *   [2.4 Fonts](#Fonts)
    *   [2.5 Desktop Launcher Menus](#Desktop_Launcher_Menus)
        *   [2.5.1 Creating Menu Entries](#Creating_Menu_Entries)
        *   [2.5.2 KDE 4 Menu Fix[1]](#KDE_4_Menu_Fix.5B1.5D)
*   [3 Running Windows Applications](#Running_Windows_Applications)
*   [4 Tips and Tricks](#Tips_and_Tricks)
    *   [4.1 Installing Microsoft Office 2007](#Installing_Microsoft_Office_2007)
    *   [4.2 OpenGL Modes](#OpenGL_Modes)
    *   [4.3 PlayOnLinux](#PlayOnLinux)
    *   [4.4 PyWinery](#PyWinery)
    *   [4.5 Sidenet Wine Configuration Utility](#Sidenet_Wine_Configuration_Utility)
    *   [4.6 Using Wine as an interpreter for Win16/Win32 binaries](#Using_Wine_as_an_interpreter_for_Win16.2FWin32_binaries)
    *   [4.7 Wineconsole](#Wineconsole)
    *   [4.8 Wine-doors](#Wine-doors)
    *   [4.9 WineTools assistant](#WineTools_assistant)
    *   [4.10 Winetricks](#Winetricks)
*   [5 Alternatives to Win16 / Win32 binaries](#Alternatives_to_Win16_.2F_Win32_binaries)
*   [6 External Resources](#External_Resources)

## 安裝

Wine is constantly updated and available in the [community] repository for i686 and in [multilib] for x86_64.

**注意:** 如果你是使用 x86_64 （64bit）的系統，你需要開啟 [multilib] 的套件庫（預設是關閉的），開啟方式如下

### 開啟multilib

在 `/etc/pacman.conf` 中找到

```
#[multilib]
#SigLevel = PackageOptional
#Include = /etc/pacman.d/mirrorlist

```

並把 [multilib] 以及 Include 前的注解符號去掉，變成：

```
[multilib]
#SigLevel = PackageOptional
Include = /etc/pacman.d/mirrorlist

```

或是自行加入這兩行。

接著更新 pacman：

```
sudo pacman -Syu

```

### 安裝 wine

```
# pacman -S wine

```

You may also require wine_gecko if your applications make use of Internet Explorer

```
# pacman -S wine_gecko

```

### Architectural differences

Wine in Arch Linux on i686 is packaged just like expected. It includes a standard 32-bit Wine installation and is unable to execute any 64-bit Windows applications. However, the x86_64 Wine package includes both, a 32-bit and a 64-bit Windows compatibility layer in one.

This so called [WoW64](https://en.wikipedia.org/wiki/WoW64 "wikipedia:WoW64") allows the user to use 32-bit and 64-bit Windows programs concurrently and even in the same WINEPREFIX with a win64 WINEARCH. The current support for this in Wine itself is limited and users are recommended to use a win32 WINEPREFIX. See [Wine#Using_WINEARCH](/index.php/Wine#Using_WINEARCH "Wine") for more information on this.

To clarify the above, the i686 package Wine will work exactly like a x86_64 package Wine with a win32 WINEPREFIX with no ill effects.

## Configuration

By default, Wine stores its configuration files and installed Windows programs in `~/.wine`. This directory is commonly called a "Wine prefix" or "Wine bottle." It is created/updated automatically whenever you run a Windows program or one of Wine's bundled programs such as winecfg. The prefix directory also contains a tree which your Windows programs will see as "C: drive."

You can override the location Wine uses for a prefix with the WINEPREFIX environment variable. This is useful if you want to use separate configurations for different Windows programs. For example if you run one program with

```
$ env WINEPREFIX=~/.win-a wine program-a.exe

```

and another with

```
$ env WINEPREFIX=~/.win-b wine program-b.exe

```

the two programs will each have separate "C: drives" and registries.

To create a default prefix without running a Windows program or other GUI tool you can use

```
$ env WINEPREFIX=~/.customprefix wineboot -u

```

**Note:** Wine prefixes should not be confused with the same kind of "containment" found with other "virtual" environments. Generally speaking, if you can access a file or resource with your user account, programs running with Wine can too. Wine is not a jail.

Configuring Wine is typically accomplished using winecfg, Wine's control panel, and regedit.

*   [winecfg](http://wiki.winehq.org/winecfg) is a GUI configuration tool for Wine. You can run it from a console window with `$ winecfg` or `$ WINEPREFIX=~/.some_prefix winecfg` 
*   [control.exe](http://wiki.winehq.org/control) is Wine's implementation of Windows' Control Panel which can be accessed with `$ wine control` 
*   [regedit](http://wiki.winehq.org/regedit) is Wine's registry editing tool. If winecfg and the Control Panel were not enough, see [WineHQ's article on Useful Registry Keys](http://wiki.winehq.org/UsefulRegistryKeys)

### Using WINEARCH

If you are using wine from [multilib], you will notice that **winecfg** will get you a 64-bit wine environment by default. You can change this behavior using the WINEARCH environment variable. Rename your ~/.wine directory and create a new wine environment by running:

```
$ WINEARCH=win32 winecfg 

```

This will get you a 32-bit wine environment. Not setting WINEARCH will get you a 64-bit one.

You can combine this with WINEPREFIX to make a separate win32 and win64 environment:

```
$ WINEARCH=win32 WINEPREFIX=~/win32 winecfg 
$ WINEPREFIX=~/win64 winecfg

```

Note that a win64 WINEARCH is meant to be able to run 32-bit Windows applications as well as 64-bit ones. However, support for this is limited in Wine and users are encouraged to use a win32 WINEPREFIX for the time being until support improves.

**Note:** During prefix creation, the 64-bit version of wine treats all folders as 64-bit prefixs and will not create a 32-bit in any existing folder. To create a 32-bit prefix you have to let wine create the folder specified in WINEPREFIX.

You can also use winetricks and WINEARCH in one command for installing something from winetricks like this (using Steam as an example):

```
env WINEARCH=win32 WINEPREFIX=~/.local/share/wineprefixes/steam winetricks steam

```

Note: you do not have create the steam subdirectory in the wineprefixes directory, it will create for you. See the Bottles section below for more information.

### Graphics Drivers

For most games, Wine requires high performance accelerated graphics drivers. This likely means using proprietary binary drivers from [NVIDIA](/index.php/NVIDIA "NVIDIA") or [Amd/ATI](/index.php/ATI "ATI"). [Intel](/index.php/Intel "Intel") drivers should mostly work as well as they are going to out of the box.

A good sign that your drivers are inadequate or not properly configured is when Wine reports the following in your terminal window:

```
Direct rendering is disabled, most likely your OpenGL drivers haven't been installed correctly

```

For x86-64 systems, additional 32-bit [multilib] or [AUR](/index.php/AUR "AUR") packages are required:

*   **NVIDIA**: `# pacman -S lib32-nvidia-utils` For older lib32-nvidia-utils (e.g. nvidia-96xx drivers), see [here](https://aur.archlinux.org/packages.php?K=lib32-nvidia-utils).
*   **Intel**: `# pacman -S lib32-intel-dri` Run Wine with `LIBGL_DRIVERS_PATH=/usr/lib32/xorg/modules/dri` 
*   **AMD/ATI**: `# pacman -S lib32-ati-dri` For ATI's proprietary drivers, install [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/) from AUR

**Note:** You might need to restart after having installed the correct library!

### Sound

By default sound issues may arise when running Wine applications. Ensure only one sound device is selected in *winecfg*. Currently, the [Alsa](/index.php/Alsa "Alsa") driver is the most supported.

If you want to use [OSS](/index.php/OSS "OSS") in Wine, you will need to install the **oss** package. The OSS driver in the kernel will not suffice.

### Fonts

If Wine applications are not showing easily readable fonts, you may not have Microsoft's Truetype fonts installed. See [MS Fonts](/index.php/MS_Fonts "MS Fonts"). If this does not help, try running `winetricks allfonts`. (See [#Winetricks](#Winetricks) below.)

After running such programs, kill all wine servers and run winecfg. Fonts should be legible now.

If the fonts look somehow smeared, import the following text file into the Wine registry with [regedit](http://wiki.winehq.org/regedit):

```
[HKEY_CURRENT_USER\Software\Wine\X11 Driver]
"ClientSideWithRender"="N"

```

### Desktop Launcher Menus

By default, installation of Wine does not create desktop menus/icons for the software which comes with Wine (e.g. for winecfg, winebrowser, etc). However, installing Windows programs with Wine, in most cases, should result in the appropriate menu/desktop icons being created. For example, if the installation program (e.g. setup.exe) would normally add an icon to your Desktop or "Start Menu" on Windows, then Wine should create corresponding freedesktop.org style .desktop files for launching your programs with Wine.

**Tip:** If menu items were *not* created while installing software or have been lost, [winemenubuilder](http://wiki.winehq.org/winemenubuilder) may be of some use.

If you wish to add on to the menu to create an Ubuntu-like Wine sub-menu, then follow these instructions:

#### Creating Menu Entries

First, install a Windows program using Wine to create the base menu. After the base menu is created, you can start to add the menu entries. In GNOME, right-click on the desktop and select "Create Launcher...". The steps might be different for KDE/Xfce. Make three launchers using these settings:

```
**Type**: Application
**Name**: Configuration
**Command**: winecfg
**Comment**: Configure the general settings for Wine

```

```
**Type**: Application
**Name**: Uninstall Programs
**Command**: wine uninstaller
**Comment**: Uninstall Windows programs under Wine properly

```

```
**Type**: Application
**Name**: Browse C:\ Drive
**Command**: wine winebrowser c:\\
**Comment**: Browse the files in the virtual Wine C:\ drive

```

Now that you have these three launchers on your desktop, it is time to put them into the menu. But, first you should change the launchers to dynamically change icons when a new icon set is installed. To do this, open the launchers that you just made in your favorite text editor. Change the following settings to these new values: *Configuration* launcher:

```
Icon[en_US]=wine-winecfg
Icon=wine-winecfg

```

*Uninstall Programs* launcher:

```
Icon[en_US]=wine-uninstaller
Icon=wine-uninstaller

```

*Browse C:\ Drive* launcher:

```
Icon[en_US]=wine-winefile
Icon=wine-winefile

```

If these settings produce a ugly/non-existent icon, it means that there are no icons for these launchers in the icon set that you have enabled. You should replace the icon settings with the explicit location of the icon that you want. Clicking the icon in the launcher's properties menu will have the same effect. A great icon set that supports these shortcuts is [GNOME-colors](http://www.gnome-look.org/content/show.php/GNOME-colors?content=82562).

Now that you have the launchers fully configured, now it is time to put them in the menu. Copy them into `~/.local/share/applications/wine/`.

Wait a second, they aren't in the menu yet! There is one last step. Create the following text file `~/.config/menus/applications-merged/wine-utilities.menu` 
```
 <!DOCTYPE Menu PUBLIC "-//freedesktop//DTD Menu 1.0//EN"
 "http://www.freedesktop.org/standards/menu-spec/menu-1.0.dtd">
 <Menu>
   <Name>Applications</Name>
   <Menu>
     <Name>wine-wine</Name>
     <Directory>wine-wine.directory</Directory>
     <Include>
 	<Filename>wine-Configuration.desktop</Filename>
     </Include>
     <Include>
 	<Filename>wine-Browse C:\ Drive.desktop</Filename>
     </Include>
     <Include>
 	<Filename>wine-Uninstall Programs.desktop</Filename>
     </Include>
   </Menu>
 </Menu>

```

Go check in the menu and there should be the minty fresh options waiting to be used!

#### KDE 4 Menu Fix[[1]](https://bugs.launchpad.net/ubuntu/+source/wine/+bug/263041)

The Wine menu items may appear in "Lost & Found" instead of the Wine menu in KDE 4\. This is because kde-applications.menu is missing the MergeDir option.

Edit `/etc/xdg/menus/kde-applications.menu`

At the end of the file add `<MergeDir>applications-merged</MergeDir>` after `<DefaultMergeDirs/>`, it should look like this:

```
        <Include>
                <And>
                        <Category>KDE</Category>
                        <Category>Core</Category>
                </And>
        </Include>
        <DefaultMergeDirs/>
        **<MergeDir>applications-merged</MergeDir>**
        <MergeFile>applications-kmenuedit.menu</MergeFile>
</Menu>

```

Alternatively you can create a symlink to a folder that KDE does see:

```
ln -s ~/.config/menus/applications-merged ~/.config/menus/kde-applications-merged

```

This has the added bonus that an update to KDE won't change it, but is per user instead of system wide.

## Running Windows Applications

**Warning:** Do not run or install Wine applications as root! See [http://wiki.winehq.org/FAQ#run_as_root](http://wiki.winehq.org/FAQ#run_as_root) for more details.

To run a 32-bit windows application:

```
$ wine <path to exe>

```

To run a 64-bit windows application on a x86-64 system:

```
$ wine64 <path to exe>

```

To install using an MSI installer, use the included msiexec utility:

```
$ msiexec installername.msi

```

**Tip:** The [official Wine site](http://www.winehq.org) contains a wealth of information about running Windows applications with Wine. Of particular interest are:

*   [The official FAQ](http://wiki.winehq.org/FAQ) - General information about Wine and Frequently Asked Questions
*   [The Wine Application Database (AppDB)](http://appdb.winehq.org/) - Information about running specific Windows applications (Known issues, ratings, guides, etc tailored to specific applications)
*   [The WineHQ Forums](http://forum.winehq.org/) - A great place to ask questions *after* you have looked through the FAQ and AppDB

If it does not "just work," these resources will often be your first stops toward getting your Windows software working.

## Tips and Tricks

These tools will assist in the installation of typical Windows components. In most cases they should be used as a last effort, as it may severely alter your wine configuration.

### Installing Microsoft Office 2007

A small tweak is needed to install the office suite. Follow these steps to accomplish it:

```
$ WINEARCH=win32 WINEPREFIX=/path/to/wineprefix winecfg
# pacman -S winetricks
$ winetricks msxml3
$ wine /path/to/office_cd/setup.exe

```

For additional info, see the [WineHQ](http://appdb.winehq.org/appview.php?iVersionId=4992) article.

### OpenGL Modes

Many games have an OpenGL mode which *may* preform better than their default DirectX mode. While the steps to enable OpenGL rendering is *application specific*, many games accept the `-opengl` parameter.

```
$ wine /path/to/3d_game.exe -opengl

```

You should of course refer to your application's documentation and Wine's [AppDB](http://appdb.winehq.org) for such application specific information.

### PlayOnLinux

[PlayOnLinux](http://www.playonlinux.com/) is a graphical Windows and DOS program manager. It contains many scripts to assist the configuration and running of progams. You can find the [PKGBUILD](https://aur.archlinux.org/packages.php?ID=14986) in AUR.

PlayOnLinux can also manage multiple Wine versions and use a specific version for each executable because of regressions. If you need to know what Wine version works best for a certain game, try the [Wine Application Database](http://appdb.winehq.org/).

### PyWinery

[PyWinery](http://code.google.com/p/pywinery/) is a graphical and simple wine-prefix manager which allows you to launch apps and manage configuration of separate prefixes, also have a button to open winetricks in the same prefix, to open prefix dir, winecfg, application uninstaller and wineDOS. You can install [PyWinery from AUR](https://aur.archlinux.org/packages.php?ID=48382). It is especially useful for having differents settings like DirectX games, office, programming, etc, and choose which prefix to use before you open an application or file.

It's recommended using winetricks by default to open. exe files, so you can choose between any wine configuration you have.

### Sidenet Wine Configuration Utility

**Note:** The link appears to be broken.

[Sidenet's wine-config](http://sidenet.ddo.jp/winetips/config.html)

*   Download the latest version
*   unpack it
*   READ THE README
*   execute

```
./setup

```

*   Follow the instructions

**Keep in mind**: Like stated on the [site](http://sidenet.ddo.jp/winetips/config.html), you're only allowed to install DCOM98 if you possess a valid License for Windows98.

### Using Wine as an interpreter for Win16/Win32 binaries

It is also possible to tell the kernel to use wine as an interpreter for all Win16/Win32 binaries. First mount the binfmt_misc filesystem:

```
# mount -t binfmt_misc none /proc/sys/fs/binfmt_misc

```

Or you can add this line to your `/etc/fstab`:

```
none /proc/sys/fs/binfmt_misc binfmt_misc defaults 0 0

```

Then, tell the kernel how to interpret Win16 and Win32 binaries:

```
echo ':DOSWin:M::MZ::/usr/bin/wine:' > /proc/sys/fs/binfmt_misc/register

```

You can add this line to `/etc/rc.local` to make this setting permanent. In this case you may want to ignore stderr to avoid error messages when changing runlevels:

```
{ echo ':DOSWin:M::MZ::/usr/bin/wine:' > /proc/sys/fs/binfmt_misc/register; } 2>/dev/null

```

Now try to run a Windows program:

```
chmod 755 exefile.exe
./exefile.exe

```

### Wineconsole

Often you may need to run .exes to patch game files, for example a widescreen mod for an old game, and running the .exe normally through wine might yield nothing happening. In this case, you can open a terminal and run the following command:

```
$ wineconsole cmd

```

Then navigate to the directory and run the .exe file from there.

### Wine-doors

[Wine-doors](http://www.wine-doors.org/)

Wine-doors is a WineTools replacement. It features a GNOME GUI and works like a package manager. Works fine in 64bit. [No longer available in the AUR].

### WineTools assistant

**Note:** This tool is currently slightly outdated, but working.

[Winetools](http://www.von-thadden.de/Joachim/WineTools) is a script that facilitates in the installation of some core components for wine in order to install other programs. Note this is not necessary for wine, but does help if you want to get Internet Explorer running.

**Note:** Microsoft policy is that you must have a license for IE6 in order to install DCOM98 or Internet Explorer 6\. If you've ever owned a copy of Windows, you should be fine.

You can download the [PKGBUILD](https://aur.archlinux.org/packages.php?ID=8913) script and see [AUR](/index.php/AUR "AUR") for instructions to build and install.

### Winetricks

[Winetricks](http://wiki.winehq.org/winetricks) is a quick script that allows one to install base requirements needed to run some Windows programs. Installable components includes DirectX 9.x, msxml (required by Microsoft Office 2007 and Internet Explorer), visual runtime libraries and many more.

You can install winetricks via pacman.

```
# pacman -S winetricks

```

Then run winetricks **as a normal user**:

```
$ winetricks

```

## Alternatives to Win16 / Win32 binaries

*   [Codeweavers](/index.php/Codeweavers "Codeweavers") - Codeweavers' Crossover Office; Aimed at Office Users

## External Resources

*   [Official Wine Website](http://www.winehq.com/)
*   [Wine Application Database](http://appdb.winehq.org/)
*   [Advanced configuring your gfx card and OpenGL settings on wine; Speed up wine](http://linuxgamingtoday.wordpress.com/2008/02/16/quick-tips-to-speed-up-your-gaming-in-wine/)
*   [FileInfo](http://wiki.gotux.net/code:perl:fileinfo) - Find Win32 PE/COFF headers in EXE/DLL/OCX files under linux/unix environment.