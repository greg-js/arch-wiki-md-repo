## Contents

*   [1 Description](#Description)
    *   [1.1 Configure needed kernel modules](#Configure_needed_kernel_modules)
    *   [1.2 Install iRiver driver/manager software](#Install_iRiver_driver.2Fmanager_software)
    *   [1.3 Verify that you can connect to your iRiver device](#Verify_that_you_can_connect_to_your_iRiver_device)
    *   [1.4 Midnight Commander setup](#Midnight_Commander_setup)
    *   [1.5 Setting up udev to automatically assign permissions](#Setting_up_udev_to_automatically_assign_permissions)
*   [2 Notes](#Notes)
    *   [2.1 Upgrading firmware](#Upgrading_firmware)

### Description

[libifp](https://www.archlinux.org/packages/?name=libifp), which provides the `ifpline` command, lets you manage your [iRiver](https://en.wikipedia.org/wiki/Iriver#Discontinued_2 "wikipedia:Iriver") MP3 music player acting in "Manager Mode" ONLY. If your player is using "UMS Mode", then you do not need this program; it will appear as a new drive when you plug it in. At the time of writing, only Manager Mode can play [Ogg Vorbis](https://en.wikipedia.org/wiki/Vorbis "wikipedia:Vorbis") format files.

libifp can upload and download files and directories, delete and create directories on the device, format the device, and upgrade your firmware. It effectively manages most of the tasks performed by the iRiver software provided for Windows, while being faster and more stable.

It is recommended that it is used in conjunction with [Midnight Commander](https://en.wikipedia.org/wiki/Midnight_Commander "wikipedia:Midnight Commander") to help manage your music files more effectively.

#### Configure needed kernel modules

Refer to [Kernel modules#Loading](/index.php/Kernel_modules#Loading "Kernel modules") and make sure the modules `usbserial` and `usb_storage` are loaded.

#### Install iRiver driver/manager software

[Install](/index.php/Install "Install") the [libifp](https://www.archlinux.org/packages/?name=libifp) package, and then reboot the system.

#### Verify that you can connect to your iRiver device

Connect iRiver device to your PC with the supplied USB cable and then run this command:

```
$ ifpline ls /

```

If successful, the output should display the root directory on your iRiver, similar to this:

```
d VOICE
d RECORD
d music

```

#### Midnight Commander setup

*   [Install](/index.php/Install "Install") Midnight Commander, provided by the [mc](https://www.archlinux.org/packages/?name=mc) package.
*   Copy the `ifpline` binary to the Midnight Commander extfs directory

```
# cp /usr/bin/ifpline /usr/share/mc/extfs/

```

*   Edit `/usr/share/mc/extfs/extfs.ini` and add a new line at the bottom:

```
ifpline

```

*   Save changes to `extfs.ini`
*   Start Midnight Commander, and in its command line, enter:

```
cd /#ifpline

```

You should now have full access to your iRiver directories via Midnight Commander. You will be able to copy and delete music tracks as you wish.

#### Setting up udev to automatically assign permissions

Put the following into the file `/etc/udev/rules.d/ifpdev.rules`:

 `/etc/udev/rules.d/ifpdev.rules` 
```
 # udev rules file for supported ifp devices
 #
 # To add an USB ifp device, add a rule to the list below between the SUBSYSTEM...
 # and LABEL... lines.
 #
 # To run a script when your ifp is plugged in, add RUN="/path/to/script"
 # to the appropriate rule.
 #

 SUBSYSTEM!="usb_device", ACTION!="add", GOTO="libifp_rules_end"

 # ifp-1xx
 SYSFS{idVendor}=="4102", SYSFS{idProduct}=="1001", GROUP="storage"
 # ifp-3xx
 SYSFS{idVendor}=="4102", SYSFS{idProduct}=="1003", GROUP="storage"
 # ifp-5xx
 SYSFS{idVendor}=="4102", SYSFS{idProduct}=="1005", GROUP="storage"
 # ifp-7xx
 SYSFS{idVendor}=="4102", SYSFS{idProduct}=="1007", GROUP="storage"
 # ifp-8xx
 SYSFS{idVendor}=="4102", SYSFS{idProduct}=="1008", GROUP="storage"
 # ifp-9xx
 SYSFS{idVendor}=="4102", SYSFS{idProduct}=="1009", GROUP="storage"
 # ifpdev
 SYSFS{idVendor}=="4102", SYSFS{idProduct}=="1010", GROUP="storage"
 # The N10
 SYSFS{idVendor}=="4102", SYSFS{idProduct}=="1011", GROUP="storage"

 LABEL="libifp_rules_end"

```

And add the user you want to have permissions to the storage [group](/index.php/Group "Group"):

```
# gpasswd -a username storage

```

### Notes

Do not delete the default folders in the `/` directory of your iRiver — it may cause issues!

Midnight Commander, by default, preserves file permissions when copying files. Because these file permissions cannot be written to your iRiver, an error message will be displayed after each file copy. To prevent these messages from appearing, uncheck the "preserve attributes" check box on Midnight Commander's copy dialog.

If you frequently copy directories to your iRiver rather than individual tracks, then select the directory to copy and check the "Dive into subdir if exists" checkbox.

The `ifpline` commands can easily be incorporated into your own shell scripts to make the management of your iRiver even easier! Run `ifpline` for a list of all supported commands.

#### Upgrading firmware

1.  Get the firmware for the manager version and name it `IFP-3XXT.HEX`.
2.  Run `ifpline firmupdate ./IFP-3XXT.HEX`.
3.  Wait for the device to update, concluding in a power-off.
4.  Unplug everything, turn on the player, and plug it back in.
5.  Run `ifpline ls /` to see some files and ensure it is working.