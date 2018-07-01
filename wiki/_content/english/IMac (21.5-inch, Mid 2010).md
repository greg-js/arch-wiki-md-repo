Despite having Radeon rather than nVidia graphics, [this](https://support.apple.com/kb/sp588?locale=en_US) iMac model suffers from a number of graphics-related problems. The problems I have encountered are:

*   The screen becomes disabled/turned off when [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") kicks in.
*   After resuming from suspend-to-RAM, the screen cannot be re-enabled even with the fix described below.
*   The system produces an interface for controlling a nonexistent backlight in `/sys/class/backlight/acpi_video0`.

## Contents

*   [1 Workaround for the KMS bug](#Workaround_for_the_KMS_bug)
*   [2 Workaround for suspend-and-resume](#Workaround_for_suspend-and-resume)
*   [3 Workaround for the fake backlight control](#Workaround_for_the_fake_backlight_control)
*   [4 Suggestions about the bootloader](#Suggestions_about_the_bootloader)

## Workaround for the KMS bug

During the initial installation process, it is simplest to add `modprobe.blacklist=radeon` to your [kernel command line](/index.php/Kernel_command_line "Kernel command line") when booting from the installation media. I did not attempt to boot in BIOS mode, though I doubt it would make much difference with regards to the black screen. You will need to keep this parameter in your kernel command line until after you have installed a graphical environment, so when you install your desktop environment, be sure to also install [xf86-video-fbdev](https://www.archlinux.org/packages/?name=xf86-video-fbdev). This will allow you to use software rendering and the high-resolution EFI framebuffer until you get the radeon problem sorted out. When you've gotten your graphical environment the way you want, install [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr), and create the following script:

 `/usr/local/bin/fix_display` 
```
#!/usr/bin/bash
/usr/bin/xrandr -d :0 --output eDP-1 --crtc 1

```

Make it executable:

 `sudo chmod +x /usr/local/bin/fix_display` 

Edit your [display manager](/index.php/Display_manager "Display manager")'s configuration so that the script runs while the greeter is starting up. I use [SDDM](/index.php/SDDM "SDDM"), so I configured it like this:

 `/etc/sddm.conf` 
```
[X11]
DisplayCommand=/usr/local/bin/fix_display
```

Note that you may need to first create this file by running `sddm --example-config > /etc/sddm.conf`.

Now, you should be able to remove the `modprobe.blacklist` parameter from your kernel command line and reboot with 3D acceleration supported.

## Workaround for suspend-and-resume

I do not know of any workaround for the suspend-and-resume issue at this time.

## Workaround for the fake backlight control

Add `acpi_backlight=none` to your [kernel command line](/index.php/Kernel_command_line "Kernel command line") and reboot. Your desktop environment should now be able to adjust the screen brightness properly. (Note that you'll have to install the [powerdevil](https://www.archlinux.org/packages/?name=powerdevil) package if you wish to adjust the brightness in [Plasma](/index.php/Plasma "Plasma").)

## Suggestions about the bootloader

Because Mac computers do not have a normal [UEFI](/index.php/UEFI "UEFI"), I advise making your bootloader follow Apple's conventions as much as possible. This will allow you to make the Arch entry in the Option-key boot menu nice and pretty, as well as allowing you to set Arch as the default OS instead of macOS. Here are the rough steps to do this. Consider these instructions a supplement to—not a replacement for—the [installation guide](/index.php/Installation_guide "Installation guide"). They only detail the steps that deviate from the normal install process.

1.  Before installing Arch, create a 1 GiB partition in Disk Utility formatted as MacOS Extended (Journaled). Name it "ArchLinux-Boot".
2.  Run `diskutil disableJournal /dev/disk*X*s*Y*` from the macOS terminal. (Replace *X* and *Y* with the disk and partition numbers from `diskutil list`.)
3.  Create a full-sized partition for the root filesystem and optionally a swap partition in Disk Utility as well. The filesystem doesn't matter for these, as they will be overwritten anyway.
4.  Boot into the install media (don't forget the workaround for graphics above)
5.  Use `gdisk` to change the partition type codes on the root and swap partitions to the proper codes for Linux Filesystem (8300) and Linux Swap (8200).
6.  [Format](/index.php/Format "Format") the partitions with your choice of filesystem.
7.  Mount your newly-formatted root filesystem on `/mnt`. Create the directories `/mnt/esp`, `/mnt/applebootpartition`, and `/mnt/boot`.
8.  Mount the EFI system partition under `/mnt/esp`
9.  Mount the HFS+ filesystem you created in Disk Utility under `/mnt/applebootpartition`.
10.  Run `mkdir -p /mnt/applebootpartition/System/Library/CoreServices /mnt/applebootpartition/loader/entries /mnt/applebootpartition/kernel`. The first set of directories emulates a macOS installation so that it will be picked up by the firmware. The second two are for Linux-specific things, as you'll see later.
11.  Bind-mount `/mnt/applebootpartition/kernel` to `/mnt/boot`
12.  Generate the fstab file. You'll probably need to correct the bind-mount fstab entries to use directories that make sense for the installed system rather than the live environment.
13.  Run `pacstrap` as specified in the main installation guide and chroot into the new system.
14.  Copy `/usr/lib/systemd/boot/efi/systemd-bootx64.efi` to `/applebootpartition/System/Library/CoreServices/boot.efi` and from there configure [systemd-boot](/index.php/Systemd-boot "Systemd-boot") as though `/applebootpartition` were the EFI system partition. `/applebootpartition/kernel` should contain your vmlinuz and [initramfs](/index.php/Initramfs "Initramfs") images.
15.  Create the file `/applebootpartition/mach_kernel` (it should be an empty file). I'm not sure whether this is actually necessary for the firmware to detect the partition as bootable.
16.  Perform any other needed installation steps, then reboot into the installed system by holding down the option key when the iMac boots.