# SugarSync

[SugarSync](https://www.sugarsync.com/) is a file sync and online backup tool similar to [Dropbox](http://www.dropbox.com/). Unfortunately, there is no native Linux client available. However, it works well through wine.

## Contents

*   [1 Installation](#Installation)
*   [2 Running the file manager](#Running_the_file_manager)
*   [3 Quick start guide](#Quick_start_guide)
*   [4 An update window popped up](#An_update_window_popped_up)

## Installation

First, install [wine](/index.php/Wine "Wine") and the following libraries: [lib32-mpg123](https://www.archlinux.org/packages/?name=lib32-mpg123), [lib32-libxml2](https://www.archlinux.org/packages/?name=lib32-libxml2), [lib32-openal](https://www.archlinux.org/packages/?name=lib32-openal), [lib32-libpng](https://www.archlinux.org/packages/?name=lib32-libpng), [lib32-libldap](https://www.archlinux.org/packages/?name=lib32-libldap).

Once the packages are installed, run winecfg (win32)

```
$ WINEARCH=win32 winecfg

```

You can keep the default options. Get the [SugarSync executable](https://www.sugarsync.com/downloads/SugarSyncSetup.exe) from the [SugarSync website](https://www.sugarsync.com/) and run it through wine:

```
$ wine SugarSyncSetup.exe

```

Follow the instructions while keeping the default options. When done, uncheck the box "Run SugarSync" and click finish.

## Running the file manager

After installation, you should find the SugarSync icon on your desktop or in the start-up menu. They are just links that invoke the following command:

```
$ env WINEPREFIX=$HOME"/.wine" wine C:\\windows\\command\\start.exe /Unix $HOME/.wine/dosdevices/c:/users/Public/Desktop/SugarSync\ Manager.lnk

```

If the installation went right, the "SugarSync Login" window just show. If not, look if you followed the installation instructions correctly.

## Quick start guide

Follow the Windows instructions in the official [Quick start guide](http://www.sugarsync.com/cskb/User_Docs/SugarSync+QuickStart+Guide.pdf).

## An update window popped up

In the case where an update window pops up, you can accept or cancel the installation, as you wish. There is nothing more to do than waiting for the download and update to finish.

Retrieved from "[https://wiki.archlinux.org/index.php?title=SugarSync&oldid=368762](https://wiki.archlinux.org/index.php?title=SugarSync&oldid=368762)"