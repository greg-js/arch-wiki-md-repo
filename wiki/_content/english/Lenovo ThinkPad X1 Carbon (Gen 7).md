Related articles

*   [Lenovo ThinkPad X1 Carbon](/index.php/Lenovo_ThinkPad_X1_Carbon "Lenovo ThinkPad X1 Carbon")
*   [Lenovo ThinkPad X1 Carbon (Gen 2)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_2) "Lenovo ThinkPad X1 Carbon (Gen 2)")
*   [Lenovo ThinkPad X1 Carbon (Gen 3)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_3) "Lenovo ThinkPad X1 Carbon (Gen 3)")
*   [Lenovo ThinkPad X1 Carbon (Gen 4)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_4) "Lenovo ThinkPad X1 Carbon (Gen 4)")
*   [Lenovo ThinkPad X1 Carbon (Gen 5)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_5) "Lenovo ThinkPad X1 Carbon (Gen 5)")
*   [Lenovo ThinkPad X1 Carbon (Gen 6)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_6) "Lenovo ThinkPad X1 Carbon (Gen 6)")
*   [Lenovo ThinkPad X1 Yoga (Gen 3)](/index.php/Lenovo_ThinkPad_X1_Yoga_(Gen_3) "Lenovo ThinkPad X1 Yoga (Gen 3)")

