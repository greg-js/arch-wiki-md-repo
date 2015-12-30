# Unreal Engine 4

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Unreal Engine 4 is the latest version of the videogame Engine Created By Epic Games

The content of this article was originally written on [this page](https://wiki.unrealengine.com/Building_On_Linux) and adapted specifically for ArchLinux

* * *

## Contents

*   [1 Minimum requirements](#Minimum_requirements)
*   [2 Installation](#Installation)
    *   [2.1 From AUR](#From_AUR)
    *   [2.2 Compile from Source Code](#Compile_from_Source_Code)
        *   [2.2.1 Satisfy Dependencies](#Satisfy_Dependencies)
        *   [2.2.2 Get the source code](#Get_the_source_code)
        *   [2.2.3 Prepare to compile](#Prepare_to_compile)
        *   [2.2.4 Compile the source code](#Compile_the_source_code)
    *   [2.3 Run Unreal Engine 4](#Run_Unreal_Engine_4)
    *   [2.4 Common Issues](#Common_Issues)
        *   [2.4.1 Compilation Problems](#Compilation_Problems)

## Minimum requirements

PC or Mac

Intel or Amd CPU@2.5GHz Quad Core **64 Bits**

GPU: NVIDIA GeForce GTX 470 or AMD Radeon 6870 HD series

RAM: 8 GB

## Installation

### From AUR

To install from AUR only put the following command in a terminal:

```
$ yaourt -S UE4

```

This command will automatically install the **binaries**.

### Compile from Source Code

* * *

#### Satisfy Dependencies

```
$ sudo pacman -S clang35 mono dos2unix cmake

```

Some users will have to either recompile their Clang or get a compiled package that does not use ld.gold

```
$ mkdir ~/bin/ && cd ~/bin/ && ln -s /bin/ld.bfd ./ld.gold

```

Then modify the .bashrc file (generally hidden in / home) and add the following line:

```
export PATH=$HOME/bin:$PATH

```

Then Close all the terminals to apply the changes

* * *

#### Get the source code

First you need to register in the [Epic Games](https://www.unrealengine.com) Webpage and link your GitHub Account to your Epic Games Account

Then Download the source code with the following command

```
$ git clone -b release [https://github.com/EpicGames/UnrealEngine.git](https://github.com/EpicGames/UnrealEngine.git)

```

* * *

#### Prepare to compile

```
$ cd UnrealEngine
$ ./Setup.sh
$ ./GenerateProjectFiles.sh

```

* * *

#### Compile the source code

To compile the source Code Execute the following commands:

```
$ make UE4Editor UE4Game UnrealPak CrashReportClient ShaderCompileWorker UnrealLightmass
$ make -j1 ShaderCompileWorker

```

This process will take a long time.

* * *

### Run Unreal Engine 4

```
$cd Engine/Binaries/Linux
$./UE4Editor

```

### Common Issues

* * *

#### Compilation Problems

If the compilation fails you should try building the Editor using the Debug profile

```
$ make UE4Editor-Linux-Debug

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Unreal_Engine_4&oldid=413829](https://wiki.archlinux.org/index.php?title=Unreal_Engine_4&oldid=413829)"