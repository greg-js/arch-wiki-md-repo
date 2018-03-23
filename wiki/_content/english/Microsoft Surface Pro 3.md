**Warning:** The warranty of the device is only valid if the OEM image of Windows is still present. A dual boot, however, will not invalidate the warranty as explained [here](http://answers.microsoft.com/en-us/surface/forum/surfpro-surfusingpro/would-dual-booting-the-surface-pro-void-its/da549e24-f986-4984-b081-25c029882163).

This page aims to document all relevant information on getting Arch Linux working on the Microsoft Surface Pro 3 tablet.

## Contents

*   [1 Booting into the installer](#Booting_into_the_installer)
    *   [1.1 Disable Secure Boot](#Disable_Secure_Boot)
    *   [1.2 Boot with Secure Boot](#Boot_with_Secure_Boot)
*   [2 Installation](#Installation)
*   [3 Extra steps](#Extra_steps)
    *   [3.1 Compile Kernel with Patches](#Compile_Kernel_with_Patches)
        *   [3.1.1 Surface Pro 3 Linux Kernel Hardware Patches](#Surface_Pro_3_Linux_Kernel_Hardware_Patches)
    *   [3.2 Enabling Touchpad](#Enabling_Touchpad)
    *   [3.3 Tuning the Pen](#Tuning_the_Pen)
    *   [3.4 Virtual Keyboard](#Virtual_Keyboard)
    *   [3.5 Booting with Secure Boot Enabled](#Booting_with_Secure_Boot_Enabled)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Invalid signature detected check secure boot policy in setup](#Invalid_signature_detected_check_secure_boot_policy_in_setup)
    *   [4.2 Keyboard Cover not working](#Keyboard_Cover_not_working)
    *   [4.3 Pen/Touchscreen issues in Xournal](#Pen.2FTouchscreen_issues_in_Xournal)

## Booting into the installer

To boot from USB, you will need to instruct the tablet to boot from USB or SD Card. Also, you may want to avoid disabling [Secure Boot](/index.php/UEFI#Secure_Boot "UEFI") as this will cause each boot to display an ugly bright red background intentionally clashing with the "Surface" splash logo.

There are three types of boots in the Surface Pro 3 [explained here](http://www.microsoft.com/surface/en-us/support/storage-files-and-folders/boot-surface-pro-from-usb-recovery-device):

1.  Normal mode
    1.  Just leave the computer go. You can change it from "Alternate Boot order" in the UEFI Setup
2.  Boot into the UEFI Setup
    1.  With the device powered off (or rebooting, but better play safe)
    2.  Press & hold Volume up
    3.  Press power button
    4.  Wait until the surface logo appears
    5.  Release Volume up
    6.  You will be presented with the UEFI Setup Menu
3.  Boot into the USB/SD card
    1.  Power off the device
    2.  Press & hold Volume down
    3.  Press power button
    4.  Wait until the surface logo appears
    5.  Release Volume down

### Disable Secure Boot

**Note:** This will cause a red background before the logo when booting.

Boot into the UEFI setup, and select *Secure Boot Control > Disable*. Now continue with the installation. See the [Microsoft steps](http://www.microsoft.com/surface/en-sg/support/warranty-service-and-recovery/how-to-use-the-bios-uefi) for more information.

### Boot with Secure Boot

See [Secure Boot](/index.php/Secure_Boot "Secure Boot").

## Installation

I have done the installation with systemd's bootctl [Systemd-boot](/index.php/Systemd-boot "Systemd-boot") (old [Gummiboot](/index.php/Gummiboot "Gummiboot")). After doing all the steps of [installation](/index.php/Installation "Installation"), you should do two more things. Booting in Secure Boot won't work for the new installation, as the vmlinuz hasn't been registered within its loader.

The easiest way is to do all the setup is the following, just before rebooting:

1.  Exit from the chroot but don't umount anything
2.  Move /mnt/boot/EFI/boot/bootx64.efi to /mnt/boot/EFI/boot/loader.efi
3.  Copy /boot/EFI/boot/bootx64.efi and HashTool.efi to /mnt/boot/EFI/boot/

(If you are unable to find HashTool in /boot, try in /usr/run)

Here, we have enabled Preloader to boot our gummiboot loader, and if it detects that something hasn't been signed, it will boot the HashTool.efi to sign the vmlinuz-image binary.

The idea is, we take the systemd bootloader and make it the one that PreLoader will boot (the one in its same folder, named loader.efi). Then, we copy both the PreLoader (which is the archiso's bootx64.efi) and the HashTool (already with that name).

This way, with Secure Boot enabled, you will be able to boot your kernel whenever you wish to, signed or not, repeating the hash storing procedure on the next boot.

## Extra steps

Although in latest kernel you have basic support for the touchpad, the screen, etc. the cameras are not yet supported by the kernel. A github repo to track the support of the Surface Pro 3 in Archlinux was created: [[1]](https://github.com/nuclearsandwich/surface3-archlinux), where you can check for the status.

The easiest way for Arch Linux users is to use a Surface Pro 3 specific package available in the AUR [linux-surfacepro3-git](https://aur.archlinux.org/packages/linux-surfacepro3-git/). You can check there the support for the different modules available, or take the patch from upstream[GitHub](https://github.com/matthewwardrop/linux-surfacepro3).

### Compile Kernel with Patches

Ref: [Kernels/Traditional compilation#Configuration](/index.php/Kernels/Traditional_compilation#Configuration "Kernels/Traditional compilation")

**Note:** The most up-to-date source at the time of writing for the kernel patches is [shvr's github repository](https://github.com/shvr/fedora-surface-pro-3-kernel/).

*   Latest stable kernel release: [f23 branch](https://github.com/shvr/fedora-surface-pro-3-kernel/commits/f23)
*   Latest RC: [master branch](https://github.com/shvr/fedora-surface-pro-3-kernel/commits/master)

#### Surface Pro 3 Linux Kernel Hardware Patches

Since kernel 4.3, only the multitouch and camera patches are required.

*   [Camera patch](https://github.com/shvr/fedora-surface-pro-3-kernel/blob/f23/surface-pro-3-Add-support-driver-for-Surface-Pro-3-b.patch)
*   [Hardware Buttons patch](https://github.com/shvr/fedora-surface-pro-3-kernel/blob/f23/Add-Microsoft-Surface-Pro-3-camera-support.patch)
*   [Type Cover patch](https://github.com/shvr/fedora-surface-pro-3-kernel/blob/f23/Add-multitouch-support-for-Microsoft-Type-Cover-3.patch)

**Note:** These patches can be automatically applied using `git-apply` from the [Git](/index.php/Git "Git") package.

### Enabling Touchpad

Ref: [GitHub](https://github.com/matthewwardrop/linux-surfacepro3/issues/1) In order to enable full functionality of the touchpad (e.g. two-finger scrolling, right click), you need to [Install](/index.php/Install "Install") the [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) package, have the kernel patch applied as well as add the following to `/etc/X11/xorg.conf.d/10-multitouch.conf`:

```
Section "InputClass"
  Identifier "Default clickpad buttons"
  MatchDriver "synaptics"
  Option "ClickPad" "true"
  Option "SoftButtonAreas" "50% 0 82% 0 0 0 0 0"
  Option "SecondarySoftButtonAreas" "58% 0 0 15% 42% 58% 0 15%"
EndSection

```

### Tuning the Pen

The pen buttons might not work out of the box. [Install](/index.php/Install "Install") the [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) package and comment the `MatchIsTablet` section in `/usr/share/X11/xorg.conf.d/10-evdev.conf`. Furthermore add `1B96:1B05 Pen` in the `MatchProduct` line of N-Trig in `/usr/share/X11/xorg.conf.d/50-wacom.conf`. Note that the purple bluetooth button is recognized but able to be bound to an action. Ref:[Reddit](https://www.reddit.com/r/SurfaceLinux/comments/3mu28a/sp3_pen_tip_button_working/)

### Virtual Keyboard

Depending on the desktop environment you are using, you might want to use different virtual keyboard. [onboard](https://www.archlinux.org/packages/?name=onboard) provides a reliable and comfortable experience. A guide for optical tweaking is provided [here](https://github.com/Vistaus/surface3-arch-antergoslinux/issues/5). If you are using [GNOME](/index.php/GNOME "GNOME"), these two extension ([1](https://extensions.gnome.org/extension/992/onboard-integration/), [2](https://extensions.gnome.org/extension/993/slide-for-keyboard/)) provide a better integration.

### Booting with Secure Boot Enabled

The recommended bootloader for UEFI with Secure Boot enabled is [systemd-boot](/index.php/Systemd-boot "Systemd-boot")

To boot with Secure Boot, you will need the following packages: [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) [efitools](https://www.archlinux.org/packages/?name=efitools)

Ref: [Surface Pro 3 and Secure Boot post-install](https://bbs.archlinux.org/viewtopic.php?pid=1570523#p1570523)

Copy `/boot/EFI/systemd/systemd-bootx64.efi` to `/boot/EFI/systemd/loader.EFI`. Copy `/usr/lib/prebootloader/HashTool.efi` and `/usr/lib/prebootloader/PreLoader.efi` to `/boot/EFI/systemd/`. Create an NVRAM entry for PreLoader.efi:

```
 efibootmgr -d /dev/sd**X** -p **Y** -c -L Preloader -l /EFI/systemd/PreLoader.efi

```

**Note:** **Y** is the partition number of the /boot partition.

Verify the entry was made and that it is first in the boot order:

```
efibootmgr

```

Enrolling your kernel in the bootloader: [Unified Extensible Firmware Interface#Secure Boot](/index.php/Unified_Extensible_Firmware_Interface#Secure_Boot "Unified Extensible Firmware Interface") Enroll HashTool.efi and vmlinuz-linux, and then reboot to system. You should now be able to boot with Secure Boot enabled.

**Note:** Since PreLoader.efi is the default boot option per [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr), if you change the kernel you will be presented with PreLoader to enroll the new kernel with HashTool again

**Note:** Ensure that you add the entry in `/boot/loader/entries/` so that you are presented the option to boot with the new kernel

## Troubleshooting

### Invalid signature detected check secure boot policy in setup

This happened to me after deleting the Secure Boot database and initializing it with Microsoft & CAs. I also had to do the recovery of the bitlocker partition, but I would follow these steps:

1.  After the reset, switch off and try to boot from the sd/usb. If you don't succeed and get the message many times:
    1.  Leaving all TPM & SecureBoot enabled and SSD Only alternate system order
    2.  Do another database reset
    3.  Enroll the Microsoft and CAs again
    4.  reboot into sd/usb with volume down
    5.  It should work now
2.  Follow steps in the Secure Boot installation
3.  After the full installation of archlinux, when you have it working, do the BitLocker recovery

If after doing these steps doesn't still work. Flash the archiso image once more and try again,

### Keyboard Cover not working

This can happen sometimes when you restart. The solution was to shutdown and reboot. (not restart)

### Pen/Touchscreen issues in Xournal

When using the [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) package there is a bug in the last official release of [xournal](https://www.archlinux.org/packages/?name=xournal) (0.48.2) where it'll incorrectly detect the Surface Pen as the touchscreen device. However it's been fixed in the latest Xournal source as per this [bug](https://sourceforge.net/p/xournal/bugs/144/). Installing the AUR package [xournal-git](https://aur.archlinux.org/packages/xournal-git/) builds the latest source including this fix. Note that you'll need to select 'NTRG0001:01 1B96:1B05' as the touchscreen device (Options > Pen and Touch).