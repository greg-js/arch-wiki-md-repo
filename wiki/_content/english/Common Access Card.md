Related articles

*   [Smartcards](/index.php/Smartcards "Smartcards")

This page explains how to setup Arch to use a US Department of Defense [Common Access Card](https://en.wikipedia.org/wiki/Common_Access_Card "wikipedia:Common Access Card") (CAC).

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Configuration](#Configuration)
*   [2 Enable pcscd](#Enable_pcscd)
*   [3 Configure browser](#Configure_browser)
    *   [3.1 Firefox](#Firefox)
        *   [3.1.1 Load security device](#Load_security_device)
        *   [3.1.2 Import the DoD Certificates](#Import_the_DoD_Certificates)
    *   [3.2 Chromium/Google Chrome](#Chromium/Google_Chrome)
*   [4 Testing](#Testing)
*   [5 Debugging](#Debugging)
    *   [5.1 opensc-tool](#opensc-tool)
    *   [5.2 pcsc-tools](#pcsc-tools)
*   [6 See also](#See_also)

## Installation

Install [ccid](https://www.archlinux.org/packages/?name=ccid) and [opensc](https://www.archlinux.org/packages/?name=opensc) from [official repositories](/index.php/Official_repositories "Official repositories").

### Configuration

**Note:** You should not have to edit your opensc configuration files by default. You should check all other setup items first (e.g. certificate imports)

If your card reader does not have a pin pad, uncomment `enable_pinpad = false` in `/etc/opensc.conf`.

Sometimes [opensc](https://www.archlinux.org/packages/?name=opensc) can struggle to identify the proper driver for CAC, instead it may choose PIV or something else. You can force the CAC driver by editing `/etc/opensc.conf` for `card_drivers = cac` and `force_card_driver = cac`

## Enable pcscd

[Start](/index.php/Start "Start") and enable `pcscd.socket`.

## Configure browser

1\. Go to: [http://iase.disa.mil/pki-pke/Pages/tools.aspx](http://iase.disa.mil/pki-pke/Pages/tools.aspx)

2\. Download certs: *"Trust Store" -> "PKI CA Certificate Bundles: PKCS#7" -> "For DoD PKI Only - Version 5.3"* (ZIP Download)

3\. Unzip the DoD PKI zip

4\. Follow browser-specific instructions

### Firefox

#### Load security device

Navigate to *Edit -> Preference -> Advanced -> Certificates -> Security Devices* and click "Load" to load a module using `/usr/lib/opensc-pkcs11.so` or `/usr/lib/pkcs11/opensc-pkcs11.so`.

**Note:** Firefox may report the module did not load correctly however you will have to check in the security devices to confirm whether the module properly loaded or not

#### Import the DoD Certificates

Install the certificates from the mentioned zip-file in *this* order, by going to *Edit -> Preference -> Advanced -> Certificates -> View Certificates -> Authorities -> Import* (make sure to at-least check the box for "Trust this CA to identify websites"):

**Note:** As of the 5.3 version of the certificate zip

1\. Certificates_PKCS7_v5.3_DoD.der.p7b

2\. Certificates_PKCS7_v5.3_DoD_DoD_Root_CA_2.der.p7b

3\. Certificates_PKCS7_v5.3_DoD_DoD_Root_CA_3.der.p7b

4\. Certificates_PKCS7_v5.3_DoD_DoD_Root_CA_4.der.p7b

5\. Certificates_PKCS7_v5.3_DoD_DoD_Root_CA_5.der.p7b

6\. Certificates_PKCS7_v5.3_DoD.pem.p7b

### Chromium/Google Chrome

1\. Add the CAC Module to the NSS DB.

Ensure that your CAC is connected, that [Chromium](/index.php/Chromium "Chromium") is closed and enter the following in a terminal: `$ modutil -dbdir sql:$HOME/.pki/nssdb/ -add "CAC Module" -libfile /usr/lib/opensc-pkcs11.so`

**Note:** You may see the message 'Failure to load dynamic library'. This can be ignored.

Upon success you will see "Module "CAC Module" added to database."

2\. Check if the CAC Module was successfully added with `$ modutil -dbdir sql:$HOME/.pki/nssdb/ -list`

3\. Navigate (in a shell) to the location of the unzip DoD PKI files and install via:

```
 for n in $(ls * | grep Chrome); do certutil -d sql:$HOME/.pki/nssdb -A -t TC -n $n -i $n; done

```

or

Re-open Chrome, Navigate to *Settings -> Show Advanced Settings -> Manage Certificates -> Authorities* to load CA bundle from the PEM-formatted file from above.

4\. Verify the authority is in Chrome under *Settings -> Show Advanced Settings -> Manage Certificates -> Authorities* then expand "org-U.S. Government" and you should see a number of "DoD" certificates listed.

## Testing

Visit your favorite CAC secured web page and you should be asked for the *Master Password* for your certificate. Enter it and if you get in, you know it's working.

If some sites/pages seem to have a problem working correctly (e.g. outlook web access won't authenticate the session for DoD webmail) try using a private/incognito session to test validity of the cert chain and remove some variables.

## Debugging

### opensc-tool

Most of this information was found in a [blog post by Firas Kraïem](http://blog.fkraiem.org/2013/03/13/linux-smart-card-authentication-howto/)

Verify opensc can see your reader

 `$ opensc-tool --list-readers ` 
```
# Detected readers (pcsc)
Nr.  Card  Features  Name
0    Yes            Generic USB2.0-CRW [Smart Card Reader Interface] (20070818000000000) 00 00
```

List plugged in card

 `$ opensc-tool --reader 0 --name `  `Personal Identity Verification Card` 

List plugged in card and drive in use

 `$ opensc-tool --reader 0 --name -v` 
```
Connecting to card in reader Generic USB2.0-CRW [Smart Card Reader Interface] (20070818000000000) 00 00...
Using card driver Personal Identity Verification Card.
Card name: Personal Identity Verification Card
```

### pcsc-tools

The [pcsc-tools](https://www.archlinux.org/packages/?name=pcsc-tools) package is also availabe in **[community]**. The program `pcsc_scan` may be helpful

```
[cceleri@ender ~]$ pcsc_scan 
PC/SC device scanner
V 1.4.21 (c) 2001-2011, Ludovic Rousseau <ludovic.rousseau@free.fr>
Compiled with PC/SC lite version: 1.8.6
Using reader plug'n play mechanism
Scanning present readers...
0: Dell Dell Smart Card Reader Keyboard 00 00

Thu Sep  5 10:41:53 2013
Reader 0: Dell Dell Smart Card Reader Keyboard 00 00
  Card state: Card removed, 

Thu Sep  5 10:41:58 2013
Reader 0: Dell Dell Smart Card Reader Keyboard 00 00
  Card state: Card inserted, 
  ATR: 3B DB 96 00 80 1F 03 00 31 C0 64 B0 F3 10 00 07 90 00 80

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

Possibly identified card (using /usr/share/pcsc/smartcard_list.txt):
3B DB 96 00 80 1F 03 00 31 C0 64 B0 F3 10 00 07 90 00 80
	DoD CAC, Oberthur ID One 128 v5.5 Dual

```

## See also

*   [PIV Usage Guides](https://piv.idmanagement.gov/engineering/)