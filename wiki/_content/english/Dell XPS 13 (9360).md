| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | ath10k |
| Bluetooth | Working | btusb |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | hid_multitouch (mousedev) |
| Webcam | Working | uvcvideo |
| USB-C / Thunderbolt 3 | Working | ? |
| Wireless switch | Working | intel_hid |
| Function/Multimedia Keys | Working | ? |
| Fingerprint sensor | Not working | ? |

Related articles

*   [Dell XPS 13 (9333)](/index.php/Dell_XPS_13_(9333) "Dell XPS 13 (9333)")
*   [Dell XPS 13 (9343)](/index.php/Dell_XPS_13_(9343) "Dell XPS 13 (9343)")
*   [Dell XPS 13 (9350)](/index.php/Dell_XPS_13_(9350) "Dell XPS 13 (9350)")
*   [Dell XPS 13 (9370)](/index.php/Dell_XPS_13_(9370) "Dell XPS 13 (9370)")
*   [Dell XPS 13 2-in-1 (9365)](/index.php/Dell_XPS_13_2-in-1_(9365) "Dell XPS 13 2-in-1 (9365)")

The Dell XPS 13 Late 2016 (9360) is the fourth-generation model of the XPS 13 line. The laptop is available since October (pre-2017 model) in both a standard edition with Windows installed as well as both a pre-2017 model and a 2017 model (with insignificant hardware differences) Developer Edition with Ubuntu 16.04 "SP1" installed, featuring kernel 4.8 as of now. There is only minor hardware differences between them, mostly in regards to the mainboard microchip manufacturers. Just like the older versions ([9333](/index.php/Dell_XPS_13_(9333) "Dell XPS 13 (9333)"), [9343](/index.php/Dell_XPS_13_(9343) "Dell XPS 13 (9343)") and [9350](/index.php/Dell_XPS_13_(9350) "Dell XPS 13 (9350)")) it is available in different hardware configurations as well. These fourth gen models includes Intel's Kaby Lake CPUs and advertised with up to 16GB LPDDR 1866 MHz RAM and a 1TB PCI SSD. It will now also be available in Rose Gold. Prior to previous information and current specifications available provided by Dell (at least to regular customers), it is not available with the 2133 MHz RAM speed. However, some models, including those available to employees and possibly Dell partners (and/or business customers), memory speed is indeed available up to 2133 Mhz LPDDR3 (non-upgradable). The same mentioned models are also available with the Intel Core i7-7660U (aswell as i7-7560U) with the Intel 640 Iris Plus onboard graphics. Respective clock frequencies are 2.5 Ghz (up to 4GHz in Turbo-mode) and 2,4 Ghz (up to 3.8 Ghz), respectively.

The installation process for Arch on the XPS 13 does not differ from any other PC. For installation help, please see the [Installation guide](/index.php/Installation_guide "Installation guide") and [UEFI](/index.php/UEFI "UEFI"). This page covers the current status of hardware support on Arch, as well as post-installation recommendations.

As of kernel 4.5, the Intel Kaby Lake architecture is supported.

## Contents

