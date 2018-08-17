[Ufsd](http://www.paragon-software.com/home/ntfs-linux-per/) is a closed-source driver for Microsoft's NTFS file system that includes read and write support, developed by Paragon GmbH. It is currently (as of 29-Aug, 2013) free for personal use. It offers significantly faster writes to ntfs filesystems than the default ntfs-3g driver. This document will describe how to setup ufsd to work on your computer.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Manual](#Manual)
    *   [2.2 Automatic](#Automatic)
*   [3 See also](#See_also)

## Installation

The ufsd packages uses [Dynamic Kernel Module Support](/index.php/Dynamic_Kernel_Module_Support "Dynamic Kernel Module Support") so you won't need to bother about rebuilding and reinstalling every time the kernel changes

*   [Install](/index.php/Install "Install") the [dkms](https://www.archlinux.org/packages/?name=dkms) package.
*   [Start](/index.php/Start "Start") and enable `dkms.service`.
*   Download the [ufsd-module-dkms](https://aur.archlinux.org/packages/ufsd-module-dkms/) tarball from the [AUR](/index.php/AUR "AUR").
*   Untar the tarball
*   Visit [http://www.paragon-software.com/home/ntfs-linux-per/download.html](http://www.paragon-software.com/home/ntfs-linux-per/download.html) and fill in the request form. You should receive an email with a download link shortly. Download the .tbz file and move it to the package folder.
*   Build and install the package

```
$ makepkg -si

```

*   Check if the module has been installed in dkms.

```
$ dkms status

```

## Usage

Test using the manual method before setting it up for automatic loading and mounting. Remember to create the target folder before mounting. And, also remember to unmount your ntfs partition if it is already mounted using ntfs-3g.

### Manual

```
# modprobe ufsd
# mount -t ufsd /dev/*your-NTFS-partition* /{mnt,...}/*folder* -o uid=*your username*,gid=users

```

### Automatic

For non-dkms setups, edit `/etc/fstab` as below:

```
# <file system>   <dir>		<type>    <options>             <dump>  <pass>
/dev/*NTFS-part*  /mnt/windows  ufsd   uid=*your username*,gid=users,noatime,umask=0222	0 0

```

For dkms setups, edit `/etc/fstab` as below:

```
# <file system>   <dir>		<type>    <options>             <dump>  <pass>
/dev/*NTFS-part*  /mnt/windows  ufsd   noauto,x-systemd.automount,uid=*your username*,gid=users,noatime,umask=0222	0 0

```

To load the ufsd driver at startup, create a `*.conf` file (e.g. `ufsd.conf`) in `/etc/modules-load.d/` that contains all modules that should be loaded:

 `/etc/modules-load.d/ufsd.conf`  `ufsd` 
**Note:** You may need to update the kernel modules db in order to avoid 'no such file or directory' error when loading ufsd. Run: `depmod -a`.

## See also

*   [Ufsd options](http://kb.paragon-software.com/paragon/include/templ/object2.jsp?objId=5833)