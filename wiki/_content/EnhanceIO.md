# EnhanceIO

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[EnhanceIO](https://github.com/stec-inc/EnhanceIO) makes it possible to use an SSD as a caching device for any other type of block device storage (HDD, Network, you name it) with almost zero configuration. Based on [Flashcache](/index.php/Flashcache "Flashcache") is it much simpler to set up. Unlike [Bcache](/index.php/Bcache "Bcache") there is no need to convert file systems.

**Warning:**

*   As always be careful and read the documentation carefully before attempting to use EnhanceIO, do not confuse your HDD and SDD and make sure the SSD does not have any important data on it.
*   There is a [known issue](https://github.com/stec-inc/EnhanceIO/issues/30) with EnhanceIO causing filesystem corruption if fsck is run on file system before cache is brought up.
*   As of October 2015 EnhanceIO is [completely broken](https://github.com/stec-inc/EnhanceIO/issues/106) on newer kernels.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Setting up the module and drives](#Setting_up_the_module_and_drives)
    *   [1.2 Getting information on caches](#Getting_information_on_caches)
    *   [1.3 Enable EnhanceIO on initcpio](#Enable_EnhanceIO_on_initcpio)

## Installation

Install [enhanceio-dkms-git](https://aur.archlinux.org/packages/enhanceio-dkms-git/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR").

**Note:** Throughout the page, `/dev/sda` will be used to indicate the slow drive and `/dev/sdb` will be used to indicate the fast drive. Be sure to change these examples to match your setup.

### Setting up the module and drives

The EnhanceIO command line interface (eio_cli) is used to manage your setup. Set up caching on your fast ssd for your slow hdd like so:

```
# eio_cli create -d /dev/sda -s /dev/sdb -c my_first_enhanceio

```

This will use the default options which are safe, if you want to enhance speed even further you might want to add `-m wb` to enable WriteBack mode instead of WriteThrough. This might put data itegrity at risk though.

The cache drive is persistent now, which means even after a reboot it will still be used. If you want to deactive it first set the cache into read-only mode to not lose any yet unwritten blocks

```
# eio_cli edit -c my_first_enhanceio -m ro

```

Then wait until

```
$ grep nr_dirty /proc/enhanceio/enchanceio_test/stats

```

returns 0\. Now all the blocks have been written to your slow hdd and it's safe to delete the caching device:

```
# eio_cli delete -c my_first_enhanceio

```

### Getting information on caches

To get basic information on caches in use try

```
# eio_cli info

```

To get detailed information use

```
$ cat /proc/enhanceio/my_first_enhanceio/stats

```

**Tip:** After initiating EnhanceIO I felt that my system had become more sluggish, this seems to be due to building up the cache first. Use your system like you normally would and open up those applications you would want to start quickly, maybe give it another reboot and observe how things fly.

### Enable EnhanceIO on initcpio

After you verify that EnhanceIO works with your system, you might want to accelerate the boot process of your system. In order to do this, EnhanceIO should start as early as possible and before the rootfs gets mounted. This can be achieved by enabling EnhanceIO in initcpio.

**Warning:** EnhanceIO does not support the WriteBack `-m wb` strategy when accelerating rootfs, only ReadOnly `-m ro` or WriteThrough (the default). If you enable WriteBack on the root volume bad things WILL happen.

First, install the [pyinstaller](https://aur.archlinux.org/packages/pyinstaller/)<sup><small>AUR</small></sup> package from the [AUR](/index.php/AUR "AUR"); we need it to compile EnhanceIO's Python `eio_cli` script into an executable for inclusion in the initcpio image.

Create the file `/etc/initcpio/hooks/enhanceio`. This is the EnhanceIO hook that performs cache initialization on boot:

```
#!/usr/bin/bash

run_hook ()
{
    local mod
    for mod in enhanceio enhanceio_lru enhanceio_fifo; do
        modprobe "$mod"
    done

    msg -n ":: Activating EnhanceIO..."
    udevadm trigger
}

```

Create the file `/etc/initcpio/install/enhanceio`. This file compiles `eio_cli` as an executable and includes everything needed to load EnhanceIO from initcpio:

```
#!/bin/bash

build ()
{
    local mod
    for mod in enhanceio enhanceio_lru enhanceio_rand enhanceio_fifo; do
        add_module "$mod"
    done

    add_binary "/usr/lib/libutil.so.1"
    add_file "/etc/udev/rules.d/94-enhanceio-my_first_enhanceio.rules"

    sudo -u ${SUDO_USER} pyinstaller --distpath=/tmp/eio_cli/dist --workpath=/tmp/eio_cli --specpath=/tmp/eio_cli --clean --onefile --noconfirm --strip --console /usr/bin/eio_cli
    add_binary "/tmp/eio_cli/dist/eio_cli" "/usr/bin/eio_cli"

    add_runscript
}

help ()
{
    echo "This hook loads the necessary modules for EnhanceIO when caching your root device."
}

```

Edit `/etc/mkinitcpio.conf` and add the `enhanceio` hook inside the HOOKS variable after **udev**, **block** and **modconf** entries:

```
HOOKS="base udev block modconf enhanceio ..."

```

Fix permissions on eio_cli:

```
chmod uga+xr /usr/bin/eio_cli

```

Finally, re-create the initcpio:

```
mkinitcpio -p linux

```

Reboot and watch your system fly.

Retrieved from "[https://wiki.archlinux.org/index.php?title=EnhanceIO&oldid=407251](https://wiki.archlinux.org/index.php?title=EnhanceIO&oldid=407251)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [File systems](/index.php/Category:File_systems "Category:File systems")