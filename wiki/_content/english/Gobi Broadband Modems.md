This is a short tutorial on connecting to the internet using your gobi modem.

## Contents

*   [1 Device identification](#Device_identification)
*   [2 gobi_loader](#gobi_loader)
*   [3 Manage Connection in Network Manager](#Manage_Connection_in_Network_Manager)
*   [4 Connection](#Connection)
    *   [4.1 wvdial](#wvdial)
*   [5 See also](#See_also)

## Device identification

Install [usbutils](https://www.archlinux.org/packages/?name=usbutils) and then examine the output of

```
$ lsusb

```

which will show the vendor and product IDs of the device.

For example, my HP un2430 modem:

```
Bus 001 Device 005: ID 03f0:371d Hewlett-Packard 

```

As of linux-3.1.1-1 the device is detected by the qcserial module, if not, you are going to have to recompile the qcserial module with your added product and vendor id.

Alternatively you can add the Product and Vendor ID by writing them into the new_id file (best both at the same time because most Gobi modules switch the Product ID when the Firmware is loaded). Here the Shell Commands i had to use (in a root shell, sudo does not work in this case for some reason): my integrated Gobi2K has the Vendor ID 04da and the Product IDs 250e (waiting for Firmware) and 250f (firmware loaded)

```
echo "04da 250e" > /sys/bus/usb-serial/drivers/qcserial/new_id
echo "04da 250f" > /sys/bus/usb-serial/drivers/qcserial/new_id

```

note that this has to be repeated when you reload the qcserial module or reboot/shutdown.

## gobi_loader

"gobi_loader is a firmware loader for Qualcomm Gobi USB chipsets. These devices appear in an uninitialised state when power is applied and require firmware to be loaded before they can be used as modems. gobi_loader adds a udev rule that will trigger loading of the firmware and make the modem usable." ([http://www.codon.org.uk/~mjg59/gobi_loader/](http://www.codon.org.uk/~mjg59/gobi_loader/))

Install [gobi-loader](https://aur.archlinux.org/packages/gobi-loader/) and [gobi-firmware](https://aur.archlinux.org/packages/gobi-firmware/) from [AUR](/index.php/AUR "AUR").

After installation, you should enter your product and vendor id in the `/lib/udev/rules.d/60-gobi.rules`

Then a simple reload of the qcserial module:

```
# rmmod qcserial
# modprobe qcserial

```

## Manage Connection in Network Manager

ModemManager is required for network manager to detect any mobile broadband devices.

This needs to be enabled with systemctl start ModemManager and systemctl enable ModemManager. As soon as they are started the Mobile Broadband option will be available from the Network Manager Applet.

Make sure [mobile-broadband-provider-info](https://www.archlinux.org/packages/?name=mobile-broadband-provider-info) and [nm-connection-editor](https://www.archlinux.org/packages/?name=nm-connection-editor) are installed.

To use this quite old modem, you need to blacklist qmi_wwan and cdc_wdm modules from loading into [modern] Linux kernel. Else, if these modules are loaded, ModemManager recognizes this modem as something new with QMI interface, and then complains about too small versions of some QMI services. [Source](https://bugs.freedesktop.org/show_bug.cgi?id=93392)

## Connection

### wvdial

*See main article: [wvdial](/index.php/Wvdial "Wvdial")*

The general procedure is to switch the device into modem mode, make sure the ttyUSB device(s) are recognized by the qcserial kernel module, and then to run wvdial to dial, connect and start pppd.

Install [wvdial](https://www.archlinux.org/packages/?name=wvdial). The configuration file `/etc/wvdial.conf` will in general depend on (a) which device you have (b) which mobile network you are connecting to. A single wvdial.conf file can be defined with named sections to be usable with several USB modems and networks, should you need them.

Run:

```
# wvdialconf

```

which will attempt to write `/etc/wvdial.conf` correctly. You will need to add the user, password and Access Point Name (APN). You can obtain these (i) from your network provider, (ii) from other users via published wvdial.confs, or (iii) by logging the USB tty traffic under another operating system (Sysinternals' Portmon).

My `/etc/wvdial.conf` looks like this:

```
[Dialer status]
Init1 = AT+CPIN?
Init2 = ATI
Modem = /dev/ttyUSB1

[Dialer pin]
Modem = /dev/ttyUSB1
Init1 = AT+CPIN=1234

[Dialer wwan]
Init1 = ATZ
Init2 = AT+CGDCONT=1,"IP","data.apn.com"
Stupid Mode = yes
Phone = *99***1#
New PPPD = yes
Modem = /dev/ttyUSB1
Username = XXXXXX
Dial Command = ATDT
Password = XXXXXX
Baud = 460800

```

To simplify the procedure, I took my SIM card out and disabled the PIN so I do not have to run "wvdial pin" before connecting to the internet.

Often there will be several devices (at `/dev/ttyUSB0`, `/dev/ttyUSB1`, `/dev/ttyUSB2` for example). If in doubt about which to use, try each of them in turn. Once the configuration files are prepared, the internet connection is established by running

```
$ wvdial <section>

```

The final wvdial command should start pppd and the obained IP address should be visible in the terminal output. At that point the internet connection should be live, which can be easily checked with a web browser or by pinging an external IP address.

## See also

*   [USB 3G Modem](/index.php/USB_3G_Modem "USB 3G Modem")
*   [Huawei E220](/index.php/Huawei_E220 "Huawei E220")
*   [Allow users to dial with wvdial](/index.php/Allow_users_to_dial_with_wvdial "Allow users to dial with wvdial")
*   [Idea netsetter(Huawei EG162G)](/index.php/Idea_netsetter(Huawei_EG162G) "Idea netsetter(Huawei EG162G)")
*   [ZTE MF636](/index.php/ZTE_MF636 "ZTE MF636")
*   [Dialup without a dialer HOWTO](/index.php/Dialup_without_a_dialer_HOWTO "Dialup without a dialer HOWTO")
*   [3G and GPRS modems with pppd alone](/index.php/3G_and_GPRS_modems_with_pppd_alone "3G and GPRS modems with pppd alone")
*   [Huawei E1550 3G modem](/index.php/Huawei_E1550_3G_modem "Huawei E1550 3G modem")