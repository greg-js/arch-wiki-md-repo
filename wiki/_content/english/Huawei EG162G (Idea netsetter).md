The HUAWEI EG162G is a EDGE/GPRS modem used for wireless internet access. Linux kernel support this at least from version 2.6.29.4 and thus setting this up is not very hard.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Plug it in](#Plug_it_in)
*   [2 Installation](#Installation)
*   [3 Configuration](#Configuration)
*   [4 Usage](#Usage)
*   [5 See also](#See_also)

## Plug it in

Plug in the device , wait for a few seconds and then run

```
$ ls /dev/ttyUSB*

```

you will see something like this:

```
/dev/ttyUSB1  /dev/ttyUSB2  /dev/ttyUSB3

```

the first one is the port of the modem.

## Installation

Now install [ppp](https://www.archlinux.org/packages/?name=ppp) and [wvdial](/index.php/Wvdial "Wvdial"), which is a dialer.

## Configuration

Edit your `/etc/wvdial.conf` and use this if you are using an idea netsetter, else use google to find the right config for your provider:

```
[Dialer Defaults]
Modem=/dev/ttyUSB1
Baud = 460800
Init 1 = AT+CGMM
Init 2 = AT+CMEE=1
Init 3 = ATE0
Init 4 = AT^HS=0,0
Init 5 = AT+CFUN?
Init 6 = AT+CLCK="SC",2
Init 7 = AT+CPIN?
Init 8 = AT+CLCK="SC",2
Modem Type = USB MODEM
Phone=*99#
Username = idea
Password = idea
Dial Command=ATDT
Stupid Mode=1
ISDN=0

```

Remember that the modem might get a different port each time you plug it in so you might need to change the `Modem=/dev/ttyUSB1` each time. For example if the output of:

```
$ ls /dev/ttyUSB*

```

is

```
/dev/ttyUSB0
/dev/ttyUSB1
/dev/ttyUSB2

```

then you need to change the 2nd line in the *wvdial* config to `Modem=/dev/ttyUSB0`.

If the output of:

```
$ ls /dev/ttyUSB*

```

shows a `/dev/ttyUSB_utps_modem`, which will be a soft link to your Idea Netsetter's modem, change the 2nd line in the *wvdial* config to `Modem=/dev/ttyUSB_utps_modem`. This link will not change every time you reconnect the device.

## Usage

Now all you need to do is run wvdial as root:

```
# wvdial

```

If you get an error 16 in wvdial it means that there is no modem present in the port specified by the config, so edit your config file accordingly.

If the connection is successfull you will see something like this:

```
# wvdial
--> WvDial: Internet dialer version 1.60
--> Cannot get information for serial port.
--> Initializing modem.
--> Sending: ATZ
ATZ
OK
--> Modem initialized.
--> Sending: ATDT*99#
--> Waiting for carrier.
ATDT*99#
CONNECT
--> Carrier detected.  Starting PPP immediately.
--> Starting pppd at Sun May 24 02:03:51 2009
--> Pid of pppd: 6361
--> Using interface ppp0
--> pppd: è|[01]¸8A[08]È@Þ[08]
--> pppd: è|[01]޸8A[08]È@Þ[08]
--> pppd: è|[01]޸8AÞ[08]È@Þ[08]
--> pppd: è|[01]¸8AÞ[08]È@Þ[08]
--> pppd: è|[01]¸8AÞ[08]È@Þ[08]
--> pppd: è|[01]¸8AÞ[08]È@Þ[08]
--> local  IP address 112.110.117.241
--> pppd: è|[01]¸8AÞ[08]È@Þ[08]
--> remote IP address 10.64.64.64
--> pppd: è|[01]¸8AÞ[08]È@Þ[08]
--> primary   DNS address 10.11.12.13
--> pppd: è|[01]¸8AÞ[08]È@Þ[08]
--> secondary DNS address 10.11.12.14
--> pppd: è|[01]¸8AÞ[08]È@Þ[08] 

```

**Note:** If you get an error 16 in wvdial it means that there is no modem present in the port specified by the config, so edit your config file accordingly.

You still will not be able to surf the net unless you have a nameserver in your `/etc/resolv.conf`. In this case add this line to it:

```
nameserver 208.67.222.222

```

If you are already conected to a LAN then change the subnet mask of the lan to 255.0.0.0 and you should be able to use the lan and the netsetter.

## See also

*   [USB 3G Modem](/index.php/USB_3G_Modem "USB 3G Modem")
*   [USB mode switch](/index.php/USB_3G_Modem#Mode_switching "USB 3G Modem")