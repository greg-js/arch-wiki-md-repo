Related articles

*   [Unreal Tournament 4](/index.php/Unreal_Tournament_4 "Unreal Tournament 4")

Unreal Engine 4 is the latest version of the videogame Engine Created By Epic Games

The content of this article was originally written on [Unreal Engine wiki](https://wiki.unrealengine.com/Building_On_Linux#Setting_up_on_Arch_Linux) and adapted specifically for Arch Linux.

## Contents

*   [1 Prerequisites](#Prerequisites)
    *   [1.1 Minimum hardware requirements](#Minimum_hardware_requirements)
    *   [1.2 Gain access to the source code](#Gain_access_to_the_source_code)
    *   [1.3 Clang compatibility](#Clang_compatibility)
*   [2 Compilation](#Compilation)
    *   [2.1 Compile manually from source code](#Compile_manually_from_source_code)
    *   [2.2 Installing from the AUR](#Installing_from_the_AUR)
    *   [2.3 Compilation time](#Compilation_time)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Compilation problems](#Compilation_problems)
    *   [3.2 Runtime problems](#Runtime_problems)
    *   [3.3 C++ code project problems](#C.2B.2B_code_project_problems)
    *   [3.4 Disable Tooltips](#Disable_Tooltips)
    *   [3.5 Random freeze under KDE](#Random_freeze_under_KDE)
    *   [3.6 Slow rendered tooltips in KDE](#Slow_rendered_tooltips_in_KDE)
*   [4 Additional Content](#Additional_Content)
    *   [4.1 Starter Content](#Starter_Content)
    *   [4.2 Marketplace Apps](#Marketplace_Apps)

## Prerequisites

### Minimum hardware requirements

*   Intel or Amd CPU@2.5GHz Quad Core **64 Bits**
*   GPU: NVIDIA GeForce GTX 470 or AMD Radeon 6870 HD series
*   RAM: 8 GB

### Gain access to the source code

The Unreal Engine source code is in a [private Github repository](https://github.com/EpicGames/UnrealEngine) requiring free registration with the developer (Epic Games) for access[[1]](https://www.unrealengine.com/en-US/ue4-on-github).

To gain access, login or register at [Epic Games Accounts](https://accounts.epicgames.com/login) and provide an accessible GitHub username at the bottom of the Epic Games ['Connected Accounts Dashboard'](https://www.unrealengine.com/dashboard/connected) page. You will then receive an invite to access the private Github repository.

### Clang compatibility

Unreal Engine might not support the latest versions of Clang. Clang 3.8.1 is confirmed to compile Unreal 4.18.3 and 4.19.2 successfully. **Do not** use Clang 3.4, as it has issues.

Install [downgrade](https://aur.archlinux.org/packages/downgrade/) to use an old version of Clang and LLVM.

## Compilation

You can compile manually from a downloaded GitHub release or install from AUR.

### Compile manually from source code

You can get [the most recent releases](https://github.com/EpicGames/UnrealEngine/releases) on GitHub as zips (~230MiB for the 4.18.3)

This will download about ~4.5 GiB of dependencies:

```
$ ./Setup.sh

```

Prepare for compilation:

```
$ ./GenerateProjectFiles.sh 

```

Then compile:

```
$ make -j1

```

This will directly compile a non-Debug version of the Unreal Engine.

For detailed info refer to [the official instructions to build on Linux](https://wiki.unrealengine.com/Building_On_Linux#Building).

### Installing from the AUR

Unreal Engine 4 is available in the [AUR](/index.php/AUR "AUR") as the [unreal-engine](https://aur.archlinux.org/packages/unreal-engine/) package.

The package is ~28 GiB installed and needs ~100 GiB to build with an output ABS package of ~4.5 GiB when compressed. This AUR package downloads ~9.5 GiB of source files plus ~4.5 GiB of dependencies.

Since the repository is private, you can [set up an SSH key](https://help.github.com/articles/generating-an-ssh-key/) so your GitHub account is used to download the source.

For a smaller download [you can use .zip releases](https://github.com/EpicGames/UnrealEngine/releases) as a source for PKGBUILD.

### Compilation time

The compilation can take from 20 minutes up to a few hours depending on your machine. As an example on a AMD FX-8350 (8 threads) with 16GB DDR3 on a SSD and Clang 3.8.1 takes roughly 40 minutes. (This doesn't include shaders compilation)

## Troubleshooting

### Compilation problems

If the compilation fails you should try building the Editor using the Debug profile[[2]](https://wiki.unrealengine.com/Building_On_Linux#Setting_up_on_Arch_Linux):

```
$ make UE4Editor-Linux-Debug

```

However, this might have some performance impact.

Another approach would be to use different clang version (e.g. 3.8 or 4.0)

### Runtime problems

If the editor doesn't start from the menu, or something doesn't work right, start it in a console and check the output for errors.

```
$ /opt/unreal-engine/Engine/Binaries/Linux/UE4Editor

```

### C++ code project problems

After creating a code project, the new project opens in a text editor instead of in UE4Editor as it should. After re-launching the editor, the new project shows up and can be opened, but on the first run, it takes a half-hour or so to compile, and since this happens in the background (no GUI) it might not seem to be doing anything. The CPU usage should show that it's still compiling, and you may want to launch the editor from a console to see progress.

### Disable Tooltips

UE4's mouse-over tooltips might be rendered very slow. They can be disabled by adding to

 `Engine/Config/ConsoleVariables.ini`  `Slate.AllowToolTips=0` 

### Random freeze under KDE

Disable index file content in the KDE file search options.

### Slow rendered tooltips in KDE

Epic suggest to allow compositing for the Unreal Editor, which is stopped by default. Source: [https://wiki.unrealengine.com/Linux_Known_Issues#KDE](https://wiki.unrealengine.com/Linux_Known_Issues#KDE)

## Additional Content

### Starter Content

The StarterContent project is installed to /opt/unreal-engine/Samples/StarterContent/StarterContent.uproject, you can browse to it from the launcher.

### Marketplace Apps

The launcher with the Unreal Marketplace is not available for Linux yet[[3]](https://forums.unrealengine.com/showthread.php?52166-Unreal-launcher-for-linux), so apps like the ContentExamples project cannot be installed from Linux[[4]](https://answers.unrealengine.com/questions/301869/download-content-from-marketplace-on-linux.html).

The marketplace apps can be downloaded using the [launcher](https://www.unrealengine.com/download) on Windows (Mac may also work), they are stored in:

```
   /Program Files (x86)/Epic Games/Launcher/VaultCache/

```

Also there is an implementation of [UE4 Marketplace Downloader](https://github.com/Allar/ue4-mp-downloader) written in JS.