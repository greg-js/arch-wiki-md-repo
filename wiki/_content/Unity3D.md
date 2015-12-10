# Unity3D

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

From [Unity - Game engine, tools and multiplatform](https://unity3d.com/unity):

_Unity is a flexible and powerful development platform for creating multiplatform 3D and 2D games and interactive experiences. It's a complete ecosystem for anyone who aims to build a business on creating high-end content and connecting to their most loyal and enthusiastic players and customers._

Not to be confused with Canonical's [Unity](/index.php/Unity "Unity").

**Note:** The Linux Editor is currently experimental. Please report all bugs to the [Unity forums](http://forum.unity3d.com/forums/linux-editor-support-feedback-experimental.93/)!

## Contents

*   [1 Installation](#Installation)
*   [2 Android Remote](#Android_Remote)
    *   [2.1 Prepare computer](#Prepare_computer)
        *   [2.1.1 Install packages](#Install_packages)
        *   [2.1.2 Configure the Editor](#Configure_the_Editor)
    *   [2.2 Prepare Android](#Prepare_Android)
    *   [2.3 Test](#Test)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Unity crashes on first launch before/while signing in](#Unity_crashes_on_first_launch_before.2Fwhile_signing_in)
    *   [3.2 Unity crashes when trying to load project](#Unity_crashes_when_trying_to_load_project)
    *   [3.3 Unity crashes if ~/.config/user-dirs.dir is missing](#Unity_crashes_if_.7E.2F.config.2Fuser-dirs.dir_is_missing)

## Installation

**Warning:** The Unity package is **huge**. For a successful installation you'll need about 8GiB of free space for the package building, and another 2.5GiB for it to install.

Simply install the [AUR](/index.php/AUR "AUR") package [unity-editor](https://aur.archlinux.org/packages/unity-editor/)<sup><small>AUR</small></sup>.

## Android Remote

[Unity Remote](http://docs.unity3d.com/Manual/UnityRemote4.html) is an Android app to help test input for Android devices. It achieves this by sending a compressed screenshot to the device each frame.

### Prepare computer

#### Install packages

[Install](/index.php/Install "Install") the [android-udev](https://www.archlinux.org/packages/?name=android-udev) package, which will ensure you have correct [udev](/index.php/Udev "Udev") rules for your device.

Install the [android-sdk](https://aur.archlinux.org/packages/android-sdk/)<sup><small>AUR</small></sup> package and one of the packages from the [java-environment](https://www.archlinux.org/packages/?name=java-environment)<sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): package not found]</sup> group, preferably JDK7, though it's reported to (and should) work with OpenJDK too.

#### Configure the Editor

Open the editor, navigate to _Edit -> Preferences_ and set the correct paths to the Android SDK and the JDK.

**Tip:**

*   The Android SDK is usually in `/opt/android-sdk`.
*   The JDK varies by the version you are using, if you want to use the default set it to `/usr/lib/jvm/default`.

The navigate to _Edit -> Project Settings -> Editor_ and set `Unity Remote Device` to `Any Android Device`.

For more help see the [Unity documentation](http://docs.unity3d.com/Manual/android-sdksetup.html).

### Prepare Android

Install [Unity Remote 4](https://play.google.com/store/apps/details?id=com.unity3d.genericremote) from the Play Store. Alternatively you can download and build it yourself from the Asset Store.

It is also [recommended](http://www.howtogeek.com/192732/android-usb-connections-explained-mtp-ptp-and-usb-mass-storage/) to set your Android device to PTP mode.

**Note:** Don’t forget to turn on “USB Debugging” on your device. Go to _Settings -> Developer_ options, then enable USB debugging. As of Android Jelly Bean 4.2 the Developer options are hidden by default. To enable them tap on _Settings -> About Phone -> Build Version_ multiple times. Then you will be able to access the _Settings -> Developer_ options.

For more help see the [Unity documentation](http://docs.unity3d.com/Manual/UnityRemote4.html).

### Test

If you have Unity opened, close it.

Connect the phone to the computer and launch Unity Remote.

Open the Editor and press play. You should now see your game transmitted to your Android device.

If it doesn't work or you have questions, see the [Unity Documentation](http://docs.unity3d.com/Manual/UnityRemote4.html).

## Troubleshooting

### Unity crashes on first launch before/while signing in

This is a rare bug where Unity's configuration gets created wrongly. You can try resetting it by:

 `$ rm -rf ~/.config/unity3d/{*.prefs,*.log,Preferences} ` 

### Unity crashes when trying to load project

Users have [reported](http://forum.unity3d.com/threads/unity-on-arch-manjaro-linux.350315/page-3#post-2271637) that unsetting `GTK_IM_MODULE` prevents the crash.

### Unity crashes if ~/.config/user-dirs.dir is missing

See how to generate the xdg files here: [Xdg user directories](/index.php/Xdg_user_directories "Xdg user directories")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Unity3D&oldid=408765](https://wiki.archlinux.org/index.php?title=Unity3D&oldid=408765)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Gaming](/index.php/Category:Gaming "Category:Gaming")