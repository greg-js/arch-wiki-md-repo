See [Kernels](/index.php/Kernels "Kernels") for the main article.

The [Arch Build System](/index.php/Arch_Build_System "Arch Build System") can be used to build a custom kernel based on the official [linux](https://www.archlinux.org/packages/?name=linux) package. This compilation method can automate the entire process, and is based on a very well tested package. You can edit the PKGBUILD to use a custom kernel configuration or add additional patches.

## Contents

*   [1 Getting the Ingredients](#Getting_the_Ingredients)
*   [2 Modifying the PKGBUILD](#Modifying_the_PKGBUILD)
    *   [2.1 Changing prepare()](#Changing_prepare())
    *   [2.2 Generate new checksums](#Generate_new_checksums)
*   [3 Compiling](#Compiling)
*   [4 Installing](#Installing)
*   [5 Boot Loader](#Boot_Loader)
*   [6 See Also](#See_Also)

## Getting the Ingredients

Since you'll be using [makepkg](/index.php/Makepkg "Makepkg"), follow the best practices outlined there first. For example, you cannot run makepkg as root/sudo. Therefore, create a `build` directory in your user home first.

```
 $ cd ~/
 $ mkdir build
 $ cd build/

```

[Install](/index.php/Install "Install") the [asp](https://www.archlinux.org/packages/?name=asp) package and the [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) package group.

You need a clean kernel to start your customization from. Fetch the latest kernel package files from ABS into your build directory by running:

```
$ asp update linux
$ asp checkout linux

```

Then, get any other file you need (e.g. custom configuration files, patches, etc.) from the respective sources.

## Modifying the PKGBUILD

Edit `PKGBUILD` and look for the `pkgbase` parameter. Change this to your custom package name, e.g.:

```
 pkgbase=linux-custom

```

Depending on the PKGBUILD you may have to also rename `linux.install` to match the modified `pkgbase`.

### Changing prepare()

In prepare function, you can apply needed kernel patch or change kernel build configuration.

If you need to change a few config options you can edit config file in the source.

Or you can use GUI tool to tweak the options. Comment `make olddefconfig` in the prepare() function of the PKGBUILD, and add your favorite tool:

 `PKGBUILD` 
```
...
  msg2 "Setting config..."
  cp ../config .config
  #make olddefconfig

  make nconfig # new CLI menu for configuration
  #make menuconfig # CLI menu for configuration
  #make xconfig # X-based configuration
  #make oldconfig # using old config from previous kernel version
  # ... or manually edit .config
...

```

**Warning:** systemd has a number of kernel configuration requirements for general use, for specific usecases (e.g., UEFI) and for specific systemd functionality (e.g., bootchart). Failure to meet these requirements can result in your system being degraded or unusable. The list of required and recommended kernel CONFIGs can be found in `/usr/share/doc/systemd/README`. Check them before you compile.These requirements also change over time. Because Arch assumes you are using the official kernel, there will be no announcement of these changes. Before you install a new version of systemd, check the version release notes to make sure your current custom kernel meets any new systemd requirements.

### Generate new checksums

[Install](/index.php/Install "Install") the [pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib) package.

As we modified config, we need to generate new checksums by running:

```
$ updpkgsums

```

## Compiling

You can now proceed to compile your kernel by the usual command `makepkg`

If you have chosen an interactive program for configuring the kernel parameters (like menuconfig), you need to be there during the compilation.

```
 $ makepkg -s

```

The `-s` parameter will download any additional dependencies used by recent kernels such as xml and docs.

**Note:**

*   Kernel sources are [PGP signed](https://www.kernel.org/signature.html#kernel-org-web-of-trust), and makepkg will attempt to verify them. See [Makepkg#Signature checking](/index.php/Makepkg#Signature_checking "Makepkg") for details.
*   [Running compilation jobs simultaneously](/index.php/Makepkg#Parallel_compilation "Makepkg") can reduce compilation time significantly on multi-core systems.

## Installing

After running *makepkg*, you can have a look at the `linux.install` file. You will see that some variables have changed.

Now, you only have to install the package as usual. Best practice is to install kernel headers first as they will be needed (e.g. to install the [nvidia](/index.php/NVIDIA#Custom_kernel "NVIDIA") driver) for the custom kernel later.

```
# pacman -U *kernel-headers_package*
# pacman -U *kernel_package*

```

## Boot Loader

Now, the folders and files for your custom kernel have been created, e.g. `/boot/vmlinuz-linux-test`. To test your kernel, update your [bootloader](/index.php/Bootloader "Bootloader") configuration file and add new entries ('default' and 'fallback') for your custom kernel. If you renamed your kernel in the *PKGBUILD pkgbase* you may have to rename the initramfs.img in your *$build/pkg/kernel/etc* before installing with pacman. That way, you can have both the stock kernel and the custom one to choose from.

## See Also

*   [https://kernel.org/doc/Documentation/kbuild/kconfig.txt](https://kernel.org/doc/Documentation/kbuild/kconfig.txt) and the parent directory