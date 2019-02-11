<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Securing the unencrypted boot partition](#Securing_the_unencrypted_boot_partition)
    *   [1.1 Booting from a removable device](#Booting_from_a_removable_device)
    *   [1.2 chkboot](#chkboot)
    *   [1.3 mkinitcpio-chkcryptoboot](#mkinitcpio-chkcryptoboot)
        *   [1.3.1 Installation](#Installation)
        *   [1.3.2 Technical Overview](#Technical_Overview)
    *   [1.4 AIDE](#AIDE)
    *   [1.5 STARK](#STARK)
*   [2 Using GPG, LUKS, or OpenSSL Encrypted Keyfiles](#Using_GPG,_LUKS,_or_OpenSSL_Encrypted_Keyfiles)
*   [3 Remote unlocking of the root (or other) partition](#Remote_unlocking_of_the_root_(or_other)_partition)
    *   [3.1 Remote unlocking (hooks: systemd, systemd-tool)](#Remote_unlocking_(hooks:_systemd,_systemd-tool))
    *   [3.2 Remote unlocking (hooks: netconf, dropbear, tinyssh, ppp)](#Remote_unlocking_(hooks:_netconf,_dropbear,_tinyssh,_ppp))
    *   [3.3 Remote unlock via wifi (hooks: build your own)](#Remote_unlock_via_wifi_(hooks:_build_your_own))
*   [4 Discard/TRIM support for solid state drives (SSD)](#Discard/TRIM_support_for_solid_state_drives_(SSD))
*   [5 The encrypt hook and multiple disks](#The_encrypt_hook_and_multiple_disks)
    *   [5.1 Expanding LVM on multiple disks](#Expanding_LVM_on_multiple_disks)
        *   [5.1.1 Adding a new drive](#Adding_a_new_drive)
        *   [5.1.2 Extending the logical volume](#Extending_the_logical_volume)
    *   [5.2 Modifying the encrypt hook for multiple partitions](#Modifying_the_encrypt_hook_for_multiple_partitions)
        *   [5.2.1 Root filesystem spanning multiple partitions](#Root_filesystem_spanning_multiple_partitions)
        *   [5.2.2 Multiple non-root partitions](#Multiple_non-root_partitions)
*   [6 Encrypted system using a detached LUKS header](#Encrypted_system_using_a_detached_LUKS_header)
    *   [6.1 Using systemd hook](#Using_systemd_hook)
    *   [6.2 Modifying encrypt hook](#Modifying_encrypt_hook)
*   [7 Encrypted /boot and a detached LUKS header on USB](#Encrypted_/boot_and_a_detached_LUKS_header_on_USB)
    *   [7.1 Preparing the disk devices](#Preparing_the_disk_devices)
        *   [7.1.1 Preparing the USB key](#Preparing_the_USB_key)
        *   [7.1.2 The main drive](#The_main_drive)
    *   [7.2 Installation procedure and custom encrypt hook](#Installation_procedure_and_custom_encrypt_hook)
        *   [7.2.1 Boot Loader](#Boot_Loader)
    *   [7.3 Changing the LUKS keyfile](#Changing_the_LUKS_keyfile)

## Securing the unencrypted boot partition

The `/boot` partition and the [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") are the two areas of the disk that are not encrypted, even in an [encrypted root](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system") configuration. They cannot usually be encrypted because the [boot loader](/index.php/Boot_loader "Boot loader") and BIOS (respectively) are unable to unlock a dm-crypt container in order to continue the boot process. An exception is [GRUB](/index.php/GRUB "GRUB"), which gained a feature to unlock a LUKS encrypted `/boot` - see [dm-crypt/Encrypting an entire system#Encrypted boot partition (GRUB)](/index.php/Dm-crypt/Encrypting_an_entire_system#Encrypted_boot_partition_(GRUB) "Dm-crypt/Encrypting an entire system").

This section describes steps that can be taken to make the boot process more secure.

**Warning:** Note that securing the `/boot` partition and MBR can mitigate numerous attacks that occur during the boot process, but systems configured this way may still be vulnerable to BIOS/UEFI/firmware tampering, hardware keyloggers, cold boot attacks, and many other threats that are beyond the scope of this article. For an overview of system-trust issues and how these relate to full-disk encryption, refer to [[1]](http://www.youtube.com/watch?v=pKeiKYA03eE).

### Booting from a removable device

**Warning:** systemd version 230 cryptsetup generator emits `RequiresMountsFor` for crypto keyfile. Therefore, when the filesystem that holds this file is unmounted, it also stops cryptsetup service. This behavior is incorrect because the filesystem and cryptokey is required only once, when the crypto container is initially setup. See [systemd issue 3816](https://github.com/systemd/systemd/issues/3816).

Using a separate device to boot a system is a fairly straightforward procedure, and offers a significant security improvement against some kinds of attacks. Two vulnerable parts of a system employing an [encrypted root filesystem](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system") are

*   the [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record"), and
*   the `/boot` partition.

These must be stored unencrypted in order for the system to boot. In order to protect these from tampering, it is advisable to store them on a removable medium, such as a USB drive, and boot from that drive instead of the hard disk. As long as you keep the drive with you at all times, you can be certain that those components have not been tampered with, making authentication far more secure when unlocking your system.

It is assumed that you already have your system configured with a dedicated partition mounted at `/boot`. If you do not, please follow the steps in [dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration"), substituting your hard disk for a removable drive.

**Note:** You must make sure your system supports booting from the chosen medium, be it a USB drive, an external hard drive, an SD card, or anything else.

Prepare the removable drive (`/dev/sdx`).

```
# gdisk /dev/sdx #format if necessary. Alternatively, cgdisk, fdisk, cfdisk, gparted...
# mkfs.ext2 /dev/sdx1
# mount /dev/sdx1 /mnt

```

Copy your existing `/boot` contents to the new one.

```
# cp -ai /boot/* /mnt/

```

Mount the new partition. Do not forget to update your [fstab](/index.php/Fstab "Fstab") file accordingly.

```
# umount /boot
# umount /mnt
# mount /dev/sdx1 /boot
# genfstab -p -U / > /etc/fstab

```

Update [GRUB](/index.php/GRUB "GRUB"). `grub-mkconfig` should detect the new partition UUID automatically, but custom menu entries may need to be updated manually.

```
# grub-mkconfig -o /boot/grub/grub.cfg
# grub-install /dev/sdx #install to the removable device, not the hard disk.

```

Reboot and test the new configuration. Remember to set your device boot order accordingly in your BIOS or [UEFI](/index.php/UEFI "UEFI"). If the system fails to boot, you should still be able to boot from the hard drive in order to correct the problem.

### chkboot

**Warning:** chkboot makes a `/boot` partition **tamper-evident**, not **tamper-proof**. By the time the chkboot script is run, you have already typed your password into a potentially compromised boot loader, kernel, or initrd. If your system fails the chkboot integrity test, no assumptions can be made about the security of your data.

Referring to an article from the ct-magazine (Issue 3/12, page 146, 01.16.2012, [[2]](http://www.heise.de/ct/inhalt/2012/03/6/)) the following script checks files under `/boot` for changes of SHA-1 hash, inode, and occupied blocks on the hard drive. It also checks the [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record"). The script cannot prevent certain type of attacks, but a lot are made harder. No configuration of the script itself is stored in unencrypted `/boot`. With a locked/powered-off encrypted system, this makes it harder for some attackers because it is not apparent that an automatic checksum comparison of the partition is done upon boot. However, an attacker who anticipates these precautions can manipulate the firmware to run his own code on top of your kernel and intercept file system access, e.g. to `boot`, and present the untampered files. Generally, no security measures below the level of the firmware are able to guarantee trust and tamper evidence.

The script with installation instructions is [available](ftp://ftp.heise.de/pub/ct/listings/1203-146.zip) (Author: Juergen Schmidt, ju at heisec.de; License: GPLv2). There is also package [chkboot](https://aur.archlinux.org/packages/chkboot/) to [install](/index.php/Install "Install").

After installation add a service file (the package includes one based on the following) and [enable](/index.php/Enable "Enable") it:

```
[Unit]
Description=Check that boot is what we want
Requires=basic.target
After=basic.target

[Service]
Type=oneshot
ExecStart=/usr/local/bin/chkboot.sh

[Install]
WantedBy=multi-user.target

```

There is a small caveat for systemd. At the time of writing, the original `chkboot.sh` script provided contains an empty space at the beginning of `#!/bin/bash` which has to be removed for the service to start successfully.

As `/usr/local/bin/chkboot_user.sh` needs to be executed right after login, you need to add it to the [autostart](/index.php/Autostart "Autostart") (e.g. under KDE -> *System Settings -> Startup and Shutdown -> Autostart*; GNOME 3: *gnome-session-properties*).

With Arch Linux, changes to `/boot` are pretty frequent, for example by new kernels rolling-in. Therefore it may be helpful to use the scripts with every full system update. One way to do so:

```
#!/bin/bash
#
# Note: Insert your <user>  and execute it with sudo for pacman & chkboot to work automagically
#
echo "Pacman update [1] Quickcheck before updating" & 
sudo -u <user> /usr/local/bin/chkboot_user.sh		# insert your logged on <user> 
/usr/local/bin/chkboot.sh
sudo -u <user> /usr/local/bin/chkboot_user.sh		# insert your logged on <user> 
echo "Pacman update [2] Syncing repos for pacman" 
pacman -Syu
/usr/local/bin/chkboot.sh
sudo -u <user> /usr/local/bin/chkboot_user.sh		# insert your logged on <user>
echo "Pacman update [3] All done, let us roll on ..."

```

### mkinitcpio-chkcryptoboot

**Warning:** This hook does **not** encrypt [GRUB](/index.php/GRUB "GRUB")'s core (MBR) code or EFI stub, nor does it protect against situations where an attacker is able to modify the behaviour of the bootloader to compromise the kernel and/or initramfs at run-time.

[mkinitcpio-chkcryptoboot](https://aur.archlinux.org/packages/mkinitcpio-chkcryptoboot/) is a [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") hook that performs integrity checks during early-userspace and advises the user not to enter his root partition password if the system appears to have been compromised. Security is achieved through an [encrypted boot partition](/index.php/Dm-crypt/Encrypting_an_entire_system#Encrypted_boot_partition_(GRUB) "Dm-crypt/Encrypting an entire system"), which is unlocked using [GRUB](/index.php/GRUB#Encrypted_/boot "GRUB")'s `cryptodisk.mod` module, and a root filesystem partition, which is encrypted with a password different from the former. This way, the [initramfs](/index.php/Initramfs "Initramfs") and [kernel](/index.php/Kernel "Kernel") are secured against offline tampering, and the root partition can remain secure even if the `/boot` partition password is entered on a compromised machine (provided that the chkcryptoboot hook detects the compromise, and is not itself compromised at run-time).

This hook requires [grub](https://www.archlinux.org/packages/?name=grub) release >=2.00 to function, and a dedicated, LUKS encrypted `/boot` partition with its own password in order to be secure.

#### Installation

[Install](/index.php/Install "Install") [mkinitcpio-chkcryptoboot](https://aur.archlinux.org/packages/mkinitcpio-chkcryptoboot/) and edit `/etc/default/chkcryptoboot.conf`. If you want the ability of detecting if your boot partition was bypassed, edit the `CMDLINE_NAME` and `CMDLINE_VALUE` variables, with values known only to you. You can follow the advice of using two hashes as is suggested right after the installation. Also, be sure to make the appropriate changes to the [kernel command line](/index.php/Kernel_command_line "Kernel command line") in `/etc/default/grub`. Edit the `HOOKS=` line in `/etc/mkinitcpio.conf`, and insert the `chkcryptoboot` hook **before** `encrypt`. When finished, [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

#### Technical Overview

[mkinitcpio-chkcryptoboot](https://aur.archlinux.org/packages/mkinitcpio-chkcryptoboot/) consists of an install hook and a run-time hook for mkinitcpio. The install hook runs every time the initramfs is rebuilt, and hashes the GRUB [EFI](/index.php/EFI "EFI") stub (`$esp/EFI/grub_uefi/grubx64.efi`) (in the case of [UEFI](/index.php/UEFI "UEFI") systems) or the first 446 bytes of the disk on which GRUB is installed (in the case of BIOS systems), and stores that hash inside the initramfs located inside the encrypted `/boot` partition. When the system is booted, GRUB prompts for the `/boot` password, then the run-time hook performs the same hashing operation and compares the resulting hashes before prompting for the root partition password. If they do not match, the hook will print an error like this:

```
CHKCRYPTOBOOT ALERT!
CHANGES HAVE BEEN DETECTED IN YOUR BOOT LOADER EFISTUB!
YOU ARE STRONGLY ADVISED NOT TO ENTER YOUR ROOT CONTAINER PASSWORD!
Please type uppercase yes to continue:

```

In addition to hashing the boot loader, the hook also checks the parameters of the running kernel against those configured in `/etc/default/chkcryptoboot.conf`. This is checked both at run-time and after the boot process is done. This allows the hook to detect if GRUB's configuration was not bypassed at run-time and afterwards to detect if the entire `/boot` partition was not bypassed.

For BIOS systems the hook creates a hash of GRUB's first stage bootloader (installed to the first 446 bytes of the bootdevice) to compare at the later boot processes. The main second-stage GRUB bootloader `core.img` is not checked.

### AIDE

Alternatively to above scripts, a hash check can be set up with [AIDE](/index.php/AIDE "AIDE") which can be customized via a very flexible configuration file.

### STARK

While one of these methods should serve the purpose for most users, they do not address all security problems associated with the unencrypted `/boot`. One approach which endeavours to provide a fully authenticated boot chain was published with POTTS as an academic thesis to implement the [STARK](http://www1.informatik.uni-erlangen.de/stark) authentication framework.

The POTTS proof-of-concept uses Arch Linux as a base distribution and implements a system boot chain with

*   POTTS - a boot menu for a one-time authentication message prompt
*   TrustedGrub - a [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") implementation which authenticates the kernel and initramfs against TPM chip registers
*   TRESOR - a kernel patch which implements AES but keeps the master-key not in RAM but in CPU registers during runtime.

As part of the thesis [installation](http://13.tc/p/potts/manual.html) instructions based on Arch Linux (ISO as of 2013-01) have been published. If you want to try it, be aware these tools are not in standard repositories and the solution will be time consuming to maintain.

## Using GPG, LUKS, or OpenSSL Encrypted Keyfiles

The following forum posts give instructions to use two factor authentication, gpg or openssl encrypted keyfiles, instead of a plaintext keyfile described earlier in this wiki article [System Encryption using LUKS with GPG encrypted keys](https://bbs.archlinux.org/viewtopic.php?id=120243):

*   GnuPG: [Post regarding GPG encrypted keys](https://bbs.archlinux.org/viewtopic.php?pid=943338#p943338) This post has the generic instructions.
*   OpenSSL: [Post regarding OpenSSL encrypted keys](https://bbs.archlinux.org/viewtopic.php?pid=947805#p947805) This post only has the `ssldec` hooks.
*   OpenSSL: [Post regarding OpenSSL salted bf-cbc encrypted keys](https://bbs.archlinux.org/viewtopic.php?id=155393) This post has the `bfkf` initcpio hooks, install, and encrypted keyfile generator scripts.
*   LUKS: [Post regarding LUKS encrypted keys](https://bbs.archlinux.org/viewtopic.php?pid=1502651#p1502651) with a `lukskey` initcpio hook. Or [#Encrypted /boot and a detached LUKS header on USB](#Encrypted_/boot_and_a_detached_LUKS_header_on_USB) below with a custom encrypt hook for initcpio.

Note that:

*   You can follow the above instructions with only two primary partitions, one boot partition (required because of encryption) and one primary LVM partition. Within the LVM partition you can have as many partitions as you need, but most importantly it should contain at least root, swap, and home logical volume partitions. This has the added benefit of having only one keyfile for all your partitions, and having the ability to hibernate your computer (suspend to disk) where the swap partition is encrypted. If you decide to do so your hooks in `/etc/mkinitcpio.conf` should look like this: `HOOKS=( ... usb usbinput (etwo or ssldec) encrypt (if using openssl) lvm2 resume ... )` and you should add `resume=/dev/<VolumeGroupName>/<LVNameOfSwap>` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").
*   If you need to temporarily store the unencrypted keyfile somewhere, do not store them on an unencrypted disk. Even better make sure to store them to RAM such as `/dev/shm`.
*   If you want to use a GPG encrypted keyfile, you need to use a statically compiled GnuPG version 1.4 or you could edit the hooks and use this AUR package [gnupg1](https://aur.archlinux.org/packages/gnupg1/)
*   It is possible that an update to OpenSSL could break the custom `ssldec` mentioned in the second forum post.

## Remote unlocking of the root (or other) partition

If you want to be able to reboot a fully LUKS-encrypted system remotely, or start it with a [Wake-on-LAN](/index.php/Wake-on-LAN "Wake-on-LAN") service, you will need a way to enter a passphrase for the root partition/volume at startup. This can be achieved by running a [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") hook that configures a network interface. Some packages listed below contribute various [mkinitcpio build hooks](/index.php/Mkinitcpio#Build_hooks "Mkinitcpio") to ease with the configuration.

**Note:**

*   Keep in mind to use kernel device names for the network interface (e.g. `eth0`) and not [udev's](/index.php/Udev "Udev") ones (e.g. `enp1s0`), as those will not work.
*   It could be necessary to add [the module for your network card](/index.php/Network_configuration#Device_driver "Network configuration") to the [MODULES](/index.php/Mkinitcpio#MODULES "Mkinitcpio") array.

### Remote unlocking (hooks: systemd, systemd-tool)

AUR package [mkinitcpio-systemd-tool](https://aur.archlinux.org/packages/mkinitcpio-systemd-tool/) provides a [systemd](https://www.archlinux.org/packages/?name=systemd)-centric mkinitcpio hook named *systemd-tool* with the following set of features for systemd in initramfs:

| 

Core features provided by the hook:

*   unified systemd + mkinitcpio configuration
*   automatic provisioning of binary and config resources
*   on-demand invocation of mkinitcpio scripts and in-line functions

 | 

Features provided by the included service units:

*   initrd debugging
*   early network setup
*   interactive user shell
*   remote ssh access in initrd
*   cryptsetup + custom password agent

 |

The [mkinitcpio-systemd-tool](https://aur.archlinux.org/packages/mkinitcpio-systemd-tool/) package requires the [systemd hook](/index.php/Mkinitcpio#Common_hooks "Mkinitcpio"). For more information be sure to read the project's [README](https://github.com/random-archer/mkinitcpio-systemd-tool/blob/master/README.md) as well as the provided default [systemd service unit files](https://github.com/random-archer/mkinitcpio-systemd-tool) to get you started.

The recommended hooks are: `base autodetect modconf block filesystems keyboard fsck systemd systemd-tool`.

### Remote unlocking (hooks: netconf, dropbear, tinyssh, ppp)

Another package combination providing remote logins to the initcpio is [mkinitcpio-netconf](https://aur.archlinux.org/packages/mkinitcpio-netconf/) and/or [mkinitcpio-ppp](https://aur.archlinux.org/packages/mkinitcpio-ppp/) (for remote unlocking using a [PPP](https://en.wikipedia.org/wiki/Point-to-Point_Protocol "wikipedia:Point-to-Point Protocol") connection over the internet) along with an [SSH](/index.php/SSH "SSH") server. You have the option of using either [mkinitcpio-dropbear](https://aur.archlinux.org/packages/mkinitcpio-dropbear/) or [mkinitcpio-tinyssh](https://aur.archlinux.org/packages/mkinitcpio-tinyssh/). Those hooks do not install any shell, so you also need to [install](/index.php/Install "Install") the [mkinitcpio-utils](https://aur.archlinux.org/packages/mkinitcpio-utils/) package. The instructions below can be used in any combination of the packages above. When there are different paths, it will be noted.

1.  If you do not have an SSH key pair yet, [generate one](/index.php/SSH_keys#Generating_an_SSH_key_pair "SSH keys") on the client system (the one which will be used to unlock the remote machine).
    **Note:** `tinyssh` only supports [Ed25519](/index.php/SSH_keys#Ed25519 "SSH keys") and [ECDSA](/index.php/SSH_keys#ECDSA "SSH keys") key types. If you chose to use [mkinitcpio-tinyssh](https://aur.archlinux.org/packages/mkinitcpio-tinyssh/), you need to create/use one of these.

2.  Insert your SSH public key (i.e. the one you usually put onto hosts so that you can ssh in without a password, or the one you just created and which ends with *.pub*) into the remote machine's `/etc/dropbear/root_key` or `/etc/tinyssh/root_key` file.
    **Tip:** This method can later be used to add other SSH public keys as needed; In the case of simply copying the content of the remote's `~/.ssh/authorized_keys`, be sure to verify that it only contains keys you intend to be using to unlock the remote machine. When adding additional keys, regenerate your initrd as well using `mkinitcpio`. See also [OpenSSH#Protection](/index.php/OpenSSH#Protection "OpenSSH").

3.  Add all three `<netconf and/or ppp> <dropbear or tinyssh> encryptssh` [hooks](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") before `filesystems` within the "HOOKS" array in `/etc/mkinitcpio.conf` (the `encryptssh` replaces the `encrypt` hook). Then [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").
    **Note:** The `net` hook provided by [mkinitcpio-nfs-utils](https://www.archlinux.org/packages/?name=mkinitcpio-nfs-utils) is **not** needed.

4.  Configure the required `cryptdevice=` [parameter](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") and add the `ip=` [kernel command parameter](/index.php/Kernel_parameters "Kernel parameters") to your bootloader configuration with the appropriate arguments. For example, if the DHCP server does not attribute a static IP to your remote system, making it difficult to access via SSH across reboots, you can explicitly state the IP you want to be using: `ip=192.168.1.1:::::eth0:none` Alternatively, you can also specify the subnet mask and gateway required by the network: `ip=192.168.1.1::192.168.1.254:255.255.255.0::eth0:none` 
    **Note:** As of version 0.0.4 of [mkinitcpio-netconf](https://aur.archlinux.org/packages/mkinitcpio-netconf/), you can nest multiple `ip=` parameters in order to configure multiple interfaces. You cannot mix it with `ip=dhcp` (`ip=:::::eth0:dhcp`) alone. An interface needs to be specified.
     `ip=ip=192.168.1.1:::::eth0:none:ip=172.16.1.1:::::eth1:none` For a detailed description have a look at the [according mkinitcpio section](/index.php/Mkinitcpio#Using_net "Mkinitcpio"). When finished, update the configuration of your [bootloader](/index.php/Bootloader "Bootloader").
5.  Finally, restart the remote system and try to [ssh to it](/index.php/OpenSSH#Client_usage "OpenSSH"), **explicitly stating the "root" username** (even if the root account is disabled on the machine, this root user is used only in the initrd for the purpose of unlocking the remote system). If you are using the [mkinitcpio-dropbear](https://aur.archlinux.org/packages/mkinitcpio-dropbear/) package and you also have the [openssh](https://www.archlinux.org/packages/?name=openssh) package installed, then you most probably will not get any warnings before logging in, because it convert and use the same host keys openssh uses (except Ed25519 keys, as dropbear does not support them). In case you are using [mkinitcpio-tinyssh](https://aur.archlinux.org/packages/mkinitcpio-tinyssh/), you have the option of installing [tinyssh-convert](https://aur.archlinux.org/packages/tinyssh-convert/) or [tinyssh-convert-git](https://aur.archlinux.org/packages/tinyssh-convert-git/) so you can use the same keys as your [openssh](https://www.archlinux.org/packages/?name=openssh) installation (currently only Ed25519 keys). In either case, you should have run [the ssh daemon](/index.php/OpenSSH#Daemon_management "OpenSSH") at least once, using the provided systemd units, so the keys can be generated first. After rebooting the machine, you should be prompted for the passphrase to unlock the root device. The system will complete its boot process and you can then ssh to it [as you normally would](/index.php/OpenSSH#Client_usage "OpenSSH") (with the remote user of your choice).

**Tip:** If you would simply like a nice solution to mount other encrypted partitions (such as `/home`) remotely, you may want to look at [this forum thread](https://bbs.archlinux.org/viewtopic.php?pid=880484).

### Remote unlock via wifi (hooks: build your own)

The net hook is normally used with an ethernet connection. In case you want to setup a computer with wireless only, and unlock it via wifi, you can create a custom hook to connect to a wifi network before the net hook is run.

Below example shows a setup using a usb wifi adapter, connecting to a wifi network protected with WPA2-PSK. In case you use for example WEP or another boot loader, you might need to change some things.

1.  Modify `/etc/mkinitcpio.conf`:
    *   Add the needed kernel module for your specific wifi adatper.
    *   Include the `wpa_passphrase` and `wpa_supplicant` binaries.
    *   Add a hook `wifi` (or a name of your choice, this is the custom hook that will be created) before the `net` hook.
        ```
        MODULES=(*module*)
        BINARIES=(wpa_passphrase wpa_supplicant)
        HOOKS=(base udev autodetect ... **wifi** net ... dropbear encryptssh ...)
        ```

2.  Create the `wifi` hook in `/etc/initcpio/hooks/wifi`:
    ```
    run_hook ()
    {
    	# sleep a couple of seconds so wlan0 is setup by kernel
    	sleep 5

    	# set wlan0 to up
    	ip link set wlan0 up

    	# assocciate with wifi network
    	# 1\. save temp config file
    	wpa_passphrase "*network ESSID*" "*pass phrase*" > /tmp/wifi

    	# 2\. assocciate
    	wpa_supplicant -B -D nl80211,wext -i wlan0 -c /tmp/wifi

    	# sleep a couple of seconds so that wpa_supplicant finishes connecting
    	sleep 5

    	# wlan0 should now be connected and ready to be assigned an ip by the net hook
    }

    run_cleanuphook ()
    {
    	# kill wpa_supplicant running in the background
    	killall wpa_supplicant

    	# set wlan0 link down
    	ip link set wlan0 down

    	# wlan0 should now be fully disconnected from the wifi network
    }
    ```

3.  Create the hook installation file in `/etc/initcpio/install/wifi`:
    ```
    build ()
    {
    	add_runscript
    }
    help ()
    {
    cat<<HELPEOF
    	Enables wifi on boot, for dropbear ssh unlocking of disk.
    HELPEOF
    }
    ```

4.  Add `ip=:::::wlan0:dhcp` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). Remove `ip=:::::eth0:dhcp` so it does not conflict.
5.  Optionally create an additional boot entry with kernel parameter `ip=:::::eth0:dhcp`.
6.  [Regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").
7.  Update the configuration of your [boot loader](/index.php/Boot_loader "Boot loader").

Remember to setup [wifi](/index.php/Wifi "Wifi"), so you are able to login once the system is fully booted. In case you are unable to connect to the wifi network, try increasing the sleep times a bit.

## Discard/TRIM support for solid state drives (SSD)

[Solid state drive](/index.php/Solid_state_drive "Solid state drive") users should be aware that, by default, TRIM commands are not enabled by the device-mapper, i.e. block-devices are mounted without the `discard` option unless you override the default.

The device-mapper maintainers have made it clear that TRIM support will never be enabled by default on dm-crypt devices because of the potential security implications.[[3]](http://www.saout.de/pipermail/dm-crypt/2011-September/002019.html)[[4]](http://www.saout.de/pipermail/dm-crypt/2012-April/002420.html) Minimal data leakage in the form of freed block information, perhaps sufficient to determine the filesystem in use, may occur on devices with TRIM enabled. An illustration and discussion of the issues arising from activating TRIM is available in the [blog](http://asalor.blogspot.de/2011/08/trim-dm-crypt-problems.html) of a *cryptsetup* developer. If you are worried about such factors, keep also in mind that threats may add up: for example, if your device is still encrypted with the previous (cryptsetup <1.6.0) default cipher `--cipher aes-cbc-essiv`, more information leakage may occur from trimmed sector observation than with the current [default](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption").

The following cases can be distinguished:

*   The device is encrypted with default dm-crypt LUKS mode:
    *   By default the LUKS header is stored at the beginning of the device and using TRIM is useful to protect header modifications. If for example a compromised LUKS password is revoked, without TRIM the old header will in general still be available for reading until overwritten by another operation; if the drive is stolen in the meanwhile, the attackers could in theory find a way to locate the old header and use it to decrypt the content with the compromised password. See [cryptsetup FAQ, section 5.19 What about SSDs, Flash and Hybrid Drives?](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#5-security-aspects) and [Full disk encryption on an ssd](https://www.reddit.com/r/archlinux/comments/2f370s/full_disk_encryption_on_an_ssd/ck5p5c5).
    *   TRIM can be left disabled if the security issues stated at the top of this section are considered a worse threat than the above bullet.

	See also [Securely wipe disk#Flash memory](/index.php/Securely_wipe_disk#Flash_memory "Securely wipe disk").

*   The device is encrypted with dm-crypt plain mode, or the LUKS header is stored [separately](#Encrypted_system_using_a_detached_LUKS_header):
    *   If plausible deniability is required, TRIM should **never** be used because of the considerations at the top of this section, or the use of encryption will be given away.
    *   If plausible deniability is not required, TRIM can be used for its performance gains, provided that the security dangers described at the top of this section are not of concern.

**Warning:** Before enabling TRIM on a drive, make sure the device fully supports TRIM commands, or data loss can occur. See [Solid State Drives#TRIM](/index.php/Solid_State_Drives#TRIM "Solid State Drives").

In [linux](https://www.archlinux.org/packages/?name=linux) 3.1 and up, support for dm-crypt TRIM pass-through can be toggled upon device creation or mount with dmsetup. Support for this option also exists in [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) version 1.4.0 and up. To add support during boot, you will need to add `:allow-discards` to the `cryptdevice` option. The TRIM option may look like this:

```
cryptdevice=/dev/sdaX:root:allow-discards

```

For the main `cryptdevice` configuration options before the `:allow-discards` see [Dm-crypt/System configuration](/index.php/Dm-crypt/System_configuration "Dm-crypt/System configuration").

If you are using a systemd based initrd, you must pass:

```
rd.luks.options=discard

```

**Note:** The `rd.luks.options=discard` kernel option does not have any effect on devices included in the initramfs image's `/etc/crypttab` file (`/etc/crypttab.initramfs` on real root). You must specify option `discard` in `/etc/crypttab.initramfs`.

Besides the kernel option, it is also required to periodically run `fstrim` or mount the filesystem (e.g. `/dev/mapper/root` in this example) with the `discard` option in `/etc/fstab`. For details, please refer to the [TRIM](/index.php/TRIM "TRIM") page.

For LUKS devices unlocked via `/etc/crypttab` use option `discard`, e.g.:

 `/etc/crypttab`  `luks-123abcdef-etc UUID=123abcdef-etc none discard` 

When manually unlocking devices on the console use `--allow-discards`.

With LUKS2 you can set `allow-discards` as a default flag for a device by opening it once with the option `--persistent`:

```
# cryptsetup --allow-discards --persistent open --type luks2 /dev/sdaX root

```

You can confirm the flag is persistently set in the LUKS2 header by looking at the `cryptsetup luksDump` output:

 `# cryptsetup luksDump /dev/sdaX | grep Flags` 
```
Flags:          allow-discards

```

In any case, you can verify whether the device actually was opened with discards by inspecting the `dmsetup table` output:

 `# dmsetup table` 
```
luks-123abcdef-etc: 0 1234567 crypt aes-xts-plain64 000etc000 0 8:2 4096 1 allow_discards

```

## The encrypt hook and multiple disks

**Tip:** `sd-encrypt` hook supports unlocking multiple devices. They can be specified on the kernel command line or in `/etc/crypttab.initramfs`. See [dm-crypt/System configuration#Using sd-encrypt hook](/index.php/Dm-crypt/System_configuration#Using_sd-encrypt_hook "Dm-crypt/System configuration").

The `encrypt` hook only allows for a **single** `cryptdevice=` entry ([FS#23182](https://bugs.archlinux.org/task/23182)). In system setups with multiple drives this may be limiting, because *dm-crypt* has no feature to exceed the physical device. For example, take "LVM on LUKS": The entire LVM exists inside a LUKS mapper. This is perfectly fine for a single-drive system, since there is only one device to decrypt. But what happens when you want to increase the size of the LVM? You cannot, at least not without modifying the `encrypt` hook.

The following sections briefly show alternatives to overcome the limitation. The first deals with how to expand a [LUKS on LVM](/index.php/Dm-crypt/Encrypting_an_entire_system#LUKS_on_LVM "Dm-crypt/Encrypting an entire system") setup to a new disk. The second with modifying the `encrypt` hook to unlock multiple disks in LUKS setups without LVM.

### Expanding LVM on multiple disks

The management of multiple disks is a basic [LVM](/index.php/LVM "LVM") feature and a major reason for its partitioning flexibility. It can also be used with *dm-crypt*, but only if LVM is employed as the first mapper. In such a [LUKS on LVM](/index.php/Dm-crypt/Encrypting_an_entire_system#LUKS_on_LVM "Dm-crypt/Encrypting an entire system") setup the encrypted devices are created inside the logical volumes (with a separate passphrase/key per volume). The following covers the steps to expand that setup to another disk.

**Warning:** Back up! While resizing filesystems may be standard, keep in mind that operations **may** go wrong and the following might not apply to a particular setup. Generally, extending a filesystem to free disk space is less problematic than shrinking one. This in particular applies when stacked mappers are used, as it is the case in the following example.

#### Adding a new drive

First, it may be desired to prepare a new disk according to [dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation"). Second, it is partitioned as a LVM, e.g. all space is allocated to `/dev/sdY1` with partition type `8E00` (Linux LVM). Third, the new disk/partition is attached to the existing LVM volume group, e.g.:

```
# pvcreate /dev/sdY1
# vgextend MyStorage /dev/sdY1

```

#### Extending the logical volume

For the next step, the final allocation of the new diskspace, the logical volume to be extended has to be unmounted. It can be performed for the `cryptdevice` root partition, but in this case the procedure has to be performed from an Arch Install ISO.

In this example, it is assumed that the logical volume for `/home` (lv-name `homevol`) is going to be expanded with the fresh disk space:

```
# umount /home
# fsck /dev/mapper/home
# cryptsetup luksClose /dev/mapper/home
# lvextend -l +100%FREE MyStorage/homevol

```

Now the logical volume is extended and the LUKS container comes next:

```
# cryptsetup open /dev/MyStorage/homevol home
# umount /home      # as a safety, in case it was automatically remounted
# cryptsetup --verbose resize home

```

Finally, the filesystem itself is resized:

```
# e2fsck -f /dev/mapper/home
# resize2fs /dev/mapper/home

```

Done! If it went to plan, `/home` can be remounted and now includes the span to the new disk:

```
# mount /dev/mapper/home /home

```

Note that the `cryptsetup resize` action does not affect encryption keys, and these have not changed.

### Modifying the encrypt hook for multiple partitions

#### Root filesystem spanning multiple partitions

It is possible to modify the encrypt hook to allow multiple hard drive decrypt root (`/`) at boot. One way:

```
# cp /usr/lib/initcpio/install/encrypt /etc/initcpio/install/encrypt2
# cp /usr/lib/initcpio/hooks/encrypt  /etc/initcpio/hooks/encrypt2
# sed -i "s/cryptdevice/cryptdevice2/" /etc/initcpio/hooks/encrypt2
# sed -i "s/cryptkey/cryptkey2/" /etc/initcpio/hooks/encrypt2

```

Add `cryptdevice2=` to your boot options (and `cryptkey2=` if needed), and add the `encrypt2` hook to your [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") before rebuilding it. See [dm-crypt/System configuration](/index.php/Dm-crypt/System_configuration "Dm-crypt/System configuration").

#### Multiple non-root partitions

Maybe you have a requirement for using the `encrypt` hook on a non-root partition. Arch does not support this out of the box, however, you can easily change the cryptdev and cryptname values in `/lib/initcpio/hooks/encrypt` (the first one to your `/dev/sd*` partition, the second to the name you want to attribute). That should be enough.

The big advantage is you can have everything automated, while setting up `/etc/crypttab` with an external key file (i.e. the keyfile is not on any internal hard drive partition) can be a pain - you need to make sure the USB/FireWire/... device gets mounted before the encrypted partition, which means you have to change the order of `/etc/fstab` (at least).

Of course, if the [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) package gets upgraded, you will have to change this script again. Unlike `/etc/crypttab`, only one partition is supported, but with some further hacking one should be able to have multiple partitions unlocked.

If you want to do this on a software RAID partition, there is one more thing you need to do. Just setting the `/dev/mdX` device in `/lib/initcpio/hooks/encrypt` is not enough; the `encrypt` hook will fail to find the key for some reason, and not prompt for a passphrase either. It looks like the RAID devices are not brought up until after the `encrypt` hook is run. You can solve this by putting the RAID array in `/boot/grub/menu.lst`, like

```
kernel /boot/vmlinuz-linux md=1,/dev/hda5,/dev/hdb5

```

If you set up your root partition as a RAID, you will notice the similarities with that setup. [GRUB](/index.php/GRUB "GRUB") can handle multiple array definitions just fine:

```
kernel /boot/vmlinuz-linux root=/dev/md0 ro md=0,/dev/sda1,/dev/sdb1 md=1,/dev/sda5,/dev/sdb5,/dev/sdc5

```

## Encrypted system using a detached LUKS header

This example follows the same setup as in [dm-crypt/Encrypting an entire system#Plain dm-crypt](/index.php/Dm-crypt/Encrypting_an_entire_system#Plain_dm-crypt "Dm-crypt/Encrypting an entire system"), which should be read first before following this guide.

By using a detached header the encrypted blockdevice itself only carries encrypted data, which gives [deniable encryption](https://en.wikipedia.org/wiki/Deniable_encryption "wikipedia:Deniable encryption") as long as the existence of a header is unknown to the attackers. It is similar to using [plain dm-crypt](/index.php/Dm-crypt/Encrypting_an_entire_system#Plain_dm-crypt "Dm-crypt/Encrypting an entire system"), but with the LUKS advantages such as multiple passphrases for the masterkey and key derivation. Further, using a detached header offers a form of two factor authentication with an easier setup than [using GPG or OpenSSL encrypted keyfiles](#Using_GPG,_LUKS,_or_OpenSSL_Encrypted_Keyfiles), while still having a built-in password prompt for multiple retries. See [Disk encryption#Cryptographic metadata](/index.php/Disk_encryption#Cryptographic_metadata "Disk encryption") for more information.

See [dm-crypt/Device encryption#Encryption options for LUKS mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") for encryption options before performing the first step to setup the encrypted system partition and creating a header file to use with `cryptsetup`:

```
# dd if=/dev/zero of=header.img bs=16M count=1
# cryptsetup luksFormat --type luks2 /dev/sdX --align-payload 32768 --header header.img

```

**Tip:** When using option `--header`, `--align-payload` allows specifying the start of encrypted data on a device. By reserving a space at the beginning of device you have the option of later [reattaching the LUKS header](/index.php/Dm-crypt/Device_encryption#Restore_using_cryptsetup "Dm-crypt/Device encryption"). See [cryptsetup(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cryptsetup.8) for values supported by `--align-payload`.

Open the container:

```
# cryptsetup open --header header.img /dev/sdX enc

```

Now follow the [LVM on LUKS setup](/index.php/Dm-crypt/Encrypting_an_entire_system#Preparing_the_non-boot_partitions "Dm-crypt/Encrypting an entire system") to your requirements. The same applies for [preparing the boot partition](/index.php/Dm-crypt/Encrypting_an_entire_system#Preparing_the_boot_partition_4 "Dm-crypt/Encrypting an entire system") on the removable device (because if not, there is no point in having a separate header file for unlocking the encrypted disk). Next move the `header.img` onto it:

```
# mv header.img /mnt/boot

```

Follow the installation procedure up to the mkinitcpio step (you should now be `arch-chroot`ed inside the encrypted system).

**Tip:** You will notice that since the system partition only has "random" data, it does not have a partition table and by that an `UUID` or a `LABEL`. But you can still have a consistent mapping using the [Persistent block device naming#by-id and by-path](/index.php/Persistent_block_device_naming#by-id_and_by-path "Persistent block device naming"). E.g. using disk id from `/dev/disk/by-id/`.

There are two options for initramfs to support a detached LUKS header.

### Using systemd hook

First create `/etc/crypttab.initramfs` and add the encrypted device to it. The syntax is defined in [crypttab(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/crypttab.5)

 `/etc/crypttab.initramfs`  `enc	/dev/disk/by-id/*your-disk_id*	none	header=/boot/header.img` 

Modify `/etc/mkinitcpio.conf` [to use systemd](/index.php/Mkinitcpio#Common_hooks "Mkinitcpio") and add the header to `FILES`.

 `/etc/mkinitcpio.conf` 
```
...
FILES=(**/boot/header.img**)
...
HOOKS=(base **systemd** autodetect **keyboard** **sd-vconsole** modconf block **sd-encrypt** **sd-lvm2** filesystems fsck)
...
```

[Regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs") and you are done.

**Note:** No cryptsetup parameters need to be passed to the kernel command line, since`/etc/crypttab.initramfs` will be added as `/etc/crypttab` in the initramfs. If you wish to specify them in the kernel command line see [dm-crypt/System configuration#Using sd-encrypt hook](/index.php/Dm-crypt/System_configuration#Using_sd-encrypt_hook "Dm-crypt/System configuration") for the supported options.

### Modifying encrypt hook

This method shows how to modify the `encrypt` hook in order to use a detached LUKS header. Now the `encrypt` hook has to be modified to let `cryptsetup` use the separate header ([FS#42851](https://bugs.archlinux.org/task/42851); base source and idea for these changes [published on the BBS](https://bbs.archlinux.org/viewtopic.php?pid=1076346#p1076346)). Make a copy so it is not overwritten on a [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") update:

```
# cp /usr/lib/initcpio/hooks/encrypt /etc/initcpio/hooks/encrypt2
# cp /usr/lib/initcpio/install/encrypt /etc/initcpio/install/encrypt2

```
 `/etc/initcpio/hooks/encrypt2 (around line 52)` 
```
warn_deprecated() {
    echo "The syntax 'root=${root}' where '${root}' is an encrypted volume is deprecated"
    echo "Use 'cryptdevice=${root}:root root=/dev/mapper/root' instead."
}

**local headerFlag=false**
for cryptopt in ${cryptoptions//,/ }; do
    case ${cryptopt} in
        allow-discards)
            cryptargs="${cryptargs} --allow-discards"
            ;;  
        **header)
            cryptargs="${cryptargs} --header /boot/header.img"
            headerFlag=true
            ;;**
        *)  
            echo "Encryption option '${cryptopt}' not known, ignoring." >&2 
            ;;  
    esac
done

if resolved=$(resolve_device "${cryptdev}" ${rootdelay}); then
    if **$headerFlag ||** cryptsetup isLuks ${resolved} >/dev/null 2>&1; then
        [ ${DEPRECATED_CRYPT} -eq 1 ] && warn_deprecated
        dopassphrase=1
```

Now edit the [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") to add the `encrypt2` and `lvm2` hooks, the `header.img` to `FILES` and the `loop` to `MODULES`, apart from other configuration the system requires:

 `/etc/mkinitcpio.conf` 
```
...
MODULES=(**loop**)
...
FILES=(**/boot/header.img**)
...
HOOKS=(base udev autodetect **keyboard** **keymap** consolefont modconf block **encrypt2** **lvm2** filesystems fsck)
...
```

This is required so the LUKS header is available on boot allowing the decryption of the system, exempting us from a more complicated setup to mount another separate USB device in order to access the header. After this set up [the initramfs](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") is created.

Next the [boot loader is configured](/index.php/Dm-crypt/Encrypting_an_entire_system#Configuring_the_boot_loader_4 "Dm-crypt/Encrypting an entire system") to specify the `cryptdevice=` also passing the new `header` option for this setup:

```
cryptdevice=/dev/disk/by-id/*your-disk_id*:enc:header

```

To finish, following [dm-crypt/Encrypting an entire system#Post-installation](/index.php/Dm-crypt/Encrypting_an_entire_system#Post-installation "Dm-crypt/Encrypting an entire system") is particularly useful with a `/boot` partition on an USB storage medium.

## Encrypted /boot and a detached LUKS header on USB

Rather than embedding the `header.img` and keyfile into the [initramfs](/index.php/Initramfs "Initramfs") image, this setup will make your system depend entirely on the usb key rather than just the image to boot, and on the encrypted keyfile inside of the encrypted boot partition. Since the header and keyfile are not included in the [initramfs](/index.php/Initramfs "Initramfs") image and the custom encrypt hook is specifically for the usb's [by-id](/index.php/Persistent_block_device_naming#by-id_and_by-path "Persistent block device naming"), you will literally need the usb key to boot.

For the usb drive, since you are encrypting the drive and the keyfile inside, it is preferred to cascade the ciphers as to not use the same one twice. Whether a [meet-in-the-middle](https://en.wikipedia.org/wiki/Meet-in-the-middle_attack "wikipedia:Meet-in-the-middle attack") attack would actually be feasible is debatable. You can do twofish-serpent or serpent-twofish.

### Preparing the disk devices

`sdb` will be assumed to be the USB drive, `sda` will be assumed to be the main hard drive.

Prepare the devices according to [dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation").

#### Preparing the USB key

Use [gdisk](/index.php/Gdisk "Gdisk") to partition the disk according to the layout [shown here](/index.php/Dm-crypt/Encrypting_an_entire_system#Preparing_the_disk_5 "Dm-crypt/Encrypting an entire system"), with the exception that it should only include the first two partitions. So as follows:

 `# gdisk /dev/sdb` 
```
Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048         1050623   512.0 MiB   EF00  EFI System
   2         1050624         1460223   200.0 MiB   8300  Linux filesystem

```

Before running `cryptsetup`, look at the [Encryption options for LUKS mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") and [Ciphers and modes of operation](/index.php/Disk_encryption#Ciphers_and_modes_of_operation "Disk encryption") first to select your desired settings.

[Prepare the boot partition](/index.php/Dm-crypt/Encrypting_an_entire_system#Preparing_the_boot_partition_5 "Dm-crypt/Encrypting an entire system") but do not `mount` any partition yet and [Format the EFI system partition](/index.php/EFI_system_partition#Format_the_partition "EFI system partition").

```
# mount /dev/mapper/cryptboot /mnt
# dd if=/dev/urandom of=/mnt/key.img bs=*filesize* count=1
# cryptsetup --align-payload=1 luksFormat /mnt/key.img
# cryptsetup open /mnt/key.img lukskey

```

*filesize* is in bytes but can be followed by a suffix such as `M`. Having too small of a file will get you a nasty `Requested offset is beyond real size of device /dev/loop0` error. As a rough reference, creating a 4M file will encrypt it successfully. You should make the file larger than the space needed since the encrypted loop device will be a little smaller than the file's size.

With a big file, you can use `--keyfile-offset=*offset*` and `--keyfile-size=*size*` to navigate to the correct position. [[5]](https://wiki.gentoo.org/wiki/Custom_Initramfs#Encrypted_keyfile)

Now you should have `lukskey` opened in a loop device (underneath `/dev/loop1`), mapped as `/dev/mapper/lukskey`.

#### The main drive

```
# truncate -s 2M /mnt/header.img
# cryptsetup --key-file=/dev/mapper/lukskey --keyfile-offset=*offset* --keyfile-size=*size* luksFormat /dev/sda --align-payload 4096 --header /mnt/header.img

```

Pick an *offset* and *size* in bytes (8192 bytes is the maximum keyfile size for `cryptsetup`).

```
# cryptsetup open --header /mnt/header.img --key-file=/dev/mapper/lukskey --keyfile-offset=*offset* --keyfile-size=*size* /dev/sda enc 
# cryptsetup close lukskey
# umount /mnt

```

Follow [Preparing the logical volumes](/index.php/Dm-crypt/Encrypting_an_entire_system#Preparing_the_logical_volumes "Dm-crypt/Encrypting an entire system") to set up LVM on LUKS.

See [Partitioning#Discrete partitions](/index.php/Partitioning#Discrete_partitions "Partitioning") for recommendations on the size of your partitions.

Once your root partition is mounted, `mount` your encrypted boot partition as `/mnt/boot` and your EFI system partition as `/mnt/efi`.

### Installation procedure and custom encrypt hook

Follow the [installation guide](/index.php/Installation_guide "Installation guide") up to the `mkinitcpio` step but do not do it yet, and skip the partitioning, formatting, and mounting steps as they have already been done.

In order to get the encrypted setup to work, you need to build your own hook, which is thankfully easy to do and here is the code you need. You will have to follow [Persistent block device naming#by-id and by-path](/index.php/Persistent_block_device_naming#by-id_and_by-path "Persistent block device naming") to figure out your own `by-id` values for the usb and main hard drive (they are linked -> to `sda` or `sdb`).

You should be using the `by-id` instead of just `sda` or `sdb` because `sdX` can change and this ensures it is the correct device.

You can name `customencrypthook` anything you want, and custom build hooks can be placed in the `hooks` and `install` folders of `/etc/initcpio`. Keep a backup of both files (`cp` them over to the `/home` partition or your user's `/home` directory after you make one). `/usr/bin/ash` is not a typo.

 `/etc/initcpio/hooks/customencrypthook` 
```
#!/usr/bin/ash

run_hook() {
    modprobe -a -q dm-crypt >/dev/null 2>&1
    modprobe loop
    [ "${quiet}" = "y" ] && CSQUIET=">/dev/null"

    while [ ! -L '/dev/disk/by-id/*usbdrive*-part2' ]; do
     echo 'Waiting for USB'
     sleep 1
    done

    cryptsetup open /dev/disk/by-id/*usbdrive*-part2 cryptboot
    mkdir -p /mnt
    mount /dev/mapper/cryptboot /mnt
    cryptsetup open /mnt/key.img lukskey
    cryptsetup --header /mnt/header.img --key-file=/dev/mapper/lukskey --keyfile-offset=''offset'' --keyfile-size=''size'' open /dev/disk/by-id/*harddrive* enc
    cryptsetup close lukskey
    umount /mnt
}

```

`*usbdrive*` is your USB drive `by-id`, and `*harddrive*` is your main hard drive `by-id`.

**Tip:** You could also close `cryptboot` using `cryptsetup close`, but having it open makes it easier to mount for system updates using [Pacman](/index.php/Pacman "Pacman") and regenerating the initramfs with [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"). The `/boot` partition must be mounted for updates that affect the [kernel](/index.php/Kernel "Kernel") or [Initramfs](/index.php/Initramfs "Initramfs"), and the initramfs will be automatically regenerated after these updates.

```
# cp /usr/lib/initcpio/install/encrypt /etc/initpcio/install/customencrypthook

```

Now edit the copied file and remove the `help()` section as it is not necessary.

 `/etc/mkinitcpio.conf (edit this only do not replace it, these are just excerpts of the necessary parts)` 
```
MODULES=(loop)
...
HOOKS=(base udev autodetect modconf block customencrypthook lvm2 filesystems keyboard fsck)
```

The `files=()` and `binaries=()` arrays are empty, and you should not have to replace `HOOKS=(...)` array entirely just edit in `customencrypthook lvm2` after `block` and before `filesystems`, and make sure `systemd`, `sd-lvm2`, and `encrypt` are removed.

#### Boot Loader

Finish the [Installation Guide](/index.php/Installation_guide#Initramfs "Installation guide") from the `mkinitcpio` step. To boot you would need either [GRUB](/index.php/GRUB "GRUB") or [efibootmgr](/index.php/Efibootmgr "Efibootmgr"). Note you can use [GRUB](/index.php/GRUB "GRUB") to support the encrypted disks by [Configuring the boot loader](/index.php/Dm-crypt/Encrypting_an_entire_system#Configuring_the_boot_loader_6 "Dm-crypt/Encrypting an entire system") but editing the `GRUB_CMDLINE_LINUX` is not necessary for this set up.

Or use Direct UEFI Secure boot by generating keys with [cryptboot](https://aur.archlinux.org/packages/cryptboot/) then signing the initramfs and kernel and creating a bootable *.efi* file for your EFI system partition with [sbupdate-git](https://aur.archlinux.org/packages/sbupdate-git/). Before using cryptboot or sbupdate note this excerpt from [Secure Boot#Using your own keys](/index.php/Secure_Boot#Using_your_own_keys "Secure Boot"):

**Tip:** Note that [cryptboot](https://aur.archlinux.org/packages/cryptboot/) requires the encrypted boot partition to be specified in `/etc/crypttab` before it runs, and if you are using it in combination with [sbupdate-git](https://aur.archlinux.org/packages/sbupdate-git/), sbupdate expects the `/boot/efikeys/db.*` files created by cryptboot to be capitalized like `DB.*` unless otherwise configured in `/etc/default/sbupdate`. Users who do not use systemd to handle encryption may not have anything in their `/etc/crypttab` file and would need to create an entry.

```
# efibootmgr -c -d /dev/*device* -p *partition_number* -L "Arch Linux Signed" -l "EFI\Arch\linux-signed.efi"

```

See [efibootmgr(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/efibootmgr.8) for an explanation of the options.

Make sure the boot order puts `Arch Linux Signed` first. If not change it with `efibootmgr -o XXXX,YYYY,ZZZZ`.

### Changing the LUKS keyfile

```
# cryptsetup --header /boot/header.img --key-file=/dev/mapper/lukskey --keyfile-offset=*offset* --keyfile-size=*size* luksChangeKey /dev/mapper/enc /dev/mapper/lukskey2 --new-keyfile-size=*newsize* --new-keyfile-offset=*newoffset*

```

Afterwards, `cryptsetup close lukskey` and [shred](/index.php/Shred "Shred") or [dd](/index.php/Securely_wipe_disk#dd "Securely wipe disk") the old keyfile with random data before deleting it, then make sure that the new keyfile is renamed to the same name of the old one: `key.img` or other name.