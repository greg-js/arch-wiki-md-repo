WvDial is a Point-to-Point Protocol dialer: it dials a modem and starts [ppp](/index.php/Ppp "Ppp") in order to connect to the Internet.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 suid](#suid)
    *   [3.2 Group](#Group)
    *   [3.3 sudo](#sudo)
*   [4 Tips and Tricks](#Tips_and_Tricks)
    *   [4.1 Low connection speed](#Low_connection_speed)
    *   [4.2 Auto Reconnect](#Auto_Reconnect)
    *   [4.3 Multiple devices](#Multiple_devices)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [wvdial](https://www.archlinux.org/packages/?name=wvdial) package.

## Configuration

When *wvdial* starts, it first loads its configuration from `/etc/wvdial.conf` and `~/.wvdialrc` . If `/etc/wvdial.conf` is not present, the easiest way to create it is to use the provided configuration utility *wvdialconf*:

```
wvdialconf /etc/wvdial.conf

```

It helps in generating the configuration file needed by *wvdial*. *wvdialconf* detects your modem, and fills in automatically the Modem, maximum Baud rate, and a good initialization string (Init options) and generates or updates the *wvdial* configuration file (`/etc/wvdial.conf`) based on this information.

It is safe to run *wvdialconf* if a configuration file already exists. In that case, only the Modem, Baud, Init, and Init2 options are changed in the [Dialer Defaults] section, and only if autodetection is successful.

**Note:** *wvdialconf* does not automatically fill in your login information. You need to edit `/etc/wvdial.conf` and specify the phone number, login name, and password of your internet account in order for *wvdial* to work.

After you have filled in your login information, *wvdial* ought to work. You can move to the next section. However for providers of USB modems that require a specific Init string and user/password combination, [mkwvconf-git](https://aur.archlinux.org/packages/mkwvconf-git/) can help generate a *wvdial* configuration (based on the [mobile-broadband-provider-info-git](https://aur.archlinux.org/packages/mobile-broadband-provider-info-git/) package).

A typical `/etc/wvdial.conf` looks like this after manual configuration:

```
[Dialer Defaults]
Init1 = ATZ
Init2 = ATQ0 V1 E1 S0=0 &C1 &D2 +FCLASS=0
Modem Type = Analog Modem
ISDN = 0
Modem = /dev/ttyUSB2
Baud = 9600

[Dialer thenet]
Phone = *99***1#
Username = thenetuser
Password = thenetpw
; Username = 9180****** (If your provider use without Username)
; Password = 9180****** (If your provider use without Password)
Stupid Mode = 1
Baud = 460800
Init3 = AT+CGDCONT=1,"IP","apn.thenet.net"

[Dialer mypin]
Init4 = AT+CPIN=1234
```

## Usage

There are a few different ways of giving regular users the ability to use *wvdial* to dial a ppp connection. This document describes three different ways, each of them differ in difficulty to set up and the implication on security.

*wvdial* is to be run as root with the following command:

```
# wvdial *option*

```

Leave *option* blank if you have not added a section or if `/etc/wvdial.conf` is auto-generated.

```
# wvdial

```

### suid

**Warning:** This is arguable the easiest setup but has major impact on system security since it means that **every user can run** *wvdial* **as root**. Please consider using one of the other solutions instead.

As normal users cannot use *wvdial* to dial a PPP connection by default, change permissions:

```
# chmod u+s /usr/bin/wvdial

```

You should see the following permissions:

```
# ls -l /usr/bin/wvdial
-rwsr-xr-x  1 root root 114368 2005-12-07 19:21 /usr/bin/wvdial

```

### Group

Another, slightly more secure way is to set up a group called `dialout` (call the group as preferred) and give members of this group permission to run *wvdial* as root.

First create the group and add the users to it:

```
# groupadd dialout
# gpasswd -a username dialout

```

**Note:** You need to logout and log back in for the current user's group list to be updated.

Then set the group and adjust the permissions on *wvdial*:

```
# chgrp dialout /usr/bin/wvdial
# chmod u+s,o= /usr/bin/wvdial

```

The files should have the following permissions:

 `$ ls -l /usr/bin/wvdial` 
```
-rwsr-x---  1 root dialout 114368 2005-12-07 19:21 /usr/bin/wvdial

```

### sudo

[sudo](/index.php/Sudo "Sudo") arguably offers the most secure option to allow regular users to establish dial-up connections using *wvdial*. It can be used to give permission both on a per-user and group basis. Another benefit of using *sudo* is that it is only needed to do the setup once; both previous solutions will be "undone" when a new package of *wvdial* is installed.

Use *visudo* to edit the file `/etc/sudoers`:

```
# visudo

```

To give a specific user permission to run *wvdial* as root, add the following line (changing the username):

```
*username* localhost = /usr/bin/wvdial

```

To give all members of a group (`dialout` in this case) the same permission:

```
%dialout localhost = /usr/bin/wvdial

```

If `ip addr` shows a pppd entry, it means that the session is ready.

## Tips and Tricks

The following are applicable to USB modems.

### Low connection speed

See [USB 3G Modem#Low connection speed](/index.php/USB_3G_Modem#Low_connection_speed "USB 3G Modem").

### Auto Reconnect

If *wvdial* randomly drops connection you can use script below:

```
#! /bin/bash
(
   while : ; do
       wvdial
       sleep 10
   done
) &

```

### Multiple devices

Often there will be several devices (at `/dev/ttyUSB0`, `/dev/ttyUSB1`, `/dev/ttyUSB2` for example). If in doubt about which to use, try each of them in turn or use `/dev/gsmmodem` (a link set up by *usb_modeswitch*) which should point to the correct one. Once the configuration files are prepared, the internet connection is established by running:

```
$ wvdial *options*

```

If necessary additional setup commands can be placed in a simple script like this:

```
usb_modeswitch
sleep 2
modprobe usbserial vendor=0xVVVV product=0xMMMM maxSize=4096
sleep 2
wvdial thenet

```

where *VVVV* is the hexadecimal vendor ID from lsusb, *MMMM* is the hexadecimal product ID when in modem mode, and "thenet" is the name of the section in `wvdial.conf` which you wish to use. The *maxSize* option may or may not be necessary. It simplifies matters if you disable the SIM PIN, but if you require it, run `wvdial mypin` before `wvdial thenet`.

The final *wvdial* command should start *pppd* and the obained IP address should be visible in the terminal output. At that point the internet connection should be live, which can be easily checked with a web browser or by pinging an external IP address.

## See also

*   [GitHub repository](https://github.com/wlach/wvdial)