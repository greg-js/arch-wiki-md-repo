# Offline installation of packages

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** ftp.archlinux.org has been shut down [[1]](https://lists.archlinux.org/pipermail/aur-general/2015-February/030268.html) (Discuss in [Talk:Offline installation of packages#](https://wiki.archlinux.org/index.php/Talk:Offline_installation_of_packages))

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
*   [2 Simpler Method: Powerpill Portable](#Simpler_Method:_Powerpill_Portable)
    *   [2.1 Requirements](#Requirements)
        *   [2.1.1 Unconnected Computer](#Unconnected_Computer)
        *   [2.1.2 Connected Computer](#Connected_Computer)
    *   [2.2 Steps](#Steps)

## Normal Method: Pacman

This method is based on [byte's](/index.php/User:Byte "User:Byte") post from [this](https://bbs.archlinux.org/viewtopic.php?id=30431) thread.

Download the package databases on a computer with internet access and transfer them to your computer.

For i686:

*   [ftp://ftp.archlinux.org/core/os/i686/core.db.tar.gz](ftp://ftp.archlinux.org/core/os/i686/core.db.tar.gz)
*   [ftp://ftp.archlinux.org/core/os/i686/core.db](ftp://ftp.archlinux.org/core/os/i686/core.db)
*   [ftp://ftp.archlinux.org/extra/os/i686/extra.db.tar.gz](ftp://ftp.archlinux.org/extra/os/i686/extra.db.tar.gz)
*   [ftp://ftp.archlinux.org/extra/os/i686/extra.db](ftp://ftp.archlinux.org/extra/os/i686/extra.db)
*   [ftp://ftp.archlinux.org/community/os/i686/community.db.tar.gz](ftp://ftp.archlinux.org/community/os/i686/community.db.tar.gz)
*   [ftp://ftp.archlinux.org/community/os/i686/community.db](ftp://ftp.archlinux.org/community/os/i686/community.db)
*   [ftp://ftp.archlinux.org/multilib/os/i686/multilib.db.tar.gz](ftp://ftp.archlinux.org/multilib/os/i686/multilib.db.tar.gz)

For x86_64:

*   [ftp://ftp.archlinux.org/core/os/x86_64/core.db.tar.gz](ftp://ftp.archlinux.org/core/os/x86_64/core.db.tar.gz)
*   [ftp://ftp.archlinux.org/core/os/x86_64/core.db](ftp://ftp.archlinux.org/core/os/x86_64/core.db)
*   [ftp://ftp.archlinux.org/extra/os/x86_64/extra.db.tar.gz](ftp://ftp.archlinux.org/extra/os/x86_64/extra.db.tar.gz)
*   [ftp://ftp.archlinux.org/extra/os/x86_64/extra.db](ftp://ftp.archlinux.org/extra/os/x86_64/extra.db)
*   [ftp://ftp.archlinux.org/community/os/x86_64/community.db.tar.gz](ftp://ftp.archlinux.org/community/os/x86_64/community.db.tar.gz)
*   [ftp://ftp.archlinux.org/community/os/x86_64/community.db](ftp://ftp.archlinux.org/community/os/x86_64/community.db)
*   [ftp://ftp.archlinux.org/multilib/os/x86_64/multilib.db.tar.gz](ftp://ftp.archlinux.org/multilib/os/x86_64/multilib.db.tar.gz)
*   [ftp://ftp.archlinux.org/multilib/os/x86_64/multilib.db](ftp://ftp.archlinux.org/multilib/os/x86_64/multilib.db)

Following steps will make sure you're working with up-to-date package lists, as if you ran `pacman -Sy`.

On offline PC , do the following as root:

```
mkdir -p /var/lib/pacman/sync/{core,extra,community,multilib}
rm -r /var/lib/pacman/sync/{core,extra,community}/*
tar -xzf core.db.tar.gz      -C /var/lib/pacman/sync/core
tar -xzf extra.db.tar.gz     -C /var/lib/pacman/sync/extra
tar -xzf community.db.tar.gz -C /var/lib/pacman/sync/community
tar -xzf multilib.db.tar.gz  -C /var/lib/pacman/sync/multilib
rm -r /var/lib/pacman/sync/*.db
cp core.db /var/lib/pacman/sync/
cp extra.db /var/lib/pacman/sync/
cp community.db /var/lib/pacman/sync/
cp multilib.db /var/lib/pacman/sync/

```

```
pacman -Sp --noconfirm package-name > pkglist

```

**Tip:** Be aware you have enabled at least one of the servers defined in the /etc/pacman.d/mirrorlist file. Otherwise all what you get is a misleading error message:error: no database for package: package-name

To update a New Arch Linux base system after installation you may enter

```
pacman -Sup --noconfirm > pkglist

```

Now open that textfile with an editor and delete all lines that are not URLs. Next, bring that list with you to a place where you have internet and either download the listed packages manually or do

```
wget -nv -i ../pkglist

```

in an empty directory. Take all the *.pkg.tar.gz files back home, put them in /var/cache/pacman/pkg and finally run

```
pacman -S package-name

```

### A simple example

This is a simple way to install a package you have downloaded

```
 pacman -U /root/Download/packagename.tar.gz

```

This is how to install several packages you have installed into a directory

```
 pacman -U /root/Download/*.tar.gz

```

### A slightly contrived example

Scenario: you have two Archlinux machines, 'Al' (with internet connection) and 'Bob' (without internet connection), and you need to install some nvidia packages and their dependencies on 'Bob'. Let's say the wanted packages are nvidia, nvidia-utils and xf86-video-nouveau, but you want to use a dedicated directory instead of /var/cache/pacman/pkg/ and a dedicated repository called nvidia (instead of the usual core, extra etc...)

#### Generate a list of packages to download

This can be done on any Archlinux machine which has up-to-date repository data bases (see above for links to database files); to create the list of links to the required packages, use:

```
pacman -Sp nvidia nvidia-utils xf86-video-nouveau > /path/to/nvidia.list

```

The file nvidia.list will contain links to the listed packages and any others which they depend on which are not already installed on Al. Unless you have cleared your cache the packages you have installed will be in your cache location. Tou can check /etc/pacman.conf for the location. It is probably something like /var/cache/pacman/pkg/

#### Download/copy the packages and their dependencies

Obviously this requires an internet connection, so on 'Al' create a directory called /path/to/nvidia for the files and run:

```
wget -P /path/to/nvidia/ -i /path/to/nvidia.list

```

Then copy the dependancies you have already instaled from the cache. Either find them manually by browsing [https://www.archlinux.org/packages/](https://www.archlinux.org/packages/) or if the total size of all your packages is not too large just copy them all

```
cp /var/cache/pacman/pkg/* /path/to/nvidia/

```

#### Create a repository database just for these packages

This can be done on either 'Al' or 'Bob' using the repo-add command which comes with pacman (from version 3?); first, change to the /path/to/nvidia directory where the packages were downloaded, then create database file called nvidia.db.tar.gz:

```
cd /path/to/nvidia
repo-add nvidia.db.tar.gz *.pkg.tar.xz

```

#### Transfer the packages

Now all the packages have been downloaded, you do not need 'Al' anymore. Copy the contents of /path/to/nvidia to a the temporary nvidia packages cache directory on 'Bob', let's say this folder is called /home/me/nvidia:

```
cp /path/to/nvidia/* /home/me/nvidia

```

Next, pacman must be made aware of this new repository of packages. First copy your current pacman.conf

```
cp /etc/pacman.conf /etc/pacman.conf.old

```

Now in /etc/pacman.conf make sure that your SigLevel is set to Never as your repository will not provide signatures

```
SigLevel = Never

```

and add the following lines at the bottom of pacman.conf:

```
[nvidia]
Server = file:///home/me/nvidia

```

You may also need to comment out the other repositories so stale defaults do not cause failed attempts to download from online Now, instruct pacman to synchronise with the dedicated nvidia repository we created:

```
pacman -Sy 

```

This command finds the nvidia.db.tar.gz file in /home/me/nvidia and expands it to /var/lib/pacman/sync/nvidia to create a database of packages contained in the nvidia repository.

#### Install the packages

Finally install the packages:

```
pacman -S nvidia nvidia-utils xf86-video nouveau

```

### Restoring online sources

Should Bob ever be put online we can resore access to the online sources by replacing /etc/pacman.conf with the previously created /etc/pacman.conf.old

#### Links and sources

Compiled from the forums, with thanks to [Heller_Barbe](https://bbs.archlinux.org/viewtopic.php?id=60856)) and [byte](https://bbs.archlinux.org/viewtopic.php?id=30431)

## Simpler Method: Powerpill Portable

[Powerpill Portable](http://xyne.archlinux.ca/scripts/pacman/#powerpill-portable) is a tool created by Xyne to simplify offline updates. It has the following requirements:

**Warning:** _Powerpill_ development has been officially discontinued: its latest version does not work with _pacman>=3.5_. See [[2]](https://bbs.archlinux.org/viewtopic.php?id=115660).

### Requirements

#### Unconnected Computer

*   powerpill
*   rsync

#### Connected Computer

*   perl
*   aria2

The connected computer does not need to be running Arch or have Pacman installed.

### Steps

An enumerated list of steps can be found [here](http://xyne.archlinux.ca/scripts/pacman/#usage-example).

Basically, simply download the Powerpill Portable script and run it on the unconnected computer. It will create a directory named "portable" and copy some files into it (the local database and everything needed to run powerpill-portable on another system, minus perl itself and aria2). Simply take the directory to the connected computer (e.g. on a USB stick) and run the "pp" script in it on that system as though it were pacman, e.g. "pp -Syu foo bar". It will download the databases and packages into the portable directory. When you're done, bring the directory back to your unconnected computer, run the "sync" script in the portable directory, then simply run the same command(s) that you ran with pp using pacman, e.g. "pacman -Syu foo bar".

Your system is now up-to-date. Simply repeat the steps to keep it that way.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Offline_installation_of_packages&oldid=400872](https://wiki.archlinux.org/index.php?title=Offline_installation_of_packages&oldid=400872)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Package management](/index.php/Category:Package_management "Category:Package management")
*   [Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch")

Hidden category:

*   [Pages or sections flagged with Template:Out of date](/index.php/Category:Pages_or_sections_flagged_with_Template:Out_of_date "Category:Pages or sections flagged with Template:Out of date")