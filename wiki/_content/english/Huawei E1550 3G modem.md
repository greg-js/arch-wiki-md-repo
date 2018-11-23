## Contents

*   [1 Introduction](#Introduction)
*   [2 Prepare device](#Prepare_device)
    *   [2.1 Switch into modem mode](#Switch_into_modem_mode)
    *   [2.2 Driver loading](#Driver_loading)
    *   [2.3 Optional: device naming](#Optional:_device_naming)
*   [3 Connecting internet](#Connecting_internet)
*   [4 Sending SMS](#Sending_SMS)
*   [5 USSD Requests](#USSD_Requests)
*   [6 Success Stories](#Success_Stories)
*   [7 References](#References)

## Introduction

This article describes how to configure Huawei E1550 3G modems.

This modem is generic modem device, but there are two kludges:

*   you need to switch it into modem mode
*   you need to load proper driver (usbserial)

## Prepare device

### Switch into modem mode

By default kernel recongnizes it as usb-storage device (SCSI CD-ROM). It is true, because of this modem contains MicroSD card (up to 4Gb) reader and internal flash.

To switch modem on you shoud run

```
$ /lib/udev/usb_modeswitch --vendor 0x12d1 --product 0x1446 --type option-zerocd

```

command.

See also the [usb_modeswitch](https://www.archlinux.org/packages/?name=usb_modeswitch) package, which you may need in future since in udev-157 modem-modeswitch has been renamed and changed as described in the [commit](http://git.kernel.org/?p=linux/hotplug/udev.git;a=commit;h=4dd9b291354e76f34b0d6d7b5c3b28d03a624418). This package does not need any modifications, just install it.

Also you can create udev's config: /etc/udev/rules.d/15-huawei-e1550.rules

```
ACTION=="add", SUBSYSTEM=="usb", ATTRS{idVendor}=="12d1", ATTRS{idProduct}=="1446", RUN+="/lib/udev/usb_modeswitch --vendor 0x12d1 --product 0x1446 --type option-zerocd"

```

After that, modem changes its USB IDs to 12d1:140c and /proc/bus/usb/devices shows new USB endpoints.

### Driver loading

usbserial is proper driver for this modem, but probably it does not recognize it, so you shold force it, passing USB IDs.

```
 # modprobe usbserial vendor=0x12d1 product=0x140c

```

or put options into /etc/modprobe.d/modprobe.conf

```
 options usbserial vendor=0x12d1 product=0x140c

```

(do not forget to 'rmmod usbserial' if it is already loaded before)

### Optional: device naming

You can generate symlinks to the ttyUSB* ports for a more human readable configuration with udev rules.

For a Huawei device which identifies with the USB ID 12D1:1001 after modeswitching and has 3 serial ports:

```
 SUBSYSTEMS=="usb", ATTRS{modalias}=="usb:v12D1p1001*", KERNEL=="ttyUSB*", ATTRS{bInterfaceNumber}=="00", ATTRS{bInterfaceProtocol}=="ff", SYMLINK+="ttyUSB_utps_modem"
 SUBSYSTEMS=="usb", ATTRS{modalias}=="usb:v12D1p1001*", KERNEL=="ttyUSB*", ATTRS{bInterfaceNumber}=="01", ATTRS{bInterfaceProtocol}=="ff", SYMLINK+="ttyUSB_utps_diag"
 SUBSYSTEMS=="usb", ATTRS{modalias}=="usb:v12D1p1001*", KERNEL=="ttyUSB*", ATTRS{bInterfaceNumber}=="02", ATTRS{bInterfaceProtocol}=="ff", SYMLINK+="ttyUSB_utps_pcui"

```

For a Huawei device which identifies with the USB ID 12D1:1003 after modeswitching and has 2 serial ports:

```
 SUBSYSTEMS=="usb", ATTRS{modalias}=="usb:v12D1p1003*", KERNEL=="ttyUSB*", ATTRS{bInterfaceNumber}=="00", ATTRS{bInterfaceProtocol}=="ff", SYMLINK+="ttyUSB_utps_modem"
 SUBSYSTEMS=="usb", ATTRS{modalias}=="usb:v12D1p1003*", KERNEL=="ttyUSB*", ATTRS{bInterfaceNumber}=="01", ATTRS{bInterfaceProtocol}=="ff", SYMLINK+="ttyUSB_utps_pcui"

```

## Connecting internet

Now you have new 2 or 3 /dev/ttyUSB* devices.Most likely first of them (ttyUSB0 if you had not such devices before) is PPP compatible modem. Use it as usual with pppd, kppp, gnome-ppp, network-manager, etc.

**Note:** If you want to use your 3G modem with [NetworkManager](/index.php/NetworkManager "NetworkManager"), you have to install the package [modemmanager](https://www.archlinux.org/packages/?name=modemmanager) and then [restart](/index.php/Restart "Restart") the `NetworkManager.service`. Now you can 'Enable Mobile Broadband' in the networkmanager applet.

## Sending SMS

You can use gammu.

Edit ~/.gammurc

```
 [gammu]
 port=/dev/ttyUSB0
 connection=at
 name=huawei e1550
 model=

```

The run command:

```
 gammu sendsms TEXT +7123456789 -text qwe

```

## USSD Requests

Use [huawei-ussd](https://aur.archlinux.org/packages/huawei-ussd/) package. Or use [ussd.php](https://github.com/gnomeby/ussd) tool.

## Success Stories

2010-August-03: I didn't do anything, I just installed usb_modeswitch-1.1.3-2 and my kernel is 2.6.33\. In the syslog (/var/log/messages.log) the usb_modeswitch can automatically configure the modem correctly but I still cannot connect to the internet using gnome network manager applet, then I installed the modemmanager package and restart the networkmanager service. Everything is working properly now.

## References

*   [USB 3G Modem](/index.php/USB_3G_Modem "USB 3G Modem")
*   [Huawei E220](/index.php/Huawei_E220 "Huawei E220")