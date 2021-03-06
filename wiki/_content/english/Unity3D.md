From [Unity - Game engine, tools and multiplatform](https://unity3d.com/unity):

	*Unity is a flexible and powerful development platform for creating multiplatform 3D and 2D games and interactive experiences. It's a complete ecosystem for anyone who aims to build a business on creating high-end content and connecting to their most loyal and enthusiastic players and customers.*

Not to be confused with Canonical's [Unity](/index.php/Unity "Unity").

**Note:** The Linux Editor is currently experimental. Please report all bugs to the [Unity forums](http://forum.unity3d.com/forums/linux-editor-support-feedback-experimental.93/)!

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Android Support](#Android_Support)
    *   [1.2 Alternative Installation Method](#Alternative_Installation_Method)
*   [2 Android Remote](#Android_Remote)
    *   [2.1 Prepare computer](#Prepare_computer)
        *   [2.1.1 Install packages](#Install_packages)
        *   [2.1.2 Configure the Editor](#Configure_the_Editor)
    *   [2.2 Prepare Android](#Prepare_Android)
    *   [2.3 Test](#Test)
*   [3 Visual Studio Code](#Visual_Studio_Code)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Unity crashes on first launch before/while signing in](#Unity_crashes_on_first_launch_before/while_signing_in)
    *   [4.2 Unity crashes when trying to load project](#Unity_crashes_when_trying_to_load_project)
    *   [4.3 Unity crashes if ~/.config/user-dirs.dirs is missing](#Unity_crashes_if_~/.config/user-dirs.dirs_is_missing)
    *   [4.4 Minor stuttering while playtesting (NVIDIA)](#Minor_stuttering_while_playtesting_(NVIDIA))
    *   [4.5 Error: Multiple Unity instances cannot open the same project](#Error:_Multiple_Unity_instances_cannot_open_the_same_project)
    *   [4.6 Android Remote not working / Running Android build fails with "Unable to forward network traffic to device"](#Android_Remote_not_working_/_Running_Android_build_fails_with_"Unable_to_forward_network_traffic_to_device")

## Installation

Simply install the [AUR](/index.php/AUR "AUR") package [unity-editor](https://aur.archlinux.org/packages/unity-editor/), [unity-editor-beta](https://aur.archlinux.org/packages/unity-editor-beta/) for the beta version or [unity-editor-lts](https://aur.archlinux.org/packages/unity-editor-lts/) for the lts version.

**Warning:** The Unity package is **huge**. For a successful installation you'll need about 17GiB of free space for the package building, and another 8GiB for it to install.

**Note:** By default the PKGBUILD redirects all the output of the installer, which downloads and processes about 2GB of data. As this process can be very long it might be useful to monitor it by using `tail -f /tmp/Unity.log`

### Android Support

Install [unity-editor-android](https://aur.archlinux.org/packages/unity-editor-android/), [unity-editor-beta-android](https://aur.archlinux.org/packages/unity-editor-beta-android/) or [unity-editor-lts-android](https://aur.archlinux.org/packages/unity-editor-lts-android/) depending on your install choice.

### Alternative Installation Method

Unity has made available a program called Unity Hub that is designed to streamline your workflow by providing a centralized location where you can manage your Unity Projects and simplifies how you find, download, and manage your Unity Editor installs. The application comes available as an AppImage. To install the Unity Hub simply install the [unityhub](https://aur.archlinux.org/packages/unityhub/) package.

## Android Remote

[Unity Remote](http://docs.unity3d.com/Manual/UnityRemote5.html) is an Android app to help test input for Android devices. It achieves this by sending a compressed screenshot to the device each frame.

### Prepare computer

#### Install packages

[Install](/index.php/Install "Install") the [android-udev](https://www.archlinux.org/packages/?name=android-udev) package, which will ensure you have correct [udev](/index.php/Udev "Udev") rules for your device.

Install the [android-sdk](https://aur.archlinux.org/packages/android-sdk/) package.

#### Configure the Editor

Open the editor, navigate to *Edit -> Preferences* and set the correct paths to the Android SDK and the JDK.

**Tip:**

*   The Android SDK is usually in `/opt/android-sdk`.
*   The JDK varies by the version you are using, if you want to use the default set it to `/usr/lib/jvm/default`.

The navigate to *Edit -> Project Settings -> Editor* and set `Unity Remote Device` to `Any Android Device`.

For more help see the [Unity documentation](http://docs.unity3d.com/Manual/android-sdksetup.html).

### Prepare Android

Install [Unity Remote 5](https://play.google.com/store/apps/details?id=com.unity3d.genericremote) from the Play Store. Alternatively you can download and build it yourself from the Asset Store.

It is also [recommended](http://www.howtogeek.com/192732/android-usb-connections-explained-mtp-ptp-and-usb-mass-storage/) to set your Android device to PTP mode.

**Note:** Don’t forget to turn on “USB Debugging” on your device. Go to *Settings -> Developer* options, then enable USB debugging. As of Android Jelly Bean 4.2 the Developer options are hidden by default. To enable them tap on *Settings -> About Phone -> Build Version* multiple times. Then you will be able to access the *Settings -> Developer* options.

**Tip:** For some devices the remote doesn't work if "Stay awake" is disabled. If you have any problems, make sure to enable it by going to *Settings -> Developer* options, then enable "Stay awake"

For more help see the [Unity documentation](http://docs.unity3d.com/Manual/UnityRemote5.html).

### Test

If you have Unity opened, close it.

Connect the phone to the computer and launch Unity Remote.

Open the Editor and press play. You should now see your game transmitted to your Android device.

If it doesn't work or you have questions, see the [Unity Documentation](http://docs.unity3d.com/Manual/UnityRemote5.html).

## Visual Studio Code

For those using the [Visual Studio Code](/index.php/Visual_Studio_Code "Visual Studio Code") as their script editor, there are a few additional steps you need to do to get it running without displaying errors similar to:

```
[fail]: The reference assemblies for framework ".NETFramework,Version=v3.5" were not found

```

```
[warn]: OmniSharp.MSBuild.ProjectFile.ProjectFileInfo Unable to create directory "/Debug/". Access to the path "/Debug/" is denied.
[fail]: OmniSharp.MSBuild.ProjectFile.ProjectFileInfo Could not write lines to file "/Debug/Assembly-CSharp.csproj.CoreCompileInputs.cache". Could not find a part of the path "/Debug/Assembly-CSharp.csproj.CoreCompileInputs.cache".

```

To eliminate these errors you need to install the following packages: [dotnet-runtime](https://www.archlinux.org/packages/?name=dotnet-runtime), [dotnet-sdk](https://www.archlinux.org/packages/?name=dotnet-sdk), [msbuild-stable](https://aur.archlinux.org/packages/msbuild-stable/), and [mono](https://www.archlinux.org/packages/?name=mono). Finally remember to install the C# extension from the VS Code Marketplace by pressing Ctrl-P and entering:

```
ext install ms-vscode.csharp

```

## Troubleshooting

### Unity crashes on first launch before/while signing in

This is a rare bug where Unity's configuration gets created wrongly. You can try resetting it by:

 `$ rm -rf ~/.config/unity3d/{*.prefs,*.log,Preferences} ` 

### Unity crashes when trying to load project

Users have [reported](http://forum.unity3d.com/threads/unity-on-arch-manjaro-linux.350315/page-3#post-2271637) that unsetting `GTK_IM_MODULE` prevents the crash.

### Unity crashes if ~/.config/user-dirs.dirs is missing

See how to generate the xdg files here: [XDG user directories](/index.php/XDG_user_directories "XDG user directories")

### Minor stuttering while playtesting (NVIDIA)

Vsync does not seem to work correctly with NVIDIA graphics cards / drivers. Solution: In [nvidia-settings](https://www.archlinux.org/packages/?name=nvidia-settings) go to "OpenGL Settings" and turn off "Sync to VBlank".

The behaviour occured/noticed when used "transform.Rotate" in combination with "Input.GetKey".

### Error: Multiple Unity instances cannot open the same project

Unity probably did not shutdown properly, in this case you should navigate to your project folder and delete **Temp** folder.

### Android Remote not working / Running Android build fails with "Unable to forward network traffic to device"

Try this workaround :

1.  Close Unity.
2.  Shutdown adb daemon with `adb kill-server`
3.  Plug in the android device.
4.  Find your device ID with `adb devices`
5.  Use `adb -s "deviceID" forward "tcp:34999" " "` replacing `"deviceID"` with the correct one.

That's it now you can open unity and test it, an error "socket bind failed" will appear that you can safely ignore.