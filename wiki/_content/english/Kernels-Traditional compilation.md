This article is an introduction to building custom kernels from **kernel.org sources**. This method of compiling kernels is the traditional method common to all distributions. It can be, depending on your background, more complicated than using the [Kernels/Arch Build System](/index.php/Kernels/Arch_Build_System "Kernels/Arch Build System"). Consider the [Arch Build System](/index.php/Arch_Build_System "Arch Build System") tools are developed and maintained to make repeatable compilation tasks efficient and safe.

## Contents

*   [1 Preparation](#Preparation)
    *   [1.1 Install the core packages](#Install_the_core_packages)
    *   [1.2 Create a kernel compilation directory](#Create_a_kernel_compilation_directory)
    *   [1.3 Download the kernel source](#Download_the_kernel_source)
    *   [1.4 Unpack the kernel source](#Unpack_the_kernel_source)
*   [2 Configuration](#Configuration)
    *   [2.1 Kernel configuration](#Kernel_configuration)
        *   [2.1.1 A. Default Arch configuration](#A._Default_Arch_configuration)
        *   [2.1.2 B. Generated configuration](#B._Generated_configuration)
    *   [2.2 Advanced configuration](#Advanced_configuration)
*   [3 Compilation and installation](#Compilation_and_installation)
    *   [3.1 Compile the kernel](#Compile_the_kernel)
    *   [3.2 Compile the modules](#Compile_the_modules)
    *   [3.3 Copy the kernel to /boot directory](#Copy_the_kernel_to_.2Fboot_directory)
    *   [3.4 Make initial RAM disk](#Make_initial_RAM_disk)
        *   [3.4.1 Automated preset method](#Automated_preset_method)
        *   [3.4.2 Manual method](#Manual_method)
    *   [3.5 Copy System.map](#Copy_System.map)
*   [4 Bootloader configuration](#Bootloader_configuration)

## Preparation

It is not necessary (or recommended) to use the root account or root privileges (i.e. via [Sudo](/index.php/Sudo "Sudo")) for kernel preparation.

### Install the core packages

Install the [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) package group, which contains necessary packages such as [make](https://www.archlinux.org/packages/?name=make) and [gcc](https://www.archlinux.org/packages/?name=gcc). It is also recommended to install the following packages, as listed in the default Arch kernel [PKGBUILD](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/PKGBUILD?h=packages/linux): [xmlto](https://www.archlinux.org/packages/?name=xmlto), [docbook-xsl](https://www.archlinux.org/packages/?name=docbook-xsl), [kmod](https://www.archlinux.org/packages/?name=kmod), [inetutils](https://www.archlinux.org/packages/?name=inetutils), [bc](https://www.archlinux.org/packages/?name=bc)

### Create a kernel compilation directory

It is recommended to create a separate build directory for your kernel(s). In this example, the directory `kernelbuild` will be created in the `home` directory:

```
$ mkdir ~/kernelbuild

```

### Download the kernel source

**Warning:** [systemd](/index.php/Systemd "Systemd") requires kernel version 3.11 and above (4.2 and above for unified [cgroups](/index.php/Cgroups "Cgroups") hierarchy support). See `/usr/share/systemd/README` for more information.

Download the kernel source from [http://www.kernel.org](http://www.kernel.org). This should be the [tarball](https://en.wikipedia.org/wiki/Tar_(computing) (`tar.xz`) file for your chosen kernel.

It can be downloaded by simply right-clicking the `tar.xz` link in your browser and selecting `Save Link As...`, or any other number of ways via alternative graphical or command-line tools that utilise HTTP, [FTP](/index.php/Ftp#FTP "Ftp"), [RSYNC](/index.php/Rsync "Rsync"), or [Git](/index.php/Git "Git").

**Note:** It is a good idea to verify the PGP signature of any downloaded kernel tarball. This ensures that it is legitimate and helps to build the Web of Trust. See [kernel.org/signature](http://kernel.org/signature.html#using-gnupg-to-verify-kernel-signatures).

In the following command-line example, [wget](https://www.archlinux.org/packages/?name=wget) has been installed and is used inside the `~/kernelbuild` directory to obtain kernel 4.8.6:

```
$ cd ~/kernelbuild
$ wget [https://www.kernel.org/pub/linux/kernel/v4.x/linux-4.8.6.tar.xz](https://www.kernel.org/pub/linux/kernel/v4.x/linux-4.8.6.tar.xz)

```

If `wget` was not used inside the build directory, it will be necessary to move the tarball into it, e.g.

```
$ mv /path/to/linux-4.8.6.tar.xz ~/kernelbuild/

```

### Unpack the kernel source

Within the build directory, unpack the kernel tarball:

```
$ tar -xvJf linux-4.8.6.tar.xz

```

To finalise the preparation, ensure that the kernel tree is absolutely clean; do not rely on the source tree being clean after unpacking. To do so, first change into the new kernel source directory created, and then run the `make mrproper` command:

```
$ cd linux-4.8.6/
$ make clean && make mrproper

```

## Configuration

This is the most crucial step in customizing the default kernel to reflect your computer's precise specifications. Kernel configuration is set in its `.config` file, which includes the use of [Kernel modules](/index.php/Kernel_modules "Kernel modules").

**Note:** It is not necessary to use the root account or root privileges at this stage.

By setting the options in `.config` properly, your kernel and computer will function most efficiently.

### Kernel configuration

You can choose from two options to set your kernel configuration:

*   A. Use the default Arch settings from an official kernel (recommended)
*   B. Generate a configuration file which matches the currently running kernel's configuration. (useful if you want to customize your kernel settings further)

**Note:** Especially if you choose option **B**, you will be prompted to manually configure your kernel with tools described in `Advanced Configuration`.

#### A. Default Arch configuration

This method will create a `.config` file for the custom kernel using the default Arch kernel settings. Ensure that a stock Arch kernel is running and use the following command inside the custom kernel source directory:

```
$ zcat /proc/config.gz > .config

```

**Warning:** If you are compiling a kernel using your current `.config` file, do not forget to rename your kernel version "CONFIG_LOCALVERSION" in the new .config or in the `General Setup --->` option using one of the user interfaces listed under Advanced Configuration. If you skip this, there is the risk of overwriting one of your existing kernels by mistake.

#### B. Generated configuration

**Tip:** Plug in all devices that you expect to use on the system if using this method.

Since kernel 2.6.32, the `localmodconfig` command will create a `.config` file for the custom kernel by disabling any and all options not currently in use by the running kernel *at the time*. In other words, it will only enable the options currently being used.

While this minimalist approach will result in a highly streamlined and efficient configuration tailored specifically for your system, there are drawbacks, such as the potential inability of the kernel to support newer hardware, peripherals, or other features.

**Note:** Again, ensure that all devices you expect to use have been connected to (and detected by) your system before running the following command

```
$ make localmodconfig

```

### Advanced configuration

**Tip:** Unless you want to see a lot of extra messages when booting and shutting down with the custom kernel, it is a good idea to deactivate the relevant debugging options.

There are several tools available to fine-tune the kernel configuration, which provide an alternative to otherwise spending hours manually configuring each and every one of the options available during compilation.

**Note:** Those tools listed below will provide you with three configuration options for each kernel feature: `y` for enabled, `n` for disabled, and `m` for enabled as kernel module (loaded when necessary).

Those tools are:

*   `make menuconfig`: Command-line ncurses interface superseded by `nconfig`
*   `make nconfig`: Newer ncurses interface for the command-line
*   `make xconfig`: User-friendly graphical interface that requires [packagekit-qt4](https://www.archlinux.org/packages/?name=packagekit-qt4) to be installed as a dependency. This is the recommended method - especially for less experienced users - as it is easier to navigate, and information about each option is also displayed.
*   `make gconfig`: Graphical configuration similar to xconfig but using gtk.

The chosen method should be run inside the kernel source directory, and all will either create a new `.config` file, or overwrite an existing one where present. All optional configurations will be automatically enabled, although any newer configuration options (i.e. with an older kernel `.config`) may not be automatically selected.

Once the changes have been made save the `.config` file. It is a good idea to make a backup copy outside the source directory. You may need to do this multiple times before you get all the options right.

If unsure, only change a few options between compilations. If you cannot boot your newly built kernel, see the list of necessary config items [here](https://www.archlinux.org/news/users-of-unofficial-kernels-must-enable-devtmpfs-support/).

Running `$ lspci -k #` from liveCD lists names of kernel modules in use. Most importantly, you must maintain CGROUPS support. This is necessary for [systemd](/index.php/Systemd "Systemd").

## Compilation and installation

**Tip:** If you want to have [gcc](https://www.archlinux.org/packages/?name=gcc) optimize for your processor's instruction sets, edit `arch/x86/Makefile` (i686) or `arch/x86_64/Makefile` (86_64) within the kernel source directory:

*   Look for `CONFIG_MK8,CONFIG_MPSC,CONFIG_MCORE2,CONFIG_MATOM,CONFIG_GENERIC_CPU` that you have chosen in `Processor type and features > Processor Family`
*   Change the call cc-options flag to `-march=native` to the one that you have selected in Processor Family, e.g. `cflags-$(CONFIG_MK8) += $(call cc-option,-march=native)`. This is probably the best way to compile with `-march=native` as it works.

*   Note: For 32bit Kernels, you need to edit `arch/x86/Makefile_32.cpu` instead and set `-march=native` for your processor.

### Compile the kernel

Compilation time will vary from as little as fifteen minutes to over an hour, depending on your kernel configuration and processor capability. See [Makeflags](/index.php/Makepkg#MAKEFLAGS "Makepkg") for details. Once the `.config` file has been set for the custom kernel, within the source directory run the following command to compile:

```
$ make

```

### Compile the modules

**Warning:** From this step onwards, commands must be either run as root or with root privileges. If not, they will fail.

Once the kernel has been compiled, the modules for it must follow. As root or with root privileges, run the following command to do so:

```
# make modules_install

```

This will copy the compiled modules into `/lib/modules/<kernel version>-<config local version>`. For example, for kernel version 4.8 installed above, they would be copied to `/lib/modules/4.8.6-ARCH`. This keeps the modules for individual kernels used separated.

**Tip:** If your system requires modules which are not distributed with the regular Linux kernel, you need to compile them for your custom kernel when it is finished. Such modules are typically those which you explicitly installed separately for your running system. See [NVIDIA#Custom kernel](/index.php/NVIDIA#Custom_kernel "NVIDIA") for an example.

### Copy the kernel to /boot directory

**Note:** Ensure that the `bzImage` kernel file has been copied from the appropriate directory for your system architecture. See below.

The kernel compilation process will generate a compressed `bzImage` (big zImage) of that kernel, which must be copied to the `/boot` directory and renamed in the process. Provided the name is prefixed with `vmlinuz-`, you may name the kernel as you wish. In the examples below, the installed and compiled 4.8 kernel has been copied over and renamed to `vmlinuz-linux48`:

*   32-bit (i686) kernel:

```
# cp -v arch/x86/boot/bzImage /boot/vmlinuz-linux48

```

*   64-bit (x86_64) kernel:

```
# cp -v arch/x86_64/boot/bzImage /boot/vmlinuz-linux48

```

### Make initial RAM disk

**Note:** You are free to name the initramfs image file whatever you wish when generating it. However, it is recommended to use the `linux<major revision><minor revision>` convention. For example, the name 'linux48' was given as '4' is the major revision and '8' is the minor revision of the 4.8 kernel. This convention will make it easier to maintain multiple kernels, regularly use mkinitcpio, and build third-party modules.

**Tip:** If you are using the LILO bootloader and it cannot communicate with the kernel device-mapper driver, you have to run `modprobe dm-mod` first.

If you do not know what making an initial RAM disk is, see [Initramfs on Wikipedia](https://en.wikipedia.org/wiki/Initrd "wikipedia:Initrd") and [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio").

#### Automated preset method

An existing [mkinitcpio preset](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") can be copied and modified so that the custom kernel initramfs images can be generated in the same way as for an official kernel. This is useful where intending to recompile the kernel (e.g. where updated). In the example below, the preset file for the stock Arch kernel will be copied and modified for kernel 4.8, installed above.

First, copy the existing preset file, renaming it to match the name of the custom kernel specified as a suffix to `/boot/vmlinuz-` when copying the `bzImage` (in this case, `linux48`):

```
# cp /etc/mkinitcpio.d/linux.preset /etc/mkinitcpio.d/linux48.preset

```

Second, edit the file and amend for the custom kernel. Note (again) that the `ALL_kver=` parameter also matches the name of the custom kernel specified when copying the `bzImage`:

 `/etc/mkinitcpio.d/linux48.preset` 
```
...
ALL_kver="/boot/vmlinuz-linux48"
...
default_image="/boot/initramfs-linux48.img"
...
fallback_image="/boot/initramfs-linux48-fallback.img"
```

Finally, generate the initramfs images for the custom kernel in the same way as for an official kernel:

```
# mkinitcpio -p linux48

```

#### Manual method

Rather than use a preset file, mkinitcpio can also be used to generate an initramfs file manually. The syntax of the command is:

```
# mkinitcpio -k <kernelversion> -g /boot/initramfs-<file name>.img

```

*   `-k` (--kernel <kernelversion>): Specifies the modules to use when generating the initramfs image. The `<kernelversion>` name will be the same as the name of the custom kernel source directory (and the modules directory for it, located in `/usr/lib/modules/`).
*   `-g` (--generate <filename>): Specifies the name of the initramfs file to generate in the `/boot` directory. Again, using the naming convention mentioned above is recommended.

For example, the command for the 4.8 custom kernel installed above would be:

```
# mkinitcpio -k linux-4.8.6 -g /boot/initramfs-linux48.img

```

### Copy System.map

The `System.map` file is not required for booting Linux. It is a type of "phone directory" list of functions in a particular build of a kernel. The `System.map` contains a list of kernel symbols (i.e function names, variable names etc) and their corresponding addresses. This "symbol-name to address mapping" is used by:

*   Some processes like klogd, ksymoops etc
*   By OOPS handler when information has to be dumped to the screen during a kernel crash (i.e info like in which function it has crashed).

**Tip:** UEFI partitions are formatted using FAT32, which does not support symlinks.

If your `/boot` is on a filesystem which supports symlinks (i.e., not FAT32), copy `System.map` to `/boot`, appending your kernel's name to the destination file. Then create a symlink from `/boot/System.map` to point to `/boot/System.map-YourKernelName`:

```
# cp System.map /boot/System.map-YourKernelName
# ln -sf /boot/System.map-YourKernelName /boot/System.map

```

After completing all steps above, you should have the following 3 files and 1 soft symlink in your `/boot` directory along with any other previously existing files:

*   Kernel: `vmlinuz-YourKernelName`
*   Initramfs: `Initramfs-YourKernelName.img`
*   System Map: `System.map-YourKernelName`
*   System Map kernel symlink

## Bootloader configuration

Add an entry for your new kernel in your bootloader's configuration file - see [GRUB](/index.php/GRUB "GRUB"), [LILO](/index.php/LILO "LILO"), [GRUB2](/index.php/GRUB2 "GRUB2"), [Syslinux](/index.php/Syslinux "Syslinux"), [systemd-boot](/index.php/Systemd-boot "Systemd-boot") or [REFInd](/index.php/REFInd "REFInd") for examples.

**Tip:** Kernel sources include a script to automate the process for LILO: `$ arch/x86/boot/install.sh`. Remember to type `lilo` as root at the prompt to update it.