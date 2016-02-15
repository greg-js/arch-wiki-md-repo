See [Kernels](/index.php/Kernels "Kernels") for the main article.

The [Arch Build System](/index.php/Arch_Build_System "Arch Build System") can be used to build a custom kernel based on the official [linux](https://www.archlinux.org/packages/?name=linux) package. This compilation method can automate the entire process, and is based on a very well tested package. You can edit the PKGBUILD to use a custom kernel configuration or add additional patches.

## Contents

*   [1 Getting the Ingredients](#Getting_the_Ingredients)
*   [2 Modifying the PKGBUILD](#Modifying_the_PKGBUILD)
    *   [2.1 Changing build()](#Changing_build.28.29)
    *   [2.2 Generate new checksums](#Generate_new_checksums)
*   [3 Compiling](#Compiling)
*   [4 Installing](#Installing)
*   [5 Boot Loader](#Boot_Loader)

## Getting the Ingredients

Since you'll be using [makepkg](/index.php/Makepkg "Makepkg"), follow the best practices outlined there first. For example, you cannot run makepkg as root/sudo. Therefore, create a `build` directory in your user home first.

```
 $ cd ~/
 $ mkdir build
 $ cd build/

```

[Install](/index.php/Install "Install") the [abs](https://www.archlinux.org/packages/?name=abs) package and the [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) package group from the [official repositories](/index.php/Official_repositories "Official repositories").

You need a clean kernel to start your customization from. Fetch the kernel package files from ABS into your build directory by running:

 `$ ABSROOT=. abs core/linux` 

If you have some problem with the firewall blocking the rsync port, you can try with -t, which uses the tarball to sync.

 `$ ABSROOT=. abs core/linux -t` 

Then, get any other file you need (e.g. custom configuration files, patches, etc.) from the respective sources.

## Modifying the PKGBUILD

Edit `PKGBUILD` and look for the `pkgbase` parameter. Change this to your custom package name, e.g.:

```
 pkgbase=linux-custom

```

**Note:** Depending on the PKGBUILD you may have to also rename `linux.install` to match the modified `pkgbase` (e.g. for [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec)).

### Changing build()

If you need to change a few config options you can use the default one and append your options to the config file:

```
$ echo '
CONFIG_DEBUG_INFO=y
CONFIG_FOO=n
' >> config.x86_64

```

Or you can use GUI tool to tweak the options. Uncomment one of the possibilities shown in the prepare() function of the PKGBUILD, e.g.:

 `PKGBUILD` 

```
...
  # load configuration
  # Configure the kernel. Replace the line below with one of your choice.
  #make menuconfig # CLI menu for configuration
  make nconfig # new CLI menu for configuration
  #make xconfig # X-based configuration
  #make oldconfig # using old config from previous kernel version
  # ... or manually edit .config
...

```

If you have already a kernel `.config` file, uncommenting one of the interactive config tools, such as `nconfig`, and loading your `.config` from there avoids any problems with kernel naming that may otherwise occur - except in the case of at least make menuconfig. See note.

**Note:**

*   If you uncomment and use 'make menuconfig' in build(), then use the menuconfig gui to load your existing config, you will run into problems with conflicting files in the end package. This is because you will overwrite the default config that PKGBUILD has modified to provide a unique install path, specifically the LOCALVERSION and LOCALVERSION_AUTO config options. To fix this, simply re-set LOCALVERSION to your custom kernel naming and LOCALVERSION_AUTO=n while still in menuconfig. For details, see [BBS#173504](https://bbs.archlinux.org/viewtopic.php?id=173504)
*   If you uncomment _return 1_, you can change to the kernel source directory after makepkg finishes extraction and then make nconfig. This lets you configure the kernel over multiple sessions. When you're ready to compile, copy the .config file over top of either config or config.x86_64 (depending on your architecture), comment _return 1_ and use **makepkg -i**. But do not use this for custom patches; put your patch commands after these lines. If you do patch manually bztar unpack and replace your patch.

**Warning:** systemd has a number of kernel configuration requirements for general use, for specific usecases (e.g., UEFI) and for specific systemd functionality (e.g., bootchart). Failure to meet these requirements can result in your system being degraded or unusable. The list of required and recommended kernel CONFIGs can be found in `/usr/share/doc/systemd/README`. Check them before you compile.These requirements also change over time. Because Arch assumes you are using the official kernel, there will be no announcement of these changes. Before you install a new version of systemd, check the version release notes to make sure your current custom kernel meets any new systemd requirements.

### Generate new checksums

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
*   [Running compilation jobs simultaneously](/index.php/Makepkg#MAKEFLAGS "Makepkg") can reduce compilation time significantly on multi-core systems.

## Installing

After the makepkg, you can have a look at the linux.install file. You will see that some variables have changed. Now, you only have to install the package as usual with pacman (or equivalent program):

```
# pacman -U <kernel-headers_package>
# pacman -U <kernel_package>

```

**Note:** Best practice is to install kernel headers first as they will be needed if you want your nvidia driver included with the [nvidia-hook](/index.php/NVIDIA#Alternate_install:_custom_kernel "NVIDIA")

## Boot Loader

Now, the folders and files for your custom kernel have been created, e.g. `/boot/vmlinuz-linux-test`. To test your kernel, update your bootloader (grub-mkconfig for GRUB) and add new entries ('default' and 'fallback') for your custom kernel. If you renamed your kernel in the _PKGBUILD pkgbase_ you may have to rename the initramfs.img in your _$build/pkg/kernel/etc_ before installing with pacman. That way, you can have both the stock kernel and the custom one to choose from.