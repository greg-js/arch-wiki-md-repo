## Contents

*   [1 Device Identification](#Device_Identification)
*   [2 Ethernet Connection Established](#Ethernet_Connection_Established)
*   [3 Commands](#Commands)
*   [4 Telnet Connection](#Telnet_Connection)
*   [5 Switch Mode in OSX](#Switch_Mode_in_OSX)
*   [6 See also](#See_also)

## Device Identification

Examine the output of lsusb. You should get:

```
$ Bus 002 Device 018: ID 19d2:1405 ZTE WCDMA Technologies MSM 

```

Here are the modes for this modem:

1225 – Default Mode. Available USB Mass Storage Device with CD-ROM and card reader. Corresponds to AT+ZCDRUN=9+AT+ZCDRUN=F

1403 – Operating Mode. Available RNDIS adapter and Mass Storage Device. Corresponds to AT+ZCDRUN=8+AT+ZCDRUN=F

1405 – CDC Ethernet Mode (the one we need). A mode similar to that described above (1403). Included in Linux after starting usb_modeswitch c default settings.

0016 – Download Mode. Under the name of ZTE., but simply a mode where available diagnostic port and two command (analog modem port and PC UI devices Huawei). Corresponds to AT+ZCDRUN=E

0076 – "real" Download Mode. Includes a standard for devices running QC methods.

If your modem does not appear as 19d2:1405 (or 1403), check [USB 3G Modem#Mode switching](/index.php/USB_3G_Modem#Mode_switching "USB 3G Modem") article.

## Ethernet Connection Established

This modem is recognised as Ethernet interface. That means you don't need special programs to work with it.

Use NetworkManager or dhcdpc.

You will see that the LED (Blue - 2G/3G or Green - 4G) on modem is not blinking. To establish a connection, the following link (CGI command) should be entered in a browser:

[http://192.168.0.1/goform/goform_set_cmd_process?goformId=CONNECT_NETWORK](http://192.168.0.1/goform/goform_set_cmd_process?goformId=CONNECT_NETWORK)

To avoid entering this link every time, switch the modem to auto-connection mode:

[http://192.168.0.1/goform/goform_set_cmd_process?goformId=SET_CONNECTION_MODE&ConnectionMode=auto_dial](http://192.168.0.1/goform/goform_set_cmd_process?goformId=SET_CONNECTION_MODE&ConnectionMode=auto_dial)

If you are setting up internet using console (and therefore you have no browser), you should make request with referer, example:

```
curl --header "Referer: http://192.168.0.1/index.html" http://192.168.0.1/goform/goform_set_cmd_process?goformId=CONNECT_NETWORK

```

otherwise you'll get response {"result":"faulure"}

## Commands

CGI command for 2G/3G/4G mode selection:

 `http://192.168.0.1/goform/goform_set_cmd_process?goformId=SET_BEARER_PREFERENCE&BearerPreference=` 

following options available after "=" sign (case-sensetive)

```
NETWORK_auto
WCDMA_preferred
GSM_preferred
Only_GSM
Only_WCDMA
Only_LTE
WCDMA_AND_GSM
WCDMA_AND_LTE
GSM_AND_LTE

```

This should be followed by the **NETWORK CONNECT** CGI command given before.

To switch the modem to **FACTORY mode** (**WARNING! Unable to recieve further CGI commands, connection will be lost!**), issue this link:

```
http://192.168.0.1/goform/goform_process?goformId=MODE_SWITCH&switchCmd=FACTORY

```

You may then need to run the following command (as root) in order to access the AT command serial port:

```
# echo 0x19d2 0x16 > /sys/module/usbserial/drivers/usb-serial:generic/new_id

```

The port should appear as `/dev/ttyUSB<var>n</var>`, e.g. `/dev/ttyUSB1`. When you discover the command port, you can use your favourite serial terminal emulation program to control the device. The commands below may be especially useful (here shown with [modem-cmd](//github.com/imZack/modem-cmd)):

```
# modem-cmd /dev/ttyUSB1 AT+ZCDRUN=8     # switch to 1403 mode (RNDIS)
# modem-cmd /dev/ttyUSB1 AT+ZCDRUN=9     # switch to 1225 mode (default)
# modem-cmd /dev/ttyUSB1 AT+ZCDRUN=F     # exit DOWNLOAD mode and switch to selected mode (RNDIS or default)

```

## Telnet Connection

The modem is available for telnet connection:

```
telnet 192.168.0.1
login: root
password: zte9x15

```

As you can see, the modem has Linux system inside. You can even install some ARM-base packages (mc, nano...) or change something in Web-menu. Explore it carefully!

## Switch Mode in OSX

For some reason this device can get stuck in mode 0016 and fails to switch to any other mode. I was unsuccessful in trying to switch modes using usb_modeswitch and sending AT commands to /dev/ttyUSB0 on various Linux systems. I successfully managed to change modes from 0016 to 1403 using Mac OSX. I was then able to use the dongle on Linux.

In mode 0016 on OSX you will see the follow interfaces:

```
/dev/tty.ZTEUSBATPort_
/dev/tty.ZTEUSBModem_
/dev/tty.ZTEUSBDIAGPort_

```

You can switch modes to 1403 by sending AT commands to the USBModem_ port by doing:

```
screen /dev/tty.ZTEUSBModem_ 9600

>>ATI
Manufacturer: ZTE CORPORATION
Model: MF823
Revision: MF823_T03
IMEI: 866948013728723
+GCAP: +CGSM

>>AT+CREG?
+CREG: 0,1
OK

>>AT+COPS?
+COPS: 0,0,"Telstra Mobile",7
OK

>>AT+ZCDRUN=8+AT+ZCDRUN=F
exit download mode result(0:FAIL 1:SUCCESS):1
OK

```

Now the device should act as a ethernet interface no matter which system you plug it into.

## See also

[whirlpool.net.au](http://forums.whirlpool.net.au/archive/2212748) - Linux & Serial Diags

[gsmforum.ru](http://www.gsmforum.ru/threads/188925-ZTE-MF823-%D0%B8-%D0%B2%D1%81%D1%91-%D1%87%D1%82%D0%BE-%D1%81-%D0%BD%D0%B8%D0%BC-%D1%81%D0%B2%D1%8F%D0%B7%D0%B0%D0%BD%D0%BE?p=934477&viewfull=1#post934477) - ZTE MF823 thread (in Russian)