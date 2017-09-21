This page contains instructions, tips, pointers, and links for installing and configuring Arch Linux on the [ASUS Zenbook UX303](http://www.asus.com/Notebooks_Ultrabooks/UX303LN/) Ultrabook.

There is a lot a models but 2 main models, UX303LN with 2 graphic cards (intel & nvidia) and UX303LA with only an intel graphic card. The previous models UX32LN and UX32LA share a lot hardware with minor differences, e.g. the touchpad (Elantech).

## Contents

*   [1 Installation problems](#Installation_problems)
*   [2 Compatibility](#Compatibility)
    *   [2.1 Hard Disk](#Hard_Disk)
    *   [2.2 Touchpad](#Touchpad)
    *   [2.3 Touch screen](#Touch_screen)
    *   [2.4 Webcam](#Webcam)
    *   [2.5 Wifi](#Wifi)
    *   [2.6 Bluetooth](#Bluetooth)
    *   [2.7 Graphics](#Graphics)
    *   [2.8 Keyboard backlight](#Keyboard_backlight)
    *   [2.9 Monitor backlight](#Monitor_backlight)
    *   [2.10 Ambient Light Sensor (ALS)](#Ambient_Light_Sensor_.28ALS.29)
    *   [2.11 QHD+ Pentile Display](#QHD.2B_Pentile_Display)
    *   [2.12 Suspend/resume](#Suspend.2Fresume)
    *   [2.13 Battery](#Battery)
    *   [2.14 Microphone](#Microphone)
*   [3 Function Keys](#Function_Keys)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 USB 3.0](#USB_3.0)

## Installation problems

None, but you should use the UEFI archlinux installation guide. The Asus UEFI accepts UEFI boot (which works well) and Legacy BIOS mode.

## Compatibility

### Hard Disk

For models with an SSD, see [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives").

For the models without a SSD as main disk, the hard disk stop/start each 30/60 seconds, add a udev rule :

```
 $ cat /etc/udev/rules.d/50-hdparm.rules
 # Configure hardisk power management: No more spin-down !!
 KERNEL=="sda", SUBSYSTEM=="block", ACTION=="add", RUN+="/usr/bin/hdparm -B 255 -S 0 /dev/sda"

```

and update the systemd hdparm service:

```
 $ cat /etc/systemd/system/hdparm.service 
 [Unit]
 Description=Local system resume actions
 After=suspend.target

 [Service]
 Type=simple
 ExecStart=/usr/bin/hdparm -B 255 -S 0 /dev/sda

 [Install]
 WantedBy=suspend.target

```

### Touchpad

The touchpad is a FocalTech model, that is supported by the Linux kernel since 4.0.1-1.

```
 dmesg | grep FLT01                                                            
 [    0.395565] pnp 00:06: Plug and Play ACPI device, IDs FLT0101 SYN0a00 SYN0002 PNP0f03 PNP0f13 PNP0f12 (active)

```

```
 cat /sys/bus/acpi/devices/FLT0101\:00/status                                  
 15 

```

```
 $ xinput   
 ⎡ Virtual core pointer                    	id=2	[master pointer  (3)]
 ⎜   ↳ FocalTechPS/2 FocalTech FocalTech Touchpad	id=14	[slave  pointer  (2)]

```

The touchpad is supported by [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") and, alternatively, [libinput](/index.php/Libinput "Libinput").

If you use [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") the sensitivity settings may need to be adjusted, because of the large touchpad area. If touchpad is not responsive, try changing the settings:

 `/etc/X11/xorg.conf.d/50-synaptics.conf` 
```
Section "InputClass"
        ....
	Option "FingerLow" "30"
	Option "FingerHigh" "35"
EndSection
```

### Touch screen

The touchscreen is an Atmel maXTouch Digitize. Simple touch works well out of the box. The 10-point multi touch works with [libinput](https://www.archlinux.org/packages/?name=libinput) installed (tested with the tools/event-debug libinput test tool).

### Webcam

The webcam is an SuYin HF1019-T838-SN03 (USB 2.0, UVC) which works well.

### Wifi

The wifi chipset is an Intel(R) Dual Band Wireless N 7260, REV=0x144\. It works well with recents kernel (fails with 3.2.0 kernel) with the iwlwifi kernel module and the firmware version 23.214.9.0\. The device name is wlp2s0.

### Bluetooth

The Bluetooth chipset is an intel N7260 model (same as the wifi chipset), which works well. Uses the intel/ibt-hw-37.7.10-fw-1.80.2.3.d.bseq firmware.

### Graphics

The main graphic chipset is an Intel Haswell chipset, which works well with the i915 xorg driver. See [Intel graphics](/index.php/Intel_graphics "Intel graphics") for details.

```
 $ lspci
 ...
 00:02.0 VGA compatible controller: Intel Corporation Haswell-ULT Integrated Graphics Controller (rev 0b)

```

Secondary graphics card is NVIDIA GeForce 840M (UX303LN model).

```
 $ lspci
 ....
 03:00.0 3D controller: NVIDIA Corporation GM108M [GeForce 840M] (rev a2)

```

The secondary card is combined with the main graphics in a hybrid [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus") configuration. The card works with nvidia drivers from the official repository. [Bumblebee](/index.php/Bumblebee "Bumblebee") can be used to take advantage of the NVIDIA card.

### Keyboard backlight

Four level positions (0 to 3) available with

```
 tee /sys/class/leds/asus::kbd_backlight/brightness <<< 3

```

### Monitor backlight

available with

```
 tee  /sys/class/backlight/intel_backlight/brightness  <<< 500

```

825 is the max value.

On kernel 3.17, max value seems to be 187

### Ambient Light Sensor (ALS)

The included Ambient Light Sensor can be accessed using the [als-dkms](https://aur.archlinux.org/packages/als-dkms/) kernel module. There is also a userspace program [als-controller](https://aur.archlinux.org/packages/als-controller/), which has the purpose of automatically adjusting the keyboard and screen backlight. Usage of the Ambient Light Sensor is described in more detail on the wiki page for the [ASUS Zenbook Prime UX31A](/index.php/ASUS_Zenbook_Prime_UX31A "ASUS Zenbook Prime UX31A").

Note that the userspace program currently does not work correctly on the UX303 as the reported brightness values differ from the Zenbook Prime.

### QHD+ Pentile Display

Some models include a 3200x1800 (faux-3200x1800 RG/BW Pentile) screen, which displays very tiny characters, and can make them difficult to read due to its incomplete subpixel matrix.

Gnome3 is able to work out the correct font size on this display, but other environments and GUI toolkits may need adjustment. See the general [HiDPI](/index.php/HiDPI "HiDPI") wiki page for possible fixes.

### Suspend/resume

Prior to Linux 4.0.1-1, this laptop had problems resuming from suspend-to-ram, and could not reliably power off. Since Linux 4.0.1-1, these issues no longer exist and suspending/resuming as well as powering off work reliably. Suspend key (Fn+F1) works out of the box with expected behavior.

If suspend fails sometimes (kernel crashes when trying to suspend), it might be due to a [bios/kernel bug](https://bugzilla.kernel.org/show_bug.cgi?id=102091). Try [blacklisting](/index.php/Blacklisting "Blacklisting") the kernel modules `mei_me` and `mei` meanwhile.

### Battery

Battery has a design capacity of 4429mAh, and is able to provide just over 3 hours of autonomy under normal circumstances (average load of around 0.3 and WiFi enabled, brightness lowered to mid-range) without serious power saving tweaks. Battery stops charging when it reaches near-full capacity on AC and acpi tool will show "discharging at zero rate" message. This behavior can be observed on a brand new battery. ACPI tools are able to correctly detect the battery state.

```
 # on AC near-full capacity
 $ acpi -i
 Battery 0: Discharging, 98%, discharging at zero rate - will never fully discharge.
 Battery 0: design capacity 4429 mAh, last full capacity 4076 mAh = 92%

```

```
 # on AC charging
 $ acpi -i
 Battery 0: Charging, 94%, 00:11:53 until charged
 Battery 0: design capacity 4429 mAh, last full capacity 4110 mAh = 92%

```

```
 # off AC
 $ acpi -i
 Battery 0: Discharging, 98%, 03:22:03 remaining
 Battery 0: design capacity 4429 mAh, last full capacity 4076 mAh = 92%

```

Battery life may depend on the type of LCD panel. The above values are shown for the model with QHD display.

There have been suggestions that "discharging at zero rate" while on AC is a battery calibration issue solvable by allowing the battery to fully discharge and then charging it back to full capacity.

It is also recommended to install the [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") AUR package. On a UX303LB laptop (Broadwell) this increases battery life significantly.

### Microphone

Microphone works out of the box. If you cannot record or use VoIP, make sure the microphone is not muted.

## Function Keys

As of kernel version 4.10 all function keys, except for automatic brightness seem to work out of the box (UX303LN)

All function keys except the backlight and "plane" mode seem to work out of the box (as of kernel 3.17). To fix, add `acpi_osi=` as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"). Example line from `/etc/default/grub`:

 `GRUB_CMDLINE_LINUX_DEFAULT="quiet acpi_osi="` 

On UX303LA (kernel 4.1.13) xev does not return any events for the standard brightness keys, but F3 and F4 seem to be detected as XF86KbdBrightnessDown and XF86KbdBrightnessUp, respectively.

On UX303UB (kernel 4.4.5-1), add the kernel parameter, and create the file `/usr/share/X11/xorg.conf.d/20-intel.conf` with the following content:

```
 Section "Device"
   Identifier  "card0"
   Driver      "intel"
   Option      "Backlight"  "intel_backlight"
   BusID       "PCI:0:2:0"
 EndSection

```

## Troubleshooting

### USB 3.0

If the USB Ports are only working with USB 2.0 devices, disable "XHCI Pre-Boot Mode" in the BIOS under "Advanced" -> "USB Configuration".

**Note:**

Be aware, that after deactivating "XHCI Pre-Boot Mode" the ports will only work in USB 2.0 mode.