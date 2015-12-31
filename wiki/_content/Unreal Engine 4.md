# Unreal Engine 4

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Unreal Engine 4 is the latest version of the videogame Engine Created By Epic Games

The content of this article was originally written on [this page](https://wiki.unrealengine.com/Building_On_Linux) and adapted specifically for Arch Linux.

## Contents

*   [1 Minimum requirements](#Minimum_requirements)
*   [2 Installation](#Installation)
    *   [2.1 Compile from source code](#Compile_from_source_code)
        *   [2.1.1 Satisfy dependencies](#Satisfy_dependencies)
        *   [2.1.2 Get the source code](#Get_the_source_code)
        *   [2.1.3 Prepare to compile](#Prepare_to_compile)
        *   [2.1.4 Compile the source code](#Compile_the_source_code)
*   [3 Run Unreal Engine 4](#Run_Unreal_Engine_4)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Compilation errors](#Compilation_errors)
        *   [4.1.1 "ConvexHull2D.h" not found](#.22ConvexHull2D.h.22_not_found)
    *   [4.2 Compilation problems](#Compilation_problems)

## Minimum requirements

*   PC or Mac
*   Intel or Amd CPU@2.5GHz Quad Core **64 Bits**
*   GPU: NVIDIA GeForce GTX 470 or AMD Radeon 6870 HD series
*   RAM: 8 GB

## Installation

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** This must be translated into a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") and uploaded to the [AUR](/index.php/AUR "AUR"), and simply linked from here. (Discuss in [Talk:Unreal Engine 4#](https://wiki.archlinux.org/index.php/Talk:Unreal_Engine_4))

### Compile from source code

#### Satisfy dependencies

Install [clang35](https://www.archlinux.org/packages/?name=clang35), [mono](https://www.archlinux.org/packages/?name=mono), [dos2unix](https://www.archlinux.org/packages/?name=dos2unix) and [cmake](https://www.archlinux.org/packages/?name=cmake).

Some users will have to either recompile their Clang or get a compiled package that does not use `ld.gold`:

```
$ mkdir ~/bin/ && cd ~/bin/ && ln -s /bin/ld.bfd ./ld.gold

```

Then modify the [.bashrc](/index.php/.bashrc ".bashrc") file and add the following line:

```
export PATH=$HOME/bin:$PATH

```

Then close all the terminals to apply the changes.

#### Get the source code

First you need to register in the [Epic Games](https://www.unrealengine.com) Webpage and link your GitHub Account to your Epic Games Account.

Then download the source code with the following command:

```
$ git clone -b release https://github.com/EpicGames/UnrealEngine.git

```

#### Prepare to compile

```
$ cd UnrealEngine
$ ./Setup.sh
$ ./GenerateProjectFiles.sh

```

#### Compile the source code

To compile the source code execute the following command:

```
$ make UE4Editor UE4Game UnrealPak CrashReportClient ShaderCompileWorker UnrealLightmass

```

This process will take a long time.

## Run Unreal Engine 4

```
$ cd Engine/Binaries/Linux
$ ./UE4Editor

```

## Troubleshooting

#### Compilation errors

##### "ConvexHull2D.h" not found

You need to modify the `SubUVAnimation.cpp` file located in `/Engine/Source/Runtime/Engine/Orivate/Particles` and override this line:

```
#include "ConvexHull2D.h"

```

with this:

```
#include "ConvexHull2d.h"

```

#### Compilation problems

If the compilation fails you should try building the Editor using the Debug profile:

```
$ make UE4Editor-Linux-Debug

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Unreal_Engine_4&oldid=413930](https://wiki.archlinux.org/index.php?title=Unreal_Engine_4&oldid=413930)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Development](/index.php/Category:Development "Category:Development")
*   [Gaming](/index.php/Category:Gaming "Category:Gaming")