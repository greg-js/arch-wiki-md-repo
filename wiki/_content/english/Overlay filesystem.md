From [the initial kernel commit](https://github.com/torvalds/linux/commit/e9be9d5e76e34872f0c37d72e25bc27fe9e2c54c)

	*Overlayfs allows one, usually read-write, directory tree to be overlaid onto another, read-only directory tree. All modifications go to the upper, writable layer. This type of mechanism is most often used for live CDs but there's a wide variety of other uses.*

	*The implementation differs from other "union filesystem" implementations in that after a file is opened all operations go directly to the underlying, lower or upper, filesystems. This simplifies the implementation and allows native performance in these cases.*

Overlayfs has been in the linux kernel since 3.18.[[1]](https://github.com/torvalds/linux/commit/e9be9d5e76e34872f0c37d72e25bc27fe9e2c54c)

## Installation

Overlayfs is enabled in the default kernel and the `overlay` module is automatically loaded upon issuing a mount command.

## Usage

To mount an overlay use the following `mount` options:

```
# mount -t overlay overlay -o lowerdir=*/lower*,upperdir=*/upper*,workdir=*/work* */merged*

```

**Note:** The working directory (*workdir*) needs to be on the same filesystem mount as the upper directory.

To add an overlayfs entry to `/etc/fstab` use the following format:

 `/etc/fstab`  `overlay */merged* overlay noauto,x-systemd.automount,lowerdir=*/lower*,upperdir=*/upper*,workdir=*/work* 0 0` 

The `noauto` and `x-systemd.automount` mount options are necessary to prevent systemd from hanging on boot because it failed to mount the overlay. The overlay is now mounted whenever it is first accessed and requests are buffered until it is ready. See [Fstab#Automount with systemd](/index.php/Fstab#Automount_with_systemd "Fstab").

## See also

*   [Overlay Filesystem documentation](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/Documentation/filesystems/overlayfs.txt)