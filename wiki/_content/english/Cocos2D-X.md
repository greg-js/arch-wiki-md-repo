Cocos2D-X is a high-performance cross platform 2D/3D game engine that supports multiple platforms such as iOS, Android, WinXP/7/8, WP8, BlackBerry, MeeGo, Marmelade, WebOS, Mac OS X. This page will focus on properly configuring this package for initial usage for the most part. For other documentation, click [here](#See_also).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 PATH Environment Variable](#PATH_Environment_Variable)
    *   [2.2 Python Scripts Workaround](#Python_Scripts_Workaround)
    *   [2.3 Disable sending usage data](#Disable_sending_usage_data)
    *   [2.4 Cross Compiling for Android](#Cross_Compiling_for_Android)
    *   [2.5 Updating SDKBOX](#Updating_SDKBOX)
*   [3 Cocos2D-X Development Notes](#Cocos2D-X_Development_Notes)
    *   [3.1 Creating a Scene with Physics](#Creating_a_Scene_with_Physics)
*   [4 See also](#See_also)

## Installation

Install [cocos2d-x-src](https://aur.archlinux.org/packages/cocos2d-x-src/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

## Configuration

### PATH Environment Variable

If you install manually, add `/<your-cocos2d-x-dir>/tools/cocos2d-console/bin`, and `/<your-cocos2d-x-dir>/tools/cocos2d-console/plugins/plugin_package` to your **PATH** environment variable mostly to run the `cocos` python2 script to create projects, and also run `sdkbox` respectively. Add the following to your respective shell configuration file (**~/.bashprofile**, **~/.zshenv**, etc):

```
export PATH=/opt/cocos2d-x/tools/cocos2d-console/bin:/opt/cocos2d-x/tools/cocos2d-console/plugins/plugin_package:${PATH}

```

If you use the version from AUR, package will automatically add all the necessary environment variables to the PATH. After installation, you need to reload the environment variables from /etc/profile. You can do it manually:

```
source /etc/profile

```

or just reload session.

### Python Scripts Workaround

Since some Cocos2D-X scripts use `python2` instead of `python3`, like `sdkbox`, simply calling `python2 foo.pyc` will not suffice since other modules will be called with "env python" which could point to python3\. To avoid this, install version from AUR, or change script headers or read [here](/index.php/Python#Dealing_with_version_problem_in_build_scripts "Python"). Don't forget to add `/usr/local/bin`, or whichever directory the workaround shell script is installed at, before `/usr/bin` in your PATH environment variable. The following should suffice:

```
export PATH=/usr/local/bin:${PATH}

```

Here's an example shell script workaround:

 `/usr/local/bin/python` 
```
#!/bin/bash
script=$(readlink -f -- "$1")
case "$script" in (/opt/cocos2d-x/*|/path/to/project1/*|/path/to/project2/*|/path/to/project3/*)
    exec python2 "$@"
esac

exec python3 "$@"

```

### Disable sending usage data

Sending the usage data can be disabled setting `enable_stat` to `false` in `/opt/cocos2d-x/tools/cocos2d-console/bin/cocos2d.ini`:

```
# sed -e 's/enable_stat=.*/enable_stat=false/g' -i /opt/cocos2d-x/tools/cocos2d-console/bin/cocos2d.ini

```

### Cross Compiling for Android

Install [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk), [android-ndk](https://aur.archlinux.org/packages/android-ndk/), [android-sdk](https://aur.archlinux.org/packages/android-sdk/) and [android-sdk-platform-tools](https://aur.archlinux.org/packages/android-sdk-platform-tools/), and also add the following to your shell configuration file:

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

## Cocos2D-X Development Notes

### Creating a Scene with Physics

*   As of Cocos2D-X version 3.14, the `HelloWorldScene.cpp` and `HelloWorldScene.h` templates have been updated in [cocos2d-x-src](https://aur.archlinux.org/packages/cocos2d-x-src/) to reflect the the fact that `cocos2d::Layer` has been deprecated. See [issue #16941](https://github.com/cocos2d/cocos2d-x/issues/16941) in the official Cocos2D-X repository.
    *   In order to create a `cocos2d::Scene` with physics, line 16 of `HelloWorld.cpp` must be changed to the following: `if ( !Scene::initWithPhysics() )`

## See also

*   [Official Programmers Guide](http://www.cocos2d-x.org/programmersguide/)
*   [Cocos2D-X Developer Guide](http://cocos.sonarlearning.co.uk/)
*   [Official API Referenece Guide](http://www.cocos2d-x.org/wiki/Reference)
*   [Texture Rendering + Blur Tutorial](http://discuss.cocos2d-x.org/t/cocos3-8-tutorial-rendertexture-blur/13622)
*   [Particle2DX](http://particle2dx.com/) - Cocos2D-X Particle Generator