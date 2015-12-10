# Flash DRM content

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

DRM content on Flash still requires HAL to play. This is apparent for example with Google Play Movies, Amazon Instant Video, WatchESPN or Demand 5 (Channel 5 UK). If you attempt to play a DRM-protected content without HAL, you may see the following error: `an error occurred and your player could not be updated`.

To deliver DRM-protected content, Flash calls several functions provided by the HAL daemon and its libraries. While Flash-based players remain popular, HAL has been deprecated and is not commonly installed on newer systems. To provide the necessary HAL functionality on such systems, you can either install the full HAL package and run the HAL daemon or install a modified HAL library "stub" that uses the modern UDisks daemon instead.

## Contents

*   [1 Using the HAL package](#Using_the_HAL_package)
    *   [1.1 Running the HAL daemon](#Running_the_HAL_daemon)
*   [2 Using the modified libhal stub](#Using_the_modified_libhal_stub)
    *   [2.1 Installing UDisks and hal-flash](#Installing_UDisks_and_hal-flash)
    *   [2.2 Running UDisks](#Running_UDisks)
*   [3 Remove Flash Player cached files](#Remove_Flash_Player_cached_files)
*   [4 See also](#See_also)

## Using the HAL package

Install the [hal](https://aur.archlinux.org/packages/hal/)<sup><small>AUR</small></sup> package from the [AUR](/index.php/AUR "AUR"). You will need to install [hal-info](https://aur.archlinux.org/packages/hal-info/)<sup><small>AUR</small></sup> first as it is a dependency for [hal](https://aur.archlinux.org/packages/hal/)<sup><small>AUR</small></sup>.

**Note:** The HAL libraries only work with [flashplugin](https://www.archlinux.org/packages/?name=flashplugin). [chromium-pepper-flash](https://aur.archlinux.org/packages/chromium-pepper-flash/)<sup><small>AUR</small></sup> does not support DRM.

### Running the HAL daemon

The HAL daemon is managed by `hal.service`, which can be controlled by [systemctl](/index.php/Systemd#Using_units "Systemd").

Alternatively, one can use the following script, which also takes care of [cleaning the cache](#Remove_Flash_Player_cached_files).

```
#!/bin/bash

## written by Mark Lee <bluerider>
## using information from <https://wiki.archlinux.org/index.php/Chromium#Google_Play_.26_Flash>

## Start and stop Hal service on command for Google Play Movie service

function main () {  ## run the main insertion function
     clear-cache;  ## remove adobe cache
     start-hal;  ## start the hal daemon
     read -p "Press 'enter' to stop hal";  ## pause the command line with a read line
     stop-hal;  ## stop the hal daemon
}

function clear-cache () {  ## remove adobe cache
     cd ~/.adobe/Flash_Player;  ## go to Flash player user directory
     rm -rf NativeCache AssetCache APSPrivateData2;  ## remove cache
}

function start-hal () {  ## start the hal daemon
     sudo systemctl start hal.service && ( ## systemd : start hal daemon
          echo "Started hal service..."
) || (
          echo "Failed to start hal service!") 
}

function stop-hal () {  ## stop the hal daemon
sudo systemctl stop hal.service && (  ## systemd : stop hal daemon
          echo "Stopped hal service..."
     ) || (
          echo "Failed to stop hal service!"
     )
}

main;  ## run the main insertion function

```

## Using the modified libhal stub

As an alternative to installing all of HAL, you can install a modified version of the libhal library from the [AUR](/index.php/AUR "AUR") that uses the modern UDisks daemon instead of the deprecated HAL. Note that this libhal provides just enough of the HAL functionality to meet Flash's needs for copy-protected delivery: if you have other programs that require HAL, this stub probably won't satisfy them and you should use the full hal package instead.

### Installing UDisks and hal-flash

You will need to install [hal-flash](https://aur.archlinux.org/packages/hal-flash/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR"), which relies on [Udisks](/index.php/Udisks "Udisks").

### Running UDisks

Since the libhal stub passes its calls to UDisks, UDisks should be running before you attempt to play DRM-protected Flash videos.

Make sure that `udisks2.service` is started, see [systemd#Using units](/index.php/Systemd#Using_units "Systemd") for details.

## Remove Flash Player cached files

To get a fresh start after installing the package(s), remove some Flash Player cached files:

```
$ rm -rf ~/.adobe/Flash_Player/{NativeCache,AssetCache,APSPrivateData2}

```

## See also

*   [Watching movies from Google Play on Arch Linux](http://isenmann.blogspot.gr/2012/08/watching-movies-from-google-play-with.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Flash_DRM_content&oldid=407798](https://wiki.archlinux.org/index.php?title=Flash_DRM_content&oldid=407798)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Multimedia players](/index.php/Category:Multimedia_players "Category:Multimedia players")