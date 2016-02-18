This article is an introduction to building custom kernels from **kernel.org sources**. This method of compiling kernels is the traditional method common to all distributions. If this seems too complicated, see some alternatives at: [Kernels#Compilation](/index.php/Kernels#Compilation "Kernels")

## Contents

*   [1 Dependencies installation](#Dependencies_installation)
*   [2 Fetching source](#Fetching_source)
*   [3 Build configuration](#Build_configuration)
    *   [3.1 Configure your kernel](#Configure_your_kernel)
        *   [3.1.1 First-timers](#First-timers)
        *   [3.1.2 Traditional menuconfig](#Traditional_menuconfig)
        *   [3.1.3 Versioning](#Versioning)
*   [4 Compilation and installation](#Compilation_and_installation)
    *   [4.1 Compile](#Compile)
    *   [4.2 Install modules](#Install_modules)
    *   [4.3 Copy the kernel to /boot directory](#Copy_the_kernel_to_.2Fboot_directory)
    *   [4.4 Make initial RAM disk](#Make_initial_RAM_disk)
    *   [4.5 Copy System.map](#Copy_System.map)
*   [5 Bootloader configuration](#Bootloader_configuration)
*   [6 Using the NVIDIA video driver with your custom kernel](#Using_the_NVIDIA_video_driver_with_your_custom_kernel)

## Dependencies installation

You need to have the following packages [installed](/index.php/Installed "Installed") (as listed in the [linux](https://www.archlinux.org/packages/?name=linux) [PKGBUILD](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/PKGBUILD?h=packages/linux)) before compiling a recent kernel version:

[xmlto](https://www.archlinux.org/packages/?name=xmlto), [docbook-xsl](https://www.archlinux.org/packages/?name=docbook-xsl), [kmod](https://www.archlinux.org/packages/?name=kmod), [inetutils](https://www.archlinux.org/packages/?name=inetutils), [bc](https://www.archlinux.org/packages/?name=bc)

## Fetching source

*   Fetch the kernel source from [http://www.kernel.org](http://www.kernel.org). This can be done with GUI or text-based tools that utilize: HTTP, [FTP](/index.php/Ftp#FTP "Ftp"), [RSYNC](/index.php/Rsync "Rsync"), or [Git](/index.php/Git "Git").

For instance, using wget via http:

```
$ wget -c [https://kernel.org/pub/linux/kernel/v4.x/linux-4.0.6.tar.xz](https://kernel.org/pub/linux/kernel/v4.x/linux-4.0.6.tar.xz)

```

*   It is always a good idea to verify the signature for any downloaded tarball. See [kernel.org/signature](http://kernel.org/signature.html#using-gnupg-to-verify-kernel-signatures) for how this works and other details.

*   Copy the kernel source to your build directory, e.g.:

```
$ cp linux-4.0.6.tar.xz ~/kernelbuild/

```

*   Unpack it and enter the source directory:

```
$ cd ~/kernelbuild
$ tar -xvJf linux-4.0.6.tar.xz
$ cd linux-4.0.6

```

Prepare for compilation by running the following command:

```
$ make mrproper

```

This ensures that the kernel tree is absolutely clean. The kernel team recommends that this command be issued prior to each kernel compilation. Do not rely on the source tree being clean after un-tarring.

## Build configuration

This is the most crucial step in customizing the kernel to reflect your computer's precise specifications. By setting the options in `.config` properly, your kernel and computer will function most efficiently.

### Configure your kernel

**Warning:** If compiling the *radeon* driver into the kernel(>3.3.3) for early KMS with a newer video card, you **must** include the firmware files for your card. Otherwise acceleration will be crippled. See [here](http://wiki.x.org/wiki/radeonBuildHowTo#Missing_Extra_Firmware)

**Warning:** systemd has a number of kernel configuration requirements for general use, for specific usecases (e.g., UEFI) and for specific systemd functionality (e.g., bootchart). Failure to meet these requirements can result in your system being degraded or unusable. The list of required and recommended kernel CONFIGs can be found in `/usr/share/doc/systemd/README`. Check them before you compile.These requirements also change over time. Because Arch assumes you are using the official kernel, there will be no announcement of these changes. Before you install a new version of systemd, check the version release notes to make sure your current custom kernel meets any new systemd requirements.

**Tip:** It is possible, to configure a kernel that does not require initramfs on ***simple configurations***. Ensure that all your modules required for video/input/disks/fs are compiled into the kernel. As well as support for DEVTMPFS_MOUNT, TMPFS, AUTOFS4_FS at the very least. If in doubt, learn about these options and what they mean *before* attempting.

#### First-timers

Two options for beginners to ease use or save time:

*   Copy the `.config` file from the running kernel, if you want to start with the default Arch settings.

 `$ zcat /proc/config.gz > .config` 

*   Use `localmodconfig`. Since kernel 2.6.32, this only selects those options which are currently being used.
    1.  Boot into stock `-ARCH` kernel, and plug in all devices that you expect to use on the system.
    2.  `cd` into your source directory and run: `$ make localmodconfig`
    3.  The resulting configuration file will be written to `.config`. You can then compile and install as stated below.

#### Traditional menuconfig

An [ncurses](https://en.wikipedia.org/wiki/Ncurses "wikipedia:Ncurses") interface to configuring the kernel is available with

 `$ make menuconfig` 

Alternatively, you can use the more modern

 `$ make nconfig` 

This will start with a fresh `.config`, unless one already exists (e.g. copied over). Option dependencies are automatically selected. And new options (i.e. with an older kernel `.config`) may or may not be automatically selected.

Make your changes to the kernel and save your config file. It is a good idea to make a backup copy outside the source directory, since you could be doing this multiple times until you get all the options right. If unsure, only change a few options between compiles. If you cannot boot your newly built kernel, see the list of necessary config items [here](https://www.archlinux.org/news/users-of-unofficial-kernels-must-enable-devtmpfs-support/). Running `$ lspci -k #` from liveCD lists names of kernel modules in use. Most importantly, you must maintain CGROUPS support. This is necessary for [systemd](/index.php/Systemd "Systemd").

#### Versioning

If you are compiling a kernel using your current config file, do not forget to rename your kernel version, or you may replace your existing one by mistake.

```
$ make menuconfig
General setup  --->
 (-ARCH) Local version - append to kernel release '4.n.n-RCn'

```

## Compilation and installation

**Tip:** If you want to have gcc optimize for your cpus instruction sets, edit `arch/x86/Makefile` and look for any of these CONFIG_MK8,CONFIG_MPSC,CONFIG_MCORE2,CONFIG_MATOM,CONFIG_GENERIC_CPU that you have chosen in Processor type and features > Processor Family and change the call cc-options flag to -march=native to the one that you have selected in Processor Family. For an example `cflags-$(CONFIG_MK8) += $(call cc-option,-march=native)`. This is probably the best way to compile with -march=native as it works.

### Compile

Compilation time will vary from 15 minutes to over an hour. This is largely based on how many options/modules are selected, as well as processor capability. See [Makeflags](/index.php/Makepkg#MAKEFLAGS "Makepkg") for details.

Run `$ make` .

### Install modules

```
# make modules_install

```

This copies the compiled modules into `/lib/modules/[kernel version + CONFIG_LOCALVERSION]`. This way, modules can be kept separate from those used by other kernels on your machine.

### Copy the kernel to /boot directory

```
# cp -v arch/x86/boot/bzImage /boot/vmlinuz-YourKernelName

```

Don't forget to replace x86 by your architecture, if needed.

### Make initial RAM disk

If you do not know what this is, please see: [Initramfs on Wikipedia](https://en.wikipedia.org/wiki/Initrd "wikipedia:Initrd") and [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio").

```
# mkinitcpio -k FullKernelName -c /etc/mkinitcpio.conf -g /boot/initramfs-YourKernelName.img

```

You are free to name the `/boot` files anything you want. However, using the [kernel-major-minor-revision] naming scheme helps to keep order if you:

*   Keep multiple kernels
*   Use mkinitcpio often
*   Build third-party modules.

**Tip:** If rebuilding images often, it might be helpful to create a separate preset file resulting in the command being something like:`# mkinitcpio -p custom`. See [here](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio")

If you are using LILO and it cannot communicate with the kernel device-mapper driver, you have to run `modprobe dm-mod` first.

### Copy System.map

The `System.map` file is not required for booting Linux. It is a type of "phone directory" list of functions in a particular build of a kernel. The `System.map` contains a list of kernel symbols (i.e function names, variable names etc) and their corresponding addresses. This "symbol-name to address mapping" is used by:

*   Some processes like klogd, ksymoops etc
*   By OOPS handler when information has to be dumped to the screen during a kernel crash (i.e info like in which function it has crashed).

**Tip:** UEFI partitions are formatted using FAT32, which does not support symlinks.

If your /boot is on a filesystem which supports symlinks (i.e., not FAT32), copy System.map to /boot, appending your kernel's name to the destination file. Then create a symlink /boot/System.map to point to /boot/System.map-YourKernelName.

```
# cp System.map /boot/System.map-YourKernelName
# ln -sf /boot/System.map-YourKernelName /boot/System.map

```

After completing all steps above, you should have the following 3 files and 1 soft symlink in your `/boot` directory along with any other previously existing files:

*   Kernel: vmlinuz-YourKernelName
*   Initramfs-YourKernelName.img
*   System Map: System.map-YourKernelName
*   System Map symlink: System.map

## Bootloader configuration

Add an entry for your new kernel in your bootloader's configuration file - see [GRUB](/index.php/GRUB "GRUB"), [LILO](/index.php/LILO "LILO"), [GRUB2](/index.php/GRUB2 "GRUB2"), [Syslinux](/index.php/Syslinux "Syslinux"), [Gummiboot](/index.php/Gummiboot "Gummiboot") or [REFInd](/index.php/REFInd "REFInd") for examples.

**Tip:** Kernel sources include a script to automate the process for LILO: `$ arch/x86/boot/install.sh`. Remember to type `lilo` as root at the prompt to update it.

## Using the NVIDIA video driver with your custom kernel

To use the NVIDIA driver with your new custom kernel, see: [How to install nVIDIA driver with custom kernel](/index.php/NVIDIA#Alternate_install:_custom_kernel "NVIDIA"). You can also install nvidia drivers from AUR.