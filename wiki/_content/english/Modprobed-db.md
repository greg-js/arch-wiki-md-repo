Related articles

*   [Kernels](/index.php/Kernels "Kernels")
*   [Linux-ck](/index.php/Linux-ck "Linux-ck")

[modprobed-db](https://aur.archlinux.org/packages/modprobed-db/) keeps a running list of ALL modules ever probed on a system and allow for easy recall. This is very useful for users wishing to build a minimal kernel via a `make localmodconfig` which simply takes every module currently probed and switches everything BUT them off in the `.config` for a kernel resulting in smaller kernel packages and reduced compilation times.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation and Setup](#Installation_and_Setup)
*   [2 Usage](#Usage)
    *   [2.1 Cron](#Cron)
    *   [2.2 Systemd](#Systemd)
    *   [2.3 Data Recall](#Data_Recall)
        *   [2.3.1 Using the Official Arch kernel PKGBUILD](#Using_the_Official_Arch_kernel_PKGBUILD)
*   [3 Recommendations](#Recommendations)
*   [4 Suggested Modules](#Suggested_Modules)
*   [5 Benefits of modprobed-db with **make localmodconfig** in custom kernels](#Benefits_of_modprobed-db_with_make_localmodconfig_in_custom_kernels)

## Installation and Setup

The [modprobed-db](https://aur.archlinux.org/packages/modprobed-db/) package is available from the [AUR](/index.php/AUR "AUR").

1.  Run `modprobed-db` which will create `$XDG_CONFIG_HOME/modprobed-db.conf` if one does not already exist.
2.  Run `modprobed-db store` to store the current loaded modules.

**Optionally:** add modules in the ignore array that you do NOT want counted, for example modules that get built or that are provided by another package. Some common ones are included by default:

 `$ cat ~/.config/modprobed-db.conf` 
```
IGNORE=(nvidia vboxdrv vboxnetflt vboxnetadp vboxpci lirc_dev lirc_i2c
osscore oss_hdaudio oss_usb tp_smapi thinkpad_ec
zavl znvpair zunicode zcommon zpios zfs spl splat)
```

## Usage

Once the initial database has been created, simply use the system (insert USB sticks, use hardware that requires modules, mount filesystems that require modules, etc.) and periodically update the databases by one of two automatic methods:

### Cron

The most convenient method to use modprobed-db is to simply add a crontab entry invoking `/usr/bin/modprobed-db store` at some regular interval.

Example running the script once every hour:

```
$ crontab -e
0 */1 * * *   /usr/bin/modprobed-db store &> /dev/null

```

### Systemd

Systemd users not wishing to use cron may use the included user service: `modprobed-db.service`. It will run modprobed-db in store mode once per hour, and at boot and on shutdown.

```
$ systemctl --user enable --now modprobed-db.service

```

Status of the service and of the timer can be queried like any service and timer:

```
$ systemctl --user status modprobed-db
$ systemctl --user list-timers

```

### Data Recall

After the database has been adequately populated, it can be read directly by [make localmodconfig](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/tree/README?id=refs/tags/v4.3.3#n205)

#### Using the Official Arch kernel PKGBUILD

The official Arch kernel PKGBUILD can be modified as shown to do this automatically:

```
 ...
    msg2 "Applying patch $src..."
    patch -Np1 < "../$src"
  done

  msg2 "Setting config..."
  cp ../config .config
  make olddefconfig

  make LSMOD=$HOME/.config/modprobed.db localmodconfig          # <---- insert this line

  make -s kernelrelease > ../version
 ...
```

## Recommendations

It is recommended that users install the package and then "use" the system for a good amount of time to allow the database to grow based on usage and capture everything the system needs before building a kernel with a **make localmodconfig**. Some suggested actions to allow appropriate modules to load and get cataloged:

*   Insert every kind of removable media (USB, DVD, CD, etc.)
*   Use every device on the machine (wifi, network, USB stuff like cameras, ipods, etc.)
*   Mount every kind of filesystem one might typically use including ext2/3/4, fat, vfat, CIFS shares, NFS shares, etc.
*   Use as many applications (that one would normally use) as possible in order to capture modules on which they depend. For example, IP blocking/filtering software like [pgl-cli](https://aur.archlinux.org/packages/pgl-cli/).
*   Users who plan to mount iso image file should do so (this will make sure to capture the **loop** and **isofs** modules).
*   Users requiring encryption software such as [truecrypt](https://www.archlinux.org/packages/?name=truecrypt) should make sure to load it, and mount some encrypted containers to ensure that the needed crypto modules are in the db.
*   Try-out different Linux-kernels; they may include modules not enabled in the default/other kernel(s)

## Suggested Modules

*   cifs
*   ext2
*   ext3
*   ext4
*   fat
*   isofs
*   loop
*   efivars
*   vfat
*   usb_storage

## Benefits of modprobed-db with **make localmodconfig** in custom kernels

1.  Reduced kernel footprint on FS
2.  Reduced compilation time

Comparisons using version 3.8.8-1 of the Arch kernel (from ABS):

**Note:** The modprobed.db on the test machine contains 209 lines; YMMV based on specific usage and needs.

| **Machine CPU** | **# of threads** | **make localmodconfig** | **# of Modules** | **Modules' Size on HDD** | **Compilation Time** |
| Intel i7-3770K @ 4.50 GHz | 8 | No | 3,025 | 129 MB | 7 min 37 sec |
| Intel i7-3770K @ 4.50 GHz | 8 | Yes | 230 | 18 MB | 1 min 13 sec |
| Intel Q9550 @ 3.40 GHz | 4 | No | 3,025 | 129 MB | 14 min 21 sec |
| Intel Q9550 @ 3.40 GHz | 4 | Yes | 230 | 18 MB | 2 min 20 sec |
| Intel E5200 @ 3.33 GHz | 2 | No | 3,025 | 129 MB | 34 min 35 sec |
| Intel E5200 @ 3.33 GHz | 2 | Yes | 230 | 18 MB | 5 min 46 sec |

*   **13x less modules built**
*   **7x less space**
*   **6x less compilation time**

Number of modules found by:

```
find /scratch/linux-3.8 -name '*.ko' | wc -l

```

Size on HDD found by:

```
find /scratch/linux-3.8 -name '*.ko' -print0 | xargs -0 du -ch

```

Compilation time found by entering a preconfigured linux-3.8.8 (using stock Arch config):

```
$ time make -jx modules

```

**Note:** The Arch standard is to gzip each module; the numbers shown in the table above are not gzip'ed but the savings ratio will be unaffected by this.