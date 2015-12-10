# Cocos2D-X

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Cocos2D-X is a high-performance cross platform 2D/3D game engine that supports multiple platforms such as iOS, Android, WinXP/7/8, WP8, BlackBerry, MeeGo, Marmelade, WebOS, Mac OS X. This page will focus entirely on properly configuring this package for initial usage. For other documentation, click [here](#See_also).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 PATH Environment Variable](#PATH_Environment_Variable)
    *   [2.2 Python Buildscripts Workaround](#Python_Buildscripts_Workaround)
    *   [2.3 Cross Compiling for Android](#Cross_Compiling_for_Android)
    *   [2.4 Updating SDKBOX](#Updating_SDKBOX)
*   [3 See also](#See_also)

## Installation

Install [cocos2d-x-src](https://aur.archlinux.org/packages/cocos2d-x-src/)<sup><small>AUR</small></sup> from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

## Configuration

### PATH Environment Variable

After installation, add `/opt/cocos2d-x/tools/cocos2d-console/bin`, and `/opt/cocos2d-x/tools/cocos2d-console/plugins/plugin_package` to your **PATH** environment variable mostly to run the `cocos` python2 script to create projects, and also run `sdkbox` respectively. Add the following to your respective shell configuration file (**~/.bashprofile**, **~/.zshenv**, etc):

```
export PATH=/opt/cocos2d-x/tools/cocos2d-console/bin:/opt/cocos2d-x/tools/cocos2d-console/plugins/plugin_package:${PATH}

```

### Python Buildscripts Workaround

Since most Cocos2D-X scripts use `python2` instead of `python3`, simply calling `python2 foo.py` will not suffice since other modules will be called with "env python" which could point to python3\. To fix this, read [here](https://wiki.archlinux.org/index.php/python#Dealing_with_version_problem_in_build_scripts). Don't forget to add `/usr/local/bin`, or whichever directory the workaround shell script is installed at, before `/usr/bin` in your PATH environment variable. The following should suffice:

```
export PATH=/usr/local/bin:${PATH}

```

### Cross Compiling for Android

Install [android-ndk](https://aur.archlinux.org/packages/android-ndk/)<sup><small>AUR</small></sup>, [android-sdk](https://aur.archlinux.org/packages/android-sdk/)<sup><small>AUR</small></sup> and [android-sdk-platform-tools](https://aur.archlinux.org/packages/android-sdk-platform-tools/)<sup><small>AUR</small></sup>, and also add the following to your shell configuration file:

```
export NDK_ROOT=/opt/android-ndk
export ANDROID_SDK_ROOT=/opt/android-sdk
export ANT_ROOT=/usr/bin

```

The `android` tool should suffice to fetch the SDK platform for a certain android version, however there are also packages in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") such as `android-platform` for downloading these SDK platforms.

### Updating SDKBOX

Cocos2D-X comes with a tool called `sdkbox` for integrating third party software development kits into projects easily. To update this tool, you must have read/write/execute access to `/opt/cocos2d-x/tools/cocos2d-console/plugins/plugin_package` and the following files in that directory: `sdkbox`, `sdkbox.bat`, `sdkbox.pyc`

For a single-user configuration, executing the following will suffice:

```
# chown $USER:$USER /opt/cocos2d-x/tools/cocos2d-console/plugins/plugin_package/{,sdkbox,sdkbox.bat,sdkbox.pyc}
$ sdkbox update

```

## See also

*   [Official Programmers Guide](http://www.cocos2d-x.org/programmersguide/)
*   [Cocos2D-X Developer Guide](http://cocos.sonarlearning.co.uk/)
*   [Official API Referenece Guide](http://www.cocos2d-x.org/wiki/Reference)
*   [Enabling Immersive Mode for Android](http://discuss.cocos2d-x.org/t/how-to-set-full-screen-on-android-4-4/10278/3) - See **Cookiebit'**s answer.
*   [Texture Rendering + Blur Tutorial](http://discuss.cocos2d-x.org/t/cocos3-8-tutorial-rendertexture-blur/13622)
*   [Particle2DX](http://particle2dx.com/) - Cocos2D-X Particle Generator

Retrieved from "[https://wiki.archlinux.org/index.php?title=Cocos2D-X&oldid=411360](https://wiki.archlinux.org/index.php?title=Cocos2D-X&oldid=411360)"