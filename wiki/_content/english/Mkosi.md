Related articles

*   [systemd](/index.php/Systemd "Systemd")
*   [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")
*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")
*   [Docker](/index.php/Docker "Docker")

**[mkosi](https://github.com/systemd/mkosi)** stands for *Make Operating System Image*, and is a tool for generating an OS tree or image that can be booted.

## Contents

*   [1 Installation](#Installation)
*   [2 Basic usage](#Basic_usage)
    *   [2.1 Example: Create and boot a Debian-Image](#Example:_Create_and_boot_a_Debian-Image)
    *   [2.2 2\. Example: Using Config-files](#2._Example:_Using_Config-files)
    *   [2.3 Configurations](#Configurations)
*   [3 See also](#See_also)

## Installation

Install [mkosi](https://aur.archlinux.org/packages/mkosi/) or [mkosi-git](https://aur.archlinux.org/packages/mkosi-git/). Depending on what Distribution you want to build install further packages:

| Distribution | Package |
| Arch | [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) |
| Debian | [debootstrap](https://www.archlinux.org/packages/?name=debootstrap), [debian-archive-keyring](https://www.archlinux.org/packages/?name=debian-archive-keyring) |
| Ubuntu |
| Fedora | [dnf](https://aur.archlinux.org/packages/dnf/) |
| OpenSUSE | [zypper-git](https://aur.archlinux.org/packages/zypper-git/) |

## Basic usage

You can create an image by calling mkosi as root

```
# mkosi

```

You can specify option as arguments or by editing files in the current folder.

### Example: Create and boot a Debian-Image

The following command will create a bootable image with latest debian-version and the package openssh-clients installed:

```
$ mkosi -d debian -t raw_gpt -b --checksum --password password --package openssh-clients,vim -o image.raw

```

you can boot it with systemd-nspawn:

```
# systemd-nspawn -b -i image.raw

```

or boot it virtualized with qemu and

```
$ qemu-system-x86_64 -m 512 -smp 2 -bios /usr/share/ovmf/x64/OVMF_CODE.fd -drive format=raw,file=image.raw

```

You can also write this image to an usb-drive and use it to boot you computer.

### 2\. Example: Using Config-files

The same image can be created by creating a config-file:

 `mkosi.default` 
```
[Files]
[Distribution]
Distribution=debian
Release=stretch

[Output]
Format=raw_gpt
Bootable=yes
Output=image.raw

[Packages]
Packages=
         openssh-client
         vim

[Validation]
Password=password

```

**Tip:** If you create a folder mkosi.cache in current working dir, mkosi will save all downloaded packages there, so you can recreate images faster.

### Configurations

Basic options can be specified as commandline argument or in a file called mkosi.default in your current folder. Most important Options:

| Argument | Option in mkosi.default | Description |
| -d | [Distribution]

Distribution=

 | Wich distribution should be installed: fedora,debian,ubuntu,arch,opensuse |
| -r | [Distribution]

Release=

 | The version of the distribution: jessie, 21, … |
| -t | [Output]

Format=

 | Format of the image to create:

*   **raw_gpt**: Imagefile with GPT-Partiontable and ext4-Filesystem
*   **raw_btrfs**: Imagefile with GPT-Partiontable and btrfs-Filesystem
*   **raw_squashfs**: Imagefile with GPT-Partiontable and squashfs-Filesystem
*   **directory**: A plain directory
*   **subvolume**: A btrfs subvolume
*   **tar**: A tar-ball of a plain directory

 |
| -b | [Output]

Bootable=yes

 | make the image bootable |
| --root-size | [Output]

RootSize=

 | Size of the root-filesystem |
| -p | [Packages]

Packages=

 | List of packages to be installed into the image |
| -o | [Output]

Output=

 | File/directory-Name |
| --password | [Validation]

Password=test

 | Set the initial Root-Password |

## See also

*   [Mkosi on Github](https://github.com/systemd/mkosi)
*   [Longer introduction](http://0pointer.net/blog/mkosi-a-tool-for-generating-os-images.html)