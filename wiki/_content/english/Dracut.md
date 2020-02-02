Related articles

*   [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")

**Note:** Read the mailing list announcement for a possible [Mkinitcpio replacement with Dracut](https://lists.archlinux.org/pipermail/arch-dev-public/2019-May/029570.html).

[dracut](https://dracut.wiki.kernel.org/) creates an initial image used by the kernel for preloading the block device modules (such as IDE, SCSI or RAID) which are needed to access the root filesystem. Upon installing [linux](https://www.archlinux.org/packages/?name=linux), you can choose between [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") and dracut. dracut is used by Fedora, RHEL, Gentoo, and Debian, among others.

You can read the full project documentation for dracut [in the kernel documentation](https://mirrors.edge.kernel.org/pub/linux/utils/boot/dracut/dracut.html).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Kernel command line options](#Kernel_command_line_options)
*   [3 Usage](#Usage)
    *   [3.1 Additional flags](#Additional_flags)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 View information about generated image](#View_information_about_generated_image)
    *   [4.2 Change compression program](#Change_compression_program)
    *   [4.3 Generate a new initramfs on kernel upgrade](#Generate_a_new_initramfs_on_kernel_upgrade)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Spaces in kernel parameters](#Spaces_in_kernel_parameters)
*   [6 See also](#See_also)

## Installation

dracut can be [installed](/index.php/Install "Install") with the [dracut](https://www.archlinux.org/packages/?name=dracut) package.

**Tip:** If dracut works on your machine **after you test it**, you can remove [mkinitcpio](https://www.archlinux.org/packages/?name=mkinitcpio).

## Configuration

If you wish to always execute dracut with a certain set of flags, you can save a specified configuration in a `.conf` file in `/etc/dracut.conf.d/`. For example:

 `/etc/dracut.conf.d/myflags.conf` 
```
hostonly="yes"
compress="lz4"
add_drivers+=" i915 "
omit_dracutmodules+=" network iscsi "
```

You can see more configuration options with [dracut.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dracut.conf.5). Fuller descriptions of each option can be found with [dracut(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dracut.8).

### Kernel command line options

You can force dracut to use kernel command line parameters in the initramfs environment. Be aware that you should [use the UUID naming scheme](#Spaces_in_kernel_parameters) for specifying block devices.

It is not necessary to specify the root block device for dracut. From [dracut.cmdline(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dracut.cmdline.7):

```
The root device used by the kernel is specified in the boot configuration file on the kernel command line, as always.

```

However, it may be useful to set some parameters early, and you can enable additional features like prompting for additional command like parameters. See [dracut.cmdline(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dracut.cmdline.7) for all options. Here are some example configuration options:

Resume from a swap partition: `resume=UUID=80895b78-7312-45bc-afe5-58eb4b579422`

Prompt for additional kernel command line parameters: `rd.cmdline=ask`

Print informational output even if "quiet" is set: `rd.info`

Kernel command line options should be placed line-by-line similar to the `/etc/dracut.conf.d/` style, in a `*.conf` file in `/etc/cmdline.d/`. For example, your kernel command line options file could look like:

 `/etc/cmdline.d/myflags.conf` 
```
resume=UUID=80895b78-7312-45bc-afe5-58eb4b579422
rd.cmdline=ask
rd.info
```

## Usage

dracut is easy to use and typically does not require user configuration, even when using non-standard setups, like [LVM on LUKS](/index.php/Dm-crypt/Encrypting_an_entire_system#LVM_on_LUKS "Dm-crypt/Encrypting an entire system").

To generate an initramfs for the running kernel:

```
# dracut /boot/initramfs-linux.img

```

To generate a fallback initramfs run:

```
# dracut -N /boot/initramfs-linux-fallback.img

```

`/boot/initramfs-linux.img` refers to the output image file. If you are using the non-regular kernel, consider changing the file name. For example, for the [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) kernel, the output file should be named `/boot/initramfs-linux-lts.img`. However, you can name these files whatever you wish as long as your [boot loader](/index.php/Boot_loader "Boot loader") configuration uses the same file names.

### Additional flags

The `--hostonly` flag creates an image that only contains the files needed to boot the local host system, instead of creating a generic image with more files. Using this flag reduces the size of the generated image, but you will not be able to use it on other computers or switch to a different root file system without generating a new image.

The `--force` flag overwrites the image file if it is already present.

More flags can be found with [dracut(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dracut.8).

## Tips and tricks

### View information about generated image

You can view information about a generated initramfs image, which you may wish to view in a pager:

```
# lsinitrd */path/to/initramfs_image* | less

```

This command will list the arguments passed to dracut when the image was created, the list of included dracut modules, and the list of all included files.

### Change compression program

To reduce the amount of time spent compressing the final image, you may change the compression program used.

**Warning:** Make sure your kernel has your chosen decompression support compiled in, otherwise you will not be able to boot. You must also have the chosen compression program package installed. Note that Linux does not support zstd compressed initramfs.

Simply add any one of the following lines (not multiple) [to your dracut configuration](#Configuration):

```
compress="cat"
compress="gzip"
compress="bzip2"
compress="lzma"
compress="xz"
compress="lzo"
compress="lz4"

```

[gzip](https://www.archlinux.org/packages/?name=gzip) is the default compression program used. `compress="cat"` will make the initramfs with no compression.

You can also use a non-officially-supported compression program:

```
compress="*program*"

```

### Generate a new initramfs on kernel upgrade

It is possible to automatically generate new initramfs images upon each kernel upgrade. The instructions here are for the default [linux](https://www.archlinux.org/packages/?name=linux) kernel, but it should be easy to add extra hooks for other kernels.

As the command to figure out the kernel version is somewhat complex, it will not work by itself in a [pacman hook](/index.php/Pacman_hook "Pacman hook"). So create a script anywhere on your system. For this example it will be created in `/usr/local/bin/`.

The script will also copy the new `vmlinuz` kernel file to `/boot/`, since the kernel packages do not place files in `/boot/` anymore.[[1]](https://lists.archlinux.org/pipermail/arch-general/2019-October/047056.html)

 `/usr/local/bin/dracut-install.sh` 
```
#!/usr/bin/env bash

args=('--no-hostonly-cmdline')

while read -r line; do
	if [[ "$line" == 'usr/lib/modules/'+([^/])'/pkgbase' ]]; then
		read -r pkgbase < "/${line}"
		kver="${line#'usr/lib/modules/'}"
		kver="${kver%'/pkgbase'}"

		install -Dm0644 "/${line%'/pkgbase'}/vmlinuz" "/boot/vmlinuz-${pkgbase}"
		dracut "${args[@]}" -f "/boot/initramfs-${pkgbase}.img" --kver "$kver"
		dracut -N -f "/boot/initramfs-${pkgbase}-fallback.img" --kver "$kver"
	fi
done

```
 `/usr/local/bin/dracut-remove.sh` 
```
#!/usr/bin/env bash

while read -r line; do
	if [[ "$line" == 'usr/lib/modules/'+([^/])'/pkgbase' ]]; then
		read -r pkgbase < "/${line}"
		rm -f "/boot/vmlinuz-${pkgbase}" "/boot/initramfs-${pkgbase}.img" "/boot/initramfs-${pkgbase}-fallback.img"
	fi
done

```

You need to make the scripts [executable](/index.php/Executable "Executable"). If you wish to add or remove flags, you should [add them to your dracut configuration](#Configuration).

The next step is creating [pacman hooks](/index.php/Pacman_hook "Pacman hook"):

 `/etc/pacman.d/hooks/90-dracut-install.hook` 
```
[Trigger]
Type = File
Operation = Install
Operation = Upgrade
Target = usr/lib/modules/*/pkgbase

[Action]
Description = Updating linux initcpios (with dracut!)...
When = PostTransaction
Exec = /usr/local/bin/dracut-install.sh
NeedsTargets

```
 `/etc/pacman.d/hooks/60-dracut-remove.hook` 
```
[Trigger]
Type = File
Operation = Remove
Target = usr/lib/modules/*/pkgbase

[Action]
Description = Removing linux initcpios...
When = PreTransaction
Exec = /usr/local/bin/dracut-remove.sh
NeedsTargets

```

You should stop [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") from creating and removing initramfs images as well, either by removing [mkinitcpio](https://www.archlinux.org/packages/?name=mkinitcpio) or with the following commands:

```
# ln -sf /dev/null /etc/pacman.d/hooks/90-mkinitcpio-install.hook
# ln -sf /dev/null /etc/pacman.d/hooks/60-mkinitcpio-remove.hook

```

## Troubleshooting

### Spaces in kernel parameters

dracut does not support quoted values with spaces in the `root=` and `resume=` [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). For example `root="PARTLABEL=Arch Linux"`. You will need to specify the parameters using a different block device naming scheme like [UUID](/index.php/UUID "UUID").

## See also

*   [Wikipedia:dracut (software)](https://en.wikipedia.org/wiki/dracut_(software) "wikipedia:dracut (software)")
*   [Gentoo:Dracut](https://wiki.gentoo.org/wiki/Dracut "gentoo:Dracut")