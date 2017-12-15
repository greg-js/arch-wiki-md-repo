Related articles

*   [Arch boot process](/index.php/Arch_boot_process "Arch boot process")
*   [Boot loaders](/index.php/Boot_loaders "Boot loaders")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")
*   [EFISTUB](/index.php/EFISTUB "EFISTUB")

[rEFInd](http://www.rodsbooks.com/refind/) is a [UEFI](/index.php/UEFI "UEFI") boot manager capable of launching [EFISTUB](/index.php/EFISTUB "EFISTUB") kernels. It is a fork of the no-longer-maintained rEFIt and fixes many issues with respect to non-Mac UEFI booting. It is designed to be platform-neutral and to simplify booting multiple OSes.

**Note:** In the entire article `*esp*` denotes the mountpoint of the [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition") aka ESP.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Scripted installation](#Scripted_installation)
        *   [1.1.1 Secure Boot](#Secure_Boot)
            *   [1.1.1.1 Using PreLoader](#Using_PreLoader)
            *   [1.1.1.2 Using shim](#Using_shim)
            *   [1.1.1.3 Using your own keys](#Using_your_own_keys)
    *   [1.2 Manual installation](#Manual_installation)
    *   [1.3 Upgrading](#Upgrading)
        *   [1.3.1 Pacman hook](#Pacman_hook)
*   [2 Configuration](#Configuration)
    *   [2.1 Passing kernel parameters](#Passing_kernel_parameters)
        *   [2.1.1 For kernels automatically detected by rEFInd](#For_kernels_automatically_detected_by_rEFInd)
        *   [2.1.2 Manual boot stanzas](#Manual_boot_stanzas)
*   [3 Installation alongside an existing UEFI Windows installation](#Installation_alongside_an_existing_UEFI_Windows_installation)
*   [4 Tools](#Tools)
    *   [4.1 UEFI shell](#UEFI_shell)
    *   [4.2 Memtest86](#Memtest86)
    *   [4.3 Key management tools](#Key_management_tools)
        *   [4.3.1 HashTool](#HashTool)
        *   [4.3.2 MokManager](#MokManager)
        *   [4.3.3 KeyTool](#KeyTool)
    *   [4.4 GPT fdisk (gdisk)](#GPT_fdisk_.28gdisk.29)
    *   [4.5 iPXE](#iPXE)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Using drivers in UEFI shell](#Using_drivers_in_UEFI_shell)
    *   [5.2 Btrfs subvolume support](#Btrfs_subvolume_support)
        *   [5.2.1 Auto detection](#Auto_detection)
        *   [5.2.2 Manual boot stanza](#Manual_boot_stanza)
    *   [5.3 Apple Macs](#Apple_Macs)
    *   [5.4 VirtualBox](#VirtualBox)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [refind-efi](https://www.archlinux.org/packages/?name=refind-efi) package.

rEFInd has **read-only** drivers for ReiserFS, Ext2, Ext4, Btrfs, ISO-9660, HFS+, and NTFS. Additionally rEFInd can use drivers from the UEFI firmware i.e. FAT (or HFS+ on Macs or ISO-9660 on some systems).

**Note:** Your kernel and initramfs need to reside on a file system which rEFInd can read.

To find additional drivers see [The rEFInd Boot Manager: Using EFI Drivers: Finding Additional EFI Drivers](http://www.rodsbooks.com/refind/drivers.html#finding).

### Scripted installation

The rEFInd package includes the *refind-install* script to simplify the process of setting rEFInd as your default EFI boot entry. The script has several options for handling differing setups and UEFI implementations, see [refind-install(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/refind-install.8). For many systems it should be sufficient to simply run:

```
# refind-install

```

This will attempt to find and mount your [ESP](/index.php/ESP "ESP"), copy rEFInd files to `/EFI/refind/` on the ESP, and use `efibootmgr` to make rEFInd the default EFI boot application.

Alternatively you can install rEFInd to the default/fallback boot path `/EFI/BOOT/BOOT*.EFI`. This is helpful for bootable USB flash drives or on systems that have issues with the NVRAM changes made by `efibootmgr`:

```
# refind-install --usedefault */dev/sdXY*

```

Where `*/dev/sdXY*` is the partition of your ESP.

You can read the comments in the install script for explanations of the various installation options.

**Note:** By default `refind-install` installs only the driver for the file system on which kernel resides. Additional file systems need to be installed manually or you can install all drivers with the `--alldrivers` option. This is useful for bootable USB flash drives e.g.:
```
# refind-install --usedefault */dev/sdXY* --alldrivers

```

After installing rEFInd's files to the ESP, verify that rEFInd has created `refind_linux.conf` containing the required [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") (e.g. `root=`) in the same directory as your kernel. If it has not created this file, you will need to set up [#Passing kernel parameters](#Passing_kernel_parameters) manually or you will most likely get a kernel panic on your next boot.

By default, rEFInd will scan all of your drives (that it has drivers for) and add a boot entry for each EFI bootloader it finds, which should include your kernel (since Arch enables [EFISTUB](/index.php/EFISTUB "EFISTUB") by default). So you may have a bootable system at this point.

**Tip:** It is always a good idea to edit the default config `/EFI/refind/refind.conf` on the ESP to ensure that the default options work for you.

**Warning:** When refind-install is run in chroot (e.g. in live system when installing Arch Linux) `/boot/refind-linux.conf` is populated with kernel options from the live system not the one on which it is installed. You need to adjust kernel options in `/boot/refind-linux.conf` manually.

#### Secure Boot

See [Managing Secure Boot](http://www.rodsbooks.com/refind/secureboot.html) for [Secure Boot](/index.php/Secure_Boot "Secure Boot") support in rEFInd.

##### Using PreLoader

See [Secure Boot#Set up PreLoader](/index.php/Secure_Boot#Set_up_PreLoader "Secure Boot") to acquire signed `PreLoader.efi` and `HashTool.efi` binaries.

Execute `refind-install` with the option `--preloader */path/to/preloader*`

```
# refind-install --preloader /usr/share/preloader-signed/PreLoader.efi

```

Next time you boot with Secure Boot enabled, HashTool will launch and you will need to enrol the hash of rEFInd (`loader.efi`), rEFInd's drivers (e.g. `ext4_x64.efi`) and kernel.

See [refind-install(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/refind-install.8) for more information.

**Tip:** The signed *HashTool* is only capable of accessing the partition it was launched from. This means if your kernel is not on the ESP, you will not be able to enrol its hash from *HashTool*. You can workaround this by using [#KeyTool](#KeyTool), since it is capable of enrolling a hash in MokList and is not limited to one partition. Remember to enrol *KeyTool'*s hash before before using it.

##### Using shim

[Install](/index.php/Install "Install") [shim-signed](https://aur.archlinux.org/packages/shim-signed/). Read [Secure Boot#shim](/index.php/Secure_Boot#shim "Secure Boot"), but skip all file copying.

To use only hashes with *shim*, execute `refind-install` with the option `--shim */path/to/shim*`

```
# refind-install --shim /usr/share/shim-signed/shimx64.efi

```

Next time you boot with Secure Boot enabled, MokManager will launch and you will need to enrol the hash of rEFInd (`grubx64.efi`), rEFInd's drivers (e.g. `ext4_x64.efi`) and kernel.

To sign rEFInd with a Machine Owner Key, install [sbsigntools](https://www.archlinux.org/packages/?name=sbsigntools).

**Tip:** If you already have [created a MOK](/index.php/Secure_Boot#shim_with_key "Secure Boot"), place the files in the directory `/etc/refind.d/keys` with the names `refind_local.key`, `refind_local.crt` and `refind_local.cer`.

Execute `refind-install` with the options `--shim */path/to/shim*` and `--localkeys`:

```
# refind-install --shim /usr/share/shim-signed/shimx64.efi --localkeys

```

*refind-install* will create the keys for you and sign itself and its drivers. You will need to sign the kernel with the same key, e.g.:

```
# sbsign --key /etc/refind.d/keys/refind_local.key --cert /etc/refind.d/keys/refind_local.crt --output /boot/vmlinuz-linux /boot/vmlinuz-linux

```

Once in MokManager add `refind_local.cer` to MoKList. `refind_local.cer` can be found inside a directory called `keys` in the rEFInd's installation directory, e.g. `*esp*/EFI/refind/keys/refind_local.cer`.

See [refind-install(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/refind-install.8) for more information.

##### Using your own keys

Follow [Secure Boot#Using your own keys](/index.php/Secure_Boot#Using_your_own_keys "Secure Boot") to create keys.

Create directory `/etc/refind.d/keys` and place Signature Database (**db**) key and certificates in it. Name the files: `refind_local.key`, `refind_local.crt` and `refind_local.cer`.

When running install script add option `--localkeys`, e.g.:

```
# refind-install --localkeys

```

rEFInd EFI binary will be signed with supplied key and certificate.

### Manual installation

**Tip:** rEFInd can boot Linux in many ways. See [The rEFInd Boot Manager: Methods of Booting Linux](http://www.rodsbooks.com/refind/linux.html) for coverage of the various approaches.

If the `refind-install` script does not work for you, rEFInd can be set up manually.

First, copy the executable to the ESP:

```
# mkdir -p *esp*/EFI/refind
# cp /usr/share/refind/refind_x64.efi *esp*/EFI/refind/

```

Then use [efibootmgr](/index.php/UEFI#efibootmgr "UEFI") to create a boot entry in the UEFI NVRAM, where `*/dev/sdX*` and `*Y*` are the device and partition number of your ESP. If you are installing rEFInd to the default UEFI path `/EFI/BOOT/BOOTX64.EFI`, you can probably skip this step.

```
# efibootmgr --create --disk */dev/sdX* --part *Y* --loader /EFI/refind/refind_x64.efi --label "rEFInd Boot Manager"

```

At this point, you should be able to reboot into rEFInd, but it will not be able to boot your kernel. If your kernel does not reside on your ESP, rEFInd can mount your partitions to find it - provided it has the right drivers.

rEFInd automatically loads all drivers from the subdirectories `drivers` and `drivers_*arch*` (e.g. `drivers_x64`) in its install directory.

```
# mkdir *esp*/EFI/refind/drivers_x64
# cp /usr/share/refind/drivers_x64/**drivername**_x64.efi *esp*/EFI/refind/drivers_x64/

```

Now rEFInd should have a boot entry for your kernel, but it will not pass the correct kernel parameters. Set up [#Passing kernel parameters](#Passing_kernel_parameters). You should now be able to boot your kernel using rEFInd. If you are still unable to boot or if you want to tweak rEFInd's settings, many options can be changed with a config file:

```
# cp /usr/share/refind/refind.conf-sample *esp*/EFI/refind/refind.conf

```

The sample config is well commented and self-explanatory.

Unless you have set `textonly` in the config file, you should copy rEFInd's icons to get rid of the ugly placeholders:

```
# cp -r /usr/share/refind/icons *esp*/EFI/refind/

```

You can try out different fonts by copying them and changing the `font` setting in `refind.conf`:

```
# cp -r /usr/share/refind/fonts *esp*/EFI/refind/

```

**Tip:** Pressing `F10` in rEFInd will save a screenshot to the top level directory of the ESP.

### Upgrading

Pacman updates the rEFInd files in `/usr/share/refind/` and will not copy new files to the ESP for you. If `refind-install` worked for your original installation of rEFInd, you can rerun it to copy the updated files. The new config file will be copied as `refind.conf-sample` so that you can integrate changes into your config file using a diff tool. If your rEFInd required [#Manual installation](#Manual_installation), you will need to figure out which files to copy yourself.

#### Pacman hook

You can automate the update process using a hook:

 `/etc/pacman.d/hooks/refind.hook` 
```
[Trigger]
Operation=Upgrade
Type=Package
Target=refind-efi

[Action]
Description = Updating rEFInd on ESP
When=PostTransaction
Exec=/usr/bin/refind-install
```

Where the `Exec=` may need to be changed to the correct update command for your setup. If you did [#Manual installation](#Manual_installation), you could create your own update script to call with the hook.

## Configuration

The rEFInd configuration `refind.conf` is located in the same directory as the rEFInd EFI application (usually `*esp*/EFI/refind` or `*esp*/EFI/BOOT`). The default config contains extensive comments explaining all its options, see [Configuring the Boot Manager](http://www.rodsbooks.com/refind/configfile.html) for more detailed explanations.

### Passing kernel parameters

There are two methods for setting the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") that rEFInd will pass to the kernel.

#### For kernels automatically detected by rEFInd

If rEFInd automatically detects your kernel, you can place a `refind_linux.conf` file containing the kernel parameters in the same directory as your kernel. You can use `/usr/share/refind/refind_linux.conf-sample` as a starting point. The first uncommented line of `refind_linux.conf` will be the default parameters for the kernel. Subsequent lines will create entries in a submenu accessible using `+`, `F2`, or `Insert`.

 `/boot/refind_linux.conf` 
```
"Boot using default options"     "root=PARTUUID=XXXXXXXX rw add_efi_memmap"
"Boot using fallback initramfs"  "root=PARTUUID=XXXXXXXX rw add_efi_memmap initrd=/boot/initramfs-linux-fallback.img"
"Boot to terminal"               "root=PARTUUID=XXXXXXXX rw add_efi_memmap systemd.unit=multi-user.target"

```

Alternatively, try running:

```
# mkrlconf

```

Which will attempt to find your kernel in `/boot` and automatically generate `refind_linux.conf`. The script will only set up the most basic kernel parameters, so be sure to check the file it created for correctness.

If you do not specify an `initrd=` parameter, rEFInd will automatically add it by searching for common RAM disk filenames in the same directory as the kernel. If you need multiple `initrd=` parameters, you must specify them manually in `refind_linux.conf`. For example, a [Microcode](/index.php/Microcode "Microcode") passed before the initramfs: `... initrd=/boot/intel-ucode.img initrd=/boot/initramfs-linux.img`.

**Warning:** `initrd` path is relative to the root of the file system on which the kernel resides. This could be `initrd=/boot/initramfs-linux.img` or, if ESP is mounted to `/boot`, `initrd=/initramfs-linux.img`.

#### Manual boot stanzas

If your kernel is not autodetected, or if you simply want more control over the options for a menu entry, you can manually create boot entries using stanzas in `refind.conf`. Ensure that `scanfor` includes `manual` or these entries will not appear in rEFInd's menu. Kernel parameters are set with the `options` keyword. rEFInd will append the `initrd=` parameter using the file specified by the `initrd` keyword in the stanza. If you need additional initrds (e.g. for [Microcode](/index.php/Microcode "Microcode")), you can specify them in `options` (and the one specified by the `initrd` keyword will be added to the end).

Manual boot stanzas are explained in [Creating Manual Boot Stanzas](http://www.rodsbooks.com/refind/configfile.html#stanzas).

 `*esp*/EFI/refind/refind.conf` 
```
...

menuentry "Arch Linux" {
	icon     /EFI/refind/icons/os_arch.png
	volume   "Arch Linux"
	loader   /boot/vmlinuz-linux
	initrd   /boot/initramfs-linux.img
	options  "root=PARTUUID=XXXXXXXX rw add_efi_memmap"
	submenuentry "Boot using fallback initramfs" {
		initrd /boot/initramfs-linux-fallback.img
	}
	submenuentry "Boot to terminal" {
		add_options "systemd.unit=multi-user.target"
	}
}

```

It is likely that you will need to change `volume` to match either a filesystem's LABEL, a PARTLABEL, or a PARTUUID of the partition where the kernel image resides. See [Persistent block device naming#by-label](/index.php/Persistent_block_device_naming#by-label "Persistent block device naming") for examples of assigning a volume label.

**Warning:** `loader` and `initrd` paths are relative to the root of `volume`.

## Installation alongside an existing UEFI Windows installation

**Note:** The usual caveats of [Dual boot with Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows") apply.

rEFInd is compatible with the EFI system partition created by a UEFI Windows installation, so there is no need to create or format another FAT32 partition when installing Arch alongside Windows. Simply mount the existing ESP and install rEFInd as usual. By default, rEFInd's autodetection feature should recognize any existing Windows/recovery bootloaders.

## Tools

rEFInd supports running various 3rd-party tools. Tools need to be installed separately. Edit `showtools` in `refind.conf` to choose which ones to show.

 `*esp*/EFI/refind/refind.conf` 
```
...
showtools [shell](#UEFI_shell), [memtest](#Memtest86), [mok_tool](#Key_management_tools), [gdisk](#GPT_fdisk_.28gdisk.29), [netboot](#iPXE), ...
...

```

### UEFI shell

See [Unified Extensible Firmware Interface#UEFI Shell](/index.php/Unified_Extensible_Firmware_Interface#UEFI_Shell "Unified Extensible Firmware Interface").

Copy `shellx64.efi` to the root of the [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition").

### Memtest86

Install [memtest86-efi](https://aur.archlinux.org/packages/memtest86-efi/) and copy it to `*esp*/EFI/tools/`.

```
# cp /usr/share/memtest86-efi/bootx64.efi *esp*/EFI/tools/memtest86.efi

```

### Key management tools

rEFInd can detect Secure Boot key management tools if they are placed in rEFInd's directory on ESP, `*esp*/` or `*esp*/EFI/tools/`.

#### HashTool

Follow [#Using PreLoader](#Using_PreLoader) and `HashTool.efi` will be placed in rEFInd's directory.

#### MokManager

Follow [#Using shim](#Using_shim) and MokManager will be placed in rEFInd's directory.

#### KeyTool

Install [efitools](https://www.archlinux.org/packages/?name=efitools).

Place KeyTool EFI binary in `*esp*/` or `*esp*/EFI/tools/` with the name `KeyTool.efi` or `KeyTool-signed.efi`.

See [Secure Boot#Using KeyTool](/index.php/Secure_Boot#Using_KeyTool "Secure Boot") for instructions on signing `KeyTool.efi`.

### GPT fdisk (gdisk)

There is no package for the EFI version of *gdisk*, but you can download a binary from *gdisk'*s author.

Download `gdisk-efi-*.zip` from [SourceForge](http://sourceforge.net/projects/gptfdisk/files/gptfdisk/), extract the archive, and copy `gdisk_x64.efi` to `*esp*/EFI/tools`.

### iPXE

**Note:** PXE support in rEFInd is **experimental**.

[refind-efi](https://www.archlinux.org/packages/?name=refind-efi) contains the iPXE UEFI binaries, you just need to copy them to `*esp*/EFI/tools/`.

```
# cp /usr/share/refind/tools_x64/ipxe_discovery_x64.efi *esp*/EFI/tools/ipxe_discovery.efi
# cp /usr/share/refind/tools_x64/ipxe_x64.efi *esp*/EFI/tools/ipxe.efi

```

## Troubleshooting

### Using drivers in UEFI shell

To use rEFInd's drivers in UEFI shell load them using command `load` and refresh mapped drives with `map -r`.

```
Shell> load FS0:\EFI\refind\drivers\ext4_x64.efi
Shell> map -r

```

Now you can access your file system from UEFI shell.

### Btrfs subvolume support

#### Auto detection

To allow kernel auto detection on a Btrfs subvolume uncomment and edit `also_scan_dirs` in `refind.conf`.

 `*esp*/EFI/refind/refind.conf`  `also_scan_dirs *subvolume*/boot` 

Next add `subvol=*subvolume*` to `rootflags` in `refind_linux.conf` and then predend `*subvolume*` to the initrd path.

 `/boot/refind_linux.conf`  `"Boot using standard options"  "root=PARTUUID=XXXXXXXX rootflags=rw,subvol=*subvolume* initrd=*subvolume*/boot/initramfs-linux.img"` 

#### Manual boot stanza

If booting a [btrfs](/index.php/Btrfs "Btrfs") subvolume as root, amend the `options` line with `rootflags=subvol=<root subvolume>`. In the example below, root has been mounted as a btrfs subvolume called 'ROOT' (e.g. `mount -o subvol=ROOT /dev/sdxY /mnt`):

 `*esp*/EFI/refind/refind.conf` 
```
...

menuentry "Arch Linux" {
        icon     /EFI/refind/icons/os_arch.png
        volume   Boot
        loader   /boot/vmlinuz-linux
        initrd   /boot/initramfs-linux.img
        options  "root=PARTUUID=XXXXXXXX rw rootflags=subvol=ROOT"

...
        }

```

A failure to do so will otherwise result in the following error message: `ERROR: Root device mounted successfully, but /sbin/init does not exist.`

### Apple Macs

[mactel-boot](https://aur.archlinux.org/packages/mactel-boot/) is an experimental "bless" utility for Linux. If that does not work, use "bless" from within OSX to set rEFInd as the default boot entry:

```
# bless --setBoot --folder *esp*/EFI/refind --file *esp*/EFI/refind/refind_x64.efi

```

### VirtualBox

Currently, VirtualBox will only boot the default `/EFI/BOOT/BOOT*.EFI` path, so `refind-install` needs to be used with at least the `--usedefault` option. See [VirtualBox#Installation in EFI mode](/index.php/VirtualBox#Installation_in_EFI_mode "VirtualBox") for more information.

## See also

*   [The rEFInd Boot Manager](http://www.rodsbooks.com/refind/) by Roderick W. Smith.
*   `/usr/share/refind/docs/README.txt`
*   [rEFInd discussion forum on Sourceforge](https://sourceforge.net/p/refind/discussion/)