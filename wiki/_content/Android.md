# Android

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Android notifier](/index.php/Android_notifier "Android notifier")
*   [Android tethering](/index.php/Android_tethering "Android tethering")

## Contents

*   [1 Exploring Android device](#Exploring_Android_device)
*   [2 Android development](#Android_development)
    *   [2.1 Android SDK core components](#Android_SDK_core_components)
    *   [2.2 Android SDK platform API](#Android_SDK_platform_API)
    *   [2.3 Development environment](#Development_environment)
        *   [2.3.1 Android Studio](#Android_Studio)
        *   [2.3.2 Eclipse](#Eclipse)
        *   [2.3.3 Netbeans](#Netbeans)
    *   [2.4 Android Debug Bridge (ADB)](#Android_Debug_Bridge_.28ADB.29)
        *   [2.4.1 Connect device](#Connect_device)
        *   [2.4.2 Figure out device IDs](#Figure_out_device_IDs)
        *   [2.4.3 Adding udev Rules](#Adding_udev_Rules)
        *   [2.4.4 Configuring adb](#Configuring_adb)
        *   [2.4.5 Detect the device](#Detect_the_device)
        *   [2.4.6 General usage](#General_usage)
        *   [2.4.7 Notes & Troubleshooting](#Notes_.26_Troubleshooting)
    *   [2.5 NVIDIA Tegra platform](#NVIDIA_Tegra_platform)
*   [3 Building Android](#Building_Android)
    *   [3.1 OS bitness](#OS_bitness)
    *   [3.2 Required packages](#Required_packages)
    *   [3.3 Java Development Kit](#Java_Development_Kit)
    *   [3.4 Setting up the build environment](#Setting_up_the_build_environment)
    *   [3.5 Downloading the source code](#Downloading_the_source_code)
    *   [3.6 Building the code](#Building_the_code)
    *   [3.7 Testing the build](#Testing_the_build)
    *   [3.8 Creating a Flashable Image](#Creating_a_Flashable_Image)
*   [4 Restoring Android](#Restoring_Android)
    *   [4.1 Fastboot](#Fastboot)
    *   [4.2 Samsung devices](#Samsung_devices)
        *   [4.2.1 Heimdall](#Heimdall)
        *   [4.2.2 Odin (Virtualbox)](#Odin_.28Virtualbox.29)
*   [5 Alternative connection methods](#Alternative_connection_methods)
    *   [5.1 adb-sync](#adb-sync)
    *   [5.2 AirDroid](#AirDroid)
    *   [5.3 FTP](#FTP)
    *   [5.4 SSH Server](#SSH_Server)
    *   [5.5 Samba](#Samba)
*   [6 Tips & Tricks](#Tips_.26_Tricks)
    *   [6.1 During Debugging "Source not found"](#During_Debugging_.22Source_not_found.22)
    *   [6.2 Linux distribution on the sdcard](#Linux_distribution_on_the_sdcard)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Android Studio: Android Virtual Devices show 'failed to load'.](#Android_Studio:_Android_Virtual_Devices_show_.27failed_to_load.27.)
    *   [7.2 aapt: No such file or directory](#aapt:_No_such_file_or_directory)
    *   [7.3 ValueError: unsupported pickle protocol](#ValueError:_unsupported_pickle_protocol)

## Exploring Android device

There are few methods of exploring your device:

*   [MTP](/index.php/MTP "MTP") over USB for files transferring.
*   [Alternative methods](#Alternative_connection_methods) (such as FTP, SSH).

For more advanced usage, development, flashing and restore:

*   [ADB](#Android_Debug_Bridge_.28ADB.29) mostly for development purposes.
*   [Restoring Android](#Restoring_Android) for flashing and restoring Android firmwares (includes fastboot).

## Android development

There are 3 steps that need to be performed before you can develop Android applications on your Arch Linux box:

1.  Install the Android SDK core component,
2.  Install one or several Android SDK Platform packages,
3.  Install one of the IDEs compatible with the Android SDK.

### Android SDK core components

**Note:** If you are running a 64-bit system, make sure the [multilib](/index.php/Multilib "Multilib") repository is enabled to avoid "error: target not found: lib32-zlib" error messages.

Before developing Android applications, you need to install the Android SDK, which is made of 3 distinct packages, all installable from [AUR](/index.php/AUR "AUR"):

1.  [android-sdk](https://aur.archlinux.org/packages/android-sdk/)<sup><small>AUR</small></sup>
2.  [android-sdk-platform-tools](https://aur.archlinux.org/packages/android-sdk-platform-tools/)<sup><small>AUR</small></sup>
3.  [android-sdk-build-tools](https://aur.archlinux.org/packages/android-sdk-build-tools/)<sup><small>AUR</small></sup>

Android-sdk will be installed on `/opt/android-sdk`. This folder has root permissions, so keep in mind to run sdk manager as root, otherwise you will not be able to modify anything in this directory. If you intend to use it as a regular user, create the Android sdk users group:

```
# groupadd sdkusers

```

Add your user into this group:

```
# gpasswd -a <user> sdkusers

```

Change folder's group.

```
# chown -R :sdkusers /opt/android-sdk/

```

Change permissions of the folder so the user that was just added to the group will be able to write in it:

```
# chmod -R g+w /opt/android-sdk/

```

Re-login or as <user> log your terminal in to the newly created group:

```
$ newgrp sdkusers

```

**Note:** As an alternative to a global install with the [AUR](/index.php/AUR "AUR") packages, the SDK can be installed to a user's home directory via [the upstream instructions](https://developer.android.com/sdk/index.html).

### Android SDK platform API

Install the desired Android SDK Platform package from the [AUR](/index.php/AUR "AUR"):

*   [android-platform](https://aur.archlinux.org/packages/android-platform/)<sup><small>AUR</small></sup> (latest)
*   [android-platform-23](https://aur.archlinux.org/packages/android-platform-23/)<sup><small>AUR</small></sup>
*   [android-platform-22](https://aur.archlinux.org/packages/android-platform-22/)<sup><small>AUR</small></sup>
*   [android-platform-21](https://aur.archlinux.org/packages/android-platform-21/)<sup><small>AUR</small></sup>
*   [android-platform-20](https://aur.archlinux.org/packages/android-platform-20/)<sup><small>AUR</small></sup>
*   [android-platform-19](https://aur.archlinux.org/packages/android-platform-19/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/android-platform-19)]</sup>
*   [android-platform-18](https://aur.archlinux.org/packages/android-platform-18/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/android-platform-18)]</sup>
*   [android-platform-17](https://aur.archlinux.org/packages/android-platform-17/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/android-platform-17)]</sup>
*   [android-platform-16](https://aur.archlinux.org/packages/android-platform-16/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/android-platform-16)]</sup>
*   [android-platform-15](https://aur.archlinux.org/packages/android-platform-15/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/android-platform-15)]</sup>
*   [android-platform-14](https://aur.archlinux.org/packages/android-platform-14/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/android-platform-14)]</sup>
*   [android-platform-13](https://aur.archlinux.org/packages/android-platform-13/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/android-platform-13)]</sup>
*   [android-platform-12](https://aur.archlinux.org/packages/android-platform-12/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/android-platform-12)]</sup>
*   [android-platform-11](https://aur.archlinux.org/packages/android-platform-11/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/android-platform-11)]</sup>
*   [android-platform-10](https://aur.archlinux.org/packages/android-platform-10/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/android-platform-10)]</sup>
*   [android-platform-9](https://aur.archlinux.org/packages/android-platform-9/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/android-platform-9)]</sup>
*   [android-platform-8](https://aur.archlinux.org/packages/android-platform-8/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/android-platform-8)]</sup>
*   [android-platform-7](https://aur.archlinux.org/packages/android-platform-7/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/android-platform-7)]</sup>
*   [android-platform-6](https://aur.archlinux.org/packages/android-platform-6/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/android-platform-6)]</sup>
*   [android-platform-5](https://aur.archlinux.org/packages/android-platform-5/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/android-platform-5)]</sup>
*   [android-platform-4](https://aur.archlinux.org/packages/android-platform-4/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/android-platform-4)]</sup>
*   [android-platform-3](https://aur.archlinux.org/packages/android-platform-3/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/android-platform-3)]</sup>
*   [android-platform-2](https://aur.archlinux.org/packages/android-platform-2/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/android-platform-2)]</sup>

### Development environment

Android Studio is the new official Android development environment based on IntelliJ IDEA. Alternatively, you can use [Eclipse](/index.php/Eclipse "Eclipse") with the official but deprecated ADT plugin, or [Netbeans](/index.php/Netbeans "Netbeans") with the NBAndroid plugin. All are described below.

#### Android Studio

[Android Studio](https://developer.android.com/sdk/index.html) is the official Android development environment based on [IntelliJ Idea](https://www.jetbrains.com/idea/). Android Studio replaces the older [Eclipse Android Developer Tools](https://developer.android.com/tools/help/adt.html) and provides integrated Android developer tools for development and debugging.

You can download and install it with the [android-studio](https://aur.archlinux.org/packages/android-studio/)<sup><small>AUR</small></sup> package from the [AUR](/index.php/AUR "AUR"). If you get an error about a missing SDK, refer to the section Getting Android SDK platform API above.

**Note:** If you are using a tiling window manager other than i3wm, you may need to apply one of the fixes mentioned in [this](https://code.google.com/p/android/issues/detail?id=57675) issue page.

**Note:** Make sure you properly [set the Java environment](/index.php/Java#Change_default_Java_environment "Java") otherwise android-studio will not start.

**Note:** Bad font rendering in Android Studio can be fixed by installing the [infinality-bundle](/index.php/Infinality#Installation_2 "Infinality") and using infinality patched openJDK 7 ([jdk7-openjdk-infinality](https://aur.archlinux.org/packages/jdk7-openjdk-infinality/)<sup><small>AUR</small></sup>) or openJDK 8 ([jdk8-openjdk-infinality](https://aur.archlinux.org/packages/jdk8-openjdk-infinality/)<sup><small>AUR</small></sup>) from the AUR as mentioned in [this](https://youtrack.jetbrains.com/issue/IDEA-57233#comment=27-876236) issue page. Patched OpenJDK8 is also available from [Infinality unofficial repository](/index.php/Unofficial_user_repositories#infinality-bundle "Unofficial user repositories").

Normally, apps are built through the Android Studio GUI. To build apps from the commandline (using e.g. `./gradlew assembleDebug`), add the following to your `~/.bashrc`:

```
export ANDROID_HOME=/opt/android-sdk

```

#### Eclipse

**Note:** Since 2014-12-08, the ADT plugin is officially considered deprecated and Android Studio is now the official IDE.

Most stuff required for Android development in Eclipse is already packaged in AUR:

Official plugin by Google – [Eclipse ADT](http://developer.android.com/sdk/eclipse-adt.html):

1.  [eclipse-android](https://aur.archlinux.org/packages/eclipse-android/)<sup><small>AUR</small></sup>

Dependencies:

1.  [eclipse-emf](https://aur.archlinux.org/packages/eclipse-emf/)<sup><small>AUR</small></sup>
2.  [eclipse-gef](https://aur.archlinux.org/packages/eclipse-gef/)<sup><small>AUR</small></sup>
3.  [eclipse-wtp](https://aur.archlinux.org/packages/eclipse-wtp/)<sup><small>AUR</small></sup>

**Note:**

*   if you get a message about unresolvable dependencies, install [Java](/index.php/Java "Java") manually and try again.
*   as an alternative, you can install the ADT via eclipse's built in "add new software" command (see instructions on ADT site).
*   if you are in real trouble, it is also possible to download Android SDK and use the bundled Eclipse. This usually works without problems.
*   if you need to install extra SDK plugins not found in the AUR, you must change the file ownership of /opt/android-sdk first. You can do this with `# chgrp -R users /opt/android-sdk ; chmod -R 0775 /opt/android-sdk` (see [File Permissions](/index.php/File_Permissions "File Permissions") for more details).

Enter the path to the Android SDK Location in

```
Windows -> Preferences -> Android

```

**Note:**

If the plugins do not show up in Eclipse after the AUR package has been upgraded, then eclipse probably has out-of-date caches. Running `sudo eclipse -clean` once should clear them. If the problem persists, uninstall eclipse and all the plugins, delete `/usr/share/eclipse`, and reinstall everything.

#### Netbeans

If you prefer using [Netbeans](/index.php/Netbeans "Netbeans") as your IDE and want to develop Android applications, download the [NBAndroid](http://www.nbandroid.org) by going to:

```
Tools -> Plugins -> Settings

```

Add the following URL: [http://nbandroid.org/release81/updates/updates.xml](http://nbandroid.org/release81/updates/updates.xml)

Then go to **Available Plugins** and install the **Android** and **JUnit** plugins. Once you have installed go to:

```
Tools -> Options -> Miscellaneous -> Android

```

and select the path where the SDK is installed (/opt/android-sdk by default). That is it, now you can create a new Android project and start developing using Netbeans.

### Android Debug Bridge (ADB)

**Tip:** For some devices, you may have to enable MTP on the device, before ADB will work. Some other devices require enable PTP mode to work.

#### Connect device

To connect to a real device or phone via ADB under Arch, you must:

1.  Install [android-tools](https://www.archlinux.org/packages/?name=android-tools). In addition, you might want to install [android-udev](https://www.archlinux.org/packages/?name=android-udev) if you wish to connect the device to the proper `/dev/` entries.
2.  Enable USB Debugging on your phone or device:
    *   Jelly Bean (4.2) and newer: Go to `Settings --> About Phone` tap “Build Number” until you get a popup that you have become a developer (7 times). Then go to `Settings --> Developer --> USB debugging` and enable it.
    *   Older versions: This is usually done from `Settings --> Applications --> Development --> USB debugging`. Reboot the phone after checking this option to make sure USB debugging is enabled.
3.  Add yourself to the _adbusers_ group:

```
# gpasswd -a _username_ adbusers

```

If [ADB recognizes your device](#Does_it_work.3F) (it is visible and accessible in IDE), you are done. Otherwise see instructions below.

#### Figure out device IDs

Each Android device has a USB vendor/product ID. An example for HTC Evo is:

```
vendor id: 0bb4
product id: 0c8d

```

Plug in your device and execute:

```
$ lsusb

```

It should come up something like this:

```
Bus 002 Device 006: ID 0bb4:0c8d High Tech Computer Corp.

```

#### Adding udev Rules

Use the rules from [Android developer](http://source.android.com/source/initializing.html#configuring-usb-access) or you can use the following template for your udev rules, just replace [VENDOR ID] and [PRODUCT ID] with yours. Copy these rules into `/etc/udev/rules.d/51-android.rules`:

 `/etc/udev/rules.d/51-android.rules` 

```
SUBSYSTEM=="usb", ATTR{idVendor}=="[VENDOR ID]", MODE="0666", GROUP="adbusers"
SUBSYSTEM=="usb",ATTR{idVendor}=="[VENDOR ID]",ATTR{idProduct}=="[PRODUCT ID]",SYMLINK+="android_adb"
SUBSYSTEM=="usb",ATTR{idVendor}=="[VENDOR ID]",ATTR{idProduct}=="[PRODUCT ID]",SYMLINK+="android_fastboot"
```

Then, to reload your new udev rules, execute:

```
# udevadm control --reload-rules

```

#### Configuring adb

Instead of using udev rules, you may create/edit `~/.android/adb_usb.ini` which contains a list of vendor IDs.

```
$ cat ~/.android/adb_usb.ini 
0x27e8

```

#### Detect the device

After you have setup the udev rules, unplug your device and replug it.

After running:

```
$ adb devices

```

you should see something like:

```
List of devices attached 
HT07VHL00676    device

```

#### General usage

You can now use adb to transfer files between the device and your computer. To transfer files to the device, use

```
$ adb push _<what-to-copy>_ _<where-to-place>_

```

To transfer files from the device, use

```
$ adb pull _<what-to-pull>_ _<where-to-place>_

```

#### Notes & Troubleshooting

*   **ADB** can also be installed via [platform tools](#Android_SDK_platform_API)(usually available in `/opt/android-sdk/platform-tools/`), so it might not be necesarry to install [android-tools](https://www.archlinux.org/packages/?name=android-tools) (available in `/usr/bin/`).

*   If you are getting an empty list (your device is not there), it may be because you have not enabled USB debugging on your device. You can do that by going to Settings => Applications => Development and enabling USB debugging. On Android 4.2 (Jelly Bean) the Development menu is hidden; to enable it go to Settings => About phone and tap Build number 7 times.

*   If there are still problems such as _adb_ displaying `???????? no permissions` under devices, try restarting the adb server as root.

```
# adb kill-server
# adb start-server

```

### NVIDIA Tegra platform

If you target your application at NVIDIA Tegra platform, you might also want to install tools, samples and documentation provided by NVIDIA. In [NVIDIA Developer Zone for Mobile](http://developer.nvidia.com/category/zone/mobile-development) there are two tools:

1.  The [Tegra Android Development Pack](http://developer.nvidia.com/tegra-resources) provides tools (NVIDIA Debug Manager) related to [Eclipse ADT](http://developer.android.com/sdk/eclipse-adt.html) and their documentation.
2.  The [Tegra Toolkit](http://developer.nvidia.com/tegra-resources) provides tools (mostly CPU and GPU optimization related), samples and documentation.

Both are currently not available in the [AUR](/index.php/AUR "AUR") anymore, because NVIDIA requires a registration/login for the download.

## Building Android

Please note that these instructions are based on the [official AOSP build instructions](http://source.android.com/source/building.html). Other Android-derived systems such as CyanogenMod will often require extra steps.

### OS bitness

Android 2.2.x (Froyo) and below are the only versions of Android that will build on a 32-bit system. For 2.3.x (Gingerbread) and above, you will need a 64-bit installation.

### Required packages

To build any version of Android, you need to install these packages:

*   32-bit and 64-bit systems: [gcc](https://www.archlinux.org/packages/?name=gcc) [git](https://www.archlinux.org/packages/?name=git) [gnupg](https://www.archlinux.org/packages/?name=gnupg) [flex](https://www.archlinux.org/packages/?name=flex) [bison](https://www.archlinux.org/packages/?name=bison) [gperf](https://www.archlinux.org/packages/?name=gperf) [sdl](https://www.archlinux.org/packages/?name=sdl) [wxgtk](https://www.archlinux.org/packages/?name=wxgtk) [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools) [curl](https://www.archlinux.org/packages/?name=curl) [ncurses](https://www.archlinux.org/packages/?name=ncurses) [zlib](https://www.archlinux.org/packages/?name=zlib) [schedtool](https://www.archlinux.org/packages/?name=schedtool) [perl-switch](https://www.archlinux.org/packages/?name=perl-switch) [zip](https://www.archlinux.org/packages/?name=zip) [unzip](https://www.archlinux.org/packages/?name=unzip) [libxslt](https://www.archlinux.org/packages/?name=libxslt) [python2-virtualenv](https://www.archlinux.org/packages/?name=python2-virtualenv) [bc](https://www.archlinux.org/packages/?name=bc)

*   64-bit systems only: [gcc-multilib](https://www.archlinux.org/packages/?name=gcc-multilib) [lib32-zlib](https://www.archlinux.org/packages/?name=lib32-zlib) [lib32-ncurses](https://www.archlinux.org/packages/?name=lib32-ncurses) [lib32-readline](https://www.archlinux.org/packages/?name=lib32-readline)

*   AUR Packages: [libtinfo](https://aur.archlinux.org/packages/libtinfo/)<sup><small>AUR</small></sup> [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/)<sup><small>AUR</small></sup>

To build Android 6+, you need to install these additional packages:

*   32-bit and 64-bit systems: [rsync](https://www.archlinux.org/packages/?name=rsync)

**Note:** You must now also install [lib32-ncurses5-compat-libs](https://aur.archlinux.org/packages/lib32-ncurses5-compat-libs/)<sup><small>AUR</small></sup> & [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/)<sup><small>AUR</small></sup> since ncurses was updated to ncurses6 and android's prebuilt clang still depends on ncurses5\. You can check what libs are still needed: `ldd prebuilts/clang/linux-x86/host/3.6/bin/clang` 

### Java Development Kit

Android 5 (Lollipop) can be built with [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk).

Older versions [require](http://source.android.com/source/initializing.html) a working **Oracle JDK** installed on your build system. It **will not** work with OpenJDK.

*   For Gingerbread through KitKat (2.3 - 4.4), Java 6 is required, which is available as [jdk6](https://aur.archlinux.org/packages/jdk6/)<sup><small>AUR</small></sup> from the AUR. See [Java](/index.php/Java "Java") if you want to use it besides another (newer) JDK version.
*   For Cupcake through Froyo (1.5 - 2.2), Java 5 is required, which is no longer available for Arch Linux.

### Setting up the build environment

Download the `repo` utility per [Android Downloading the Source guide](https://source.android.com/source/downloading.html).

```
$ mkdir ~/bin
$ export PATH=~/bin:$PATH
$ curl [https://storage.googleapis.com/git-repo-downloads/repo](https://storage.googleapis.com/git-repo-downloads/repo) > ~/bin/repo
$ chmod a+x ~/bin/repo

```

Create a directory to build.

```
$ mkdir ~/android
$ cd ~/android

```

You will need to change the default Python from version 3 to version 2:

```
$ virtualenv2 venv # Creates a directory, venv/, containing the Virtualenv

```

**Note:** During build you may receive error pertaining to missing python modules. A quick and dirty fix is to symlink /usr/lib/python2.7/* to ~/android/venv/python2.7/ (Change ~/android to reflect your build directory if different than above).

Example:

```
$ ln -s /usr/lib/python2.7/* /Data/Android_Build/venv/lib/python2.7/

```

Activate the Virtualenv, which will update $PATH to point at Python 2.

**Note:** this activation is only active for the current terminal session.

```
$ source venv/bin/activate

```

### Downloading the source code

This will clone the repositories. You **only** need to do this the first time you build Android, or if you want to switch branches.

*   The `repo` has a `-j` switch that operates similarly to the one used with `make`. Since it controls the number of simultaneous downloads, you should adjust the value depending on downstream network bandwidth.

*   You will need to specify a **branch** (release of Android) to check out with the `-b` switch. If you leave the switch out, you will get the so-called **master branch**.

```
$ repo init -u [https://android.googlesource.com/platform/manifest](https://android.googlesource.com/platform/manifest) -b master
$ repo sync -j4

```

**Note:** To further decrease sync times, you can utilize the -c switch with the repo command as such:

```
$ repo sync -j8 -c

```

The `-c` switch will only sync the branch which is specified in the manifest, which in turn is determined by the branch specified with the `-b` switch, or the default branch set by the repository maintainer.

Wait a long time. Just the uncompiled source code, along with the `.repo` and `.git` directories that are used to keep track of it, are well over 10 GB.

**Note:** If you want to update your local copy of the Android source, at a later time, simply enter the build directory, load the Virtualenv, and re-sync:

```
$ repo sync

```

### Building the code

This should do what you need for AOSP:

```
$ source build/envsetup.sh
$ lunch full-eng
$ make -j4

```

If you run **lunch** without arguments, it will ask what build you want to create. Use -j with a number between one and two times number of cores/threads.

The build takes a very long time.

**Note:** If `make` fails with something like

```
flex-2.5.39: loadlocale.c:131: _nl_intern_locale_data: Assertion `cnt < (sizeof (_nl_value_type_LC_COLLATE) / sizeof (_nl_value_type_LC_COLLATE[0]))' failed.

```

try running `LANG=C make` instead.

**Note:** Make sure you have enough RAM.

Android will use the /tmp directory heavily. By default the size of the partition the /tmp folder is mounted on is half the size of your RAM. If it fills up, the build will fail. 4GB of RAM or more is recommended.

*   Alternatively, you can get rid of the tmpfs from [fstab](/index.php/Fstab "Fstab") all together.

**Note:** From the [Android Building and Running guide](https://source.android.com/source/building-running.html#build-the-code):

"GNU make can handle parallel tasks with a -jN argument, and it's common to use a number of tasks N that's between 1 and 2 times the number of hardware threads on the computer being used for the build. E.g. on a dual-E5520 machine (2 CPUs, 4 cores per CPU, 2 threads per core), the fastest builds are made with commands between make -j16 and make -j32."

### Testing the build

When finished, run/test the final image(s).

```
$ emulator

```

### Creating a Flashable Image

To create an image that can be flashed it is necessary to:

```
make -j8 updatepackage

```

This will create a zip image under **out/target/product/hammerhead** (hammerhead being the device name) that can be flashed.

## Restoring Android

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Android#](https://wiki.archlinux.org/index.php/Talk:Android))

In some cases, you want to return to the stock Android after flashing custom ROMs to your Android mobile device. For flashing instructions of your device, please use [XDA forums](http://forum.xda-developers.com/).

### Fastboot

Fastboot (as well as [ADB](#Connecting_to_a_real_device_-_Android_Debug_Bridge_.28ADB.29)) comes together with a package [android-tools](https://www.archlinux.org/packages/?name=android-tools) from the [official repositories](/index.php/Official_repositories "Official repositories").

**Note:** Restoring firmwares using `fastboot` can be quite tricky, but you might want to browse [XDA developers forums](http://www.xda-developers.com/) for a stock firmware, which is mostly a `*.zip` file, but inside of it, comes with the firmware files and `flash-all.sh` script. For example, [Google Nexus](https://developers.google.com/android/nexus/images) firmwares include `flash-all.sh` script or another example could be for OnePlus One - [XDA thread](http://forum.xda-developers.com/oneplus-one/general/guide-return-opo-to-100-stock-t2826541), where you can find firmwares with included `flash-all.sh` script.

### Samsung devices

Samsung devices can't be flashed using **Fastboot** tool. Alternatives are only **Heimdall** and **Odin** (by using Windows and VirtualBox).

#### Heimdall

[Heimdall](http://glassechidna.com.au/heimdall/) is a cross-platform open-source tool suite used to flash firmware (also known as ROMs) onto Samsung mobile devices and is also known as an alternative to [Odin](http://odindownload.com/). It can be installed as [heimdall](https://www.archlinux.org/packages/?name=heimdall) or [heimdall-git](https://aur.archlinux.org/packages/heimdall-git/)<sup><small>AUR</small></sup>.

The flashing instructions can be found on Heimdall's [GitHub page](https://github.com/Benjamin-Dobell/Heimdall/tree/master/Linux) or on [XDA forums](http://forum.xda-developers.com/showthread.php?t=1922461).

#### Odin (Virtualbox)

It is also possible to restore stock Android on the Samsung devices using [Odin](http://odindownload.com/), but inside the [VirtualBox](/index.php/VirtualBox "VirtualBox"). For more information, see [XDA thread](http://forum.xda-developers.com/showthread.php?t=758634).

Arch Linux related steps:

1.  Install [VirtualBox](/index.php/VirtualBox "VirtualBox") together with its [extension pack](/index.php/VirtualBox#Extension_pack "VirtualBox") and [guest additions](/index.php/VirtualBox#Guest_additions_disc "VirtualBox").
2.  Install your preferred, but compatible with Odin, Windows operating system (with VirtualBox guest additions) into a virtual hard drive using VirtualBox
3.  Open VirtualBox settings of your Windows operating system, navigate to **USB**, then tick (or make sure it is ticked) **Enable USB 2.0 (EHCI) Controller**.
4.  At VirtualBox running Windows operating system, click in the menu bar **Devices**, then **USB Devices**, then click on your Samsung mobile device connected to your computer via USB.

Windows related links:

*   Samsung drivers can be downloaded from [here](http://androidxda.com/download-samsung-usb-drivers).
*   Odin can be downloaded from [here](https://www.androidfilehost.com/?fid=23501681358557126).
*   Samsung Android firmwares can be downloaded from [here](http://www.sammobile.com/firmwares/).

If you want to make sure that everything is working and ready, connect your Samsung device turned on into a Download mode, and open Odin. The white box (a big one at the bottom-left) named **Message**, should print a line similar to this:

```
<ID:0/003> Added!!

```

which means that your device is visible to Odin and is ready to be flashed.

**Note:** There are no general instructions of restoring stock firmware on Samsung mobile devices. You have to use [Google](https://www.google.com) and [XDA developers forums](http://www.xda-developers.com) to find a flashing instructions for specific device. For example, this is how the [thread](http://goo.gl/cZLyF8) about the Samsung Galaxy S4 looks like

## Alternative connection methods

### adb-sync

[adb-sync](https://github.com/google/adb-sync) (available in [adb-sync-git](https://aur.archlinux.org/packages/adb-sync-git/)<sup><small>AUR</small></sup>) is a tool to synchronize files between a PC and an Android device using the ADB

### AirDroid

[AirDroid](http://goo.gl/EZQ9GQ) is an Android app to access files from your web browser.

### FTP

You run a FTP server on Arch and connect to it from your phone, or the other way around: run a FTP server on your phone and connect to it from Arch.

See [List of applications/Internet#FTP](/index.php/List_of_applications/Internet#FTP "List of applications/Internet"). There are a lot of FTP clients/servers available for Android.

### SSH Server

There are many SSH servers available for Android, it allows you to transfer files using `scp` command. See also [SSH](/index.php/SSH "SSH").

### Samba

See [Samba](/index.php/Samba "Samba").

## Tips & Tricks

### During Debugging "Source not found"

Most probably the debugger wants to step into the Java code. As the source code of Android does not come with the Android SDK, this leads to an error. The best solution is to use step filters to not jump into the Java source code. Step filters are not activated by default. To activate them:

```
Window -> Preferences -> Java -> Debug -> Step Filtering

```

Consider to select them all. If appropriate you can add the android.* package. See the forum post for more information: [http://www.eclipsezone.com/eclipse/forums/t83338.rhtml](http://www.eclipsezone.com/eclipse/forums/t83338.rhtml)

### Linux distribution on the sdcard

You can install Debian like in this [thread](http://forum.xda-developers.com/showthread.php?t=631389). Excellent guide to installing Arch in chroot (in parallel with Android) can be found on [archlinuxarm.org forum](http://archlinuxarm.org/forum/viewtopic.php?f=27&t=1361&start=40).

## Troubleshooting

### Android Studio: Android Virtual Devices show 'failed to load'.

Make sure you've exported the variable `ANDROID_HOME` as explained in [Android Studio](/index.php/Android_Studio "Android Studio").

### aapt: No such file or directory

The build tools include 32-bit binaries. For this reason they require 32-bit libraries. If you happened to install the SDK manually, you will additionally need to install **multilib/lib32-libstdc++5** and **multilib/lib32-zlib**.

### ValueError: unsupported pickle protocol

One fix is to issue:

```
rm ~/.repopickle_.gitconfig

```

If that does not work, then try this:

```
rm `find /path/to/android-root -name .repopickle_config`

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Android&oldid=417219](https://wiki.archlinux.org/index.php?title=Android&oldid=417219)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Development](/index.php/Category:Development "Category:Development")
*   [Mobile devices](/index.php/Category:Mobile_devices "Category:Mobile devices")

Hidden categories:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")
*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")