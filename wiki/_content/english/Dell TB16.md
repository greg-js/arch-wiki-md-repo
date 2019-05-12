Dell's [TB16](https://www.dell.com/en-us/shop/dell-business-thunderbolt-dock-tb16-with-240w-adapter/apd/452-bcnu/pc-accessories) is a popular Thunderbolt Dock with power-delivery, ethernet, USB, audio, HDMI, DisplayPort, mini-DP and VGA. It works well in Linux when configured correctly with up-to-date firmware.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configuration](#Configuration)
    *   [1.1 Thunderbolt Security](#Thunderbolt_Security)
    *   [1.2 Dell Type-C Dock Configuration](#Dell_Type-C_Dock_Configuration)
*   [2 Firmware Updates](#Firmware_Updates)
*   [3 Troubleshooting](#Troubleshooting)
*   [4 External Links](#External_Links)

## Configuration

### Thunderbolt Security

You shoulder either:

*   Disable Thunderbolt security in the BIOS (recommended)
*   Use [boltctl](/index.php/Thunderbolt#User_device_authorization "Thunderbolt") to temporarily authorize or permanently enroll the *dock* ***and*** *cable*.

Thunderbolt security "works" but may result in random instability, particularly system freezes on resume. It's suggested to ensure your system is completely stable before enabling this.

### Dell Type-C Dock Configuration

The TB16 is commonly used with Dell laptops, which have a special BIOS option which [may cause stability issues](https://www.reddit.com/r/sysadmin/comments/9bwqt8/dell_tb16_dock_rant_seriously_dont_buy_this_thing/). You should disable the following option:

*   Dell Type-C Dock Configuration
    *   Always Allow Dell Docks (uncheck this)

## Firmware Updates

The firmware updates provided for Windows at Dell's [TB16 Support: Drivers](https://www.dell.com/support/home/us/en/04/product-support/product/dell-thunderbolt-dock-tb16/drivers) page include firmware that cannot be updated in Linux, such as the ASMedia USB Host Controller firmware which fixes numerous instability USB issues and Synaptics controller (DisplayPort).

To summarize [jasondclinton's post on reddit](https://www.reddit.com/r/Dell/comments/8vjqch/if_dell_pushed_out_firmware_update_v100_for_the/e1sjczx/):

1.  The NVM updates to the TB controller can be flashed by Linux (using the standard nvm_nonactive nvm_authenticate sysfs interface)
2.  There is no way to install the ASMedia, Synaptics, etc firmwares - so you might as well flash everything from Windows.
3.  You need all the latest updates for the docker firmware updater to even see the TB16.

Ensure you have the latest:

1.  BIOS firmware
2.  Windows Update
3.  Dell Update
4.  Thunderbolt NVM firmware (for the Thunberbolt controller on your device) - should be covered by Windows & Dell updates
5.  TB16 firmware updater from the [drivers page above](https://www.dell.com/support/home/us/en/04/product-support/product/dell-thunderbolt-dock-tb16/drivers).

Even after having used the firmware updater, there are still other firmwares from the same Dell support page, which supersede the versions included in the firmware updater, that should be downloaded and installed afterwards, e.g. the ASMedia driver / firmware. If in doubt, install all updates on the page.

jasondclinton also notes that the official NVM updates are often far behind Intel's latest releases (e.g. TB16's 1.0.0 firmware includes NVM 16 wherehas Intel had already released NVM 33 at time of writing). It is unknown if there's an easy way to update these independently.

## Troubleshooting

Issues such as the USB bus (and all connected devices) failing when plugging/unplugging devices are improved by following all the instructions above (notably, Thunderbolt Security, "Dell Type-C Dock configuration options" and firmware updates). Read the firmware updates section carefully: not all updates are possible via Linux.

Some devices behave differently in the dock vs directly on laptop's USB ports, e.g. Microsoft's keyboard receiver is erratically put to sleep. You can wake them up in [powertop](/index.php/Powertop "Powertop") or see [Power management#USB autosuspend](/index.php/Power_management#USB_autosuspend "Power management") on how to blacklist particular devices.

## External Links

*   [Reddit r/sysadmin: Dell TB16 Dock Rant - Seriously don't buy this thing...](https://www.reddit.com/r/sysadmin/comments/9bwqt8/dell_tb16_dock_rant_seriously_dont_buy_this_thing/)
*   [Reddit r/Dell: If Dell pushed out firmware update v1.00 for the TB16...](https://www.reddit.com/r/Dell/comments/8vjqch/if_dell_pushed_out_firmware_update_v100_for_the/)