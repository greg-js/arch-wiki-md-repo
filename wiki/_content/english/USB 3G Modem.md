Related articles

*   [wvdial](/index.php/Wvdial "Wvdial")
*   [Direct Modem Connection](/index.php/Direct_Modem_Connection "Direct Modem Connection")
*   [3G and GPRS modems with pppd](/index.php/3G_and_GPRS_modems_with_pppd "3G and GPRS modems with pppd")
*   [Category:Modems](/index.php/Category:Modems "Category:Modems")

A number of mobile telephone networks around the world offer mobile internet connections over UMTS (or EDGE or GSM) using a portable USB modem device.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Remove the PIN](#Remove_the_PIN)
*   [2 Device identification](#Device_identification)
*   [3 Mode switching](#Mode_switching)
*   [4 Connection](#Connection)
    *   [4.1 Network Manager](#Network_Manager)
    *   [4.2 pppd](#pppd)
    *   [4.3 wvdial](#wvdial)
    *   [4.4 netctl](#netctl)
    *   [4.5 libmbim](#libmbim)
    *   [4.6 sakis3g](#sakis3g)
    *   [4.7 Connection halts after few minutes running](#Connection_halts_after_few_minutes_running)
*   [5 Tips and Tricks](#Tips_and_Tricks)
    *   [5.1 AT commands](#AT_commands)
    *   [5.2 Low connection speed](#Low_connection_speed)
    *   [5.3 Monitor used bandwidth](#Monitor_used_bandwidth)
    *   [5.4 Reading SMS](#Reading_SMS)
    *   [5.5 Fix image quality](#Fix_image_quality)

## Remove the PIN

First of all use your SIM card in a normal phone and disable the PIN request if present. If the SIM card asks the PIN wvdial will not work.

Failing that, you can also use *mmcli*, which is provided by [modemmanager](https://www.archlinux.org/packages/?name=modemmanager), to unlock the SIM card:

```
# mmcli --sim=*SIMNUMBER* --pin=*PIN*

```

where *SIMNUMBER* can be found using `mmcli --list-modems` and `mmcli --modem=[PATH|INDEX]`.

## Device identification

Examine the output of

```
$ lsusb

```

which will show the vendor and product IDs of the device. Note that some devices will show *two* different product IDs at different times as explained below.

## Mode switching

Often these devices will have two modes (1) USB flash memory storage (2) USB Modem. The first mode, sometimes known as ZeroCD, is often used to deliver an internet communications program for another operating system and is generally of no interest to Linux users. Additionally some have a slot into which the user can insert an additional flash memory card.

A useful utility for switching these devices into modem mode is [usb_modeswitch](https://www.archlinux.org/packages/?name=usb_modeswitch), available in the [official repositories](/index.php/Official_repositories "Official repositories").

Udev rules are supplied with the package in `/lib/udev/rules.d/40-usb_modeswitch.rules`. This contains entries for many devices, which it will switch to modem mode upon insertion.

When a device is switched, its product ID may change to a different value. The vendor ID will remain unchanged. This can be seen in the output of `lsusb`.

Some devices are supported in the USB serial kernel module called "option" (after the Option devices, but not limited to just those) and may be used without usb_modeswitch.

Udev itself included a utility called `/lib/udev/modem-modeswitch`. In udev 157 this was renamed to `/lib/udev/mobile-action-modeswitch` and morphed into a tool that only switches Mobile Action cables. For other devices use `usb_modeswitch`.

**Note:** You can find an alternative way to do this base on eject command [here](/index.php/ZTE_MF110/MF190#Switch_from_CD_mode_to_modem_mode_on_the_device "ZTE MF110/MF190").

## Connection

### Network Manager

After installing [usbutils](https://www.archlinux.org/packages/?name=usbutils) and [usb_modeswitch](https://www.archlinux.org/packages/?name=usb_modeswitch), you just need to install [modemmanager](https://www.archlinux.org/packages/?name=modemmanager) to make the modem work with [NetworkManager](/index.php/NetworkManager "NetworkManager").

Make sure both NetworkManager and ModemManager services are running, see [systemd#Using units](/index.php/Systemd#Using_units "Systemd") for details.

Make sure [mobile-broadband-provider-info](https://www.archlinux.org/packages/?name=mobile-broadband-provider-info) and [nm-connection-editor](https://www.archlinux.org/packages/?name=nm-connection-editor) are installed.

A system restart might be necessary for ModemManager to detect the USB modem. After you restart the NetworkManager-applet and plug the modem in again NetworkManager should recognize the modem in the menu without further configuration. Setting up the modem in NetworkManager is self-explanatory, you should only need the login-information provided by your network provider.

In case NetworkManager does not recognize the modem, check the output of ModemManager.service:

```
# systemctl status ModemManager

```

If you get error messages such as "Couldn't check support for device" and "not supported by any plugin", you may have to whitelist your device using the ModemManager filter rules [https://www.freedesktop.org/software/ModemManager/api/1.8.0/ref-overview-modem-filter.html](https://www.freedesktop.org/software/ModemManager/api/1.8.0/ref-overview-modem-filter.html)

Whilst running ModemManager gammu will not work. SMS and Ussd codes can be still used with [modem-manager-gui](https://www.archlinux.org/packages/?name=modem-manager-gui).

### pppd

[pppd](/index.php/Pppd "Pppd") can be used to configure 3g connections. Step by step instruction is available on [3G and GPRS modems with pppd](/index.php/3G_and_GPRS_modems_with_pppd "3G and GPRS modems with pppd"). Optionally, [pppconfig](https://aur.archlinux.org/packages/pppconfig/) can be used to simplify the pppd configuration using dialog interface.

### wvdial

See main article: [wvdial](/index.php/Wvdial "Wvdial")

### netctl

Netctl can be used to establish a connection using a USB modem. An example configuration file provided by [netctl](https://www.archlinux.org/packages/?name=netctl) is located at `/etc/netctl/examples/mobile_ppp`. Minimally you will probably have to specify

 `/etc/netctl/mobile_ppp` 
```
Interface=cdc-wdmX
Connection=mobile_ppp
PhoneNumber=XxxxXXXX
AccessPointName=Broadband

```

See the [netctl](/index.php/Netctl "Netctl") article and [netctl.profile](https://github.com/joukewitteveen/netctl/blob/master/docs/netctl.profile.5.txt) for more information.

### libmbim

Install `libmbim` from the official repositories. To bring up the modem you can use `mbim-network` which is a wrapper for `mmcli` calls. First create a profile for mbim-network.

 `/etc/mbim-network.conf`  `APN=Broadband` Now connect to the network with `# mbim-network /dev/cdc-wdmX start` . Then bring up the interface and get an ip address:
```
# ip link set wwanY up
# dhcpcd wwanY

```

### sakis3g

There may be the chance that the modem stick is supported by [sakis3g](http://www.sakis3g.com/) which is an all in one command line script and automates all the steps above. Install [sakis3g](https://aur.archlinux.org/packages/sakis3g/) from the [AUR](/index.php/AUR "AUR").

### Connection halts after few minutes running

This problem occurs on some modems which locked by a mobile operator. You can successfully connect to the internet but after few minutes connection halts and your modem reboots. That happens because an operator built a some checks into modem firmware so a modem checks if a branded software is running on your pc, but usually that software is Windows-only, and obviously you don't use it. Fix (it works on ZTE-mf190 at least) is simple - send this command through serial port (use minicom or similar soft):

```
AT+ZCDRUN=E\r

```

This command will delete a NODOWNLOAD.FLG file in the modem's filesystem - it will disable such checks.

## Tips and Tricks

### AT commands

There are some useful commands:

*   AT^U2DIAG=0 - the device is only Modem
*   AT^U2DIAG=1 - device is in modem mode + CD ROM
*   AT^U2DIAG=255 - the device in modem mode + CD ROM + Card Reader
*   AT^U2DIAG=256 - the device in modem mode + Card Reader
*   AT+CPIN=<PIN-CODE> - enter PIN-code
*   AT+CUSD=1,<PDU-encoded-USSD-code>,15 - USSD request, result can be found (probably) in /dev/ttyUSB2.

Encode "*100#" to PDU format:

```
perl -e '@a=split(//,unpack("b*","*100#")); for ($i=7; $i < $#a; $i+=8) { $a[$i]="" } print uc(unpack("H*", pack("b*", join("", @a))))."
"'

```

Decode "AA180C3602" from PDU format:

```
perl -e '@a=split(//,unpack("b*", pack("H*","AA180C3602"))); for ($i=6; $i < $#a; $i+=7) {$a[$i].="0" } print pack("b*", join("", @a)).""'

```

Answer decoding (this example is balance response: 151.25):

```
perl -e 'print pack("H*", "003100350031002C003200350020044004430431002E0020");'

```

Some operators return USSD result in PDU encoding, so you should check proper decoding method.

*   AT+CSQ - get signal quality (AT+CSQ=?)
*   AT+GMI - get manufacturer
*   AT+GMM - get model
*   AT+GMR - get revision
*   AT+GMN - get IMEI
*   AT+COPS? - get operator info
*   AT^CARDLOCK="NCK-code" - unlock modem. NCK-code should be calculated by IMEI. After that modem can work with any GSM-provider.
*   AT^SYSCFG=mode, order, band, roaming, domain - System Config

Mode:

*   2 Automatic search
*   13 2G ONLY
*   14 3G ONLY
*   16 No change

Order:

*   0 Automatic search
*   1 2G first, then 3G
*   2 3G first, then 2G
*   3 No change

Band:

*   80 GSM DCS systems
*   100 Extended GSM 900
*   200 Primary GSM 900
*   200000 GSM PCS
*   400000 WCDMA IMT 2000
*   3FFFFFFF Any band
*   40000000 No change of band

Roaming:

*   0 Not supported
*   1 Roaming is supported
*   2 No change

Domain:

*   0 CS_ONLY
*   1 PS_ONLY
*   2 CS_PS
*   3 ANY
*   4 No change

### Low connection speed

Someone claims that the connection speed under linux is lower than Windows [[1]](https://bbs.archlinux.org/viewtopic.php?id=111513). This is a short summary for possible solutions which are not fully verified.

In most of conditions, the low speed is caused by bad receiver signals and too many people in cell. But you still could use the following method to try to improve the connection speed:

*   QoS parameter can be set with the `AT+CGEQMIN` and `AT+CGEQREQ` commands. It should also be possible to decrease and limit the connection speed. Add the following `Init` command in `/etc/wvdial.conf`:

```
Init6 = AT+CGEQMIN=1,4,64,640,64,640
Init7 = AT+CGEQREQ=1,4,64,640,64,640

```

*   Baud parameter in `/etc/wvdial.conf` could be used to increase the connection speed:

```
Baud = 460800

```

It is advisable to see the baud rate set by the official modem application for Windows (possibly `9600` on Vista).

### Monitor used bandwidth

Frequently a 3G connection obtained via a mobile phone operator comes with restricted bandwidth, so that you are only allowed to use a certain bandwidth per time (e.g. 1GB per month). While it is quite straight-forward to know which type of network applications are pretty bandwidth extensive (e.g. video streaming, gaming, torrent, etc.), it may be difficult to keep an overview about overall consumed bandwidth.

A number of tools are available to help with that. Two console tools are [vnstat](https://www.archlinux.org/packages/?name=vnstat), which allows to keep track of bandwith over time, and [iftop](https://www.archlinux.org/packages/?name=iftop) to monitor bandwidth of individual sessions. If you are a [KDE](/index.php/KDE "KDE") user, [knemo](https://www.archlinux.org/packages/?name=knemo) might help. All are available in the [official repositories](/index.php/Official_repositories "Official repositories").

### Reading SMS

This was tested on a Huawei EM770W (GTM382E) 3g card integrated into an Acer Aspire AS3810TG laptop.

```
$ pacman -S gnokii
$ mkdir -p $XDG_CONFIG_HOME/gnokii

```

Usually the configuration directory is `~/.config/gnokii`.

```
$ cp /etc/gnokiirc ~/.config/gnokii/config

```

Edit `~/.config/gnokii/config` as follows:

 `port = /dev/ttyUSB0` 

You may have to use a different port depending on your configuration, for example `/dev/ttyUSB1` or something else:

```
model = AT
connection = serial
```

You need to be part of the `uucp` group to use `/dev/ttyUSB0`, for example if your user is called "x":

```
# gpasswd -a x uucp
$ newgrp uucp

```

The *newgrp* command allows you to take advantage of the new group assignment immediately without having to logout/login.

Then launch gnokii:

```
$ xgnokii

```

Click on the "SMS" icon button, a window opens up. Then click: "messages->activate sms reading". Your messages will show up in the window.

**Command line script**:

A small command line script using gnokii to read SMS on your SIM card (not phone memory) without having to start a GUI:

```
$ gnokii --getsms SM 0 end 2>&1|grep Text -A1 -B3|grep -v Text

```

What it does:

```
gnokii # invoke gnokii
--getsms SM 0 end # read SMS from SM-memory location (=SIM card) starting at 0 and reading all occupied memory locations ("end")
2>&1 # connect STDERR to STDOUT to make sure the output from the --getsms command can be piped to grep
|grep Text # pipe output from gnokii to grep, anchoring at output containing "Text"
-A1 -B3 # print one line after the matched pattern and three lines before the matched pattern
|grep -v Text # grep result to another grep to exclude the "Text" line (-v for inverting the pattern)

```

Granted this does not work very well if your SMS contains the word "Text", but you may adapt the script to your liking.

### Fix image quality

If you are getting low quality images while browsing the web over a mobile broadband connection with the hints "shift+r improves the quality of this image" and "shift+a improves the quality of all images on this page", follow these instructions:

[Install](/index.php/Install "Install") [tinyproxy](https://www.archlinux.org/packages/?name=tinyproxy), available in the [official repositories](/index.php/Official_repositories "Official repositories").

Edit /etc/tinyproxy/tinyproxy.conf and insert the following two lines:

```
AddHeader "Pragma" "No-Cache"
AddHeader "Cache-Control" "No-Cache"

```

Start tinyproxy:

```
systemctl start tinyproxy

```

Configure your browser to use localhost:8888 as a proxy server and you are all done. This is especially useful if you are using, for example, Google Chrome which, unlike Firefox, does not allow you to modify the Pragma and Cache-Control headers.