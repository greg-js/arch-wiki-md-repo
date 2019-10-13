Related articles

*   [Android tethering](/index.php/Android_tethering "Android tethering")
*   [Android Debug Bridge](/index.php/Android_Debug_Bridge "Android Debug Bridge")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Transferring files](#Transferring_files)
*   [2 App development](#App_development)
    *   [2.1 Android Studio](#Android_Studio)
    *   [2.2 SDK packages](#SDK_packages)
        *   [2.2.1 Android Emulator](#Android_Emulator)
        *   [2.2.2 Other SDK packages in the AUR](#Other_SDK_packages_in_the_AUR)
        *   [2.2.3 Making /opt/android-sdk group-writeable](#Making_/opt/android-sdk_group-writeable)
    *   [2.3 Other IDEs](#Other_IDEs)
        *   [2.3.1 Netbeans](#Netbeans)
        *   [2.3.2 Eclipse](#Eclipse)
*   [3 Building](#Building)
    *   [3.1 Required packages](#Required_packages)
    *   [3.2 Java Development Kit](#Java_Development_Kit)
    *   [3.3 Setting up the build environment](#Setting_up_the_build_environment)
    *   [3.4 Downloading the source code](#Downloading_the_source_code)
    *   [3.5 Building the code](#Building_the_code)
    *   [3.6 Testing the build](#Testing_the_build)
    *   [3.7 Creating a flashable Image](#Creating_a_flashable_Image)
*   [4 Flashing](#Flashing)
    *   [4.1 Fastboot](#Fastboot)
    *   [4.2 Samsung devices](#Samsung_devices)
        *   [4.2.1 Heimdall](#Heimdall)
        *   [4.2.2 Odin (Virtualbox)](#Odin_(Virtualbox))
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Android Studio: Android Virtual Devices show 'failed to load'.](#Android_Studio:_Android_Virtual_Devices_show_'failed_to_load'.)
    *   [5.2 Android Studio: 'failed to create the SD card'](#Android_Studio:_'failed_to_create_the_SD_card')
    *   [5.3 Eclipse: During Debugging "Source not found"](#Eclipse:_During_Debugging_"Source_not_found")
    *   [5.4 ValueError: unsupported pickle protocol](#ValueError:_unsupported_pickle_protocol)
    *   [5.5 libGL error: failed to load driver: swrast OR AVD doesn't load and no error message displayed](#libGL_error:_failed_to_load_driver:_swrast_OR_AVD_doesn't_load_and_no_error_message_displayed)
    *   [5.6 sh: glxinfo: command not found](#sh:_glxinfo:_command_not_found)
    *   [5.7 Android Emulator: no keyboard input in xfwm4](#Android_Emulator:_no_keyboard_input_in_xfwm4)

## Transferring files

There are various ways to transfer files between a computer and an Android device:

*   USB cable
    *   [Media Transfer Protocol](/index.php/Media_Transfer_Protocol "Media Transfer Protocol") for modern Android devices
    *   [USB mass storage](https://en.wikipedia.org/wiki/USB_Mass_Storage "wikipedia:USB Mass Storage") for older devices
    *   [Android Debug Bridge](/index.php/Android_Debug_Bridge "Android Debug Bridge")
*   special USB sticks / regular USB stick with adapter
*   [Bluetooth](/index.php/Bluetooth "Bluetooth")
*   Arch Linux software with Android counterparts
    *   client or server for protocols that can be used to transfer files (eg. [SSH](/index.php/SSH "SSH"), [FTP](/index.php/FTP "FTP"), [Samba](/index.php/Samba "Samba") or HTTP)
    *   [KDE Connect](/index.php/KDE_Connect "KDE Connect") ([kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect)) – integrates your Android device with the KDE desktop (featuring synced notifications & clipboard, multimedia control, and file/URL sharing).
    *   [cloud synchronization clients](/index.php/Cloud_synchronization_clients "Cloud synchronization clients")
    *   [Syncthing](/index.php/Syncthing "Syncthing")
    *   [sendanywhere](https://aur.archlinux.org/packages/sendanywhere/) – cross-platform file sharing

## App development

The officially supported way to build Android apps is to use [#Android Studio](#Android_Studio).[[1]](https://developer.android.com/training/basics/firstapp/creating-project)

### Android Studio

[Android Studio](https://developer.android.com/studio/index.html) is the official Android development environment based on [IntelliJ IDEA](https://en.wikipedia.org/wiki/IntelliJ_IDEA "wikipedia:IntelliJ IDEA"). It provides integrated Android developer tools for development and debugging.

You can [install](/index.php/Install "Install") it with the [android-studio](https://aur.archlinux.org/packages/android-studio/) package.

**Note:**

*   Make sure you properly [set the Java environment](/index.php/Java#Change_default_Java_environment "Java") otherwise android-studio will not start.
*   If Android Studio shows up as a blank window try [exporting](/index.php/Export "Export") `_JAVA_AWT_WM_NONREPARENTING=1`, see [issue #57675](https://code.google.com/p/android/issues/detail?id=57675).

The Android Studio Setup Wizard installs the required [#SDK packages](#SDK_packages) and places the SDK by default in `~/Android/Sdk`.

To build apps from the command-line (using e.g. `./gradlew assembleDebug`) set the [ANDROID_SDK_ROOT](https://developer.android.com/studio/command-line/variables#android_sdk_root) [environment variable](/index.php/Environment_variable "Environment variable") to your SDK location.

### SDK packages

Android SDK packages can be installed directly from upstream using [#Android Studio](#Android_Studio)'s [SDK Manager](https://developer.android.com/studio/intro/update#sdk-manager) or the [sdkmanager](https://developer.android.com/studio/command-line/sdkmanager) command line tool (part of the Android SDK Tools). Some Android SDK packages are also available as [AUR](/index.php/AUR "AUR") packages, they generally install to `/opt/android-sdk/`.

The [required SDK packages](https://developer.android.com/studio/intro/update#recommended) are:

| Android SDK Package | SDK-style path | AUR package | AUR dummy | CLI tools |
| [SDK Tools](https://developer.android.com/studio/releases/sdk-tools) | tools | [android-sdk](https://aur.archlinux.org/packages/android-sdk/) | [android-sdk-dummy](https://aur.archlinux.org/packages/android-sdk-dummy/) | sdkmanager, apkanalizer, avdmanager, mksdcard, proguard |
| [SDK Build-Tools](https://developer.android.com/studio/releases/build-tools) | build-tools;*version* | [android-sdk-build-tools](https://aur.archlinux.org/packages/android-sdk-build-tools/) | [android-sdk-build-tools-dummy](https://aur.archlinux.org/packages/android-sdk-build-tools-dummy/) | apksigner, zipalign |
| [SDK Platform-Tools](https://developer.android.com/studio/releases/platform-tools) | platform-tools | [android-sdk-platform-tools](https://aur.archlinux.org/packages/android-sdk-platform-tools/) | [android-sdk-platform-tools-dummy](https://aur.archlinux.org/packages/android-sdk-platform-tools-dummy/) | [adb](/index.php/Adb "Adb"), [#fastboot](#Fastboot) and systrace |
| [SDK Platform](https://developer.android.com/studio/releases/platforms) | platforms;android-*level* | [android-platform](https://aur.archlinux.org/packages/android-platform/), [older versions](https://aur.archlinux.org/packages/?K=android-platform-) | unnecessary |

The [android-tools](https://www.archlinux.org/packages/?name=android-tools) package provides [adb](/index.php/Adb "Adb"), [#fastboot](#Fastboot), `e2fsdroid` and `mke2fs.android` from the SDK Platform-Tools along with `mkbootimg` and `ext2simg`.

**Note:**  

*   Since the Android SDK contains 32-bit binaries, you must enable the [multilib](/index.php/Multilib "Multilib") repository. Otherwise you will get `error: target not found: lib32-*` error messages.
*   If you choose to directly install SDK packages from upstream, install the AUR packages of the *AUR dummy* column to pull in the required dependencies.

#### Android Emulator

The [Android Emulator](https://developer.android.com/studio/run/emulator) is available as the `emulator` SDK package, the [android-emulator](https://aur.archlinux.org/packages/android-emulator/) package. And there's also a dummy package for it: [android-emulator-dummy](https://aur.archlinux.org/packages/android-emulator-dummy/).

To run the Android Emulator you need an Intel or ARM System Image. You can install them through the AUR[[2]](https://aur.archlinux.org/packages/?K=android-+system+image), with the sdkmanager or using Android Studio's [AVD Manager](https://developer.android.com/studio/run/managing-avds).

#### Other SDK packages in the AUR

The [Android Support Library](https://developer.android.com/topic/libraries/support-library/) is now available online from [Google's Maven repository](https://developer.android.com/studio/build/dependencies#google-maven). You can also install it offline through the `extras;android;m2repository` SDK package (also available as [android-support-repository](https://aur.archlinux.org/packages/android-support-repository/)).

#### Making /opt/android-sdk group-writeable

The AUR packages install the SDK in `/opt/android-sdk/`. This directory has root [permissions](/index.php/Permissions "Permissions"), so keep in mind to run sdk manager as root. If you intend to use it as a regular user, create the Android sdk users group, add your user.

```
# groupadd android-sdk
# gpasswd -a <user> android-sdk

```

Set an access control list to let members of the newly created group write into the android-sdk folder. As running sdkmanager can also create new files, set the ACL as default ACL. the X in the default group entry means "allow execution if executable by the owner (or anyone else)"

```
# setfacl -R -m g:android-sdk:rwx /opt/android-sdk
# setfacl -d -m g:android-sdk:rwX /opt/android-sdk  

```

Re-login or as <user> log your terminal in to the newly created group:

```
$ newgrp android-sdk

```

### Other IDEs

Android Studio is the official Android development environment based on IntelliJ IDEA. Alternatively, you can use [Netbeans](/index.php/Netbeans "Netbeans") with the NBAndroid-V2\. All are described below.

#### Netbeans

If you prefer using [Netbeans](/index.php/Netbeans "Netbeans") as your IDE and want to develop Android applications, use [NBAndroid-V2](https://github.com/NBANDROIDTEAM/NBANDROID-V2) .

Install [android-sdk](https://aur.archlinux.org/packages/android-sdk/) package

Add the following URL by going to *Tools > Plugins > Settings*:

| Netbeans version | URL |
| Netbeans 8.1 | [http://server.arsi.sk/nbandroid81/updates.xml](http://server.arsi.sk/nbandroid81/updates.xml) |
| Netbeans 8.2 | [http://server.arsi.sk/nbandroid82/updates.xml](http://server.arsi.sk/nbandroid82/updates.xml) |

Then go to *Available Plugins* and install the *Gradle-Android-support* plugin.

#### Eclipse

**Note:** The Eclipse ADT plugin is no longer supported. Google recommends to use Android Studio instead.[[3]](https://android-developers.googleblog.com/2016/11/support-ended-for-eclipse-android.html)

The official, but deprecated, [Eclipse ADT](http://developer.android.com/sdk/eclipse-adt.html) plugin can be installed with the [eclipse-android](https://aur.archlinux.org/packages/eclipse-android/) package.

**Note:**

*   if you get a message about unresolvable dependencies, install [Java](/index.php/Java "Java") manually and try again.
*   as an alternative, you can install the ADT via eclipse's built in "add new software" command (see instructions on ADT site).
*   if you are in real trouble, it is also possible to download Android SDK and use the bundled Eclipse. This usually works without problems.
*   if you need to install extra SDK plugins not found in the AUR, you must change the file ownership of /opt/android-sdk first. You can do this with `# chgrp -R users /opt/android-sdk ; chmod -R 0775 /opt/android-sdk` (see [File Permissions](/index.php/File_Permissions "File Permissions") for more details).

Enter the path to the Android SDK Location in *Windows > Preferences > Android*.

**Note:** If the plugins do not show up in Eclipse after the AUR package has been upgraded, then eclipse probably has out-of-date caches. Running `sudo eclipse -clean` once should clear them. If the problem persists, uninstall eclipse and all the plugins, delete `/usr/share/eclipse`, and reinstall everything.

## Building

Please note that these instructions are based on the [official AOSP build instructions](https://source.android.com/source/building). Other Android-derived systems such as LineageOS will often require extra steps.

### Required packages

To build any version of Android, you need to install these packages:

*   [lib32-gcc-libs](https://www.archlinux.org/packages/?name=lib32-gcc-libs) [git](https://www.archlinux.org/packages/?name=git) [gnupg](https://www.archlinux.org/packages/?name=gnupg) [flex](https://www.archlinux.org/packages/?name=flex) [bison](https://www.archlinux.org/packages/?name=bison) [gperf](https://www.archlinux.org/packages/?name=gperf) [sdl](https://www.archlinux.org/packages/?name=sdl) [wxgtk2](https://www.archlinux.org/packages/?name=wxgtk2) [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools) [curl](https://www.archlinux.org/packages/?name=curl) [ncurses](https://www.archlinux.org/packages/?name=ncurses) [zlib](https://www.archlinux.org/packages/?name=zlib) [schedtool](https://www.archlinux.org/packages/?name=schedtool) [perl-switch](https://www.archlinux.org/packages/?name=perl-switch) [zip](https://www.archlinux.org/packages/?name=zip) [unzip](https://www.archlinux.org/packages/?name=unzip) [libxslt](https://www.archlinux.org/packages/?name=libxslt) [python2-virtualenv](https://www.archlinux.org/packages/?name=python2-virtualenv) [bc](https://www.archlinux.org/packages/?name=bc) [rsync](https://www.archlinux.org/packages/?name=rsync) [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/) [lib32-zlib](https://www.archlinux.org/packages/?name=lib32-zlib) [lib32-ncurses](https://www.archlinux.org/packages/?name=lib32-ncurses) [lib32-readline](https://www.archlinux.org/packages/?name=lib32-readline) [lib32-ncurses5-compat-libs](https://aur.archlinux.org/packages/lib32-ncurses5-compat-libs/)

The [aosp-devel](https://aur.archlinux.org/packages/aosp-devel/) metapackage provides them all for simple installation.

Additionally, LineageOS requires the following packages: [xml2](https://aur.archlinux.org/packages/xml2/), [lzop](https://www.archlinux.org/packages/?name=lzop), [pngcrush](https://www.archlinux.org/packages/?name=pngcrush), [imagemagick](https://www.archlinux.org/packages/?name=imagemagick)

They can be installed with the [lineageos-devel](https://aur.archlinux.org/packages/lineageos-devel/) metapackage.

**Note:** Installing both [maven](https://www.archlinux.org/packages/?name=maven) and [gradle](https://www.archlinux.org/packages/?name=gradle) to build LineageOS may result in a build speed improvement as the build process will prefer the system's

### Java Development Kit

The [required JDK version](https://source.android.com/source/requirements) depends on the Android version you are building:

*   For Android 7 and 8 (Nougat and Oreo), OpenJDK 8 is required, which is available with the [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk) package.
*   For Android 5 and 6 (Lollipop and Marshmallow), OpenJDK 7 is required, which is available with the [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) package.

Older versions require a working **Oracle JDK** installed on your build system. It **will not** work with OpenJDK.

*   For Gingerbread through KitKat (2.3 - 4.4), Java 6 is required, which is available as [jdk6](https://aur.archlinux.org/packages/jdk6/) from the AUR.
*   For Cupcake through Froyo (1.5 - 2.2), Java 5 is required, which is available as [jdk5](https://aur.archlinux.org/packages/jdk5/) from the AUR.

**Note:** Android expects Java in `/usr/lib/jvm/java-*version*-openjdk-amd64`.

Set JAVA_HOME to avoid this requirement and match the Arch Linux installation path. Example:

```
$ export JAVA_HOME=/usr/lib/jvm/java-*version*-openjdk

```
This change will be valid only for the current terminal session.

### Setting up the build environment

[Install](/index.php/Install "Install") the [repo](https://www.archlinux.org/packages/?name=repo) package.

Create a directory to build.

```
$ mkdir ~/android
$ cd ~/android

```

The Android build process expects `python` to be python2\. Prepend it to the `PATH`:

```
$ mkdir bin
$ ln -s /bin/python2 bin/python
$ export PATH=$PWD/bin:$PATH

```

Alternatively, create a python2 virtual environment and activate it:

```
$ virtualenv2 --system-site-packages venv
$ source venv/bin/activate

```

**Note:**

*   This activation is only active for the current terminal session. The virtual env will be kept in the `venv` folder.
*   Passing "--system-site-packages" to virtualenv2 points your virtual environment to your installed python2.7 modules. This should give you all python modules you need for the build, assuming you've installed the required dependencies such as python2-mako.
*   If during the build you still receive errors pertaining to missing python modules a quick and dirty fix might be to symlink /usr/lib/python2.7/* to ~/android/venv/lib/python2.7/ (Change ~/android to reflect your build directory if different than above).

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

*   Make sure you have enough RAM. Android will use the `/tmp` directory heavily. By default the size of the partition the `/tmp` folder is mounted on is half the size of your RAM. If it fills up, the build will fail. 4GB of RAM or more is recommended. Alternatively, you can get rid of the tmpfs from [fstab](/index.php/Fstab "Fstab") all together.
*   From the [Android Building and Running guide](https://source.android.com/source/building#build-the-code):

"GNU make can handle parallel tasks with a `-jN` argument, and it's common to use a number of tasks N that's between 1 and 2 times the number of hardware threads on the computer being used for the build. E.g. on a dual-E5520 machine (2 CPUs, 4 cores per CPU, 2 threads per core), the fastest builds are made with commands between `make -j16` and `make -j32`."

### Testing the build

When finished, run/test the final image(s).

```
$ emulator

```

### Creating a flashable Image

To create an image that can be flashed it is necessary to:

```
make -j8 updatepackage

```

This will create a zip image under `**out/target/product/hammerhead**` (hammerhead being the device name) that can be flashed.

## Flashing

In some cases, you want to return to the stock Android after flashing custom ROMs to your Android mobile device. For flashing instructions of your device, please use [XDA forums](http://forum.xda-developers.com/).

### Fastboot

Fastboot (as well as [ADB](/index.php/ADB "ADB")) is included in the [android-tools](https://www.archlinux.org/packages/?name=android-tools) package.

**Note:** Restoring firmwares using `fastboot` can be quite tricky, but you might want to browse [XDA developers forums](http://www.xda-developers.com/) for a stock firmware, which is mostly a `*.zip` file, but inside of it, comes with the firmware files and `flash-all.sh` script. For example, [Google Nexus](https://developers.google.com/android/nexus/images) firmwares include `flash-all.sh` script or another example could be for OnePlus One - [XDA thread](http://forum.xda-developers.com/oneplus-one/general/guide-return-opo-to-100-stock-t2826541), where you can find firmwares with included `flash-all.sh` script.

### Samsung devices

Samsung devices can't be flashed using **Fastboot** tool. Alternatives are only **Heimdall** and **Odin** (by using Windows and VirtualBox).

#### Heimdall

[Heimdall](http://glassechidna.com.au/heimdall/) is a cross-platform open-source tool suite used to flash firmware (also known as ROMs) onto Samsung mobile devices and is also known as an alternative to [Odin](http://odindownload.com/). It can be installed as [heimdall](https://www.archlinux.org/packages/?name=heimdall).

The flashing instructions can be found on Heimdall's [GitLab repository](https://gitlab.com/BenjaminDobell/Heimdall/tree/master/Linux) or on [XDA forums](http://forum.xda-developers.com/showthread.php?t=1922461).

#### Odin (Virtualbox)

**Note:** This section only covers preparation and **not** flashing instructions. Search [XDA developers forums](http://www.xda-developers.com) to find flashing instructions for a specific device. For example, [Samsung Galaxy S4](https://forum.xda-developers.com/showthread.php?t=2265477).

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

## Troubleshooting

### Android Studio: Android Virtual Devices show 'failed to load'.

Make sure you've exported the variable `ANDROID_HOME` as explained in [#Android Studio](#Android_Studio).

### Android Studio: 'failed to create the SD card'

If you try to run an AVD (Android Virtual Device) under x86_64 Arch and get the error above, install the [lib32-gcc-libs](https://www.archlinux.org/packages/?name=lib32-gcc-libs) package from the [multilib](/index.php/Multilib "Multilib") repository.

### Eclipse: During Debugging "Source not found"

Most probably the debugger wants to step into the Java code. As the source code of Android does not come with the Android SDK, this leads to an error. The best solution is to use step filters to not jump into the Java source code. Step filters are not activated by default. To activate them: *Window > Preferences > Java > Debug > Step Filtering*. Consider to select them all. If appropriate you can add the android.* package. See the forum post for more information: [http://www.eclipsezone.com/eclipse/forums/t83338.rhtml](http://www.eclipsezone.com/eclipse/forums/t83338.rhtml)

### ValueError: unsupported pickle protocol

One fix is to issue:

```
$ rm ~/.repopickle_.gitconfig

```

If that does not work, then try this:

```
$ find /path/to/android-root -name .repopickle_config -delete

```

### libGL error: failed to load driver: swrast OR AVD doesn't load and no error message displayed

Sometimes, beginning to load an AVD will cause an error message similar to this to be displayed, or the loading process will appear to finish but no AVD will load and no error message will be displayed.

The AVD loads an incorrect version of libstdc++, you can remove the folder libstdc++ from `~/.android-sdk/emulator/lib64` (for 64-bit) or `~/.android-sdk/emulator/lib` (for 32-bit) , e.g.:

```
$ rm -r ~/.android-sdk/emulator/lib64/libstdc++

```

Note that in versions before Android Studio 3.0, this directory was in a different location:

```
$ rm -r ~/Android/Sdk/emulator/lib64/libstdc++

```

Alternatively you can set and export ANDROID_EMULATOR_USE_SYSTEM_LIBS in ~/.profile as:

```
export ANDROID_EMULATOR_USE_SYSTEM_LIBS=1

```

Reference: [Android Studio user guide](https://developer.android.com/studio/command-line/variables.html#studio_jdk)

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

You can try to install glxinfo ([mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos)) but if your computer has enough power you could simply use software to render graphics. To do so, go to *Tools > Android > AVD Manager*, edit the *AVD* (click the pencil icon), then select *Software - GLES 2.0* for *Emulated Performance > Graphics*.

### Android Emulator: no keyboard input in xfwm4

In xfwm4, the vertical toolbar buttons window that is on the right of the emulator takes focus from the emulator and consumes keyboard events. ([bug report](https://issuetracker.google.com/issues/37094173))

You can use the workaround described in [this Stack Overflow answer](https://stackoverflow.com/a/42720450/1366471):

1.  Open the xfwm4 settings.
2.  Switch to the Focus tab.
3.  Change the Focus Model to "Focus follow mouse".
4.  Disable *Automatically raise windows when they receive focus* option below.