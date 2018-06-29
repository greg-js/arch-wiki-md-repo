Related articles

*   [Archiso_offline](/index.php/Archiso_offline "Archiso offline")

## Contents

*   [1 Normal Method: Pacman](#Normal_Method:_Pacman)
    *   [1.1 A simple example](#A_simple_example)
    *   [1.2 A slightly contrived example](#A_slightly_contrived_example)
        *   [1.2.1 Generate a list of packages to download](#Generate_a_list_of_packages_to_download)
        *   [1.2.2 Download/copy the packages and their dependencies](#Download.2Fcopy_the_packages_and_their_dependencies)
        *   [1.2.3 Create a repository database just for these packages](#Create_a_repository_database_just_for_these_packages)
        *   [1.2.4 Transfer the packages](#Transfer_the_packages)
        *   [1.2.5 Install the packages](#Install_the_packages)
    *   [1.3 Restoring online sources](#Restoring_online_sources)
        *   [1.3.1 Links and sources](#Links_and_sources)

## Normal Method: Pacman

This method is based on [byte's](/index.php/User:Byte "User:Byte") post from [this](https://bbs.archlinux.org/viewtopic.php?id=30431) thread.

Download the package databases on a computer with internet access and transfer them to your computer. If needed, change `MIRROR` to any mirror from the [mirror status list](https://www.archlinux.org/mirrors/status/).

```
#!/bin/bash

ARCH='x86_64'
MIRROR='[https://mirrors.kernel.org/archlinux/'](https://mirrors.kernel.org/archlinux/')

wget "${MIRROR}/community/os/${ARCH}/community.db"
wget "${MIRROR}/core/os/${ARCH}/core.db"
wget "${MIRROR}/extra/os/${ARCH}/extra.db"
wget "${MIRROR}/multilib/os/${ARCH}/multilib.db"
```

Following steps will make sure you are working with up-to-date package lists, as if you ran `pacman -Sy`.

After transferring the `*.db` files to the offline PC, do the following:

```
# cp *.db /var/lib/pacman/sync/
# pacman -Sp --noconfirm *package-name* > pkglist

```

**Tip:** Be aware you have enabled at least one of the servers defined in the `/etc/pacman.d/mirrorlist` file. Otherwise all what you get is a misleading error message: `error: no database for package: package-name`.

To update a New Arch Linux base system after installation you may enter

```
# pacman -Sup --noconfirm > pkglist

```

Now open that textfile with an editor and delete all lines that are not URLs. Next, bring that list with you to a place where you have internet and either download the listed packages manually or run `wget` in an empty directory:

```
# wget -nv -i ../pkglist

```

**Tip:** When using [cygwin](https://www.cygwin.com) or some other kind of Windows environment to download the packages the filenames will get mangled, since default Windows file naming requires to escape e.g. colons. To avoid this (under cygwin, since it doesn't follow such restrictions) use `wget --restrict-file-names=unix`.

Take all the `*.pkg.tar.gz` files back home, put them in `/var/cache/pacman/pkg` and finally run

```
# pacman -S *package-name*

```

### A simple example

This is a simple way to install a package you have downloaded:

```
# pacman -U /root/Download/packagename.tar.gz

```

This is how to install several packages you have installed into a directory

```
# pacman -U /root/Download/*.tar.gz

```

### A slightly contrived example

Scenario: you have two Arch Linux machines, 'Al' (with internet connection) and 'Bob' (without internet connection), and you need to install some [NVIDIA](/index.php/NVIDIA "NVIDIA") packages and their dependencies on 'Bob'. In this example, the wanted packages are [nvidia](https://www.archlinux.org/packages/?name=nvidia), [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils), and [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau), but you want to use a dedicated directory instead of `/var/cache/pacman/pkg/` and a dedicated repository called nvidia (instead of the usual core, extra etc...)

#### Generate a list of packages to download

This can be done on any Arch Linux machine which has up-to-date repository data bases (see above for links to database files); to create the list of links to the required packages, use:

```
# pacman -Sp nvidia nvidia-utils xf86-video-nouveau > /path/to/nvidia.list

```

The file `nvidia.list` will contain links to the listed packages and any others which they depend on which are not already installed on 'Al'. Unless you have cleared your cache the packages you have installed will be in your cache location. You can check `/etc/pacman.conf` for the location. It is probably something like `/var/cache/pacman/pkg/`.

#### Download/copy the packages and their dependencies

Obviously this requires an internet connection, so on 'Al' create a directory called `/path/to/nvidia` for the files and run:

```
# wget -P /path/to/nvidia/ -i /path/to/nvidia.list

```

Then copy the dependencies you have already installed from the cache. Either find them manually by browsing [https://www.archlinux.org/packages/](https://www.archlinux.org/packages/) or if the total size of all your packages is not too large just copy them all

```
# cp /var/cache/pacman/pkg/* /path/to/nvidia/

```

#### Create a repository database just for these packages

This can be done on either 'Al' or 'Bob' using the `repo-add` command which comes with [pacman](https://www.archlinux.org/packages/?name=pacman) (from version 3?); first, change to the `/path/to/nvidia` directory where the packages were downloaded, then create database file called `nvidia.db.tar.gz`:

```
$ cd /path/to/nvidia
# repo-add nvidia.db.tar.gz *.pkg.tar.xz

```

#### Transfer the packages

Now all the packages have been downloaded, you do not need 'Al' anymore. Copy the contents of `/path/to/nvidia` to a the temporary NVIDIA packages cache directory on 'Bob'. In this example, this folder is called `/home/me/nvidia`:

```
$ cp /path/to/nvidia/* /home/me/nvidia

```

Next, [pacman](https://www.archlinux.org/packages/?name=pacman) must be made aware of this new repository of packages. First copy your current `pacman.conf`:

```
# cp /etc/pacman.conf /etc/pacman.conf.old

```

Now in `/etc/pacman.conf` make sure that your `SigLevel` is set to `Never` as your repository will not provide signatures

```
SigLevel = Never

```

and add the following lines at the bottom of `pacman.conf`:

```
[nvidia]
Server = file:///home/me/nvidia

```

You may also need to comment out the other repositories so stale defaults do not cause failed attempts to download from online Now, instruct [pacman](https://www.archlinux.org/packages/?name=pacman) to synchronize with the dedicated NVIDIA repository we created:

```
# pacman -Sy 

```

This command finds the `nvidia.db.tar.gz` file in `/home/me/nvidia` and expands it to `/var/lib/pacman/sync/nvidia` to create a database of packages contained in the NVIDIA repository.

#### Install the packages

Finally install the packages:

```
# pacman -S nvidia nvidia-utils xf86-video nouveau

```

### Restoring online sources

Should Bob ever be put online we can restore access to the online sources by replacing `/etc/pacman.conf` with the previously created `/etc/pacman.conf.old`.

#### Links and sources

Compiled from the forums, with thanks to [Heller_Barbe](https://bbs.archlinux.org/viewtopic.php?id=60856)) and [byte](https://bbs.archlinux.org/viewtopic.php?id=30431)