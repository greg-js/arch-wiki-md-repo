Related articles

*   [Disk encryption](/index.php/Disk_encryption "Disk encryption")
*   [TrueCrypt](/index.php/TrueCrypt "TrueCrypt")
*   [Tomb](/index.php/Tomb "Tomb")

*tcplay* is a free, fully featured and stable [TrueCrypt](/index.php/TrueCrypt "TrueCrypt") implementation including multiple keyfiles and cipher cascades.

Source: [github project home](https://github.com/bwalex/tc-play)

## Contents

*   [1 Installation](#Installation)
*   [2 Encrypting a file as a virtual volume](#Encrypting_a_file_as_a_virtual_volume)
*   [3 Mounting an existing container for a user](#Mounting_an_existing_container_for_a_user)
*   [4 Using tcplay-helper](#Using_tcplay-helper)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [tcplay](https://www.archlinux.org/packages/?name=tcplay) package.

## Encrypting a file as a virtual volume

Invoke

```
 $ losetup -f

```

to find the first unused loopback device; in this example, `/dev/loop0`.

**Note:** As of udev 181-5, the `loop` device module is no longer auto-loaded.

Create a new container `foo.tc`, 20M in size for instance, in the working directory:

```
 # fallocate -l 20M foo.tc
 # losetup /dev/loop0 foo.tc
 # tcplay -c -d /dev/loop0 -a whirlpool -b AES-256-XTS

```

Enter a secure password for the volume, and confirm the query to overwrite `foo.tc` with the new volume. tcplay will then write random data into the volume. Map the volume and create a filesystem on it in order to mount

```
 # tcplay -m foo.tc -d /dev/loop0
 # mkfs.ext4 /dev/mapper/foo.tc
 # mount /dev/mapper/foo.tc /mnt/truecrypt/

```

To unset the container,

```
 # umount /mnt/truecrypt
 # dmsetup remove foo.tc
 # losetup -d /dev/loop0

```

## Mounting an existing container for a user

Consider `/dev/loop0` the first unused loop device, `foo.tc` the TrueCrypt container, `/home/you/truecrypt/` the desired mount point. The user `you` in this example has `uid=1000` and `gid=100`. The steps for mounting the container as a virtual volume are:

1.  Associate loop device with the container
2.  Map the container to the loop device
3.  Mount the container in the filesystem

The following commands perform the above actions.

```
 # losetup /dev/loop0 foo.tc
 # tcplay -m foo.tc -d /dev/loop0
 # mount -o nodev,nosuid,uid=1000,gid=100 /dev/mapper/foo.tc /home/you/truecrypt/

```

Note, if the container uses ext4 or another filesystem that supports file ownership, the `uid` and `gid` parameters aren't needed and will not work. Therefore the third command would be simply:

```
 # mount -o nodev,nosuid /dev/mapper/foo.tc /home/you/truecrypt/

```

To reverse them:

```
 # umount /home/you/truecrypt/
 # dmsetup remove foo.tc
 # losetup -d /dev/loop0

```

## Using tcplay-helper

The [tcplay-helper-git](https://aur.archlinux.org/packages/tcplay-helper-git/) tool simplifies the process of creating, mounting and unmounting tc-play containers. The tool is still a work-in-progress, but should work fine for most users wanting to work with simple secure tc-play containers.

The following command creates a 3Mb container called foo.tc.

```
 # tcplay-helper create foo.tc 3M

```

To mount the container file we can either mount it as root with the following command. The container will be mounted under /mnt/truecrypt/

```
 # tcplay-helper open foo.tc

```

Alternatively, we can supply a username to mount the container as.

```
 # tcplay-helper open foo.tc archie

```

Finally, to close the container this command does the trick.

```
 # tcplay-helper close foo.tc

```

## See also

*   [Manual page for tcplay](http://leaf.dragonflybsd.org/cgi/web-man?command=tcplay&section=8)
*   [Jason Ryan: Replacing TrueCrypt](http://jasonwryan.com/blog/2013/01/10/truecrypt/)
*   [TrueCrypt Homepage](http://www.truecrypt.org/)
*   [HOWTO: Truecrypt Gentoo wiki](http://www.gentoo-wiki.info/HOWTO_Truecrypt)
*   [Truecrypt Tutorial on HowToForge](http://www.howtoforge.com/truecrypt_data_encryption)
*   [There is a good chance the CIA has a backdoor?](http://www.privacylover.com/encryption/analysis-is-there-a-backdoor-in-truecrypt-is-truecrypt-a-cia-honeypot/) (via [wp](https://secure.wikimedia.org/wikipedia/en/wiki/Truecrypt))
*   [tcplay-helper documentation](https://github.com/robertmuil/tcplay-helper)