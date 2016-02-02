# Wvdial

WvDial is a Point-to-Point Protocol dialer: it dials a modem and starts pppd in order to connect to the Internet.

## Contents

*   [1 Configuration](#Configuration)
*   [2 Using wvdial](#Using_wvdial)
    *   [2.1 Using suid](#Using_suid)
    *   [2.2 Using a dialout group](#Using_a_dialout_group)
    *   [2.3 Using sudo](#Using_sudo)
*   [3 Tips and Tricks](#Tips_and_Tricks)
    *   [3.1 Low connection speed](#Low_connection_speed)
        *   [3.1.1 QoS parameter](#QoS_parameter)
        *   [3.1.2 Baud parameter](#Baud_parameter)
    *   [3.2 Auto Reconnect](#Auto_Reconnect)
    *   [3.3 Multiple devices](#Multiple_devices)

## Configuration

When WvDial starts, it first loads its configuration from `/etc/wvdial.conf` and `~/.wvdialrc` . If `/etc/wvdial.conf` is not present, the easiest way to create it is to use the provided configuration utility wvdialconf.

```
wvdialconf /etc/wvdial.conf

```

It helps in generating the configuration file needed by WvDial. wvdialconf detects your modem, and fills in automatically the Modem, maximum Baud rate, and a good initialization string (Init options) and generates or updates the WvDial configuration file (`/etc/wvdial.conf`) based on this information.

It is safe to run wvdialconf if a configuration file already exists. In that case, only the Modem, Baud, Init, and Init2 options are changed in the [Dialer Defaults] section, and only if autodetection is successful.

**Note:** Wvdialconf does not automatically fill in your login information. You need to edit `/etc/wvdial.conf` and specify the phone number, login name, and password of your internet account in order for WvDial to work.

After you have filled in your login information, wvdial ought to work. You can move to the next section. However for providers of USB modems that require a specific Init string and user/password combination, [mkwvconf-git](https://aur.archlinux.org/packages/mkwvconf-git/)<sup><small>AUR</small></sup> can help generate a wvdial configuration (based on the [mobile-broadband-provider-info-git](https://aur.archlinux.org/packages/mobile-broadband-provider-info-git/)<sup><small>AUR</small></sup> package).

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

## Using wvdial

There are a few different ways of giving regular users the ability to use **wvdial** to dial a ppp connection. This document describes three different ways, each of them differ in difficulty to set up and the implication on security.

wvdial is to be run as root with the following command:

```
# wvdial <section>

```

Leave <section> blank if you have not added a section or if `/etc/wvdial.conf` is auto-generated.

```
# wvdial

```

### Using suid

This is arguable the easiest setup but has major impact on system security since it means that _every user can run wvdial as root_. Please consider using one of the other solutions instead.

As normal users cannot use wvdial to dial a ppp connection by default, change permissions:

```
# chmod u+s /usr/bin/wvdial

```

You should see the following permissions:

```
# ls -l /usr/bin/wvdial
-rwsr-xr-x  1 root root 114368 2005-12-07 19:21 /usr/bin/wvdial

```

### Using a dialout group

Another, slightly more secure way is to set up a group called **dialout** (call the group as prefered) and give members of this group permission to run `wvdial` as root.

First create the group and add the users to it:

```
# groupadd dialout
# gpasswd -a username dialout

```

**Note:** You need to logout and log back in for the current user's group list to be updated.

Then set the group and adjust the permissions on `wvdial`:

```
# chgrp dialout /usr/bin/wvdial
# chmod u+s,o= /usr/bin/wvdial

```

The files should have the following permissions:

```
$ ls -l /usr/bin/wvdial

```

```
-rwsr-x---  1 root dialout 114368 2005-12-07 19:21 /usr/bin/wvdial

```

### Using sudo

	_See main article: [sudo](/index.php/Sudo "Sudo")_

[sudo](/index.php/Sudo "Sudo") arguably offers the most secure option to allow regular users to establish dial-up connections using `wvdial`. It can be used to give permission both on a per-user and group basis. Another benefit of using `sudo` is that it is only needed to do the setup once; both previous solutions will be "undone" when a new package of `wvdial` is installed.

Use `visudo` to edit the file `/etc/sudoers`:

```
# visudo

```

To give a specific user permission to run `wvdial` as root, add the following line (changing the username):

```
username localhost = /usr/bin/wvdial

```

To give all members of a group (`dialout` in this case) the same permission:

```
%dialout localhost = /usr/bin/wvdial

```

If `ip addr` shows a pppd entry, it means that the session is ready.

## Tips and Tricks

The following are applicable to USB modems.

### Low connection speed

Someone claims that the connection speed under linux is lower than Windows. [https://bbs.archlinux.org/viewtopic.php?id=111513](https://bbs.archlinux.org/viewtopic.php?id=111513)

A short summary for possible solutions which are not fully verified. In most of conditions, the low speed is caused by bad receiver signals and too many people in cell. But you still could use the following method to try to improve the connection speed.

#### QoS parameter

AT+CGEQMIN and AT+CGEQREQ command could used to set the Qos command. And also it should be possible to used to decrease and limit the connect speed. Add the following Init command in `/etc/wvdial.conf`.

```
Init6 = AT+CGEQMIN=1,4,64,640,64,640
Init7 = AT+CGEQREQ=1,4,64,640,64,640

```

#### Baud parameter

Baud parameter in `/etc/wvdial.conf` could be used to increase the connection speed.

```
Baud = 460800

```

It is advisable to see the baud rate set by the official modem application under Windows.

### Auto Reconnect

If wvdial randomly drops connection you can use script below.

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

Often there will be several devices (at /dev/ttyUSB0, /dev/ttyUSB1, /dev/ttyUSB2 for example). If in doubt about which to use, try each of them in turn or use /dev/gsmmodem (a link set up by usb_modeswitch) which should point to the correct one. Once the configuration files are prepared, the internet connection is established by running

```
$ wvdial <section>

```

If necessary additional setup commands can be placed in a simple script like this:

```
usb_modeswitch
sleep 2
modprobe usbserial vendor=0xVVVV product=0xMMMM maxSize=4096
sleep 2
wvdial thenet

```

where VVVV is the hexadecimal vendor ID from lsusb, MMMM is the hexadecimal product ID _when in modem mode_, and "thenet" is the name of the section in wvdial.conf which you wish to use. The maxSize option may or may not be necessary. It simplifies matters if you disable the SIM PIN, but if you require it, run "wvdial mypin" before "wvdial thenet".

The final wvdial command should start pppd and the obained IP address should be visible in the terminal output. At that point the internet connection should be live, which can be easily checked with a web browser or by pinging an external IP address.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Wvdial&oldid=414627](https://wiki.archlinux.org/index.php?title=Wvdial&oldid=414627)"