This page explains how to setup Arch to use a US Department of Defense [Common Access Card](https://en.wikipedia.org/wiki/Common_Access_Card "wikipedia:Common Access Card") (CAC). It was tested with a Dell Smart Card Reader Keyboard and a SCM SCR3310\. Others may not work.

## Contents

*   [1 Installation](#Installation)
*   [2 Enable pcscd](#Enable_pcscd)
*   [3 Configure browser](#Configure_browser)
    *   [3.1 Firefox](#Firefox)
        *   [3.1.1 Load security device](#Load_security_device)
        *   [3.1.2 Import the DoD Certificates](#Import_the_DoD_Certificates)
*   [4 Testing](#Testing)
*   [5 Debugging](#Debugging)

## Installation

Install [ccid](https://www.archlinux.org/packages/?name=ccid) and [opensc](https://www.archlinux.org/packages/?name=opensc) from [official repositories](/index.php/Official_repositories "Official repositories").

There are two places in `/etc/opensc.conf` that comment out `enable_pinpad = false`. If you card reader does not have a pin pad, uncomment these lines.

## Enable pcscd

[Start](/index.php/Start "Start") and enable `pcscd.service`.

## Configure browser

### Firefox

#### Load security device

Navigate to Edit -> Preference -> Advanced -> Certificates -> Security Devices and load a module using `/usr/lib/opensc-pkcs11.so`.

#### Import the DoD Certificates

If you're using a branded version of [Firefox](/index.php/Firefox "Firefox") you should be able to go to [http://dodpki.c3pki.chamb.disa.mil/rootca.html](http://dodpki.c3pki.chamb.disa.mil/rootca.html) and click on the high-level certificates to install them and be done.

The primary root certificate used has a CN of "DoD Root CA 2": this certificate can be converted to PEM format for use in other browsers:

1.  Download the CA bundle. This includes approximately 36 certificates. `$ curl -O [http://dodpki.c3pki.chamb.disa.mil/rel3_dodroot_2048.p7b](http://dodpki.c3pki.chamb.disa.mil/rel3_dodroot_2048.p7b)`
2.  Extract the root certificate into a PEM-formatted file.

`$ openssl pkcs7 -inform DER -in rel3_dodroot_2048.p7b -print_certs | sed -n '/subject=.*CN=DoD Root CA 2/,${/^$/q;P;D}' > DoD_Root_CA_2.pem`

## Testing

Visit your favorite CAC secured web page and you should be asked for the *Master Password* for your certificate. Enter it and if you get in, you know it's working.

## Debugging

The [pcsc-tools](https://www.archlinux.org/packages/?name=pcsc-tools) package is also availabe in **[community]**. The program `pcsc_scan` may be helpful

```
[cceleri@ender ~]$ pcsc_scan 
PC/SC device scanner
V 1.4.21 (c) 2001-2011, Ludovic Rousseau <ludovic.rousseau@free.fr>
Compiled with PC/SC lite version: 1.8.6
Using reader plug'n play mechanism
Scanning present readers...
0: Dell Dell Smart Card Reader Keyboard 00 00

```

```
Thu Sep  5 10:41:53 2013
Reader 0: Dell Dell Smart Card Reader Keyboard 00 00
  Card state: Card removed, 

```

```
Thu Sep  5 10:41:58 2013
Reader 0: Dell Dell Smart Card Reader Keyboard 00 00
  Card state: Card inserted, 
  ATR: 3B DB 96 00 80 1F 03 00 31 C0 64 B0 F3 10 00 07 90 00 80

```

```
ATR: 3B DB 96 00 80 1F 03 00 31 C0 64 B0 F3 10 00 07 90 00 80
+ TS = 3B --> Direct Convention
+ T0 = DB, Y(1): 1101, K: 11 (historical bytes)
  TA(1) = 96 --> Fi=512, Di=32, 16 cycles/ETU
    250000 bits/s at 4 MHz, fMax for Fi = 5 MHz => 312500 bits/s
  TC(1) = 00 --> Extra guard time: 0
  TD(1) = 80 --> Y(i+1) = 1000, Protocol T = 0 
-----
  TD(2) = 1F --> Y(i+1) = 0001, Protocol T = 15 - Global interface bytes following 
-----
  TA(3) = 03 --> Clock stop: not supported - Class accepted by the card: (3G) A 5V B 3V 
+ Historical bytes: 00 31 C0 64 B0 F3 10 00 07 90 00
  Category indicator byte: 00 (compact TLV data object)
    Tag: 3, len: 1 (card service data byte)
      Card service data byte: C0
        - Application selection: by full DF name
        - Application selection: by partial DF name
        - EF.DIR and EF.ATR access services: by GET RECORD(s) command
        - Card with MF
    Tag: 6, len: 4 (pre-issuing data)
     Data: B0 F3 10 00
    Mandatory status indicator (3 last bytes)
      LCS (life card cycle): 07 (Operational state (activated))
      SW: 9000 (Normal processing.)
+ TCK = 80 (correct checksum)

```

```
Possibly identified card (using /usr/share/pcsc/smartcard_list.txt):
3B DB 96 00 80 1F 03 00 31 C0 64 B0 F3 10 00 07 90 00 80
	DoD CAC, Oberthur ID One 128 v5.5 Dual

```