*   [1 Content Adaptive Brightness Control](#Content_Adaptive_Brightness_Control)
*   [2 Power Saving](#Power_Saving)
*   [3 NVM Express SSD Power Saving](#NVM_Express_SSD_Power_Saving)
*   [4 Video](#Video)
    *   [4.1 Module-based Powersaving Options](#Module-based_Powersaving_Options)
    *   [4.2 Blank screen issue after booting](#Blank_screen_issue_after_booting)
*   [5 Wireless](#Wireless)
*   [6 Bluetooth](#Bluetooth)
*   [7 Thunderbolt 3 / USB 3.1](#Thunderbolt_3_.2F_USB_3.1)
    *   [7.1 Ethernet repeatedly disconnects/reconnects with Dell USB-C adapter (DA200)](#Ethernet_repeatedly_disconnects.2Freconnects_with_Dell_USB-C_adapter_.28DA200.29)
    *   [7.2 USB-C Compatibility Chart](#USB-C_Compatibility_Chart)
    *   [7.3 Thunderbolt Firmware updates](#Thunderbolt_Firmware_updates)
*   [8 SATA controller](#SATA_controller)
*   [9 Touchpad](#Touchpad)
    *   [9.1 Remove psmouse errors from dmesg](#Remove_psmouse_errors_from_dmesg)
*   [10 Touchscreen](#Touchscreen)
    *   [10.1 Gestures](#Gestures)
    *   [10.2 Scrolling in Firefox](#Scrolling_in_Firefox)
*   [11 Keyboard Backlight](#Keyboard_Backlight)
*   [12 Hidden Keyboard Keys](#Hidden_Keyboard_Keys)
    *   [12.1 Unobtrusive mode](#Unobtrusive_mode)
*   [13 Firmware Updates](#Firmware_Updates)
*   [14 Troubleshooting](#Troubleshooting)
    *   [14.1 EFISTUB does not boot](#EFISTUB_does_not_boot)
    *   [14.2 Not waking from suspend](#Not_waking_from_suspend)
    *   [14.3 Power Drain after waking from standby](#Power_Drain_after_waking_from_standby)
    *   [14.4 Popping sound on headphones/external speakers](#Popping_sound_on_headphones.2Fexternal_speakers)
    *   [14.5 Crackling sound with screen changes](#Crackling_sound_with_screen_changes)
    *   [14.6 Coil Whine](#Coil_Whine)
    *   [14.7 Freezing after waking from suspend](#Freezing_after_waking_from_suspend)
    *   [14.8 Continuous hissing sound with headphones](#Continuous_hissing_sound_with_headphones)
*   [15 Fingerprint sensor](#Fingerprint_sensor)
*   [16 See Also](#See_Also)

## Content Adaptive Brightness Control

In the XPS 13 the display panels (both FHD and QHD+) come with Content Adaptive Brightness Control (usually referred to as CABC or DBC) embedded in the panel firmware - it adjusts the screen brightness depending on the content displayed on the screen. While it saves a bit of power, it is generally undesirable, especially for Linux users who are likely to be switching between dark and light screen content. Dell has issued a fix for this, however it is only available to run in Windows. The fix is available [directly from Dell](http://www.dell.com/support/home/us/en/04/drivers/driversdetails?driverId=312K3&lwp=rt).

To test if your XPS 13 is affected by the CABC, go to this [test page](http://tylerwatt12.com/dc/). It is possible to apply Dell's firmware update using a portable Windows 10 on a USB device:

1.  Install (for example) [woeusb-git](https://aur.archlinux.org/packages/woeusb-git/)
2.  Download a Windows 10 ISO from [Microsoft's website](https://www.microsoft.com/en-in/software-download/windows10ISO)
3.  Create a portable Windows 10 installation [using woeusb](https://www.addictivetips.com/ubuntu-linux-tips/make-windows-usb-drive-on-linux-woeusb/)
4.  Boot the XPS 13 from your Windows 10 USB device (F12)
5.  In Windows, download and install the latest driver for the [Intel Graphics controller](http://www.dell.com/support/home/us/en/04/drivers/driversdetails?driverId=M10YG)
6.  Then download and install [this tool](http://www.dell.com/support/home/us/en/04/drivers/driversdetails?driverId=312K3) to update the panel firmware. The tool gives you the option to disable CABC
7.  Reboot (from USB)
8.  Reboot to Arch Linux and rerun the [test](http://tylerwatt12.com/dc/)

## Power Saving

It's possible to save around ~10/20% energy with somes tricks.

First, we can disable SD-Card adapter in bios settings (-0.5W~)

Then, it's possible to undervolt CPU and GPU with [intel-undervolt](/index.php/Undervolting_CPU#intel-undervolt "Undervolting CPU")

This is an example of best stable values for a I5-7200u (depend of your cpu):

CPU (0): -160.16 mV GPU (1): -125.00 mV CPU Cache (2): -89.84 mV

Edit the config file

`sudo nano /etc/intel-undervolt.conf`

This is an example for i5-7200u

`# CPU Undervolting`

`apply 0 'CPU' -160`

`apply 1 'GPU' -125`

`apply 2 'CPU Cache' -90`

`apply 3 'System Agent' 0`

`apply 4 'Analog I/O' 0`

`interval 5000`

then enable/start the daemon :)

`sudo systemctl enable intel-undervolt && sudo systemctl start intel-undervolt`

## NVM Express SSD Power Saving

For some devices it might be necessary to set a higher value for the `nvme_core.default_ps_max_latency_us` parameter to enable all power saving states. This parameter has to be set on the [kernel command line](/index.php/Kernel_command_line "Kernel command line").

For the Toshiba 512GB SSD used in some models of the XPS 13 the value to enable all states is 170000 (the combined latency of entering and leaving the highest power state, add `nvme_core.default_ps_max_latency_us=170000` to your kernel command line). For the 1TB SSD this valued should be increased to 180000 instead. To check if all states are enabled you can use the [nvme-cli](https://aur.archlinux.org/packages/nvme-cli/) package, which provides the `nvme-cli` command:

```
# nvme get-feature -f 0x0c -H /dev/nvme0
get-feature:0xc (Autonomous Power State Transition), Current value:0x000001
Autonomous Power State Transition Enable (APSTE): Enabled
Auto PST Entries  .................
Entry[ 0]   
.................
Idle Time Prior to Transition (ITPT): 1500 ms
Idle Transition Power State   (ITPS): 3
.................
Entry[ 1]   
.................
Idle Time Prior to Transition (ITPT): 1500 ms
Idle Transition Power State   (ITPS): 3
.................
Entry[ 2]   
.................
Idle Time Prior to Transition (ITPT): 1500 ms
Idle Transition Power State   (ITPS): 3
.................
Entry[ 3]   
.................
Idle Time Prior to Transition (ITPT): 8500 ms
Idle Transition Power State   (ITPS): 4
.................

```

If the power states are enabled there should be values for ITPT and ITPS in the first entries. Also the ITPS-value of the last filled entry should be the highest power saving-state of the SSD (which can be viewed using `smartctl -a /dev/nvme0` or `nvme id-ctrl /dev/nvme0`).

## Video

The video should work with the `i915` driver of the current [linux](https://www.archlinux.org/packages/?name=linux) kernel. Consult [Intel graphics](/index.php/Intel_graphics "Intel graphics") for a detailed installation and configuration guide as well as for [Intel graphics#Troubleshooting](/index.php/Intel_graphics#Troubleshooting "Intel graphics").

If you have the QHD+ (3200x1800) model, also check out [HiDPI](/index.php/HiDPI "HiDPI") for UI scaling configurations.

*But there might be video issues left for this model. **Please help by contributing any feedback** about similar issues you might have experience(d) to this bugreport ([https://bugs.freedesktop.org/show_bug.cgi?id=100671](https://bugs.freedesktop.org/show_bug.cgi?id=100671)).*

### Module-based Powersaving Options

For the HD 620 graphics card the following modules are working: (see [Intel graphics#Module-based Powersaving Options](/index.php/Intel_graphics#Module-based_Powersaving_Options "Intel graphics"))

```
modeset=1 enable_fbc=1 

```

The first argument is to enable modesetting if it's not set by default. The second argument is needed to activate framebuffer compression power savings. These values should work well!

```
enable_guc=3

```

This argument is used to enable GuC updates. GuC is a small proprietary binary blob released by intel to update the GuC binary in faster intervals than the kernel release does. It is used for graphics workload scheduling on the various graphics parallel engines. More details at ([https://01.org/linuxgraphics/downloads/firmware](https://01.org/linuxgraphics/downloads/firmware)). The GuC binary for kaby lake is included since firmware release linux-firmware 20170217 in the official repository. HuC is also a binary blob from intel. It's designed to offload some of the media functions from the CPU to GPU. As of kernel 4.12, HuC is loaded if GuC is enabled. One can check with 'cat /sys/kernel/debug/dri/0/i915_huc_load_status' and 'cat /sys/kernel/debug/dri/0/i915_guc_load_status'.

```
enable_psr=1

```

Panel Self Refresh (PSR) is working for eDP 1.3 and up and does stop the creation of new frames when the screen content is static to save energy. If you experience problems with PSR try to set 'disable_power_well=0' or disable otherwise. It may also be required to add the `modconf` hook to [Mkinitcpio](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") to avoid a hang after resume on both Xorg and Wayland.

**Note:** Some users have reported problems with `enable_psr==1` where on first boot or after resume the panel stays black once reaching the [desktop environment](/index.php/Desktop_environment "Desktop environment"), only refreshing after switching to and from a tty. In this case it is required to simply remove the option.

```
NOT WORKING: semaphores=1 

```

The semaphore option is NOT working for kaby lake CPUs and won't enable even if you set the option to 1.

### Blank screen issue after booting

If using "late start" [KMS](/index.php/KMS "KMS") (the default) and the screen goes blank when loading modules, it may help to add `i915` and `intel_agp` to the initramfs or using a special [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"). Consult [Intel graphics#Blank screen during boot, when "Loading modules"](/index.php/Intel_graphics#Blank_screen_during_boot.2C_when_.22Loading_modules.22 "Intel graphics") for more information about the kernel parameter way and have a look at [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting") for a guide on how to setup the modules for the initramfs.

## Wireless

The Killer 1535 Wirless Adapter is functional and the ath10k firmware is included in recent linux kernel versions. The connection speed reported by iw is limited to 1-6Mbits/s. However this is just the output being wrong. The real connection speed is not limited to this value.

[Some users are experiencing issues](http://en.community.dell.com/support-forums/network-internet-wireless/f/3324/t/19998908?pi41127=3), where the connection is dropped under heavy load but reconnects within a brief moment. This might not be noticed during browsing at all but becomes apparent in online games. There is [a firmware update proposed by DELL](http://en.community.dell.com/techcenter/os-applications/f/4613/p/20002634/20994007#20994007) to fix the issue, but it might not fix all the issues. In at least one case the new firmware did not fix the connection loss / low connection speed problem. Signs of this problem seems to be two kinds of messages in dmesg:

```
pcieport 0000:00:1c.4: AER: Corrected error received: id=00e4
pcieport 0000:00:1c.4: PCIe Bus Error: severity=Corrected, type=Data Link Layer, id=00e4(Transmitter ID)
pcieport 0000:00:1c.4:   device [8086:9d14] error status/mask=00001000/00002000
pcieport 0000:00:1c.4:    [12] Replay Timer Timeout  

```

And also:

```
CPU: 3 PID: 1410 Comm: irq/133-ath10k_ Not tainted 
Hardware name: Dell Inc. XPS 13 9360/0839Y6, BIOS 2.1.0 08/02/2017
Call Trace:
  <IRQ>
  dump_stack+0x63/0x82
  __warn+0xcb/0xf0
  warn_slowpath_null+0x1d/0x20
  net_rx_action+0x274/0x3a0
  ? irq_finalize_oneshot.part.35+0xe0/0xe0

```

As of February 2018, Dell support suggests to update the firmware of the network adapter in the following way:

1.  Confirm that you have QCA6174 checking the output of `sudo lspci`
2.  [Download](https://codeload.github.com/kvalo/ath10k-firmware/zip/master) the latest firmware and extract the contents from [git](https://github.com/kvalo/ath10k-firmware)
3.  Substitute the `QCA6174` folder in `/lib/firmware/ath10k/` with the one downloaded
4.  Inside the new folder, rename `firmware-4.bin_WLAN.RM.2.0-00180-QCARMSWPZ-1` to `firmware-4.bin`
5.  Reboot and test the new Killer Wi-Fi firmware

Update: Internet connection dropped even with the firmware from the above fix. Using the newer firmware `firmware-6.bin_WLAN.RM.4.4.1-00102-QCARMSWP-1` by downloading that file from [https://github.com/kvalo/ath10k-firmware/blob/master/QCA6174/hw3.0/4.4.1.c1/firmware-6.bin_RM.4.4.1.c1-00042-QCARMSWP-1](https://github.com/kvalo/ath10k-firmware/blob/master/QCA6174/hw3.0/4.4.1.c1/firmware-6.bin_RM.4.4.1.c1-00042-QCARMSWP-1), copying it to `/usr/lib/firmware/ath10k/QCA6174/hw3.0/` and renaming it to `firmware-6.bin` fixes this. Reboot and verify that this newer firmware is used by verifying that `dmesg | grep ath` outputs:

```
ath10k_pci 0000:3a:00.0: firmware ver RM.4.4.1.c1-00042-QCARMSWP-1 api 6 features wowlan,ignore-otp crc32 40fb7bdd

```

The latest bios update (2.9.0), which also contains important microcode security updates, manages to make these crashes occur no matter what firmware you load. Installing an [alternative intel wifi card](https://www.amazon.com/Intel-Dual-Band-Wireless-Ac-8265/dp/B01MZA1AB2) solves the problem.

## Bluetooth

After following the instructions given at [Bluetooth](/index.php/Bluetooth "Bluetooth") tethering of internet connections via phone works immediately.

## Thunderbolt 3 / USB 3.1

The USB-C port supports Thunderbolt 3, Displayport-over-USB-C and USB power delivery as well as USB 3.1.

### Ethernet repeatedly disconnects/reconnects with Dell USB-C adapter (DA200)

Use of a power management package (such as [TLP](/index.php/TLP "TLP")) may cause the ethernet adapter to repeatedly disconnect and reconnect. If this happens, disable/blacklist USB autosuspend for the ethernet adapter. (On my laptop, this is the device <tt>Bus 004 Device 007: ID 0bda:8153 Realtek Semiconductor Corp</tt> in the output of <tt>lsusb</tt>.)

Also disabling or reducing power of wifi may help: [http://en.community.dell.com/support-forums/network-internet-wireless/f/3324/t/19995423](http://en.community.dell.com/support-forums/network-internet-wireless/f/3324/t/19995423)

### USB-C Compatibility Chart

**Note:** *A comprehensive and up to date list of USB type C adapters and hubs is present in the [discussion](/index.php/Talk:Dell_XPS_13_(9360)#USB-C_Compatibility_Chart "Talk:Dell XPS 13 (9360)") page.*

### Thunderbolt Firmware updates

The thunderbolt controller in the laptop has an embedded firmware. The laptop ships with firmware version NVM 18, and the most recent available version from Dell's website is NVM 26\. If encountering compatibility problems with Thunderbolt accessories (such as the DA-200), the firmware may need to be updated. If you have fwupd (see: [#Firmware Updates](#Firmware_Updates)) set up then you should receive this update automatically. Otherwise, you can install it manually as follows.

Dell maintained a github repository with the firmware, but abandoned it now that the firmware is on LVFS. The current version is available as `0x075B_secure.bin` (or 0x082A for newer model, see instructions below) inside the [Windows package](http://www.dell.com/support/home/us/en/19/drivers/driversdetails?driverId=4FC9M). This can be extracted with [p7zip](https://www.archlinux.org/packages/?name=p7zip).

Here is a short list of steps to update the Thunderbolt-Firmware on linux 4.13+ (use at your own risk):

*   Force enable the thunderbolt controller (or plug in a device to enable it)

```
# echo 1 | sudo tee /sys/bus/wmi/devices/86CCFD48-205E-4A77-9C48-2021CBEDE341/force_power 

```

*   Check your model ID. If it's 0x082A, use the 0x082A firmware instead of the 0x075B one.

```
# cat /sys/bus/thunderbolt/devices/0-0/device

```

*   Flash the 9360 firmware from the thunderbolt-nvm-linux repository to a non active NVME memory spot

```
# dd if=payloads/0x075B.bin of=/sys/bus/thunderbolt/devices/0-0/nvm_non_active0/nvmem

```

*   Trigger the update process

```
# echo 1 > /sys/bus/thunderbolt/devices/0-0/nvm_authenticate

```

*   At this point, your screen should flickr a couple of time. Verify that the update is done by checking that authenticate returns 0

```
# cat /sys/bus/thunderbolt/devices/0-0/nvm_authenticate

```

*   Verify the new nvme version (it should return 26.1)

```
# cat /sys/bus/thunderbolt/devices/0-0/nvm_version

```

*   Put the controller back in normal mode

```
# echo 0 | sudo tee /sys/bus/wmi/devices/86CCFD48-205E-4A77-9C48-2021CBEDE341/force_power

```

## SATA controller

When the SATA-controller is set to `RAID On` in Bios, the SSD is not recognized. Set to `AHCI` before attempting to install Arch.

## Touchpad

The touchpad has no explicit buttons. The buttons are built into the pads surface. There is a small line printed on the pad separating left from right click button. The pad has a **middle button** built in! (works with libinput without any configuration): To issue a middle click, simply press on the middle area right between the virtual left and click buttons - so on the small printed separator line.

### Remove psmouse errors from dmesg

If `dmesg | grep -i psmouse` returns an error, but your touchpad still works, then it might be a good idea to disable `psmouse`. First create a config file:

```
# nano /etc/modprobe.d/modprobe.conf

blacklist psmouse

```

Then add this file to `/etc/mkinitcpio.conf`:

```
...
FILES=(/etc/modprobe.d/modprobe.conf)
...

```

Rebuild your initial ramdisk image (see [Mkinitcpio#Image creation and activation](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio")).

## Touchscreen

The touchscreen works without additional configuration. The bug resulting in a disabled touchscreen after resume was fixed with kernel 4.8.5.

### Gestures

Refer to [libinput#Gestures](/index.php/Libinput#Gestures "Libinput") for information about the current development state and available methods.

### Scrolling in Firefox

See [Firefox/Tweaks#Pixel-perfect trackpad scrolling](/index.php/Firefox/Tweaks#Pixel-perfect_trackpad_scrolling "Firefox/Tweaks"). This enables both touchscreen scrolling and high-res trackpad scrolling.

## Keyboard Backlight

By default, the keyboard backlight turns off after 10 seconds of inactivity. Some users might find this too short and annoying. The delay can be increased (or decreased) by editing this file:

```
/sys/devices/platform/dell-laptop/leds/dell\:\:kbd_backlight/stop_timeout

```

You can also change the brightness (0-2) by editing the following file. This is identical to pressing F10 on your keyboard:

```
/sys/devices/platform/dell-laptop/leds/dell\:\:kbd_backlight/brightness

```

## Hidden Keyboard Keys

There are additional Fn+<Key> (sequences) that are not marked at all on the keyboard but underlying hardware generates them anyway. Here they are (if you find more add them to the table below):

<caption>Hidden Fn Keys</caption>
| Fn+<Key> | Resulting key (sequence) |
| Fn+Ins | XF86Sleep |
| Fn+Super_L | Super_R |
| Fn+B | Pause |
| Fn+R | Print |
| Fn+S | Scroll_Lock |
| Fn+A / D / E / F / G / T / Q / W | XF86Launch3 |

### Unobtrusive mode

If enabled in BIOS, pressing Fn+F7 will disable sound, keyboard and screen backlight, the charging LED and the LED on the power button. Unfortunately there seems to be no way to disable just the LEDs- some users recommend black electrical tape. The output of `smbios-token-ctl -d` only list changes related to screen, keyboard and sound when unobtrusive mode is active.

## Firmware Updates

Dell provides firmware updates via [fwupd](https://www.archlinux.org/packages/?name=fwupd). See [Flashing BIOS from Linux#fwupd](/index.php/Flashing_BIOS_from_Linux#fwupd "Flashing BIOS from Linux"). Please note if you have used a bind mount partition for /boot, you will not be able to use the fwupd utility; Instead format a USB as FAT32 and put the bios update .exe on. Reboot into the one-time-boot menu and update the BIOS flash through there.

Alternatively, the BIOS update can be downloaded from the [Dell website](http://www.dell.com/support/home/us/en/04/Drivers/DriversDetails?driverId=GVNVJ), and placed in a location accessible to the firmware. This could be the '/boot' folder, or a FAT32 formatted USB stick. Then restart your laptop and hit F12 while starting. In the boot menu choose firmware update and select the new file!

## Troubleshooting

### EFISTUB does not boot

The BIOS does not pass any boot parameters to the kernel. Use a UEFI [boot loader](/index.php/Boot_loader "Boot loader") instead.

### Not waking from suspend

Update the BIOS to 1.0.7 to patch this issue.

### Power Drain after waking from standby

Some users recognised ~2W more power consumption after waking up from standby. Go to the UEFI Firmware Settings (tap the F2 key when the Dell logo appears) and uncheck the 'Enable Thunderbolt Boot Support'. You may use [powertop](https://www.archlinux.org/packages/?name=powertop) or [powerstat-git](https://aur.archlinux.org/packages/powerstat-git/) to reproduce and check this behaviour yourself.

### Popping sound on headphones/external speakers

Power saving being enabled on the audio chip will cause the hissing and popping to appear.

Have a look at [ALSA troubleshooting#Pops when starting and stopping playback](/index.php/ALSA_troubleshooting#Pops_when_starting_and_stopping_playback "ALSA troubleshooting") and [ALSA troubleshooting#Popping sound after resuming from suspension](/index.php/ALSA_troubleshooting#Popping_sound_after_resuming_from_suspension "ALSA troubleshooting").

If you are using [tlp](https://www.archlinux.org/packages/?name=tlp), it will activate power saving by default when on battery. Edit `/etc/default/tlp` and disable it.

### Crackling sound with screen changes

Some users experienced a weird crackling, white noise sound when the display is changing its contents after waking the computer from S3 sleep..

This issue should be patched as of the 4.14.15 kernel.

If you're still encountering this issue, try manually applying this patch[[1]](https://lkml.org/lkml/2018/1/22/169). Adding the kernel parameter `i915 enable_guc=1` as described in [Intel graphics](/index.php/Intel_graphics "Intel graphics") might also help, however multiple people have reported that this does not fix the problem completely.

### Coil Whine

Unfortunately Dell still did not fix this issue and the sound for my model was very loud. The issue seems to be connected to the graphic card. For some users, it is possible to reduce it a lot by activating frame buffer compression "enable_fbc=1" [Intel graphics#Framebuffer compression (enable_fbc)](/index.php/Intel_graphics#Framebuffer_compression_.28enable_fbc.29 "Intel graphics"). The coil whine will then start again under heavy graphic load. For the touchscreen model, this may be very often, due to the high resolution screen. In a similar vein, the display can be run at a lower resolution, again reducing the load on the graphics card.

### Freezing after waking from suspend

Installing [xf86-video-intel-git](https://aur.archlinux.org/packages/xf86-video-intel-git/) is [reported](https://bbs.archlinux.org/viewtopic.php?pid=1698282#p1698282) to fix this.

### Continuous hissing sound with headphones

Open alsamixer and set "Headphone Mic Boost" gain to 10 dB (See discussion on [reddit](https://www.reddit.com/r/Dell/comments/4j1zz4/headphones_have_static_noise_with_ubuntu_1604_on/)). Note that this does reduce the volume slightly.

You may also run the equivalent command:

```
$ amixer -c PCH cset 'name=Headphone Mic Boost Volume' 1

```

PulseAudio will rewrite these ALSA settings. So if you use PulseAudio you should change its config to make them permanent:

 `/usr/share/pulseaudio/alsa-mixer/paths/analog-input-headphone-mic.conf` 
```
[Element Headphone Mic Boost]
required-any = any
switch = select
# Replace "volume = merge" by:
volume = 1
override-map.1 = all
override-map.2 = all-left,all-right

```
 `/usr/share/pulseaudio/alsa-mixer/paths/analog-input-internal-mic.conf` 
```
[Element Headphone Mic Boost]
switch = off
# Replace "volume = off" by:
volume = 1

```

## Fingerprint sensor

Dell officially does not support fingerprint reader functionality [[2]](http://en.community.dell.com/techcenter/os-applications/f/4613/t/20006668), however an effort on reverse engineering the protocol of Validity 138a:0090, 138a:0094, 138a:0097 fingerprint readers can be found at github [[3]](https://github.com/nmikhailov/Validity90).

## See Also

*   [Arch Forum thread for Dell XPS 13 (9360)](https://bbs.archlinux.org/viewtopic.php?id=217865)
*   [Service Manual for Dell XPS 13 (9360)](http://topics-cdn.dell.com/pdf/xps-13-9360-laptop_service%20manual2_en-us.pdf)