**Tip:** A great resource for thinkpads is [https://www.thinkwiki.org/wiki/ThinkWiki](https://www.thinkwiki.org/wiki/ThinkWiki)

The Lenovo ThinkPad X1 Carbon, 7th generation is an ultrabook introduced in early 2019\. It features a 14" screen, 8th-gen Intel Core processors and integrated [Intel UHD 620 graphics](/index.php/Intel_graphics "Intel graphics").

To ensure you have this version, [install](/index.php/Install "Install") the package [dmidecode](https://www.archlinux.org/packages/?name=dmidecode) and run:

```
# sudo dmidecode -s system-version
ThinkPad X1 Carbon 7th

```

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 BIOS](#BIOS)
    *   [1.1 Updates](#Updates)
        *   [1.1.1 Automatic (Linux Vendor Firmware Service)](#Automatic_(Linux_Vendor_Firmware_Service))
        *   [1.1.2 Manual (fwupdmgr)](#Manual_(fwupdmgr))
    *   [1.2 Enabling S3](#Enabling_S3)
    *   [1.3 Verifying S3](#Verifying_S3)
    *   [1.4 S3 Suspend Bug with Bluetooth Devices](#S3_Suspend_Bug_with_Bluetooth_Devices)
    *   [1.5 BIOS configurations](#BIOS_configurations)
*   [2 Power management/Throttling issues](#Power_management/Throttling_issues)
    *   [2.1 Throttling fix](#Throttling_fix)
    *   [2.2 Touchpad Issues](#Touchpad_Issues)
*   [3 Volume Controls](#Volume_Controls)
*   [4 Disabling red LED in ThinkPad logo](#Disabling_red_LED_in_ThinkPad_logo)
*   [5 Additional resources](#Additional_resources)

## BIOS

The most convenient way to install Arch Linux is by disabling "Secure Boot" `Security -> Secure Boot - Set to "Disabled"`. However it is possible to self-sign your kernel and boot with it enabled. For further information have a look at the [Secure Boot](/index.php/Secure_Boot "Secure Boot") article.

In case your `efivars` are not properly set it is most likely due to you not being booted into [UEFI](/index.php/UEFI "UEFI"). Should the problem persist be sure to consult the [UEFI#UEFI variables](/index.php/UEFI#UEFI_variables "UEFI") section.

### Updates

#### Automatic (Linux Vendor Firmware Service)

[In August of 2018 Lenovo has joined](https://blogs.gnome.org/hughsie/2018/08/06/please-welcome-lenovo-to-the-lvfs/) the [Linux Vendor Firmware Service (LVFS)](https://fwupd.org/) project, which enables firmware updates from within the OS. BIOS updates (and possibly other firmware such as the Thunderbolt controller) can be queried for and installed through [fwupd](/index.php/Fwupd "Fwupd").

#### Manual (fwupdmgr)

Lenovo provides a cabinet file that can be directly installed with fwupdmgr. Take the most recent `.cab` file from the [Lenovo ThinkPad X1 Carbon (Gen 6) driver website](https://pcsupport.lenovo.com/fr/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x1-carbon-6th-gen-type-20kh-20kg/downloads).

1.  Make sure the AC adapter is firmly connected to the target computer.
2.  Launch Terminal.
3.  Move to the directory where the cabinet file was placed.
4.  Run `fwupdmgr install xxxxxxxx.cab` to schedule firmware update.
5.  Restart the system.
6.  The computer will be restarted and the UEFI BIOS will be updated.

### Enabling S3

To enable S3 support, make sure you go into the BIOS configuration, and `Config -> Power -> Sleep State - Set to "Linux"`. This should make S3 available. To verify, after making the changes in the BIOS configuration, boot into Linux, and run the `dmesg` command again to make sure that S3 is now available.

### Verifying S3

To check whether S3 is recognized and usable by Linux, run:

```
dmesg | grep -i "acpi: (supports"

```

and check for `S3` in the list.

### S3 Suspend Bug with Bluetooth Devices

Occasionally your Thinkpad will wake up immediately after suspending with certain [bluetooth](/index.php/Bluetooth "Bluetooth") devices added. To prevent this, remove the devices or disable [bluetooth](/index.php/Bluetooth "Bluetooth") before suspending.

### BIOS configurations

*   `Config -> Thunderbolt BIOS Assist Mode - Set to "Enabled"`. When disabled, on Linux, power usage appears to be significantly higher because of a substantial number of CPU wakeups during s2idle.

## Power management/Throttling issues

Due to wrong configured power management registers the CPU may consume a lot less power than under windows and the thermal throttling occurs at 80°C (97°C when using Windows, see [T480s throttling bug](https://www.reddit.com/r/thinkpad/comments/870u0a/t480s_linux_throttling_bug/)).

There is a [post in the official Lenovo forum](https://forums.lenovo.com/t5/Linux-Discussion/T480s-low-cTDP-and-trip-temperature-in-Linux/td-p/4028489) to inform Lenovo about this issue.

### Throttling fix

[thermald](https://aur.archlinux.org/packages/thermald/) replaces the lenovo_fix used previously. Install [thermald](https://aur.archlinux.org/packages/thermald/), then run

```
sudo systemctl enable --now thermald.service

```

### Touchpad Issues

The touchpad works fine out of the box, except that [TLP](/index.php/TLP "TLP") does not detect that the Synaptics Touchpad is indeed an input device, so it does not exclude it from the USB_AUTOSUSPEND feature. You can tell that this is the issue if the touchpad works for just a moment after waking up from suspend, and then stops working again.

The fix is to add the touchpad to the USB_BLACKLIST in TLP's config:

```
USB_BLACKLIST="06cb:00bd" <=========== use lsusb to get the correct UUID

```

## Volume Controls

In order for volume controls to work correctly you must edit `/usr/share/pulseaudio/alsa-mixer/paths/analog-output.conf.common` by adding the following above `[Element PCM]`:

```
[Element Master]
switch = mute
volume = ignore

```

A reboot is required for this change to take affect.

## Disabling red LED in ThinkPad logo

To disable the red LED in the ThinkPad logo on the cover:

1\. Enable writing to the embedded controller registers by adding the kernel parameter `ec_sys.write_support=1`. If you use UEFI boot, you can add this parameter in `/boot/efi/loader/entries/arch.conf` under "options".

2\. Then, you can disable directly the LED with this command:

```
# echo -n -e "\x0a" | sudo dd of="/sys/kernel/debug/ec/ec0/io" bs=1 seek=12 count=1 conv=notrunc 2> /dev/null

```

**To disable the LED at startup, you can create a systemd service:**

1\. Create a sh script (/root/disable_led.sh for instance) and put this :

```
#!/bin/bash
echo -n -e "\x0a" | dd of="/sys/kernel/debug/ec/ec0/io" bs=1 seek=12 count=1 conv=notrunc 2> /dev/null

```

2\. Create a new service unit file in {{ic|/etc/systemd/system} called "led.service", and insert the following:

```
Description=Disabling thinkpad led

[Service]
ExecStart=/root/disable_led.sh

[Install]
WantedBy=multi-user.target

```

3\. Start and enable this service:

```
# systemctl start led.service
# systemctl enable led.service

```

## Additional resources

*   [ThinkWiki X1 Carbon 6th Gen page](https://www.thinkwiki.org/wiki/Category:X1_Carbon_(7th_Gen))
*   [Dell XPS 13 9370 quirks](https://gist.github.com/greigdp/bb70fbc331a0aaf447c2d38eacb85b8f): Some pointers on getting Watt usage down to ~2W, Intel video powersaving features might be interesting, see also the [Intel graphics](/index.php/Intel_graphics "Intel graphics") page for interesting power-saving options.
*   [Intel Blog: Best practice to debug Linux* suspend/hibernate issues](https://01.org/blogs/rzhang/2015/best-practice-debug-linux-suspend/hibernate-issues), including the [pm-graph](https://github.com/01org/pm-graph) tool to analyze power usage during suspend