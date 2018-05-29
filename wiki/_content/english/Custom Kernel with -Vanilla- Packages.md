See [Kernels](/index.php/Kernels "Kernels") for the main article.

Based on the german article "Eigenen Kernel erstellen"

In this article I want to show you how to create your custom kernel with the packages from [https://www.kernel.org](https://www.kernel.org) (the "vanilla" kernel). This means that you don't be able to install or uninstall this kernel with pacman and you don't have the adjustments from the Arch Linux team. The kernel is thought too be installed parallel to the arch linux kernel.

If you wan't to use the packages from the Arch Linux Repositories and manipulate the "linux" package with ABS (Arch Build System), see this article: [Kernels/Arch Build System](/index.php/Kernels/Arch_Build_System "Kernels/Arch Build System")

In general this article is not for beginners because you must know some basics to understand the processes and the effects.

## Contents

*   [1 Remarks before beginning](#Remarks_before_beginning)
*   [2 Preparing the workspace and the materials](#Preparing_the_workspace_and_the_materials)
*   [3 Compiling the kernel](#Compiling_the_kernel)
*   [4 Installing the kernel](#Installing_the_kernel)
*   [5 Cleaning the workspace](#Cleaning_the_workspace)

## Remarks before beginning

**Suitability**

*   advantages
    *   You can quickly get your own kernel
    *   Extremely well adaptable to your own hardware
*   disadvantages
    *   Configuration requires some experience with the linux kernel
    *   Subsequently no longer changeable

## Preparing the workspace and the materials

**Get the Source Code Package**

You will find the sources on [https://www.kernel.org/](https://www.kernel.org/).
In this example I show you the way to do with version 4.16.12.

In my case the exact link is [https://cdn.kernel.org/pub/linux/kernel/v4.x/linux-4.16.12.tar.xz](https://cdn.kernel.org/pub/linux/kernel/v4.x/linux-4.16.12.tar.xz). In the forerun I will speak of linux 4.16.12 but you must use your version of the package which you have loaded from [https://www.kernel.org](https://www.kernel.org).

**Unpacking**

Run this commands as root user

```
cp $downloaddir/linux-4.16.12.tar.xz /usr/src/
cd /usr/src
tar xf linux-4.16.12.tar.xz
cd /usr/src/linux-4.16.12

```

**Configuring the kernel**

We will take the configuration of the kernel included in Arch Linux as our basis.
In my case it is linux 4.16.12\. Catch: This config is also based on the patches installed or added to the kernel included in Arch Linux. The reuse of this config can go well, but does not have to. This commands have be run as root like before.

```
zcat /proc/config.gz > /usr/src/linux-4.16.12/.config
make oldconfig

```

The first command reads out the configuration from the kernel which is currently running. Open .config with an editor like gedit, nano or pluma. Then change this line:

```
CONFIG_LOCALVERSION="-ARCH"

```

To this line:

```
CONFIG_LOCALVERSION=""

```

## Compiling the kernel

**Compiling**

The modules and the kernel were compiled with this command:

```
 make

```

This process takes normally about twenty minutes.

## Installing the kernel

**Installing**

The directories apply to both systems: x86 and x86_64.

You need to run the commands as root. Copying the kernel image to /boot/:

```
 cp arch/x86/boot/bzImage /boot/vmlinuz-4.16.12
 cp System.map /boot/
 cp .config /boot/kconfig

```

**Installing the modules**

Run this command as root:

```
make modules_install

```

**Preparing the linux headers**

Because the linux headers can't be used after cleaning the workpspace, you must run this commands as root and copy the files from "build" and "source" into the modules directory:

```
cd /usr/lib/modules/4.16.12/
mv build build.bak
mv source source.bak
mkdir build source
cp -r build.bak/* build/
cp -r source.bak/* source/
rm build.bak
rm source.bak

```

**Installing DKMS Modules**

If you don't use DKMS, you can skip this step and go on with generating the initramfs.
Run the following commands as root:

```
dkms add MODULENAME/MODULEVERSION --all
dkms build MODULENAME/MODULEVERSION -k 4.16.12
dkms install MODULENAME/MODULEVERSION -k 4.16.12

```

Naturally you must change MODULENAME and MODULEVERSION with the data of your module / modules.

**Generating the initramfs and update GRUB**

Warning: A initramfs (earlier initrd) must be created because many features of our kernel are loaded as modules. Run the following commands as root to generate the initramfs and update GRUB:

```
mkinitcpio -k 4.16.12 -g /boot/initramfs-4.16.12.img
grub-mkconfig -o /boot/grub/grub.cfg

```

## Cleaning the workspace

**Cleaning**

You need to run this command in your source directory:

```
make clean

```