Many Lenovo ThinkPads come with a mobile broadband modem. By inserting a SIM card into the modem, it is possible to use a cellular network to connect to the internet.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Requirements](#Requirements)
*   [2 Procedure](#Procedure)
*   [3 Alternative method](#Alternative_method)
*   [4 Getting around BIOS-level whitelist restrictions](#Getting_around_BIOS-level_whitelist_restrictions)
    *   [4.1 Settings for Sierra Wireless EM7455](#Settings_for_Sierra_Wireless_EM7455)
        *   [4.1.1 General description](#General_description)
        *   [4.1.2 Step-by-step](#Step-by-step)
        *   [4.1.3 Remarks](#Remarks)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 WWAN/LTE GUI](#WWAN/LTE_GUI)
*   [6 See also](#See_also)

## Requirements

The broadband modems in newer ThinkPads use the QMI modem protocol---see [this article](http://sigquit.wordpress.com/2012/08/20/an-introduction-to-libqmi/) for more information. These modems will show up as `/dev/cdc-wdm` on the filesystem.

It is not yet (September 2014) possible to initialize a QMI modem for use on Linux. Use Windows to activate the modem using [Lenovo's activation app](http://support.lenovo.com/us/en/downloads/migr-68495) (or web search for "Lenovo mobile broadband" for the correct app for your modem). The modem will not work until it has been correctly initialized using the app.

## Procedure

[Install](/index.php/Install "Install") the [libqmi](https://www.archlinux.org/packages/?name=libqmi) package available in the [official repositories](/index.php/Official_repositories "Official repositories"), which provides the `qmicli` and `qmi-network` programs. Also install [net-tools](https://www.archlinux.org/packages/?name=net-tools), which provides the `ifconfig` command.

There is a [helper script](https://raw.githubusercontent.com/penguin2716/qmi_setup/master/qmi_setup.sh) for `qmi-network` available on GitHub. Save the script to somewhere in your `$PATH` and make it executable, and then review the script. The values of some of the variables might need to be changed, especially `WWAN_DEV`.

Load the kernel modules `qmi_wwan` and `qcserial`:

```
$ modprobe qmi_wwan
$ modprobe qcserial
```

Also read the readme on the [GitHub page of the QMI helper](https://github.com/penguin2716/qmi_setup) for any further prerequisites. In particular, you may need to set the APN provided by your cellular internet provider in `/etc/qmi-network.conf`.

 `/etc/qmi-network.conf`  `APN=foo.bar.net` 

Finally, running `qmi_setup.sh start` should start the cellular internet connection.

## Alternative method

Reference information: [http://www.thinkwiki.org/wiki/Qualcomm_Gobi_2000](http://www.thinkwiki.org/wiki/Qualcomm_Gobi_2000)

First of all you need to make sure what model your modem is. Open your thinkpads backplate and look for IC or FCC ID. For this example we're going to use GOBI2000 (IC: 2723A-GOBI2000, FCC ID: J9CGOBI2000-L)

Enable your modem device from you BIOS I/O settings.

Download the driver installer exe from support.lenovo.com/en_US/downloads/detail.page?DocID=DS001302 and extract it with Wine. It will unpack the drivers to ~/.wine/drive_c/DRIVERS/WWANQL. The unpacker will prompt you to install the drivers automatically after unpacking, but if you need the installer again it's GobiInstaller.msi in previously mentioned folder. The installer will in turn unpack the firmware images to ~/.wine/drive_c/Program\ Files\ \(x86\)/QUALCOMM/Images/Lenovo . Now refer to the reference information on what firmware you want/need. Generally you are good to go with the Generic UMTS and Default Firmware (Forlders 6 an UMTS)

Download gobi loader from [http://www.codon.org.uk/~mjg59/gobi_loader/](http://www.codon.org.uk/~mjg59/gobi_loader/), follow the instructions to make and install (you might need to 'sudo make install'). Now copy the 3 previous firmware files to /lib/firmware/gobi (if the folder doesn't exist, create it). Insert your sim card to the port found under your battery pack and restart. Your modem should now show up in your network manager.

## Getting around BIOS-level whitelist restrictions

In newer ThinkPad models, it is normally impossible to swap the LTE modem for a supported one due to BIOS-level restrictions ("whitelists" of allowed M.2 expansion cards) implemented in all modern Lenovo laptops. However, a method has been found to configure any Sierra Wireless EM73xx/EM74xx modem to "evade" the whitelist checks, so these modems can be used normally.

We will assume the model to be `Sierra Wireless EM7455` here.

### Settings for Sierra Wireless EM7455

#### General description

Use `AT!CUSTOM="FASTENUMEN",0` AT command to disable the modem's *USB fast enumeration* feature. The modem will take a significantly longer time to appear on the USB bus and the firmware will "miss" the modem at boot time.

Alternatively, use `AT!CUSTOM="FASTENUMEN",2` to selectively enable *USB fast enumeration* for warm boots only. The modem will reappear faster on S3 resume but still evade the whitelist checks on regular boots *and* reboots (the mechanism of this effect is not fully clear to the author).

This comes with a downside: because the firmware does not "see" the modem, it will not export the [WWAN rfkill](/index.php/Wireless_network_configuration#Rfkill_caveat "Wireless network configuration") but instead it will unconditionally assert the `W_DISABLE` pin of the M.2 slot, forcing the modem into "airplane mode". Use `AT!PCOFFEN=2` AT command to configure the modem to ignore this pin.

#### Step-by-step

1\. Boot the laptop with the stock modem in place and WWAN card access enabled in BIOS setup.

2\. Suspend the laptop (make sure it is configured to use S3).

3\. Hot-swap the stock Fibocom modem with the Sierra Wireless one, then resume. Whitelists are not consulted at S3 resume.

Check that the modem is present on the USB bus:

```
# lsusb
<...>
Bus 001 Device 004: ID 1199:9071 Sierra Wireless, Inc.
<...>

```

Remember the VID (vendor ID) of the modem (`1199` in this example).

4\. Stop ModemManager, if it is running:

```
 # systemctl stop ModemManager

```

5\. Optionally, update the modem firmware with the `qmi-firmware-update` tool:

```
# cd /path/to/extracted/firmware
# qmi-firmware-update -d 1199 -u *.cwe *.nvu

```

6\. Change the modem's USB composition to enable AT command ports:

```
# qmicli -d /dev/cdc-wdm1 --dms-swi-set-usb-composition=8

```

7\. Power-cycle the modem as advised by `qmicli`:

```
# qmicli -d /dev/cdc-wdm1 --dms-set-operating-mode=offline
# qmicli -d /dev/cdc-wdm1 --dms-set-operating-mode=reset

```

8\. Wait for the modem to reappear, then verify:

```
# qmicli -d /dev/cdc-wdm1 --dms-swi-get-usb-composition
[/dev/cdc-wdm1] Successfully retrieved USB compositions:
            USB composition 6: DM, NMEA, AT, QMI
        [*] USB composition 8: DM, NMEA, AT, MBIM
            USB composition 9: MBIM

```

9\. Verify that the three serial ports `/dev/ttyUSB0`, `/dev/ttyUSB1` and `/dev/ttyUSB2` are now available (assuming you do not have any other USB-serial converters plugged in):

```
# ls -l /dev/ttyUSB*
crw-rw---- 1 root uucp 188, 0 Feb 14 20:11 /dev/ttyUSB0
crw-rw---- 1 root uucp 188, 1 Feb 14 20:11 /dev/ttyUSB1
crw-rw---- 1 root uucp 188, 2 Feb 14 20:11 /dev/ttyUSB2

```

10\. Attach to `/dev/ttyUSB2` with a serial terminal emulator of your choice (e. g. `screen`):

```
# screen /dev/ttyUSB2 115200

```

11\. Enter the AT commands (note that you do not need to type `OK`, the replies are included here as part of a session transcript):

11.1\. Enable command echo (if echo is initially disabled, you won't see this command as you type it):

```
ATE1
OK

```

11.2\. Unlock engineering commands:

```
AT!ENTERCND="A710"
OK

```

11.3\. Check customization options (these are the author's options):

```
AT!CUSTOM?
!CUSTOM: 
             GPSENABLE          0x01
             GPSSEL             0x01
             IPV6ENABLE         0x01
             SIMLPM             0x01
             SINGLEAPNSWITCH    0x01

OK

```

11.4\. Configure *USB fast enumeration* (swap `2` for `0` if you want to play it safe):

```
AT!CUSTOM="FASTENUMEN",2
OK

```

11.5\. Verify:

```
AT!CUSTOM?
!CUSTOM: 
             GPSENABLE          0x01
             GPSSEL             0x01
             IPV6ENABLE         0x01
             SIMLPM             0x01
             FASTENUMEN         0x02
             SINGLEAPNSWITCH    0x01

OK

```

*(it should now show the `FASTENUMEN` option alongside others)*

11.6\. Configure the modem to ignore W_DISABLE:

```
AT!PCOFFEN=2
OK

```

11.7\. Verify:

```
AT!PCOFFEN?
2

OK

```

11.8\. Reset the modem:

```
AT!RESET
OK

```

*(the terminal will disconnect after a while)*

12\. Wait for the modem to reappear, then verify configuration by rebooting / powering down / hard resetting the laptop.

#### Remarks

For more information (including the original thought process that led to this discovery), see these [lenovo](https://forums.lenovo.com/t5/Linux-Discussion/X1C-gen-6-Fibocom-L850-GL-Ubuntu-18-04/m-p/4307332/highlight/true#M12232) [threads](https://forums.lenovo.com/t5/Linux-Discussion/Getting-Sierra-EM7455-and-similar-to-work-on-X1C6/td-p/4326043) and this [reddit](https://www.reddit.com/r/thinkpad/comments/a3yd2j/sierra_wireless_em7455_seems_working_with_my/) thread.

You may also apply other useful configuration options described [here](https://github.com/danielewood/sierra-wireless-modems).

## Troubleshooting

*   Ensure that you have initialized the modem on Windows.

### WWAN/LTE GUI

Install [NetworkManager](/index.php/NetworkManager "NetworkManager") and [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) to make your life easier finding the correct APN for your SIM card.

## See also

*   [Thinkwiki](http://www.thinkwiki.org)