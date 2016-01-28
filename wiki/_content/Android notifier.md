# Android notifier

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Android Notifier is a linux application that receives notifications on sms, mms, battery status and more from your phone to your Linux, Mac or Windows PC. This article is about installing and running it in the background on Arch Linux.

## Contents

*   [1 Prerequisites](#Prerequisites)
*   [2 Installation](#Installation)
*   [3 Configuration](#Configuration)
*   [4 Starting android-notifier](#Starting_android-notifier)
*   [5 Alternative Desktop Client](#Alternative_Desktop_Client)

## Prerequisites

*   Android app installed on your phone: Remote Notifier by Rodrigo Damazio, from [Google Play](https://play.google.com/store/apps/details?id=org.damazio.notifier) or [F-Droid](https://f-droid.org/repository/browse/?fdid=org.damazio.notifier).
    *   [Author's site](http://code.google.com/p/android-notifier/)
    *   [More at Appbrain](http://www.appbrain.com/app/remote-notifier-for-android/org.damazio.notifier/)
*   Port 10600 tcp/udp open in your firewall

## Installation

Get it from AUR: [android-notifier-desktop](https://aur.archlinux.org/packages/android-notifier-desktop/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/android-notifier-desktop)]</sup>

## Configuration

To configure android-notifier, run `/usr/share/android-notifier-desktop/run.sh -p`.

To show help run `/usr/share/android-notifier-desktop/run.sh -h`.

## Starting android-notifier

Add this command to for example .xinitrc:

```
/usr/share/android-notifier-desktop/run.sh &

```

Or just run it from terminal.

## Alternative Desktop Client

Another option for running desktop notification client is [Cyborg](https://github.com/hades/Cyborg). This client does not support some features of original application, such as encryption

Retrieved from "[https://wiki.archlinux.org/index.php?title=Android_notifier&oldid=394837](https://wiki.archlinux.org/index.php?title=Android_notifier&oldid=394837)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Status monitoring and notification](/index.php/Category:Status_monitoring_and_notification "Category:Status monitoring and notification")
*   [Mobile devices](/index.php/Category:Mobile_devices "Category:Mobile devices")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")