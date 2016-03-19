| **Device** | **Status** | **Modules** |
| Video | Works after configuration | i915 |
| Wireless | Works after configuration | brcmfmac |
| Bluetooth | Works after installing firmware | btbcm |
| Audio | Working | snd_hda_intel |
| Touchpad | Works after configuration |  ? |
| Webcam | Working | uvcvideo |
| Card Reader | Working | rtsx_pci |
| Wireless switch | Will work in Linux 4.6 | intel-hid |
| Function/Multimedia Keys | Working |  ? |

The Dell XPS 13 2016 (9350) is the third-generation model of the XPS 13 line. Unlike its predecessor, it has no official Linux support yet. Just like the older versions ([Dell XPS 13](/index.php/Dell_XPS_13 "Dell XPS 13") and [Dell XPS 13 (2015)](/index.php/Dell_XPS_13_(2015) "Dell XPS 13 (2015)")) it can be bought in different hardware configurations.

The installation process for Arch on the XPS 13 does not differ from any other PC. For installation help, please see the [Installation guide](/index.php/Installation_guide "Installation guide"), [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") and [UEFI](/index.php/UEFI "UEFI"). This page covers the current status of hardware support on Arch, as well as post-installation recommendations.

As of kernel 4.3, the Intel Skylake architecture is supported.

## Contents

*   [1 BIOS updates](#BIOS_updates)
*   [2 SATA controller](#SATA_controller)
*   [3 NVM Express SSD](#NVM_Express_SSD)
    *   [3.1 Cannot find root device](#Cannot_find_root_device)
    *   [3.2 Note on Mount Options](#Note_on_Mount_Options)
*   [4 Wireless](#Wireless)
*   [5 Bluetooth](#Bluetooth)
*   [6 Video](#Video)
*   [7 Touchpad](#Touchpad)
*   [8 Sound](#Sound)
    *   [8.1 PulseAudio Workaround](#PulseAudio_Workaround)
*   [9 Microphone](#Microphone)
*   [10 Links](#Links)

## BIOS updates

[BIOS update 1.2.3](http://www.dell.com/support/home/us/en/04/Drivers/DriversDetails?driverId=T0R1K) was released on 2016-01-29\. Store the update binary on your EFI partition (`/boot/EFI`) or on a USB flash drive, reboot, and choose BIOS Update in the F12 boot menu.

## SATA controller

When the SATA-controller is set to "RAID On" in Bios, the hard disk (at least the SSD) is not recognized. Set to "Off" or "AHCI" before attempting to install Arch. If dual boot to Windows is intended, follow [[1]](https://support.microsoft.com/en-us/kb/2795397) to work around the "INACCESSIBLE_BOOT_DEVICE" error.

## NVM Express SSD

### Cannot find root device

The location of the `nvme` module for ["NVM Express"](https://en.wikipedia.org/wiki/NVM_Express "wikipedia:NVM Express") SSD has changed between [linux](https://www.archlinux.org/packages/?name=linux) kernel version 4.3 and 4.4\. If you experience "cannot find root device" on boot, it may be due to the [`nvme` module not being present in `initramfs`](https://bugs.archlinux.org/task/47761). In this case, the following may resolve your issue.

Edit your `/etc/mkinitcpio.conf` file:

```
   ...
   MODULES="... nvme"
   ...

```

Then update the bootloader.

```
   # mkinitcpio -p linux

```

where `linux` is the name of the image loaded on boot. If you installed [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/) then change that to `linux-mainline`.

### Note on Mount Options

As reported by a few users on [the forum](https://bbs.archlinux.org/viewtopic.php?pid=1593544#p1593544) using the `discard` mount option for your filesystem is not recommended by Intel in [the reference guide of the driver](https://downloadmirror.intel.com/23929/eng/Intel_Linux_NVMe_Driver_Reference_Guide_330602-002.pdf).

An answer from [Intel Communities](https://communities.intel.com/thread/75161?start=0&tstart=0) suggests that the best option is to use the `fstrim` timer which is provided by [util-linux](https://www.archlinux.org/packages/?name=util-linux) and can be enabled simply through:

```
# systemctl enable fstrim.timer

```

## Wireless

The built-in Broadcom BCM4350 is now supported in the current [linux](https://www.archlinux.org/packages/?name=linux) kernel (as of version 4.4.1-1). The wireless module `brcmfmac` also needs the firmware `brcmfmac4350-pcie.bin` from the related [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) package.

If you have not already done so, enable the testing repository to retrieve the package in `/etc/pacman.conf`:

```
 # The testing repositories are disabled by default. To enable, uncomment the
 # repo name header and Include lines. You can add preferred servers immediately
 # after the header, and they will be used before the default mirrors.

 [core]
 Include = /etc/pacman.d/mirrorlist

 [testing]
 Include = /etc/pacman.d/mirrorlist

```

The order matters. If you put the `[testing]` repository before `[core]` you are setting `pacman` to default to the *testing* repository for all packages. Otherwise only packages that you install with `# pacman -S testing/*package-name*` will be pulled from the *testing* repository. This way is preferred if you only need the [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) from *testing* and want to keep on *core* for others. You might want to install `testing/linux` as well, but it is not mandatory if both the core and testing versions are on the same major version.

## Bluetooth

**Note:** **Intel WiFi users:** If your WiFi card supports Bluetooth, then the BT interface should be available out-of-the-box, as the required firmware is included in [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware).

The Broadcom Bluetooth firmware is not available in the kernel (the same as for 2015 model [source](http://tech.sybreon.com/2015/03/15/xps13-9343-ubuntu-linux/)), so you will have to retrieve it from the [[2]](http://downloads.dell.com/FOLDER03272920M/1/9350_Network_Driver_XMJK7_WN32_12.0.1.720_A00.EXE). You need to extract the `.exe` file with [p7zip](https://www.archlinux.org/packages/?name=p7zip) and then convert it to a `.hcd` file with *hex2hcd* from [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils):

```
$ 7z x 9350_Network_Driver_XMJK7_WN32_12.0.1.720_A00.EXE
$ cp Win32/BCM4350C5_003.006.007.0095.1703.hex ./
$ hex2hcd BCM4350C5_003.006.007.0095.1703.hex
# mv BCM4350C5_003.006.007.0095.1703.hcd /lib/firmware/brcm/BCM-0a5c-6412.hcd

```

After reboot, the firmware should be available for your Bluetooth interface.

## Video

The video should work with the `i915` driver of the current [linux](https://www.archlinux.org/packages/?name=linux) kernel. If you experience a blank screen issue after booting, try loading the driver early in the boot process (see [Intel graphics#Blank screen during boot, when "Loading modules"](/index.php/Intel_graphics#Blank_screen_during_boot.2C_when_.22Loading_modules.22 "Intel graphics")):

 `/etc/mkinitcpio.conf`  `MODULES="... i915 ..."` 
**Note:** Some hardware also need `intel_agp`. If you do, you should write `"... intel_agp i915 ..."` (the order matters).

Then update the bootloader.

```
   # mkinitcpio -p linux

```

Where `linux` is the name of the image loaded on boot. If you installed [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/) then change that to `linux-mainline`.

If you are using an older kernel 4.3 or earlier, you also require the kernel parameter `i915.preliminary_hw_support=1`, see [Intel graphics#Driver not working for Intel Skylake chips](/index.php/Intel_graphics#Driver_not_working_for_Intel_Skylake_chips "Intel graphics"). (For later kernels 4.3+ or [linux-bcm4350](https://aur.archlinux.org/packages/linux-bcm4350/) the parameter is unnecessary.)

If you have the newer i7-6560 CPU with Iris 540 graphics, the GPU hangs every few minutes with the current kernel (4.4.1) and up. This is probably due to this bug [https://bugs.freedesktop.org/show_bug.cgi?id=94161](https://bugs.freedesktop.org/show_bug.cgi?id=94161) and can be countered by either disabling DRI in your Xorg configuration:

 `/etc/X11/xorg.conf.d/20-intel.conf`  `Option "DRI" "False"` 

or by adding `i915.enable_rc6=0` to the kernel boot parameters.

See also [Intel_graphics#X_freeze.2Fcrash_with_intel_driver](/index.php/Intel_graphics#X_freeze.2Fcrash_with_intel_driver "Intel graphics")

## Touchpad

Only key-presses work out of the box. Installing `xf86-input-synaptics` and restarting X fixes the problem (see [Dell Studio XPS 13](/index.php/Dell_Studio_XPS_13 "Dell Studio XPS 13")). `xf86-input-libinput` may be a good alternative that also handles touchscreen - see [libinput](/index.php/Libinput "Libinput") for configuration.

If `dmesg | grep -i psmouse` returns an error, but your touchpad still works, then it might be a good idea to disable `psmouse`. First create a config file:

```
   # nano /etc/modprobe.d/modprobe.conf

   blacklist psmouse

```

Then add this file to `/etc/mkinitcpio.conf`:

```
   ...
   FILES="/etc/modprobe.d/modprobe.conf"
   ...

```

Then update the bootloader.

```
   # mkinitcpio -p linux

```

where `linux` is the name of the image loaded on boot. If you installed [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/) then change that to `linux-mainline`.

## Sound

Some people reported white hissing/crackling noises when using headphones. To get rid of them you can run `alsamixer` from [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils). Select your soundcard with F6 and set the headset-gain to 22 (3rd lever from the left) or use the `amixer` command:

```
 $ amixer -c 0 cset 'numid=10' 1
 numid=10,iface=MIXER,name='Headphone Mic Boost Volume'
   ; type=INTEGER,access=rw---R--,values=2,min=0,max=3,step=0
   : values=1,1
   | dBscale-min=0.00dB,step=10.00dB,mute=0

```

Also people noticed loud popping-noises when sound was not playing. You can turn off the sound_power_save in `tlp`

```
   # nano /etc/default/tlp
   ...
   SOUND_POWER_SAVE_ON_BAT = 0 
   ...

```

### PulseAudio Workaround

PulseAudio will override the above setting every time you log in/out of your environment (or every time the PulseAudio service is restarted), even if the `alsa-restore.service` is enabled at [start](/index.php/Start "Start") up.

To work around this issue, edit `/usr/share/pulseaudio/alsa-mixer/paths/analog-input-headphone-mic.conf` and comment out the section `[Element Headphone Mic Boost]`:

```
 ---
 #[Element Headphone Mic Boost]
 #required-any = any
 #switch = select
 #volume = merge
 #override-map.1 = all
 #override-map.2 = all-left,all-right
 ---

```

Similarly in `/usr/share/pulseaudio/alsa-mixer/paths/analog-input-internal-mic.conf`, comment out the same section:

```
 ---
 #[Element Headphone Mic Boost]
 #switch = off
 #volume = off
 ---

```

This will prevent PulseAudio to fiddle with the gain setting at all. However, you must make the same modifications every time the PulseAudio package is updated.

## Microphone

**Note:** Not all hardware has the "Digital" channel

For ALSA, increase "Digital" channel for microphone to work.

## Links

General Discussion Thread on Arch Forum [[3]](https://bbs.archlinux.org/viewtopic.php?pid=1579113)