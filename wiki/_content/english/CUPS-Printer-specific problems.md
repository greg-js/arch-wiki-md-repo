Related articles

*   [CUPS](/index.php/CUPS "CUPS")
*   [CUPS/Troubleshooting](/index.php/CUPS/Troubleshooting "CUPS/Troubleshooting")

This article contains printer or manufacturer-specific instructions for [CUPS](/index.php/CUPS "CUPS"). See [OpenPrinting](http://www.openprinting.org/printers) if your printer is not already listed here, or if none of the listed drivers work.

**Note:** If you add a printer to this list, consider contributing your entry to [OpenPrinting](https://wiki.linuxfoundation.org/openprinting/database/databaseintro) - that way users of other distributions will also benefit!

## Contents

*   [1 Brother](#Brother)
    *   [1.1 Network printers](#Network_printers)
    *   [1.2 Custom drivers](#Custom_drivers)
        *   [1.2.1 Manually installing from the RPM packages](#Manually_installing_from_the_RPM_packages)
    *   [1.3 Updating the firmware](#Updating_the_firmware)
*   [2 Canon](#Canon)
    *   [2.1 CARPS](#CARPS)
    *   [2.2 USB over IP (BJNP)](#USB_over_IP_.28BJNP.29)
    *   [2.3 cnijfilter](#cnijfilter)
*   [3 Dell](#Dell)
*   [4 Epson](#Epson)
    *   [4.1 Utilities](#Utilities)
        *   [4.1.1 escputil](#escputil)
        *   [4.1.2 mtink](#mtink)
        *   [4.1.3 Stylus-toolbox](#Stylus-toolbox)
    *   [4.2 Custom drivers](#Custom_drivers_2)
        *   [4.2.1 Avasys](#Avasys)
*   [5 HP](#HP)
    *   [5.1 HPLIP](#HPLIP)
    *   [5.2 foo2zjs](#foo2zjs)
*   [6 Konica Minolta](#Konica_Minolta)
    *   [6.1 foo2zjs](#foo2zjs_2)
*   [7 Lexmark](#Lexmark)
    *   [7.1 Utilities](#Utilities_2)
    *   [7.2 Custom drivers](#Custom_drivers_3)
*   [8 Oki](#Oki)
*   [9 Ricoh](#Ricoh)
*   [10 Samsung](#Samsung)
*   [11 Xerox or FujiXerox](#Xerox_or_FujiXerox)
    *   [11.1 Custom drivers](#Custom_drivers_4)
        *   [11.1.1 Phaser 3100MFP](#Phaser_3100MFP)
        *   [11.1.2 Phaser 6000B](#Phaser_6000B)
        *   [11.1.3 Phaser 6125N](#Phaser_6125N)

## Brother

| Printer | Driver/filter | Notes |
| DCP-135C | [brother-dcp135c](https://aur.archlinux.org/packages/brother-dcp135c/) |
| DCP-150C | [brother-dcp150c](https://aur.archlinux.org/packages/brother-dcp150c/) |
| DCP-7020 | [foomatic](/index.php/CUPS#Foomatic "CUPS") | Or Brother's driver. |
| DCP-7030 | [brother-dcp7030](https://aur.archlinux.org/packages/brother-dcp7030/) |
| DCP-7065DN | [brother-dcp7065dn](https://aur.archlinux.org/packages/brother-dcp7065dn/) |
| FAX-2820 | [brother-cups-wrapper-laser](https://aur.archlinux.org/packages/brother-cups-wrapper-laser/) |
| FAX-2840 | [brother-fax2840](https://aur.archlinux.org/packages/brother-fax2840/) | Or [foomatic](/index.php/CUPS#Foomatic "CUPS") - works mostly with `hpijs-pcl5e.ppd`. Same as the HL-2170W. |
| FAX-2940 | [brother-fax2940](https://aur.archlinux.org/packages/brother-fax2940/) |
| HL-2030 | [foomatic](/index.php/CUPS#Foomatic "CUPS") | Or [brother-hl2030](https://aur.archlinux.org/packages/brother-hl2030/) |
| HL-2035 | [foomatic](/index.php/CUPS#Foomatic "CUPS") | Should be compatible with any drivers for the HL-2030. |
| HL-2040 | [foomatic](/index.php/CUPS#Foomatic "CUPS") | Or [brother-hl2040](https://aur.archlinux.org/packages/brother-hl2040/) |
| HL-2130 | [foomatic](/index.php/CUPS#Foomatic "CUPS") (using the HL-2140 driver) | Or [hplip](https://www.archlinux.org/packages/?name=hplip) |
| HL-2140 | [foomatic](/index.php/CUPS#Foomatic "CUPS") | Or [brother-hl2140](https://aur.archlinux.org/packages/brother-hl2140/) |
| HL-2170W | [foomatic](/index.php/CUPS#Foomatic "CUPS") | Or Brother's driver. |
| HL-2230 | [foomatic](/index.php/CUPS#Foomatic "CUPS") | Same as HL-2170W. Select HL-2170W as the driver in CUPS admin when adding a printer. |
| HL-2250DN | [brother-hl2250dn](https://aur.archlinux.org/packages/brother-hl2250dn/) |
| HL-2270DW | [brother-hl2270dw](https://aur.archlinux.org/packages/brother-hl2270dw/) |
| HL-2280DW | [brother-hl2280dw](https://aur.archlinux.org/packages/brother-hl2280dw/) |
| HL-2340DW | [brother-hll2340dw](https://aur.archlinux.org/packages/brother-hll2340dw/) |
| HL-3045CN | Install Brother's driver. |
| HL-3140CW | [brother-hl3140cw](https://aur.archlinux.org/packages/brother-hl3140cw/) | Use IPP and Brother's driver to avoid page-shrinking and endless blank printouts |
| HL-3150CDW | [brother-hl3150cdw](https://aur.archlinux.org/packages/brother-hl3150cdw/) |
| HL-3170CDW | [brother-hl3170cdw](https://aur.archlinux.org/packages/brother-hl3170cdw/) |
| HL-5140 | [foomatic](/index.php/CUPS#Foomatic "CUPS") | Or Brother's driver. |
| HL-5340 | [foomatic](/index.php/CUPS#Foomatic "CUPS") | Using the *Generic PCL 6/PCL XL Printer - CUPS+Gutenprint* ([gutenprint](https://www.archlinux.org/packages/?name=gutenprint) and [foomatic-db-gutenprint-ppds](https://www.archlinux.org/packages/?name=foomatic-db-gutenprint-ppds)). Or Brother's driver, which may result in failed prints with postscript errors. |
| HL-L2300D | [brother-hll2300d](https://aur.archlinux.org/packages/brother-hll2300d/) |
| HL-L2350DW | [brother-hll2350dw](https://aur.archlinux.org/packages/brother-hll2350dw/) |
| HL-L2380DW | [brother-hll2380dw](https://aur.archlinux.org/packages/brother-hll2380dw/) |
| HL-L2395DW | [brother-hll2395dw](https://aur.archlinux.org/packages/brother-hll2395dw/) | Use socket protocol (`socket://hostname-or-ip:9100`). |
| HL-L5100DN | HP LaserJet Foomatic driver | This model will emulate a HP LaserJet. `lpd://hostname-or-ip/BINARY_P1` |
| MFC-420CN | [brother-mfc-420cn](https://aur.archlinux.org/packages/brother-mfc-420cn/) |
| MFC-440CN | [brother-mfc-440cn](https://aur.archlinux.org/packages/brother-mfc-440cn/) |
| MFC-7360N | [brother-mfc7360n](https://aur.archlinux.org/packages/brother-mfc7360n/) |
| MFC-7840W | [brother-mfc-7840w](https://aur.archlinux.org/packages/brother-mfc-7840w/) |
| MFC-9320CW | Install Brother's driver. |
| MFC-9332CDW | [brother-mfc-9332cdw](https://aur.archlinux.org/packages/brother-mfc-9332cdw/) |
| MFC-9840CDW | [foomatic](/index.php/CUPS#Foomatic "CUPS") | Or Brother's driver. This printer also works with the generic PCL-6 driver from the [gutenprint](https://www.archlinux.org/packages/?name=gutenprint) package. Use **pcl_p1** for the printer's address when using the PCL-6 driver. |
| MFC-J470DW | [brother-mfc-j470dw](https://aur.archlinux.org/packages/brother-mfc-j470dw/) |
| MFC-J4710DW | [brother-mfc-j4710dw](https://aur.archlinux.org/packages/brother-mfc-j4710dw/) |
| MFC-J480DW | [brother-mfc-j480dw](https://aur.archlinux.org/packages/brother-mfc-j480dw/) | Use `ipp://` described below. |
| MFC-J5520DW | [brother-mfc-j5520dw](https://aur.archlinux.org/packages/brother-mfc-j5520dw/) |
| MFC-J5910DW | [brother-mfc-j5910dw](https://aur.archlinux.org/packages/brother-mfc-j5910dw/) |
| MFC-J650DW | Install Brother's driver. |
| MFC-J885DW | [brother-mfc-j885dw](https://aur.archlinux.org/packages/brother-mfc-j885dw/) |
| MFC-J985DW | [brother-mfc-j985dw](https://aur.archlinux.org/packages/brother-mfc-j985dw/) |
| MFC-L2700DW | [brother-mfc-l2700dw](https://aur.archlinux.org/packages/brother-mfc-l2700dw/) | Please look also at the comments section of the AUR package page. |
| QL-500 | [brother-ql500](https://aur.archlinux.org/packages/brother-ql500/) |
| QL-570 | [brother-ql570](https://aur.archlinux.org/packages/brother-ql570/) |
| QL-580N | [brother-ql580n](https://aur.archlinux.org/packages/brother-ql580n/) |
| QL-650TD | [brother-ql650td](https://aur.archlinux.org/packages/brother-ql650td/) |
| QL-700 | [brother-ql700](https://aur.archlinux.org/packages/brother-ql700/) |
| QL-710W | [brother-ql710w](https://aur.archlinux.org/packages/brother-ql710w/) |
| QL-720NW | [brother-ql720nw](https://aur.archlinux.org/packages/brother-ql720nw/) |
| QL-1050 | [brother-ql1050](https://aur.archlinux.org/packages/brother-ql1050/) |
| QL-1050N | [brother-ql1050n](https://aur.archlinux.org/packages/brother-ql1050n/) |
| QL-1060 | [brother-ql1060n](https://aur.archlinux.org/packages/brother-ql1060n/) |
| TD-2020 | [brother-td2020](https://aur.archlinux.org/packages/brother-td2020/) |
| TD-2120N | [brother-td2120n](https://aur.archlinux.org/packages/brother-td2120n/) |
| TD-2130N | [brother-td2130n](https://aur.archlinux.org/packages/brother-td2130n/) |
| TD-4000 | [brother-td4000](https://aur.archlinux.org/packages/brother-td4000/) |
| TD-4100N | [brother-td4100n](https://aur.archlinux.org/packages/brother-td4100n/) |
| Printer | Driver/filter | Notes |

### Network printers

For network printers, use `ipp://**printer_ip**/ipp/port1` as printer address. For some older printers, this might not work. If not, try `lpd://**printer_ip**/BINARY_P1` instead.

Some printers use the socket protocol. For these printers, use `socket://**printer_ip**:9100`. For http, use `http://**printer_ip**/POSTSCRIPT_P1`.

### Custom drivers

Brother provides custom drivers on their website, either in source tarball, rpm, or deb form. [Packaging Brother printer drivers](/index.php/Packaging_Brother_printer_drivers "Packaging Brother printer drivers") covers creating [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") from the existing RPM packages.

**Note:** The source packages might be a better alternative to the rpm packages, provided they contain all the needed files.

#### Manually installing from the RPM packages

**Warning:** This should ideally be automated in a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")

[Install](/index.php/Install "Install") the [rpmextract](https://www.archlinux.org/packages/?name=rpmextract) package, and extract both rpm packages using `rpmextract.sh`. Extracting both files will create a var and a usr directory - move the contents of both directories into the corresponding root directories.

Run the cups wrapper file in `/usr/local/Brother/cupswrapper`. This should automatically install and configure your brother printer.

For some of the drivers 32 bit libraries may need to be installed from [multilib](/index.php/Multilib "Multilib").

### Updating the firmware

[Install](/index.php/Install "Install") [net-snmp](https://www.archlinux.org/packages/?name=net-snmp) and run:

```
snmpwalk -c public $PRINTER_IP | grep -A 1 3.6.1.4.1.2435.2.4.3.99.3.1.6.1.2

```

At this point, you will have the relevant data to get a valid firmware download link from Brother. The file should look similar to the one below:

 `request.xml` 
```
 <REQUESTINFO>
    <FIRMUPDATETOOLINFO>
        <FIRMCATEGORY>MAIN</FIRMCATEGORY>
        <OS>LINUX</OS>
        <INSPECTMODE>1</INSPECTMODE>
    </FIRMUPDATETOOLINFO>

    <FIRMUPDATEINFO>
        <MODELINFO>
            <SELIALNO></SELIALNO>
            <NAME>MFC-9330CDW</NAME>
            <SPEC>0401</SPEC>
            <DRIVER></DRIVER>
            <FIRMINFO>
                <FIRM>
                    <ID>MAIN</ID>
                    <VERSION>R1506121801:4504</VERSION>
                </FIRM>
                <FIRM>
                    <ID>SUB1</ID>
                    <VERSION>1.07</VERSION>
                </FIRM>
                <FIRM>
                    <ID>SUB2</ID>
                    <VERSION>L1505291600</VERSION>
                </FIRM>
            </FIRMINFO>
        </MODELINFO>
        <DRIVERCNT>1</DRIVERCNT>
        <LOGNO>2</LOGNO>
        <ERRBIT></ERRBIT>
        <NEEDRESPONSE>1</NEEDRESPONSE>
    </FIRMUPDATEINFO>
 </REQUESTINFO>

```

Post this file to Brother:

```
curl -X POST -d @request.xml [https://firmverup.brother.co.jp/kne_bh7_update_nt_ssl/ifax2.asmx/fileUpdate](https://firmverup.brother.co.jp/kne_bh7_update_nt_ssl/ifax2.asmx/fileUpdate) -H "Content-Type:text/xml" > response.xml

```

In `response.xml` you will find a `<PATH>` tag that contains the firmware download URL. Next, download the firmware, push it to the printer, and let the printer process it. Before that is done, change the Admin password to something known, it will be used as the user to log into the FTP site (VERY bad practice, don't do this).

```
wget [http://update-akamai.brother.co.jp/CS/LZ4266_W.djf](http://update-akamai.brother.co.jp/CS/LZ4266_W.djf)
ftp $PRINTER_IP
 bin
 hash
 send LZ4266_W.djf
 bye

```

With that, the printer will restart, and the latest firmware will be installed and (hopefully) your printing woes will be solved.

## Canon

There are many possible drivers for Canon printers. [Many Canon printers](http://gimp-print.sourceforge.net/p_Supported_Printers.php) are supported by [gutenprint](https://www.archlinux.org/packages/?name=gutenprint). Some of Canon's LBP, iR, and MF printers use a driver supporting the UFR II/UFR II LT/LIPSLX protocols, which is available as [cndrvcups-lb](https://aur.archlinux.org/packages/cndrvcups-lb/) or [cndrvcups-lb-bin](https://aur.archlinux.org/packages/cndrvcups-lb-bin/). Others use the [#CARPS](#CARPS), [#cnijfilter](#cnijfilter) ([cnijfilter2](/index.php/AUR "AUR") / [cnijfilter2-bin](/index.php/AUR "AUR")), or [Canon CAPT](/index.php/Canon_CAPT "Canon CAPT") drivers.

| Printer | Driver/filter | Notes |
| iP4300 | [gutenprint](https://www.archlinux.org/packages/?name=gutenprint) | Or use the [TurboPrint](http://www.turboprint.info/) driver. |
| LBP810 | [Canon CAPT](/index.php/Canon_CAPT "Canon CAPT") |
| LBP1120 |
| LBP1210 |
| LBP2900 |
| LBP3000 |
| LBP3010 |
| LBP3018 |
| LBP3050 |
| LBP3100 |
| LBP3108 |
| LBP3150 |
| LBP3200 |
| LBP3210 |
| LBP3250 |
| LBP3300 |
| LBP3310 |
| LBP3500 |
| LBP5000 |
| LBP5050 series |
| LBP5100 |
| LBP5300 |
| LBP6000 |
| LBP6018 |
| LBP6020 |
| LBP6200 |
| LBP6300 |
| LBP6300n |
| LBP6310dn |
| LBP7010C |
| LBP7018C |
| LBP7200Cdn (network mode) |
| LBP7200C series |
| LBP7210Cdn |
| LBP9100C |
| MF4720w | [cndrvcups-lb-bin](https://aur.archlinux.org/packages/cndrvcups-lb-bin/) |
| MG4200 series | [cnijfilter-mg4200](https://aur.archlinux.org/packages/cnijfilter-mg4200/) | Avoid the [web interface](/index.php/CUPS#Web_interface "CUPS") when adding the printer as it won't find the PPD file. |
| MX490 | [cnijfilter2](https://aur.archlinux.org/packages/cnijfilter2/)
[cnijfilter2-bin](https://aur.archlinux.org/packages/cnijfilter2-bin/) |
| MX492 |
| TS8050 | Without [cnijfilter2](https://aur.archlinux.org/packages/cnijfilter2/) printing will fail with a filter error or you might get "Rendering Completed" and nothing will print |
| TS9020 | [canon-ts9020](https://aur.archlinux.org/packages/canon-ts9020/) |
| Printer | Driver/filter | Notes |

Some Canon printers will use a similar setup to the iP4500, so consider modifying the [cnijfilter-ip4500](https://aur.archlinux.org/packages/cnijfilter-ip4500/) package for other, similar printers.

### CARPS

Some of Canon's printers use Canon's proprietary Canon Advanced Raster Printing System (CARPS) driver. [Rainbow Software](http://www.rainbow-software.org/2014/01/23/cups-driver-for-canon-carps-printers/) have managed to reverse engineer the CARPS data format and have successfully created a CARPS CUPS driver, which is available as [carps-cups](https://aur.archlinux.org/packages/carps-cups/). The project's [GitHub](https://github.com/ondrej-zary/carps-cups) page includes a list of working printers.

### USB over IP (BJNP)

Some Canon printers use Canon's proprietary USB over IP BJNP protocol to communicate over the network. There is a CUPS backend for this, which is available as [cups-bjnp](https://aur.archlinux.org/packages/cups-bjnp/).

### cnijfilter

Some printers using the cnijfilter drivers support the `cnijnet` protocol. To find the [printer URI](/index.php/CUPS#Printer_URI "CUPS") run

```
$ cnijnetprn --search auto

```

and use the `cnijnet:/` URI in the output.

## Dell

| Printer | Driver/filter | Notes |
| 1250C | [foo2zjs-nightly](https://aur.archlinux.org/packages/foo2zjs-nightly/) | See [http://cybercom.net/~dcoffin/hbpl](http://cybercom.net/~dcoffin/hbpl), the patch has been merged into upstream. The printer may also work with the [Xerox Phaser 6000B driver](#Phaser_6000B). |
| C1660NW | [foo2zjs-nightly](https://aur.archlinux.org/packages/foo2zjs-nightly/) | The printer may also work with the [Xerox Phaser 6000B driver](#Phaser_6000B). |
| E515,

E515dw

 | Install [Dell's driver](http://downloads.dell.com/FOLDER03040853M/1/Printer_E515dw_Driver_Dell_A00_LINUX.zip). | Both *e515dwcupswrapper-3.2.0-1.i386.deb* and *e515dwlpr-3.2.0-1.i386.deb* need to be installed. You could either write a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), use [debtap](https://aur.archlinux.org/packages/debtap/), or use [dpkg](https://aur.archlinux.org/packages/dpkg/) (using dpkg is not recommended as the files will not be managed by [pacman](/index.php/Pacman "Pacman")). The driver works on both the x86_64 and i386 platforms, but may require [multilib](/index.php/Multilib "Multilib"). |
| S1130n | [dell-unified-printer-driver](https://aur.archlinux.org/packages/dell-unified-printer-driver/) | Driver conflicts with samsung-unified-driver-printer (both create rastertospl and libscmssc.so) |
| 1130 |
| 1133 |
| 1135n |
| 1815 |
| 2145cn |
| 2335dn |
| 2355dn |
| 5330 |
| B1160 |
| B1160w |
| B1165nfw |
| B1260dn |
| B1265dfw |
| B1265dnf |
| B2365dnf |
| Printer | Driver/filter | Notes |

## Epson

[epson-inkjet-printer-escpr](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr/) and [epson-inkjet-printer-escpr2](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr2/) are sets of drivers using the Epson Inkjet Printer Driver (ESC/P-R) for Linux.

| Printer | Driver/filter | Notes |
| AcuLaser CX11(NF) | [epson-alcx11-filter](https://aur.archlinux.org/packages/epson-alcx11-filter/) |
| AcuLaser C900 | This printer uses Epson's driver, with a device URI of '**usb://EPSON/AL-C900'**, and may need the pipsplus service to be running. |
| EP-50V | [epson-inkjet-printer-escpr2](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr2/) |
| EP-879A |
| EP-880A |
| ET-2700 | [epson-inkjet-printer-escpr](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr/) |
| ET-2750 |
| ET-3700 | [epson-inkjet-printer-escpr2](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr2/) |
| ET-3750 |
| ET-4750 |
| EW-M571T | [epson-inkjet-printer-escpr](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr/) |
| EW-M670FT | [epson-inkjet-printer-escpr2](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr2/) |
| L380 | [epson-inkjet-printer-201601w](https://aur.archlinux.org/packages/epson-inkjet-printer-201601w/) |
| L382 |
| L4150 | [epson-inkjet-printer-escpr](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr/) |
| L4160 |
| L6160 | [epson-inkjet-printer-escpr2](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr2/) |
| L6170 |
| L6190 |
| LP-S5000 | This printer requires a [custom driver from Avasys](#Avasys). |
| PM-520 | [epson-inkjet-printer-escpr2](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr2/) |
| PX-M5080F |
| PX-M5081F |
| PX-M680F |
| PX-M7070FX |
| PX-M780F |
| PX-M781F |
| PX-M884F |
| PX-S5080 |
| PX-S7070X |
| PX-S884 |
| TX125 | [epson-inkjet-printer-n10-nx127](https://aur.archlinux.org/packages/epson-inkjet-printer-n10-nx127/) |
| WF-3720 | [epson-inkjet-printer-escpr2](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr2/) |
| WF-4720 |
| WF-4730 |
| WF-4740 |
| WF-7210 |
| WF-7710 |
| WF-7720 |
| WF-C869R |
| XP-446 | [epson-inkjet-printer-escpr](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr/) |
| XP-5100 | [epson-inkjet-printer-escpr2](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr2/) |
| XP-6000 |
| XP-8500 |
| XP-15000 |
| Printer | Driver/filter | Notes |

### Utilities

#### escputil

escputil is part of the [gutenprint](https://www.archlinux.org/packages/?name=gutenprint) package, and performs some utility functions on Epson printers such as nozzle cleaning.

#### mtink

This is a printer status monitor which enables to get the remaining ink quantity, to print test patterns, to reset printer and to clean nozzle. It use an intuitive graphical user interface.

#### Stylus-toolbox

This is a GUI using escputil and cups drivers. It supports nearly all USB printer of Epson and displays ink quantity, can clean and align print heads and print test patterns.

### Custom drivers

#### Avasys

**Warning:** This section involves installing packages without [pacman](/index.php/Pacman "Pacman"). These directions should ideally be automated with a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

"Source" code of the driver is available on the [avasys website](http://www.avasys.jp), in Japanese, however it includes a 32 bit binary which will cause problem on 64 bit system.

*   [Install](/index.php/Install "Install") the [psutils](https://www.archlinux.org/packages/?name=psutils), [bc](https://www.archlinux.org/packages/?name=bc), [libstdc++5](https://www.archlinux.org/packages/?name=libstdc%2B%2B5) packages ([lib32-libstdc++5](https://www.archlinux.org/packages/?name=lib32-libstdc%2B%2B5) on 64bit).

*   Download the source code of the driver.
*   Compile and install the driver.

```
$ ./configure --prefix=/usr
$ make
# make install

```

If you have any problems on a 64 system, some other lib32 libraries may be required. Please adjust this page if that is the case.

## HP

See also [CUPS/Troubleshooting#HP issues](/index.php/CUPS/Troubleshooting#HP_issues "CUPS/Troubleshooting").

Most HP printers will use [hplip](https://www.archlinux.org/packages/?name=hplip), but some may use [hpoj](https://aur.archlinux.org/packages/hpoj/). Some laser printers are also supported by [foo2zjs-nightly](https://aur.archlinux.org/packages/foo2zjs-nightly/).

| Printer | Driver/filter | Notes |
| DeskJet 710C | [pnm2ppa](https://aur.archlinux.org/packages/pnm2ppa/) |
| DeskJet 712C |
| DeskJet 720C |
| DeskJet 722C |
| DeskJet 820se |
| DeskJet 820Cxi |
| DeskJet 1000Cse |
| DeskJet 1000Cxi |
| LaserJet P1606dn | [hplip](https://www.archlinux.org/packages/?name=hplip) + [hplip-plugin](https://aur.archlinux.org/packages/hplip-plugin/) | Or [foo2zjs-nightly](https://aur.archlinux.org/packages/foo2zjs-nightly/), or [AirPrint](/index.php/CUPS#CUPS "CUPS"). |
| LaserJet Pro MFP M126nw | [hplip](https://www.archlinux.org/packages/?name=hplip) + [hplip-plugin](https://aur.archlinux.org/packages/hplip-plugin/) |
| Photosmart 2575 | [hplip](https://www.archlinux.org/packages/?name=hplip) | Or use the hpijs driver in [foomatic](/index.php/CUPS#Foomatic "CUPS"). |
| Printer | Driver/filter | Notes |

### HPLIP

**Note:** As of hplip v3.17.11 hpijs is not longer available. If you have printers using hpijs they will fail to print. You must modify them and select the new hpcups driver instead.

[hplip](https://www.archlinux.org/packages/?name=hplip) provides drivers for HP DeskJet, OfficeJet, Photosmart, Business Inkjet, and some LaserJet printers, and also provides an easy to use setup tool. See [https://developers.hp.com/hp-linux-imaging-and-printing/supported_devices/index](https://developers.hp.com/hp-linux-imaging-and-printing/supported_devices/index) for the list of supported printers.

To run the setup tool with the GUI qt frontend:

```
# hp-setup -u

```

To run the setup tool with the command line frontend:

```
# hp-setup -i

```

To set up directly the configuration of a network connected HP printer:

```
# hp-setup -i *<ip address>*

```

To run systray spool manager:

```
$ hp-systray

```

To generate a URI for a given ip address:

```
# hp-makeuri *<ip address>*

```

PPD files are in `/usr/share/ppd/HP/`.

If your printer is [listed as requiring a binary plugin](https://developers.hp.com/hp-linux-imaging-and-printing/binary_plugin.html), install the [hplip-plugin](https://aur.archlinux.org/packages/hplip-plugin/) package from [AUR](/index.php/AUR "AUR"). If the binary plugin [hplip-plugin](https://aur.archlinux.org/packages/hplip-plugin/) is a requirement you will need to [start](/index.php/Start "Start") the `org.cups.cupsd.service` before the PPD is recognized by [hplip](https://www.archlinux.org/packages/?name=hplip).

**Note:**

[hplip](https://www.archlinux.org/packages/?name=hplip) depends on [foomatic-db-engine](https://www.archlinux.org/packages/?name=foomatic-db-engine) which prevents the drivers list from appearing when a printer is added to CUPS via the web user interface (following error : "Unable to get list of printer drivers"). Possible workarounds:

*   **Either:** Install [hplip](https://www.archlinux.org/packages/?name=hplip) first, then retrieve the PPD file that matches your printer from `/usr/share/ppd/HP/`. Next, remove [hplip](https://www.archlinux.org/packages/?name=hplip) entirely as well as any unnecessary dependencies. Finally, install the printer manually using the CUPS web UI, selecting the PPD file you retrieved, and then re-install [hplip](https://www.archlinux.org/packages/?name=hplip). After a reboot, you should have a fully working printer.
*   **Or:** Remove [hplip](https://www.archlinux.org/packages/?name=hplip), [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) and [foomatic-db-engine](https://www.archlinux.org/packages/?name=foomatic-db-engine) along with any unnecessary dependencies. Reinstall [hplip](https://www.archlinux.org/packages/?name=hplip) and restart CUPS. Install your printer using the CUPS web UI, which should now be able to find the drivers automatically. No reboot needed.

### foo2zjs

[foo2zjs](http://foo2zjs.rkkda.com/) supports some HP LaserJet printers. As of June 2018 the hplip package interferes with [foo2zjs-nightly](https://aur.archlinux.org/packages/foo2zjs-nightly/), as described at [this forum post](https://bbs.archlinux.org/viewtopic.php?pid=1662809) and [FS#58815](https://bugs.archlinux.org/task/58815).

## Konica Minolta

| Printer | Driver/filter | Notes |
| Minolta Magicolor 1600W | [foomatic](/index.php/CUPS#Foomatic "CUPS") |
| Minolta Magicolor 1680MF |
| Minolta Magicolor 1690MF |
| Minolta Magicolor 2480MF |
| Minolta Magicolor 2490MF |
| Minolta Magicolor 2530DL |
| Minolta Magicolor 4690MF |
| Printer | Driver/filter | Notes |

### foo2zjs

[#foo2zjs](#foo2zjs), mentioned above for supporting some HP printers, also support some Minolta printers.

## Lexmark

### Utilities

Lexmark provides a utility called lexijtools with the drivers.

### Custom drivers

Lexmark does provide Linux drivers for all their hardware. The following packages are required:

*   [cups](https://www.archlinux.org/packages/?name=cups)
*   [sane](https://www.archlinux.org/packages/?name=sane)
*   [ncurses](https://www.archlinux.org/packages/?name=ncurses)
*   [libusb](https://www.archlinux.org/packages/?name=libusb)
*   [libxext](https://www.archlinux.org/packages/?name=libxext)
*   [libxtst](https://www.archlinux.org/packages/?name=libxtst)
*   [libxi](https://www.archlinux.org/packages/?name=libxi)
*   [libstdc++5](https://www.archlinux.org/packages/?name=libstdc%2B%2B5)
*   [krb5](https://www.archlinux.org/packages/?name=krb5)
*   [lua](https://www.archlinux.org/packages/?name=lua) (for the automated installer)
*   [Java](/index.php/Java "Java") (for the automated installer, and some of the Lexmark tools)

The drivers will need to be [downloaded](http://support.lexmark.com/index?page=driversdownloads) from Lexmark's website. Preferably, create a package (see [Creating packages](/index.php/Creating_packages "Creating packages")) and install it. Here is a basic [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") that still needs work but will give an idea of what is required.

 `PKGBUILD` 
```
# Contributor: Todd Partridge (Gen2ly) toddrpartridge (at) yahoo

pkgname=cups-lexmark-Z2300-2600
pkgver=1
pkgrel=1
pkgdesc="Lexmark Z2300 and 2600 Series printer driver for cups"
arch=('i686')
url="http://www.lexmark.com/"
license=('custom')
depends=('cups' 'glibc' 'ncurses' 'libusb' 'libxext' 'libxtst' 'libxi' 'libstdc++5' 'krb5' 'lua' 'java-runtime')
conflicts=('z600' 'cjlz35le-cups' 'cups-lexmark-700')
source=(lexmark-inkjet-08-driver-1.0-1.i386.tar.gz.sh)
md5sums=(3c37eb87e3dad4853bf29344f9695134)

package() {
  # Extract installer
  sh lexmark-inkjet-08-driver-1.0-1.i386.tar.gz.sh --target Installer-Files
  cd Installer-Files
  mkdir Driver
  tar xvvf instarchive_all --lzma -C Driver/
  cd Driver
  tar xv lexmark-inkjet-08-driver-1.0-1.i386.tar.gz -C $pkgdir
}

```

Keep in mind you can use the automated installer but doing so will leave the resulting changes untracked. The PPD will be installed into `/usr/local/lexmark/lxk08/etc/` or similar, depending on the printer model.

## Oki

| Printer | Driver/filter | Notes |
| C110 | [foomatic](/index.php/CUPS#Foomatic "CUPS") |
| MC561 | [foomatic-db-nonfree](/index.php/CUPS#Foomatic "CUPS") |
| Printer | Driver/filter | Notes |

## Ricoh

Install [openprinting-ppds-pxlmono-ricoh](https://aur.archlinux.org/packages/openprinting-ppds-pxlmono-ricoh/) if your device is black and white, or [openprinting-ppds-pxlcolor-ricoh](https://aur.archlinux.org/packages/openprinting-ppds-pxlcolor-ricoh/) if it's color. Note that Ricoh copiers are sometimes branded as Savin, Gestetner, Lanier, Rex-Rotary, Nashuatec, and/or IKON. So, if you have a device bearing one of these brands, it may be supported by these drivers as well.

*   [List of supported black and white models](https://www.openprinting.org/driver/pxlmono-Ricoh)
*   [List of supported color models](https://www.openprinting.org/driver/pxlcolor-Ricoh)

For winprinters (Ricoh series SP100 and SP200) try out [ricoh-sp100-git](https://aur.archlinux.org/packages/ricoh-sp100-git/).

| Printer | Driver/filter | Notes |
| SP 112 | [ricoh-sp100-git](https://aur.archlinux.org/packages/ricoh-sp100-git/) |
| SP 201n | [ricoh-sp100-git](https://aur.archlinux.org/packages/ricoh-sp100-git/) |
| 213W | *Generic PCL Laser* | Obtain a WPS code by holding down the wifi button for 2 seconds, then hitting the stop/start button. |
| Printer | Driver/filter | Notes |

## Samsung

For printers requiring the *cnijfilter* drivers, search for the correct driver [in the AUR](https://aur.archlinux.org/packages.php?K=cnijfilter)

| Printer | Driver/filter | Notes |
| ML-2010 | [splix](https://www.archlinux.org/packages/?name=splix) |
| SCX-4200 | [splix](https://www.archlinux.org/packages/?name=splix) |
| Newer printers? | [samsung-unified-driver](https://aur.archlinux.org/packages/samsung-unified-driver/) |
| Printer | Driver/filter | Notes |

## Xerox or FujiXerox

| Printer | Driver/filter | Notes |
| DocuPrint 203A | [hplip](https://www.archlinux.org/packages/?name=hplip) | Using the **DocuPrint P8e(hpijs)** driver, or the Brother driver on FujiXerox's website (see [#Brother](#Brother) for more information on how to install custom Brother drivers). |
| Phaser 3100MFP | Install Xerox's driver | See [#Phaser 3100MFP](#Phaser_3100MFP) for more instructions. |
| Phaser 6115MFP | [foomatic](/index.php/CUPS#Foomatic "CUPS") |
| Phaser 6121MFP | [foomatic](/index.php/CUPS#Foomatic "CUPS") |
| Printer | Driver/filter | Notes |

### Custom drivers

#### Phaser 3100MFP

**Warning:** This section involves installing packages without [pacman](/index.php/Pacman "Pacman"). These directions should ideally be automated with a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

Once you have downloaded the drivers, execute the driver installer and accept the licence:

```
# cd printer
# ./XeroxPhaser3100.install

```

Note that the driver is 32 bit, so some 32 bit libraries will be required on an x86_64 system.

For the scanner, create an /etc/sane.d directory if it doesn't already exist, because it's need by the installer:

```
# mkdir -p /etc/sane.d

```

Now install the driver:

```
# cd scanner/
# ./XeroxPhaser3100sc.install

```

Again, on an x86_64 install, 32 bit libraries will be needed.

#### Phaser 6000B

[Install](/index.php/Install "Install") the [xerox-phaser-6010](https://github.com/aur-archive/xerox-phaser-6010) package (archived from the AUR). The driver may require older versions of [nettle](https://www.archlinux.org/packages/?name=nettle) and [gnutls](https://www.archlinux.org/packages/?name=gnutls) to be installed, since the binary blob linked against older versions of the shared libraries provided by those packages. The oldest known-good versions are `nettle-2.7.1-1` and `gnutls-3.3.13-1`.

#### Phaser 6125N

**Warning:** This section involves installing packages without [pacman](/index.php/Pacman "Pacman"). These directions should ideally be automated with a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

FujiXerox does not support Linux on this model. An old rpm [is available](http://onlinesupport.fujixerox.com/tiles/common/hc_drivers_download.jsp?system=%27Linux%27&shortdesc=null&xcrealpath=http://www.fujixeroxprinters.com/downloads/uploaded/dpc525a_linux_.0.0.tar_81c2.zip) but does not seem to work.

A slightly adapted [custom driver](https://rickvanderzwet.nl/trac/personal/wiki/XeroxPhaser6125N) has been found to work out of the box.

To install the tarball, run

```
# tar -C / --keep-newer-files -xvzf cups-xerox-phaser-6125n-1.0.0.tar.gz

```