# Sync and connect with Windows Mobile

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This page is a howto for connecting your Windows Mobile device with Archlinux. Afterwards you can sync and install cabs just like you can do with activesync in windows. It uses the kde app synce-kde, but gnome and *box users can relax, the only qt-deps are qscintilla-2.3.2-2 and pyqt-4.4.4-2\. And they are small.

## Contents

*   [1 Installation](#Installation)
*   [2 Connecting to your phone](#Connecting_to_your_phone)
*   [3 Troubleshooting](#Troubleshooting)
*   [4 Other problems](#Other_problems)
*   [5 Work with PocketPC files from file manager](#Work_with_PocketPC_files_from_file_manager)

## Installation

1.  [Install](/index.php/Install "Install") [synce-odccm](https://aur.archlinux.org/packages/synce-odccm/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/synce-odccm)]</sup> package from the [AUR](/index.php/AUR "AUR")
2.  [Install](/index.php/Install "Install") [synce-kde](https://www.archlinux.org/packages/?name=synce-kde) and [synce-sync-engine](https://www.archlinux.org/packages/?name=synce-sync-engine) packages, available in the [Official repositories](/index.php/Official_repositories "Official repositories")

## Connecting to your phone

1.  Start odccm: `# odccm` 
2.  Start sync-engine. You can use "sync-engine -d" to have it running in the background as a daemon.
3.  Start synce-kpm
4.  Connect your WM phone.

Now you can sync your phone, install cabs and so on. Have fun.Before syncing you will have to create a partnership with your phone. Just as with active sync in Windows.

## Troubleshooting

If your phone does not show in synce-kpm, make sure the activesync-setting in your phone is set to "activesync", and not "mass storage device"" or similar. (Settings → Connections → USB connection settings)

## Other problems

There is only one problem I have experienced with this. Sometimes it will stop working, and you will get an error report on your phone saying device.exe had a problem and was teminated. To fix this, simply go to USB-connection setting, choose "mass storage device" and select Ok, and then select "active sync" and again ok.

If the above did not work, you might have to quit/kill sync-engine and odccm, and restart them. Start odccm first. This seems to be necessary when sync-engine is stuck at " Authorization pending - waiting for password on device" You will get output if you start sync-engine without the -d option.

I think this problem arises after the phone has suspended, but I'm not quite sure what really causes it.

## Work with PocketPC files from file manager

There is a [SynCE FS](http://www.lvivier.info/SynceFS/) project, which is aimed to provide a possibility to work with winmobile device filesystem as a remote filesystem. It ts based on [SynCE](http://synce.sourceforge.net) and [Coda](http://www.coda.cs.cmu.edu/).

Install [syncefs](https://aur.archlinux.org/packages/syncefs/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/syncefs)]</sup>, available in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). To use SynCE FS, you need a working SynCE installation.

At the first step you need to load `coda` [kernel module](/index.php/Kernel_module "Kernel module").

At the next step you need to start SynCE tools: `odccm` and `sync-engine`.

Finally you can mount your PocketPC filesystem with a command:

 `mount /mnt/synce` 

(Directory /mnt/synce is normally created during installation. If not - please create it manually.)

Now you can use your PocketPC filesystem from /mnt/synce directory.

**Tip:**

To mount PocketPC filesystem as ordinal user (non-root), you need to add the following to your fstab:

 `none /mnt/synce cefs rw,user,noauto,codadev=/dev/cfs0 0 0` 

Retrieved from "[https://wiki.archlinux.org/index.php?title=Sync_and_connect_with_Windows_Mobile&oldid=392699](https://wiki.archlinux.org/index.php?title=Sync_and_connect_with_Windows_Mobile&oldid=392699)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Mobile devices](/index.php/Category:Mobile_devices "Category:Mobile devices")