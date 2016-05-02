Unreal Engine 4 is the latest version of the videogame Engine Created By Epic Games

The content of this article was originally written on [this page](https://wiki.unrealengine.com/Building_On_Linux) and adapted specifically for Arch Linux.

## Contents

*   [1 Minimum requirements](#Minimum_requirements)
*   [2 Installation](#Installation)
    *   [2.1 Register to get the source code](#Register_to_get_the_source_code)
    *   [2.2 Installing from the AUR](#Installing_from_the_AUR)
    *   [2.3 Compile from source code](#Compile_from_source_code)
        *   [2.3.1 Satisfy dependencies](#Satisfy_dependencies)
        *   [2.3.2 Get the source code](#Get_the_source_code)
        *   [2.3.3 Prepare to compile](#Prepare_to_compile)
        *   [2.3.4 Compile the source code](#Compile_the_source_code)
*   [3 Run Unreal Engine 4](#Run_Unreal_Engine_4)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Compilation problems](#Compilation_problems)

## Minimum requirements

*   Intel or Amd CPU@2.5GHz Quad Core **64 Bits**
*   GPU: NVIDIA GeForce GTX 470 or AMD Radeon 6870 HD series
*   RAM: 8 GB

## Installation

#### Register to get the source code

First you need to register on the [Epic Games](https://www.unrealengine.com) Webpage and link your GitHub account to your Epic Games account.

### Installing from the AUR

Unreal Engine 4 is available in the [AUR](/index.php/AUR "AUR") as the [unreal-engine](https://aur.archlinux.org/packages/unreal-engine/) package.

The package is 22 GiB once installed, so it needs about 100 GiB free space to build. There is about 7 GiB of source files to download, and the compilation might take a few hours.

Since the repository is private, you can [set up an SSH key](https://help.github.com/articles/generating-an-ssh-key/) so your GitHub account is used to download the source.

### Compile from source code

#### Satisfy dependencies

Install [clang35](https://www.archlinux.org/packages/?name=clang35), [mono](https://www.archlinux.org/packages/?name=mono), [dos2unix](https://www.archlinux.org/packages/?name=dos2unix) and [cmake](https://www.archlinux.org/packages/?name=cmake).

Some users will have to either recompile their Clang or get a compiled package that does not use `ld.gold`:

If you installed clang35 from the repositories do the following:

```
$ mkdir ~/bin/ && cd ~/bin/ && ln -s /bin/ld.bfd ./ld.gold

```

Then modify the [.bashrc](/index.php/.bashrc ".bashrc") file and add the following line:

```
export PATH=$HOME/bin:$PATH

```

Then close all the terminals to apply the changes.

#### Get the source code

Download the source code with the following command, logging in with a github account which is registered on unrealengine.com:

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

#### Compilation problems

If the compilation fails you should try building the Editor using the Debug profile:

```
$ make UE4Editor-Linux-Debug

```