Related articles

*   [Common Access Card](/index.php/Common_Access_Card "Common Access Card")

This page explains how to setup your system in order to use a [smart card](https://en.wikipedia.org/wiki/Smart_card "wikipedia:Smart card") reader.

## Contents

*   [1 Installation](#Installation)
*   [2 Scan for card reader](#Scan_for_card_reader)
*   [3 Configuration](#Configuration)
    *   [3.1 Mozilla Firefox](#Mozilla_Firefox)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Smargo/TV Card reader](#Smargo/TV_Card_reader)
    *   [4.2 p11tool](#p11tool)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Firefox can't access data](#Firefox_can't_access_data)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [ccid](https://www.archlinux.org/packages/?name=ccid) and [opensc](https://www.archlinux.org/packages/?name=opensc) from the [official repositories](/index.php/Official_repositories "Official repositories").

If the card reader does not have a PIN pad, [append](/index.php/Append "Append") the line(s) and set `enable_pinpad = false` in the opensc configuration file `/etc/opensc.conf`.

**Note:** The package [ccid](https://www.archlinux.org/packages/?name=ccid) provides a generic USB interface driver for smart card reader. If the smart card at hand is not supported by the generic driver or simply it needs a specific one, feel free to install the best for that device.

[Start](/index.php/Start "Start") and/or [enable](/index.php/Enable "Enable") the `pcscd.service`.

**Tip:** If you get the error `Failed to start pcscd.service: Unit pcscd.socket not found.`, just reload systemd units with this `systemctl daemon-reload` command.

## Scan for card reader

[Install](/index.php/Install "Install") [pcsc-tools](https://www.archlinux.org/packages/?name=pcsc-tools) and start the *pcsc_scan* utility, then connect the Smart card reader and finally insert a card. If you see output like this, the smart card reader and also the card have been successfully recognized.

```
$ pcsc_scan 
PC/SC device scanner
V 1.5.2 (c) 2001-2017, Ludovic Rousseau <ludovic.rousseau@free.fr>
Using reader plug'n play mechanism
Scanning present readers...
0: Alcor Micro AU9560 00 00

Sat Aug  5 18:49:32 2017
 Reader 0: Alcor Micro AU9560 00 00
  Card state: Card removed, 

Sat Aug  5 19:00:35 2017
 Reader 0: Alcor Micro AU9560 00 00
  Card state: Card inserted, 
  ATR:  *FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF*

ATR:  *FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF*
+ TS = 3B --> Direct Convention
+ T0 = DF, Y(1): 1101, K: 15 (historical bytes)
  TA(1) = 18 --> Fi=372, Di=12, 31 cycles/ETU
    129032 bits/s at 4 MHz, fMax for Fi = 5 MHz => 161290 bits/s
  TC(1) = 00 --> Extra guard time: 0
  TD(1) = 81 --> Y(i+1) = 1000, Protocol T = 1 
-----
  TD(2) = 31 --> Y(i+1) = 0011, Protocol T = 1 
-----
  TA(3) = FE --> IFSC: 254
  TB(3) = 7D --> Block Waiting Integer: 7 - Character Waiting Integer: 13
+ Historical bytes: 00 6B 02 0C 01 82 01 11 01 43 4E 53 10 31 80
  Category indicator byte: 00 (compact TLV data object)
    Tag: 6, len: B (pre-issuing data)
      Data:  *FF FF FF FF FF FF FF FF FF FF*
    Mandatory status indicator (3 last bytes)
      LCS (life card cycle): 10 (Proprietary)
      SW: 3180 (Error not defined by ISO 7816)
+ TCK = FC (correct checksum)

Possibly identified card (using /usr/share/pcsc/smartcard_list.txt):
*FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF*
      Italian healtcare card (TS) National Service Card (CNS) (HealthCare)

```

**Note:** In this example the smart card reader is an *Alcor Micro AU9560* and the inserted card is an *Italian CNS* card.

## Configuration

### Mozilla Firefox

The browser needs to set the new security-related device. Open the **Security Devices** page (reach it via Preferences, Privacy & Security, Certificates), then click **Load** and set the Module Name to "CAC Module" and Module filename to `/usr/lib/opensc-pkcs11.so`.

## Tips and tricks

### Smargo/TV Card reader

When interfacing with a TV-card for live TV and recording (PVR/DVR), you may need to assign the smartcard reader to the `video` [user group](/index.php/User_group "User group") allowing decryption. When using a Smargo Smartreader consider the following [udev](/index.php/Udev "Udev") rule:

 `/etc/udev/rules.d/98-smargo.rules`  `SUBSYSTEM=="tty", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", GROUP="video", MODE="0666", SYMLINK+="smargo"` 

Set `/dev/smargo` as the reader device when using softcam applications like OSCam.

### p11tool

If using packages from the GnuTLS suite, such as p11tool, the the OpenSC driver might not properly load. (This can be determined if you run `p11tool --list-tokens` and you do not see your hardware token in the list.) Users can create a file that allows the OpenSC driver to be properly loaded:

 `/usr/share/p11-kit/modules/opensc.module`  `module: opensc-pkcs11.so` 

## Troubleshooting

### Firefox can't access data

If the browser is not able to use the smart card data, probably it is not aware of the service which provides access to the device. This happens if you plug in the smart card reader after you open Firefox. To solve this issue, simply restart Firefox.

## See also

*   [Debian:Smartcards](https://wiki.debian.org/Smartcards "debian:Smartcards")