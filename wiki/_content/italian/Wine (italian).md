[Wine](http://www.winehq.org/)

(Wine Is Not an Emulator) è un software scritto con lo scopo di permettere il funzionamento dei programmi sviluppati per il sistema operativo Microsoft Windows Sui sistemi GNU/Linux e altri sistemi compatibili. Wine consente infatti di utilizzare applicazioni per Windows come se fossero applicazioni scritte appositamente per sistemi GNU/Linux senza dover emulare la struttura, ma implementando di un layer di compatibilità fornendo così il collegamento alle API necessarie per il funzionamento delle applicazioni. (ecco perché Wine non è da intendersi un emulatore)

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
    *   [2.1 WINEPREFIX](#WINEPREFIX)
    *   [2.2 WINEARCH](#WINEARCH)
    *   [2.3 Driver grafici](#Driver_grafici)
    *   [2.4 Audio](#Audio)
        *   [2.4.1 Supporto per MIDI](#Supporto_per_MIDI)
    *   [2.5 Librerie aggiuntive](#Librerie_aggiuntive)
    *   [2.6 Fonts](#Fonts)
    *   [2.7 Desktop launcher menus](#Desktop_launcher_menus)
        *   [2.7.1 Creating menu entries for Wine utilities](#Creating_menu_entries_for_Wine_utilities)
        *   [2.7.2 Removing menu entries](#Removing_menu_entries)
        *   [2.7.3 KDE 4 menu fix](#KDE_4_menu_fix)
*   [3 Running Windows applications](#Running_Windows_applications)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Changing the language](#Changing_the_language)
    *   [4.2 Installing Microsoft Office 2010](#Installing_Microsoft_Office_2010)
    *   [4.3 Proper mounting of optical media images](#Proper_mounting_of_optical_media_images)
    *   [4.4 Burning optical media](#Burning_optical_media)
    *   [4.5 OpenGL modes](#OpenGL_modes)
    *   [4.6 Using Wine as an interpreter for Win16/Win32 binaries](#Using_Wine_as_an_interpreter_for_Win16.2FWin32_binaries)
    *   [4.7 Wineconsole](#Wineconsole)
    *   [4.8 Winetricks](#Winetricks)
    *   [4.9 Temp directory on tmpfs](#Temp_directory_on_tmpfs)
*   [5 Third-party interfaces](#Third-party_interfaces)
    *   [5.1 CrossOver](#CrossOver)
    *   [5.2 PlayOnLinux/PlayOnMac](#PlayOnLinux.2FPlayOnMac)
    *   [5.3 PyWinery](#PyWinery)
    *   [5.4 Q4wine](#Q4wine)
*   [6 See also](#See_also)

## Installazione

**Attenzione:** Se attraverso l'account utente è possibile accedere ai file di sistema anche i programmi installati attraverso Wine **possono accedere agli stessi file**. Se si ritiene che la sicurezza del sistema sia la priorità considerare la Virtualizzazione come una possibile alternativa.

Per installare Wine è necessario scaricare il pacchetto [wine](https://www.archlinux.org/packages/?name=wine), disponibile nei repository ufficiali. Nel caso in cui si desideri effettuare l'installazione su un sistema a 64-bit è necessario abilitare il repository [Multilib](/index.php/Multilib "Multilib").

Probabilmente si vorrà installare [wine_gecko](https://www.archlinux.org/packages/?name=wine_gecko) e [wine-mono](https://www.archlinux.org/packages/?name=wine-mono) per le applicazioni che richiedono il supporto rispettivamente per Internet Explorer e .NET. Questi pacchetti non sono strettamente richiesti da Wine ma ne ampliano le funzioni.

**Differenze tra architetture**

Wine per default è un'applicazione a 32-bit, perciò, non è in grado di eseguire qualsiasi applicazione di Windows a 64-bit.

Il pacchetto per sistemi x86_64 viene compilato con l'opzione `--enable-win64`. In questo modo viene attivata la versione di Wine di [WoW64](https://en.wikipedia.org/wiki/WoW64 "wikipedia:WoW64").

*   In Windows, questo complicato sottosistema permette all'utente di eseguire programmi a 32-bit o 64-bit in contemporanea e nella stessa cartella.
*   In Wine, l'utente avrà cartelle separate. Per maggiori informazioni vedere [Wine64](http://wiki.winehq.org/Wine64).

Se in un ambiente a 64-bit si riscontrano problemi con `winetricks` o con programmi, provare a creare un nuovo ambiente a 32-bit `WINEPREFIX`. Leggere: [#Using WINEARCH](#Using_WINEARCH). Utilizzando il pacchetto a 64-bit con `WINEARCH=win32` si dovrà agire come se si stesse lavorando con il pacchetto per i686.

## Configurazione

Tipicamente la configurazione di Wine avviene attraverso i seguenti strumenti:

*   [winecfg](http://wiki.winehq.org/winecfg) è uno strumento di configurazione ad interfaccia grafica. Per avviarlo da console digitare: `$ winecfg`, oppure `$ WINEPREFIX=~/.some_prefix winecfg`.
*   [control.exe](http://wiki.winehq.org/control) è un'implementazione di Wine nel Pannello di controllo di Windows a cui è possibile accedere con: `$ wine control`
*   [regedit](http://wiki.winehq.org/regedit) è l'editor di registro di Wine. Se winecfg e il Pannello di Controllo non sono abbastanza ricchi di funzionalità, leggere [WineHQ's article on Useful Registry Keys](http://wiki.winehq.org/UsefulRegistryKeys)

### WINEPREFIX

Wine mantiene i file di configurazione e i programmi Windows installati per impostazione predefinita in `~/.wine`.Questa cartella viene creata/aggiornata automaticamente quando viene eseguito un programma Windows oppure un programma da `winecfg`. Questa cartella inoltre contiene una lista con i programmi Windows installati che è possibile leggere con `C:` (the C-drive).

Con la variabile d'ambiente `WINEPREFIX` è possibile modificare la posizione dei file di configurazione. Ciò è particolarmente utile nel caso si voglia mantenere confugurazioni separate per differenti programmi Windows. La prima volta che viene avviato un programma, Wine creerà automaticamente una cartella contenente un drive C: e un registro.

Per esempio, avviando un programma con: `$ env WINEPREFIX=~/.win-a wine program-a.exe` e un'altro con: `$ env WINEPREFIX=~/.win-b wine program-b.exe` I due programmi avranno due drive C: e due registri separati.

**Nota:** Wine non è una sandbox! I programmi eseguiti sotto Wine hanno accesso al tutto il resto del sistema! (per esempio, `Z:` viene indicato con `/`, attenzione a queste considerazioni.)

Per creare un file di configurazione standard senza avviare un programma Windows o altri strumenti grafici usare:

```
$ env WINEPREFIX=~/.customprefix wineboot -u

```

### WINEARCH

Nel caso in cui il sistema sia a 64-bit, Wine avvierà automaticamente un ambiente a 64-bit. Per modificare tale comportamento utilizzare la variabile d'ambiente `WINEARCH`. Rinominare la cartella `~/.wine` e creare un nuovo ambiente Wine eseguendo `$ WINEARCH=win32 winecfg`. Questa operazione creerà un ambiente a 32-bit per Wine.

Inoltre è possibile combinare l'operazione precendente con `WINEPREFIX` per creare così due ambienti separati, 32-bit e 64-bit:

```
$ WINEARCH=win32 WINEPREFIX=~/win32 winecfg 
$ WINEPREFIX=~/win64 winecfg

```

**Nota:** Durante la creazione di prefix, the 64-bit version of wine treats all folders as 64-bit prefixes and will not create a 32-bit in any existing folder. To create a 32-bit prefix you have to let wine create the folder specified in `WINEPREFIX`.

You can also use `WINEARCH` in combination with other Wine programs, such as winetricks (using Steam as an example):

```
env WINEARCH=win32 WINEPREFIX=~/.local/share/wineprefixes/steam winetricks steam

```

**Tip:** You can make variables like `WINEPREFIX` or `WINEARCH` persistent by using [~/.bashrc](/index.php/Bash#Shell_and_environment_variables "Bash").

### Driver grafici

For most games, Wine requires high performance accelerated graphics drivers. This likely means using proprietary [NVIDIA](/index.php/NVIDIA "NVIDIA") or [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") drivers, although the open source [ATI](/index.php/ATI "ATI") driver is increasingly become proficient for use with Wine. [Intel](/index.php/Intel "Intel") drivers should mostly work as well as they are going to out of the box.

See [Gaming On Wine: The Good & Bad Graphics Drivers](http://www.phoronix.com/scan.php?page=news_item&px=MTI5NjU) for more details.

A good sign that your drivers are inadequate or not properly configured is when Wine reports the following in your terminal window:

```
Direct rendering is disabled, most likely your OpenGL drivers have not been installed correctly

```

For x86-64 systems, additional [multilib](/index.php/Multilib "Multilib") packages are required. Please install the one that is listed in the *Multilib Package* column in the table in [Xorg#Driver installation](/index.php/Xorg#Driver_installation "Xorg").

**Note:** You might need to restart X after having installed the correct library.

### Audio

By default sound issues may arise when running Wine applications. Ensure only one sound device is selected in `winecfg`. Currently, the [Alsa](/index.php/Alsa "Alsa") driver is the most supported.

If you want to use [Alsa](/index.php/Alsa "Alsa") driver in Wine, and are using x86_64, you'll need to install the [lib32-alsa-lib](https://www.archlinux.org/packages/?name=lib32-alsa-lib). If you are also using PulseAudio, you will need to install [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse).

If you want to use [OSS](/index.php/OSS "OSS") driver in Wine, you will need to install the [lib32-alsa-oss](https://www.archlinux.org/packages/?name=lib32-alsa-oss) package. The OSS driver in the kernel will not suffice.

If `winecfg` **still** fails to detect the audio driver (Selected driver: (none)), [configure it via the registry](http://wiki.jswindle.com/index.php/Wine_Registry#Configuring_Sound).

Games that use advanced sound systems may require installations of [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal).

#### Supporto per MIDI

[MIDI](/index.php/MIDI "MIDI") was a quite popular system for video games music in the 90\. If you are trying out old games, it is not uncommon that the music will not play out of the box. Wine has excellent MIDI support. However you first need to make it work on your host system. See the wiki page for more details. Last but not least you need to make sure Wine will use the correct MIDI output. See the [Wine Wiki](http://wiki.winehq.org/MIDI) for a detailed setup.

### Librerie aggiuntive

*   Some applications (e.g. Office 2003/2007) require the MSXML library to parse HTML or XML, in such cases you need to install [lib32-libxml2](https://www.archlinux.org/packages/?name=lib32-libxml2).

*   Some applications that play music may require [lib32-mpg123](https://www.archlinux.org/packages/?name=lib32-mpg123).

*   Some applications that use native image manipulation libraries may require [lib32-giflib](https://www.archlinux.org/packages/?name=lib32-giflib) and [lib32-libpng](https://www.archlinux.org/packages/?name=lib32-libpng).

*   Some applications that require encryption support may require [lib32-gnutls](https://www.archlinux.org/packages/?name=lib32-gnutls).

### Fonts

If Wine applications are not showing easily readable fonts, you may not have Microsoft's Truetype fonts installed. See [MS Fonts](/index.php/MS_Fonts "MS Fonts"). If this does not help, try running `winetricks allfonts`.

After running such programs, kill all wine servers and run `winecfg`. Fonts should be legible now.

If the fonts look somehow smeared, import the following text file into the Wine registry with [regedit](http://wiki.winehq.org/regedit):

```
[HKEY_CURRENT_USER\Software\Wine\X11 Driver]
"ClientSideWithRender"="N"

```

### Desktop launcher menus

When installing Windows programs with Wine, should result in the appropriate menu/desktop icons being created. For example, if the installation program (e.g. `setup.exe`) would normally add an icon to your Desktop or "Start Menu" on Windows, then Wine should create corresponding freedesktop.org style `.desktop` files for launching your programs with Wine.

**Tip:** If menu items were *not* created while installing software or have been lost, [winemenubuilder](http://wiki.winehq.org/winemenubuilder) may be of some use.

#### Creating menu entries for Wine utilities

By default, installation of Wine does not create desktop menus/icons for the software which comes with Wine (e.g. for `winecfg`, `winebrowser`, etc). These instructions will add entries for these applications.

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
"[http://www.freedesktop.org/standards/menu-spec/menu-1.0.dtd](http://www.freedesktop.org/standards/menu-spec/menu-1.0.dtd)">
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

Menu entries created by Wine are located in `~/.local/share/applications/wine/Programs/`. Remove the program's `.desktop` entry to remove the application from the menu.

#### KDE 4 menu fix

The Wine menu items [may appear](https://bugs.launchpad.net/ubuntu/+source/wine/+bug/263041) in `"Lost & Found"` instead of the Wine menu in KDE 4\. This is because `kde-applications.menu` is missing the `MergeDir` option.

Edit `/etc/xdg/menus/kde-applications.menu`

At the end of the file add `<MergeDir>applications-merged</MergeDir>` after `<DefaultMergeDirs/>`, it should look like this:

```
<Menu>
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
$ ln -s ~/.config/menus/applications-merged ~/.config/menus/kde-applications-merged

```

This has the added bonus that an update to KDE won't change it, but is per user instead of system wide.

## Running Windows applications

**Warning:** Do not run or install Wine applications as root! See [Running Wine as root](http://wiki.winehq.org/FAQ#run_as_root) for the official statement.

To run a windows application:

```
$ wine <path to exe>

```

To install using an MSI installer, use the included msiexec utility:

```
$ msiexec installername.msi

```

## Tips and tricks

**Tip:** In addition to the links provided in the beginning of the article the following may be of interest:

*   [The Wine Application Database (AppDB)](http://appdb.winehq.org/) - Information about running specific Windows applications (Known issues, ratings, guides, etc tailored to specific applications)
*   [The WineHQ Forums](http://forum.winehq.org/) - A great place to ask questions *after* you have looked through the FAQ and AppDB

### Changing the language

Some programs may not offer a language selection, they will guess the desired language upon the sytem locales. Wine will transfer the current environment (including the locales) to the application, so it should work out of the box. If you want to force a program to run in a specific locale (which is fully [generated](/index.php/Locale "Locale") on your system), you can call Wine with the following setting:

```
LC_ALL=xx_XX.encoding wine /my/program

```

For instance

```
LC_ALL=it_IT.UTF-8 wine /my/program

```

### Installing Microsoft Office 2010

**Note:** Microsoft Office 2013 does not run at all.

Microsoft Office 2010 works without any problems (tested with Microsoft Office Home and Student 2010, Wine 1.5.27 and 1.7.5). Activation over Internet also works.

Start by installing [wine-mono](https://www.archlinux.org/packages/?name=wine-mono), [wine_gecko](https://www.archlinux.org/packages/?name=wine_gecko), [samba](https://www.archlinux.org/packages/?name=samba), and [lib32-libxml2](https://www.archlinux.org/packages/?name=lib32-libxml2).

Proceed with launching the installer:

```
$ export WINEPREFIX=.wine # any path to a writable folder on your home directory will do
$ export WINEARCH="win32"
$ wine /path/to/office_cd/setup.exe

```

You could also put the above exports into your `.bashrc`.

Once installation completes, open Word or Excel to activate over the Internet. Once activated, close the application. Then run `winecfg`, and set **riched20** (under libraries) to **(native,builtin)**. This will enable Powerpoint to work.

For additional info, see the [WineHQ](http://appdb.winehq.org/appview.php?iVersionId=4992) article.

**Note:** If the activation over internet doesn't work and you want to activate by phone, be sure **riched20** is set to *(native,builtin)* in order to see the drop-down list of countries.

**Note:** [playonlinux](https://www.archlinux.org/packages/?name=playonlinux) provides custom installer scripts that make the installation of Office 2003, 2007 and 2010 an ease. You just have to provide the setup.exe or ISO and the installer will guide you seamlessly through the installation procedure. You do not have to deal with the underlying Wine at all.

### Proper mounting of optical media images

Some applications will check for the optical media to be in drive. They may check for data only, in which case it might be enough to configure the corresponding path as being a CD-ROM drive in `winecfg`. However, other applications will look for a media name and/or a serial number, in which case the image has to be mounted with these special properties.

Some virtual drive tools do not handle these metadata, like fuse-based virtual drives (Acetoneiso for instance). CDEmu will handle it correctly.

### Burning optical media

To burn CDs or DVDs, you will need to load the `sg` [kernel module](/index.php/Kernel_modules "Kernel modules").

### OpenGL modes

Many games have an OpenGL mode which *may* perform better than their default DirectX mode. While the steps to enable OpenGL rendering is *application specific*, many games accept the `-opengl` parameter.

```
$ wine /path/to/3d_game.exe -opengl

```

You should of course refer to your application's documentation and Wine's [AppDB](http://appdb.winehq.org) for such application specific information.

### Using Wine as an interpreter for Win16/Win32 binaries

It is also possible to tell the kernel to use wine as an interpreter for all Win16/Win32 binaries:

```
echo ':DOSWin:M::MZ::/usr/bin/wine:' > /proc/sys/fs/binfmt_misc/register

```

To make the setting permanent, create a `/etc/binfmt.d/wine.conf` file with the following content:

```
# Start WINE on Windows executables
:DOSWin:M::MZ::/usr/bin/wine:

```

systemd automatically mounts the `/proc/sys/fs/binfmt_misc` filesystem using `proc-sys-fs-binfmt_misc.mount` (and automount) and runs the `systemd-binfmt.service` to load your settings.

Try it out by running a Windows program:

```
chmod +x exefile.exe
./exefile.exe

```

If all went well, exefile.exe should run.

### Wineconsole

Often you may need to run `.exe`s to patch game files, for example a widescreen mod for an old game, and running the `.exe` normally through wine might yield nothing happening. In this case, you can open a terminal and run the following command:

```
$ wineconsole cmd

```

Then navigate to the directory and run the `.exe` file from there.

### Winetricks

[Winetricks](http://wiki.winehq.org/winetricks) is a script to allow one to install base requirements needed to run Windows programs. Installable components include DirectX 9.x, MSXML (required by Microsoft Office 2007 and Internet Explorer), Visual Runtime libraries and many more.

You can install [winetricks](https://www.archlinux.org/packages/?name=winetricks) via [pacman](/index.php/Pacman "Pacman") or use the [winetricks-svn](https://aur.archlinux.org/packages/winetricks-svn/) package available in the [AUR](/index.php/AUR "AUR"). Then run it with:

```
$ winetricks

```

### Temp directory on tmpfs

To limit wine from writing its Temporary files to a physical disk, one can define an alternative location, like tmpfs, removing Temp directory and creating a symlink:

```
$ rm -r ~/.wine/drive_c/users/$USER/Temp
$ ln -s /tmp/ ~/.wine/drive_c/users/$USER/Temp

```

## Third-party interfaces

These have their own sites, and are not supported in the Wine forums.

### CrossOver

[CrossOver](http://www.codeweavers.com/about/) Has its own [wiki page](/index.php/CrossOver "CrossOver").

### PlayOnLinux/PlayOnMac

[PlayOnLinux](http://www.playonlinux.com/) ([playonlinux](https://www.archlinux.org/packages/?name=playonlinux)) is a graphical Windows and DOS program manager. It contains scripts to assist the configuration and running of programs, it can manage multiple Wine versions and even use a specific version for each executable (eg. because of regressions). If you need to know which Wine version works best for a certain game, try the [Wine Application Database](http://appdb.winehq.org/).

### PyWinery

[PyWinery](http://code.google.com/p/pywinery/) is a graphical and simple wine-prefix manager which allows you to launch apps and manage configuration of separate prefixes, also have a button to open winetricks in the same prefix, to open prefix dir, `winecfg`, application uninstaller and wineDOS. You can install [PyWinery from AUR](https://aur.archlinux.org/packages.php?ID=48382). It is especially useful for having differents settings like DirectX games, office, programming, etc, and choose which prefix to use before you open an application or file.

It's recommended using winetricks by default to open **.exe** files, so you can choose between any wine configuration you have.

### Q4wine

[Q4Wine](http://q4wine.brezblock.org.ua/) is a graphical wine-prefix manager which allows you to manage configuration of prefixes. Notably it allows exporting QT themes into the wine configuration so that they can integrate nicely. You can find the [q4wine](https://aur.archlinux.org/packages/q4wine/) package in [multilib](/index.php/Multilib "Multilib").

## See also

*   [Official Wine website](http://www.winehq.com/)
*   [Wine application database](http://appdb.winehq.org/)
*   [Advanced configuring your gfx card and OpenGL settings on wine; Speed up wine](http://linuxgamingtoday.wordpress.com/2008/02/16/quick-tips-to-speed-up-your-gaming-in-wine/)
*   [FileInfo](http://wiki.gotux.net/code:perl:fileinfo) - Find Win32 PE/COFF headers in EXE/DLL/OCX files under linux/unix environment.
*   [Gentoo's Wine Wiki Page](https://wiki.gentoo.org/wiki/Wine)