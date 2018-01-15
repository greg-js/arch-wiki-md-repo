Related articles

*   [Android tethering](/index.php/Android_tethering "Android tethering")

## Contents

*   [1 Exploring Android device](#Exploring_Android_device)
*   [2 Android development](#Android_development)
    *   [2.1 Android Studio](#Android_Studio)
    *   [2.2 Manual SDK installation](#Manual_SDK_installation)
        *   [2.2.1 Android SDK core components](#Android_SDK_core_components)
        *   [2.2.2 Android SDK platform API](#Android_SDK_platform_API)
        *   [2.2.3 Android System Images](#Android_System_Images)
    *   [2.3 Other IDEs](#Other_IDEs)
        *   [2.3.1 Netbeans](#Netbeans)
        *   [2.3.2 Eclipse](#Eclipse)
    *   [2.4 Android Debug Bridge](#Android_Debug_Bridge)
        *   [2.4.1 Connect device](#Connect_device)
        *   [2.4.2 Figure out device IDs](#Figure_out_device_IDs)
        *   [2.4.3 Adding udev Rules](#Adding_udev_Rules)
        *   [2.4.4 Configuring adb](#Configuring_adb)
        *   [2.4.5 Detect the device](#Detect_the_device)
        *   [2.4.6 General usage](#General_usage)
        *   [2.4.7 Notes & Troubleshooting](#Notes_.26_Troubleshooting)
    *   [2.5 NVIDIA Tegra platform](#NVIDIA_Tegra_platform)
*   [3 Building Android](#Building_Android)
    *   [3.1 Required packages](#Required_packages)
    *   [3.2 Java Development Kit](#Java_Development_Kit)
    *   [3.3 Setting up the build environment](#Setting_up_the_build_environment)
    *   [3.4 Downloading the source code](#Downloading_the_source_code)
    *   [3.5 Building the code](#Building_the_code)
    *   [3.6 Testing the build](#Testing_the_build)
    *   [3.7 Creating a Flashable Image](#Creating_a_Flashable_Image)
*   [4 Restoring Android](#Restoring_Android)
    *   [4.1 Fastboot](#Fastboot)
    *   [4.2 Samsung devices](#Samsung_devices)
        *   [4.2.1 Heimdall](#Heimdall)
        *   [4.2.2 Odin (Virtualbox)](#Odin_.28Virtualbox.29)
*   [5 Connection software](#Connection_software)
*   [6 Tips & Tricks](#Tips_.26_Tricks)
    *   [6.1 During Debugging "Source not found"](#During_Debugging_.22Source_not_found.22)
    *   [6.2 Linux distribution on the sdcard](#Linux_distribution_on_the_sdcard)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Android Studio: Android Virtual Devices show 'failed to load'.](#Android_Studio:_Android_Virtual_Devices_show_.27failed_to_load.27.)
    *   [7.2 Android Studio: 'failed to create the SD card'](#Android_Studio:_.27failed_to_create_the_SD_card.27)
    *   [7.3 ValueError: unsupported pickle protocol](#ValueError:_unsupported_pickle_protocol)
    *   [7.4 libGL error: failed to load driver: swrast OR AVD doesn't load and no error message displayed](#libGL_error:_failed_to_load_driver:_swrast_OR_AVD_doesn.27t_load_and_no_error_message_displayed)
    *   [7.5 sh: glxinfo: command not found](#sh:_glxinfo:_command_not_found)
    *   [7.6 Android Emulator: no keyboard input in xfwm4](#Android_Emulator:_no_keyboard_input_in_xfwm4)

## Exploring Android device

When you connect a modern Android device via USB to a computer you can use [MTP](/index.php/MTP "MTP") to transfer files and [#Android Debug Bridge](#Android_Debug_Bridge) to debug it.

Files can generally be transferred with various protocols ([SSH](/index.php/SSH "SSH"), [FTP](/index.php/Category:File_Transfer_Protocol "Category:File Transfer Protocol"), [Samba](/index.php/Samba "Samba"), HTTP). You just need to setup a client and a server (via apps Android can act as either one).

For flashing and restoring Android firmware see [#Restoring Android](#Restoring_Android).

See [#Connection software](#Connection_software) for software available for Arch Linux that can be used to connect to Android.

## Android development

To develop Android applications you need three things:

*   the Android SDK core component
*   one or several Android SDK Platform packages
*   an IDE

The official IDE for Android is [#Android Studio](#Android_Studio), which comes with its own SDK manager.

### Android Studio

[Android Studio](https://developer.android.com/studio/index.html) is the official Android development environment based on [IntelliJ Idea](https://www.jetbrains.com/idea/). It provides integrated Android developer tools for development and debugging.

You can [install](/index.php/Install "Install") it with the [android-studio](https://aur.archlinux.org/packages/android-studio/) package. If you get an error about a missing SDK, refer to [#Android SDK platform API](#Android_SDK_platform_API) above.

**Note:**

*   If you are using a tiling window manager other than [i3](/index.php/I3 "I3"), you may need to apply one of the fixes mentioned in [this](https://code.google.com/p/android/issues/detail?id=57675) issue page.
*   Make sure you properly [set the Java environment](/index.php/Java#Change_default_Java_environment "Java") otherwise android-studio will not start.

Normally, apps are built through the Android Studio GUI. To build apps from the commandline (using e.g. `./gradlew assembleDebug`), add the following to your `~/.bashrc`:

```
export ANDROID_HOME=/opt/android-sdk

```

### Manual SDK installation

If you are using [#Android Studio](#Android_Studio) and want the IDE to manage your SDK installation, you can skip this section.

#### Android SDK core components

**Note:**

*   If you are running a 64-bit system, make sure the [multilib](/index.php/Multilib "Multilib") repository is enabled to avoid `error: target not found: lib32-*` error messages.

Before developing Android applications, you need to install the Android SDK, which is made of 4 distinct packages, all installable from [AUR](/index.php/AUR "AUR"):

1.  [android-platform](https://aur.archlinux.org/packages/android-platform/)
2.  [android-sdk](https://aur.archlinux.org/packages/android-sdk/)
3.  [android-sdk-platform-tools](https://aur.archlinux.org/packages/android-sdk-platform-tools/)
4.  [android-sdk-build-tools](https://aur.archlinux.org/packages/android-sdk-build-tools/)

If supporting older devices, or working with older code, [android-support](https://aur.archlinux.org/packages/android-support/) and [android-support-repository](https://aur.archlinux.org/packages/android-support-repository/) might be required.

Android-sdk will be installed on `/opt/android-sdk/`. This folder has root permissions, so keep in mind to run sdk manager as root, otherwise you will not be able to modify anything in this directory. If you intend to use it as a regular user, create the Android sdk users group:

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

**Note:** As an alternative to a global install with the [AUR](/index.php/AUR "AUR") packages, the SDK can be installed to a user's home directory via [the upstream instructions](https://developer.android.com/sdk/index.html). You may also use the android-*-dummy packages in the [AUR](/index.php/AUR "AUR") to handle the system dependencies.

#### Android SDK platform API

Install the desired Android SDK Platform package from the [AUR](/index.php/AUR "AUR"):

*   [android-platform](https://aur.archlinux.org/packages/android-platform/) – the latest API
*   the [AUR](/index.php/AUR "AUR") also contains older APIs[[1]](https://aur.archlinux.org/packages/?K=android-platform-)

#### Android System Images

Install the desired [Android system image](https://aur.archlinux.org/packages/?K=android-+system+image) package from the [AUR](/index.php/AUR "AUR"). The Images are needed for emulating a specific android device. They are not needed if you want to develop with an android phone.

### Other IDEs

Android Studio is the official Android development environment based on IntelliJ IDEA. Alternatively, you can use [Netbeans](/index.php/Netbeans "Netbeans") with the NBAndroid plugin. All are described below.

#### Netbeans

If you prefer using [Netbeans](/index.php/Netbeans "Netbeans") as your IDE and want to develop Android applications, download the [NBAndroid](http://www.nbandroid.org) by going to *Tools > Plugins > Settings*.

Add the following URL: [http://nbandroid.org/release81/updates/updates.xml](http://nbandroid.org/release81/updates/updates.xml)

Then go to *Available Plugins* and install the *Android* and *JUnit* plugins. Once you have installed go to *Tools > Options > Miscellaneous > Android*.

and select the path where the SDK is installed (`/opt/android-sdk` by default). That is it, now you can create a new Android project and start developing using Netbeans.

#### Eclipse

**Note:** The Eclipse ADT plugin is no longer supported. Google recommends to use Android Studio instead.[[2]](https://android-developers.googleblog.com/2016/11/support-ended-for-eclipse-android.html)

The official, but deprecated, [Eclipse ADT](http://developer.android.com/sdk/eclipse-adt.html) plugin can be installed with the [eclipse-android](https://aur.archlinux.org/packages/eclipse-android/) package.

**Note:**

*   if you get a message about unresolvable dependencies, install [Java](/index.php/Java "Java") manually and try again.
*   as an alternative, you can install the ADT via eclipse's built in "add new software" command (see instructions on ADT site).
*   if you are in real trouble, it is also possible to download Android SDK and use the bundled Eclipse. This usually works without problems.
*   if you need to install extra SDK plugins not found in the AUR, you must change the file ownership of /opt/android-sdk first. You can do this with `# chgrp -R users /opt/android-sdk ; chmod -R 0775 /opt/android-sdk` (see [File Permissions](/index.php/File_Permissions "File Permissions") for more details).

Enter the path to the Android SDK Location in *Windows > Preferences > Android*.

**Note:** If the plugins do not show up in Eclipse after the AUR package has been upgraded, then eclipse probably has out-of-date caches. Running `sudo eclipse -clean` once should clear them. If the problem persists, uninstall eclipse and all the plugins, delete `/usr/share/eclipse`, and reinstall everything.

### Android Debug Bridge

**Tip:**

*   For some devices, you may have to enable MTP on the device, before ADB will work. Some other devices require enable PTP mode to work.
*   Many devices' udev rules are included in [libmtp](https://www.archlinux.org/packages/?name=libmtp), so if you have this installed, the following steps may not be necessary.
*   Make sure your USB cable is capable of both charge and data. Many USB cables bundled with mobile devices do not include the USB data pin.

#### Connect device

To connect to a real device or phone via ADB under Arch, you must:

1.  Install [android-tools](https://www.archlinux.org/packages/?name=android-tools). In addition, you might want to install [android-udev](https://www.archlinux.org/packages/?name=android-udev) if you wish to connect the device to the proper `/dev/` entries.
2.  plug in your android device via USB.
3.  Enable USB Debugging on your phone or device:
    *   Jelly Bean (4.2) and newer: Go to *Settings > About Phone* tap *Build Number* 7 times until you get a popup that you have become a developer. Then go to *Settings > Developer > USB debugging* and enable it. The device will ask to allow the computer with its fingerprint to connect. allowing it permanent will copy `$HOME/.android/adbkey.pub` onto the devices `/data/misc/adb/adb_keys` folder.
    *   Older versions: This is usually done from *Settings > Applications > Development > USB debugging*. Reboot the phone after checking this option to make sure USB debugging is enabled.

If [ADB recognizes your device](#Detect_the_device) (`adb devices` shows it as `"device" and not as "unauthorized"`, or it is visible and accessible in IDE), you are done. Otherwise see instructions below.

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

Use the rules from [android-udev](https://www.archlinux.org/packages/?name=android-udev) (or [android-udev-git](https://aur.archlinux.org/packages/android-udev-git/)), install them manually from [Android developer](https://source.android.com/source/initializing#configuring-usb-access), or use the following template for your [udev rules](/index.php/Udev_rules "Udev rules"), just replace `[VENDOR ID]` and `[PRODUCT ID]` with yours. Copy these rules into `/etc/udev/rules.d/51-android.rules`:

 `/etc/udev/rules.d/51-android.rules` 
```
SUBSYSTEM=="usb", ATTR{idVendor}=="[VENDOR ID]", MODE="0660", GROUP="adbusers"
SUBSYSTEM=="usb",ATTR{idVendor}=="[VENDOR ID]",ATTR{idProduct}=="[PRODUCT ID]",SYMLINK+="android_adb"
SUBSYSTEM=="usb",ATTR{idVendor}=="[VENDOR ID]",ATTR{idProduct}=="[PRODUCT ID]",SYMLINK+="android_fastboot"

```

Then, to reload your new udev rules, execute:

```
# udevadm control --reload-rules

```

Make sure you are member of `adbusers` [group](/index.php/Group "Group") to access `adb` devices.

#### Configuring adb

Instead of using udev rules, you may create/edit `~/.android/adb_usb.ini` which contains a list of vendor IDs.

 `~/.android/adb_usb.ini` 
```
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
$ adb push *<what-to-copy>* *<where-to-place>*

```

To transfer files from the device, use

```
$ adb pull *<what-to-pull>* *<where-to-place>*

```

#### Notes & Troubleshooting

*   **ADB** can also be installed via [platform tools](#Android_SDK_platform_API)(usually available in `/opt/android-sdk/platform-tools/`), so it might not be necessary to install [android-tools](https://www.archlinux.org/packages/?name=android-tools) (available in `/usr/bin/`).

*   If you are getting an empty list (your device is not there), it may be because you have not enabled USB debugging on your device. You can do that by going to *Settings > Applications > Development* and enabling USB debugging. On Android 4.2 (Jelly Bean) the Development menu is hidden; to enable it go to *Settings > About phone* and tap Build number 7 times.

*   If there are still problems such as *adb* displaying `???????? no permissions` under devices, try restarting the adb server as root.

```
# adb kill-server
# adb start-server

```

*   On moto e it could happen to have a different vendor/product id while you are on sideload or fastboot, verify again lsusb if you get no permission.

### NVIDIA Tegra platform

If you target your application at NVIDIA Tegra platform, you might also want to install tools, samples and documentation provided by NVIDIA. In [NVIDIA Developer Zone for Mobile](http://developer.nvidia.com/category/zone/mobile-development) there are two tools:

1.  The [Tegra Android Development Pack](http://developer.nvidia.com/tegra-resources) provides tools (NVIDIA Debug Manager) related to [Eclipse ADT](http://developer.android.com/sdk/eclipse-adt.html) and their documentation.
2.  The [Tegra Toolkit](http://developer.nvidia.com/tegra-resources) provides tools (mostly CPU and GPU optimization related), samples and documentation.

Both are currently not available in the [AUR](/index.php/AUR "AUR") anymore, because NVIDIA requires a registration/login for the download.

## Building Android

Please note that these instructions are based on the [official AOSP build instructions](https://source.android.com/source/building). Other Android-derived systems such as LineageOS will often require extra steps.

### Required packages

To build any version of Android, you need to install these packages:

*   [lib32-gcc-libs](https://www.archlinux.org/packages/?name=lib32-gcc-libs) [git](https://www.archlinux.org/packages/?name=git) [gnupg](https://www.archlinux.org/packages/?name=gnupg) [flex](https://www.archlinux.org/packages/?name=flex) [bison](https://www.archlinux.org/packages/?name=bison) [gperf](https://www.archlinux.org/packages/?name=gperf) [sdl](https://www.archlinux.org/packages/?name=sdl) [wxgtk2](https://www.archlinux.org/packages/?name=wxgtk2) [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools) [curl](https://www.archlinux.org/packages/?name=curl) [ncurses](https://www.archlinux.org/packages/?name=ncurses) [zlib](https://www.archlinux.org/packages/?name=zlib) [schedtool](https://www.archlinux.org/packages/?name=schedtool) [perl-switch](https://www.archlinux.org/packages/?name=perl-switch) [zip](https://www.archlinux.org/packages/?name=zip) [unzip](https://www.archlinux.org/packages/?name=unzip) [libxslt](https://www.archlinux.org/packages/?name=libxslt) [python2-virtualenv](https://www.archlinux.org/packages/?name=python2-virtualenv) [bc](https://www.archlinux.org/packages/?name=bc) [rsync](https://www.archlinux.org/packages/?name=rsync) [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/) [lib32-zlib](https://www.archlinux.org/packages/?name=lib32-zlib) [lib32-ncurses](https://www.archlinux.org/packages/?name=lib32-ncurses) [lib32-readline](https://www.archlinux.org/packages/?name=lib32-readline) [lib32-ncurses5-compat-libs](https://aur.archlinux.org/packages/lib32-ncurses5-compat-libs/)

The [aosp-devel](https://aur.archlinux.org/packages/aosp-devel/) metapackage provides them all for simple installation.

**Note:** The PGP signatures for [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/) and [lib32-ncurses5-compat-libs](https://aur.archlinux.org/packages/lib32-ncurses5-compat-libs/) may cause errors, that can be solved by manually importing the needed signature:
```
$ gpg --recv-keys 702353E0F7E48EDB

```

Additionally, LineageOS requires the following packages: [xml2](https://aur.archlinux.org/packages/xml2/), [lzop](https://www.archlinux.org/packages/?name=lzop), [pngcrush](https://www.archlinux.org/packages/?name=pngcrush), [imagemagick](https://www.archlinux.org/packages/?name=imagemagick)

They can be installed with the [lineageos-devel](https://aur.archlinux.org/packages/lineageos-devel/) metapackage.

**Note:** Installing both [maven](https://www.archlinux.org/packages/?name=maven) and [gradle](https://www.archlinux.org/packages/?name=gradle) to build LineageOS may result in a build speed improvement as the build process will prefer the system's

### Java Development Kit

The [required JDK version](https://source.android.com/source/requirements) depends on the Android version you're building:

*   For Android 7 and 8 (Nougat and Oreo), OpenJDK 8 is required, which is available with the [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk) package.
*   For Android 5 and 6 (Lollipop and Marshmallow), OpenJDK 7 is required, which is available with the [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) package.

Older versions require a working **Oracle JDK** installed on your build system. It **will not** work with OpenJDK.

*   For Gingerbread through KitKat (2.3 - 4.4), Java 6 is required, which is available as [jdk6](https://aur.archlinux.org/packages/jdk6/) from the AUR.
*   For Cupcake through Froyo (1.5 - 2.2), Java 5 is required, which is available as [jdk5](https://aur.archlinux.org/packages/jdk5/) from the AUR.

**Note:** Android expect java in /usr/lib/jvm/java-x-openjdk-amd64, where x is the java version.

Set JAVA_HOME to avoid this requirement and match archlinux installation path. Example:

```
$ export JAVA_HOME=/usr/lib/jvm/java-x-openjdk

```
This change will be valid only for the current terminal session.

### Setting up the build environment

[Install](/index.php/Install "Install") the [repo](https://www.archlinux.org/packages/?name=repo) package.

Create a directory to build.

```
$ mkdir ~/android
$ cd ~/android

```

The Android build process expects `python` to be python2\. Create a python2 virtual environment and activate it:

```
$ virtualenv2 venv
$ source venv/bin/activate

```

**Note:**

*   This activation is only active for the current terminal session. The virtual env will be kept in the `venv` folder.
*   During build you may receive error pertaining to missing python modules. A quick and dirty fix is to symlink /usr/lib/python2.7/* to ~/android/venv/lib/python2.7/ (Change ~/android to reflect your build directory if different than above).

Example:

```
$ ln -s /usr/lib/python2.7/* ~/android/venv/lib/python2.7/

```

or (assuming build directory Data/Android_Build):

```
$ ln -s /usr/lib/python2.7/* /Data/Android_Build/venv/lib/python2.7/

```

### Downloading the source code

This will clone the repositories. You **only** need to do this the first time you build Android, or if you want to switch branches.

*   The `repo` has a `-j` switch that operates similarly to the one used with `make`. Since it controls the number of simultaneous downloads, you should adjust the value depending on downstream network bandwidth.

*   You will need to specify a **branch** (release of Android) to check out with the `-b` switch. If you leave the switch out, you will get the so-called **master branch**.

```
$ repo init -u https://android.googlesource.com/platform/manifest -b master
$ repo sync -j4

```

**Note:** To further decrease sync times, you can utilize the -c switch with the repo command as such:
```
$ repo sync -j8 -c

```

The `-c` switch will only sync the branch which is specified in the manifest, which in turn is determined by the branch specified with the `-b` switch, or the default branch set by the repository maintainer.

Wait a long time. Just the uncompiled source code, along with the `.repo` and `.git` directories that are used to keep track of it, are well over 10 GB. As of Android 6.0.1, the entire codebase totals 40 GB.

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

**Note:**

*   Make sure you have enough RAM. Android will use the /tmp directory heavily. By default the size of the partition the /tmp folder is mounted on is half the size of your RAM. If it fills up, the build will fail. 4GB of RAM or more is recommended. Alternatively, you can get rid of the tmpfs from [fstab](/index.php/Fstab "Fstab") all together.
*   From the [Android Building and Running guide](https://source.android.com/source/building#build-the-code):

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

This will create a zip image under `**out/target/product/hammerhead**` (hammerhead being the device name) that can be flashed.

## Restoring Android

In some cases, you want to return to the stock Android after flashing custom ROMs to your Android mobile device. For flashing instructions of your device, please use [XDA forums](http://forum.xda-developers.com/).

### Fastboot

Fastboot (as well as [ADB](#Android_Debug_Bridge)) is included in the [android-tools](https://www.archlinux.org/packages/?name=android-tools) package.

**Note:** Restoring firmwares using `fastboot` can be quite tricky, but you might want to browse [XDA developers forums](http://www.xda-developers.com/) for a stock firmware, which is mostly a `*.zip` file, but inside of it, comes with the firmware files and `flash-all.sh` script. For example, [Google Nexus](https://developers.google.com/android/nexus/images) firmwares include `flash-all.sh` script or another example could be for OnePlus One - [XDA thread](http://forum.xda-developers.com/oneplus-one/general/guide-return-opo-to-100-stock-t2826541), where you can find firmwares with included `flash-all.sh` script.

### Samsung devices

Samsung devices can't be flashed using **Fastboot** tool. Alternatives are only **Heimdall** and **Odin** (by using Windows and VirtualBox).

#### Heimdall

[Heimdall](http://glassechidna.com.au/heimdall/) is a cross-platform open-source tool suite used to flash firmware (also known as ROMs) onto Samsung mobile devices and is also known as an alternative to [Odin](http://odindownload.com/). It can be installed as [heimdall](https://aur.archlinux.org/packages/heimdall/).

The flashing instructions can be found on Heimdall's [GitHub page](https://github.com/Benjamin-Dobell/Heimdall/tree/master/Linux) or on [XDA forums](http://forum.xda-developers.com/showthread.php?t=1922461).

#### Odin (Virtualbox)

**Note:** This section only covers preparation and **not** flashing instructions. Search [XDA developers forums](http://www.xda-developers.com) to find a flashing instructions for specific device. For example, [Samsung Galaxy S4](https://forum.xda-developers.com/showthread.php?t=2265477).

It is also possible to restore [firmware (Android)](http://www.sammobile.com/firmwares/) on the Samsung devices using [Odin](http://odindownload.com/), but inside the [VirtualBox](/index.php/VirtualBox "VirtualBox").

Arch Linux (host) preparation:

1.  Install [VirtualBox](/index.php/VirtualBox "VirtualBox") together with its [extension pack](/index.php/VirtualBox#Extension_pack "VirtualBox") and [guest additions](/index.php/VirtualBox#Guest_additions_disc "VirtualBox").
2.  Install your preferred, but compatible with Odin, Windows operating system (with VirtualBox guest additions) into a virtual hard drive using VirtualBox.
3.  Open VirtualBox settings of your Windows operating system, navigate to *USB*, then tick (or make sure it is ticked) **Enable USB 2.0 (EHCI) Controller**.
4.  At VirtualBox running Windows operating system, click in the menu bar *Devices > USB Devices*, then click on your Samsung mobile device from the list, which is connected to your computer via USB.

Windows (guest) preparation:

1.  Install [Samsung drivers](http://androidxda.com/download-samsung-usb-drivers).
2.  Install [Odin](http://odindownload.com/).
3.  Download required [Samsung firmware (Android)](http://www.sammobile.com/firmwares/) for your smartphone model.

Check if configuration is working:

1.  Turn your device into Download mode and connect to your Linux machine.
2.  In virtual machine toolbar, select *Devices > USB > ...Samsung...* device.
3.  Open Odin. The white box (a big one at the bottom-left side) named **Message**, should print a line similar to this:

```
<ID:0/003> Added!!

```

which means that your device is visible to Odin & Windows operating system and is ready to be flashed.

## Connection software

*   [adb-sync](https://github.com/google/adb-sync) (available as [adb-sync-git](https://aur.archlinux.org/packages/adb-sync-git/)) – a tool to synchronize files between a PC and an Android device using the ADB protocol.
*   [AndroidScreencast](http://xsavikx.github.io/AndroidScreencast) (available as [androidscreencast-bin](https://aur.archlinux.org/packages/androidscreencast-bin/)) – view and control your Android device from a PC (via ADB).
*   [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect) – integrates your Android device with the KDE desktop (featuring synced notifications & clipboard, multimedia control, and file/URL sharing).
*   [sendanywhere](https://aur.archlinux.org/packages/sendanywhere/) – cross-platform file sharing

## Tips & Tricks

### During Debugging "Source not found"

Most probably the debugger wants to step into the Java code. As the source code of Android does not come with the Android SDK, this leads to an error. The best solution is to use step filters to not jump into the Java source code. Step filters are not activated by default. To activate them: *Window > Preferences > Java > Debug > Step Filtering*. Consider to select them all. If appropriate you can add the android.* package. See the forum post for more information: [http://www.eclipsezone.com/eclipse/forums/t83338.rhtml](http://www.eclipsezone.com/eclipse/forums/t83338.rhtml)

### Linux distribution on the sdcard

You can install Debian like in this [thread](http://forum.xda-developers.com/showthread.php?t=631389). Excellent guide to installing Arch in chroot (in parallel with Android) can be found on [archlinuxarm.org forum](http://archlinuxarm.org/forum/viewtopic.php?f=27&t=1361&start=40).

## Troubleshooting

### Android Studio: Android Virtual Devices show 'failed to load'.

Make sure you've exported the variable `ANDROID_HOME` as explained in [#Android Studio](#Android_Studio).

### Android Studio: 'failed to create the SD card'

If you try to run an AVD (Android Virtual Device) under x86_64 Arch and get the error above, install the [lib32-gcc-libs](https://www.archlinux.org/packages/?name=lib32-gcc-libs) package from the [Multilib](/index.php/Multilib "Multilib") repository.

### ValueError: unsupported pickle protocol

One fix is to issue:

```
$ rm ~/.repopickle_.gitconfig

```

If that does not work, then try this:

```
$ find /path/to/android-root -name .repopickle_config -exec rm {} +

```

### libGL error: failed to load driver: swrast OR AVD doesn't load and no error message displayed

Sometimes, beginning to load an AVD will cause an error message similar to this to be displayed, or the loading process will appear to finish but no AVD will load and no error message will be displayed.

The AVD loads an incorrect version of libstdc++, you can remove the folder libstdc++ from `~/Android/Sdk/emulator/lib64/` (for 64-bit) or `~/Android/Sdk/emulator/lib/` (for 32-bit) , e.g.:

```
$ rm -r ~/Android/Sdk/emulator/lib64/libstdc++

```

Alternatively you can set and export ANDROID_EMULATOR_USE_SYSTEM_LIBS in ~/.profile as:

```
export ANDROID_EMULATOR_USE_SYSTEM_LIBS=1

```

Reference: Android Studio user guide, [https://developer.android.com/studio/command-line/variables.html#studio_jdk](https://developer.android.com/studio/command-line/variables.html#studio_jdk)

Fix for the .desktop file might be achieved by using env command, prefixing the Exec line [Desktop entries#Modify environment variables](/index.php/Desktop_entries#Modify_environment_variables "Desktop entries")

```
env ANDROID_EMULATOR_USE_SYSTEM_LIBS=1

```

### sh: glxinfo: command not found

Here's the full error:

```
Cannot launch AVD in emulator.
Output:
sh: glxinfo: command not found
sh: glxinfo: command not found
libGL error: unable to load driver: swrast_dri.so
libGL error: failed to load driver: swrast
X Error of failed request:  BadValue (integer parameter out of range for operation)
  Major opcode of failed request:  154 (GLX)
  Minor opcode of failed request:  24 (X_GLXCreateNewContext)
  Value in failed request:  0x0
  Serial number of failed request:  32
  Current serial number in output stream:  33
QObject::~QObject: Timers cannot be stopped from another thread

```

You can try to install glxinfo (Its [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos)) but if your computer has enough power you could simply use software to render graphics. To do so, go to *Tools > Android > AVD Manager*, edit the *AVD* (click the pencil icon), then select *Software - GLES 2.0* for *Emulated Performance > Graphics*.

### Android Emulator: no keyboard input in xfwm4

In xfwm4, the vertical toolbar buttons window that's on the right of the emulator takes focus from the emulator and consumes keyboard events. ([bug report](https://issuetracker.google.com/issues/37094173))

You can use the workaround described in [this StackOverflow answer](https://stackoverflow.com/a/42720450/1366471):

1.  Go to xfwm4 settings
2.  Find Focus tab
3.  Change Focus Model to "Focus follow mouse"
4.  Disable "Automatically raise windows when they receive focus" option bellow.