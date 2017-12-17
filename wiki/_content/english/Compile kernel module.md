Related articles

*   [Kernel](/index.php/Kernel "Kernel")
*   [Kernel modules](/index.php/Kernel_modules "Kernel modules")

Sometimes you may wish to compile Linux's [Kernel module](/index.php/Kernel_module "Kernel module") without recompiling the whole kernel.

**Note:** You can only replace existing module if it is compiled as module (M) and not builtin (y) into kernel.

## Contents

*   [1 Build environment](#Build_environment)
*   [2 Source configuration](#Source_configuration)
*   [3 Module compilation](#Module_compilation)
*   [4 Module installation](#Module_installation)
*   [5 See also](#See_also)

## Build environment

Firstly you will need to install build dependencies such as compiler([base-devel](https://www.archlinux.org/groups/x86_64/base-devel/)) and [linux-headers](https://www.archlinux.org/packages/?name=linux-headers).

Next you will need to get source code for exact kernel version you are running. You may try use newer kernel sources but most likely compiled module will not load.

Find kernel version with

```
$ uname -r

```

Then acquire the required source, see [Kernels/Traditional compilation#Download the kernel source](/index.php/Kernels/Traditional_compilation#Download_the_kernel_source "Kernels/Traditional compilation"). If you fetch latest source using [Git](/index.php/Git "Git") you will need to checkout needed version using tag (eg. v4.1).

## Source configuration

When you have source code, enter that directory and clean it with (note it will delete .config.old and rename .config to .config.old)

```
$ make mrproper

```

Then you need to copy your current existing kernel configuration to this build dir

```
$ cp /usr/lib/modules/$(uname -r)/build/.config ./
$ cp /usr/lib/modules/$(uname -r)/build/Module.symvers ./

```

Next ensure configuration is adjusted for kernel sources (if you are using kernel sources for exact current version then it should not ask anything, but for newer sources than current kernel you might be asked about new options).

Also if module you want to compile have some compilation options such as debug build you can also adjust them with any of make config/menuconfig/xconfig (see README)

```
$ make oldconfig

```

## Module compilation

In order to load our module cleanly, we must find the value of the EXTRAVERSION component of the current kernel version number so we can match the version number exactly in our kernel source. EXTRAVERSION is a variable set in the kernel top-level Makefile, but the Makefile in a vanilla kernel source will have EXTRAVERSION empty; it is set only as part of the Arch kernel build process. The value of the current kernel's EXTRAVERSION (usually `-1`) can be found in one of two ways:

1.  Look at the top of `/usr/lib/modules/$(uname -r)/build/Makefile`
2.  Run `uname -r` and look for the string between the third kernel version number and `-ARCH` (the Arch-specific setting for LOCALVERSION as set in the kernel .config file). For example, with a kernel version of `4.9.65-1-ARCH`, the EXTRAVERSION is `-1`.

Once the EXTRAVERSION value is known, we prepare the source for module compilation:

```
$ make EXTRAVERSION=<YOUR EXTRAVERSION HERE> modules_prepare

```

Example:

```
$ make EXTRAVERSION=-1 modules_prepare

```

Alternatively, if you are happy to load modules with modprobe using the `--force-vermagic` option to ignore mismatches in the kernel version number, you can simply run:

```
$ make modules_prepare

```

**Note:** While the Makefile at `/usr/lib/modules/$(uname -r)/build/Makefile` could be copied over the Makefile in the kernel source to avoid manually specifying the EXTRAVERSION on the command line, that could cause a different kernel version mismatch to occur. If the kernel source has been obtained through a version control tool such as git, simply copying over the Makefile would cause the working copy to be dirty, which the kernel build process would recognize, causing it to append `+` to the LOCALVERSION configuration setting. For example: `4.9.65-1-ARCH+`.

Finally, compile wanted module by specifying its directory. (You can find module location with modinfo or find)

```
$ make M=fs/btrfs

```

## Module installation

Now after successful compilation you just need to gzip and copy it over for your current kernel.

If you are replacing some existing module you will need to overwrite it (and remember that reinstalling [linux](https://www.archlinux.org/packages/?name=linux) will replace it with default module)

```
$ gzip fs/btrfs/btrfs.ko
# cp -f fs/btrfs/btrfs.ko.gz /usr/lib/modules/`uname -r`/kernel/fs/btrfs/

```

Or alternatively, you can place the updated module in the updates folder (create it if it doesn't already exist).

```
$ cp fs/btrfs/btrfs.ko.gz /usr/lib/modules/`uname -r`/updates

```

However if you are adding a new module you can just copy it to extramodules (note, this is just example as btrfs will not get loaded from here)

```
# cp fs/btrfs/btrfs.ko.gz /usr/lib/modules/`uname -r`/extramodules/

```

If you are compiling a module for early boot (e.g. updated module) which is copied to [Initramfs](/index.php/Initramfs "Initramfs") then you must remember to regenerate it with (otherwise your compiled module will not be loaded). Furthermore, if you are using the "updates" folder method, you may need to rebuild the module dependency tree with "depmod" before regenerating [Initramfs](/index.php/Initramfs "Initramfs")

```
# mkinitcpio -p linux

```

## See also

*   [Linux Kernel Newbies](https://kernelnewbies.org/)
*   [The Linux Kernel Module Programming Guide](http://www.tldp.org/LDP/lkmpg/2.6/html/)