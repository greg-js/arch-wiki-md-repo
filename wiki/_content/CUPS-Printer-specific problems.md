# CUPS/Printer-specific problems

See [CUPS](/index.php/CUPS "CUPS") for the main article.

This article contains printer or manufacturer-specific instructions for [CUPS](/index.php/CUPS "CUPS"). See [OpenPrinting](http://www.openprinting.org/printers) if your printer is not already listed here, or if none of the listed drivers work.

## Contents

*   [1 Brother](#Brother)
    *   [1.1 Network printers](#Network_printers)
    *   [1.2 Custom drivers](#Custom_drivers)
        *   [1.2.1 Manually installing from the RPM packages](#Manually_installing_from_the_RPM_packages)
*   [2 Canon](#Canon)
    *   [2.1 CARPS](#CARPS)
    *   [2.2 CAPT](#CAPT)
*   [3 Dell](#Dell)
    *   [3.1 Custom drivers](#Custom_drivers_2)
        *   [3.1.1 Xerox Phaser 6000B](#Xerox_Phaser_6000B)
*   [4 Epson](#Epson)
    *   [4.1 Utilities](#Utilities)
        *   [4.1.1 escputil](#escputil)
        *   [4.1.2 mtink](#mtink)
        *   [4.1.3 Stylus-toolbox](#Stylus-toolbox)
    *   [4.2 Custom drivers](#Custom_drivers_3)
        *   [4.2.1 Avasys](#Avasys)
*   [5 FujiXerox](#FujiXerox)
*   [6 HP](#HP)
    *   [6.1 HPLIP Driver](#HPLIP_Driver)
*   [7 Konica](#Konica)
*   [8 Lexmark](#Lexmark)
    *   [8.1 Utilities](#Utilities_2)
    *   [8.2 Custom drivers](#Custom_drivers_4)
*   [9 Oki](#Oki)
*   [10 Samsung](#Samsung)
*   [11 Xerox](#Xerox)
    *   [11.1 Custom drivers](#Custom_drivers_5)
        *   [11.1.1 Phaser 3100MFP](#Phaser_3100MFP)

## Brother

| Printer | Driver/filter | Notes |
| DCP-135C | [brother-dcp135c](https://aur.archlinux.org/packages/brother-dcp135c/) |
| DCP-150C | [brother-dcp150c](https://aur.archlinux.org/packages/brother-dcp150c/) |
| DCP-7020 | [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) | Or Brother's driver. |
| DCP-7030 | [brother-dcp7030](https://aur.archlinux.org/packages/brother-dcp7030/) |
| DCP-7065DN | [brother-dcp7065dn](https://aur.archlinux.org/packages/brother-dcp7065dn/) |
| HL-2030 | [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) | Or [brother-hl2030](https://aur.archlinux.org/packages/brother-hl2030/) |
| HL-2035 | [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) | Should be compatible with any drivers for the HL-2030. |
| HL-2040 | [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) | Or [brother-hl2040](https://aur.archlinux.org/packages/brother-hl2040/) |
| HL-2130 | [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) (using the HL-2140 driver) | Or [hplip](https://www.archlinux.org/packages/?name=hplip) |
| HL-2140 | [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) | Or [brother-hl2140](https://aur.archlinux.org/packages/brother-hl2140/) |
| HL-2170W | [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) | Or Brother's driver. |
| HL-2250DN | [brother-hl2250dn](https://aur.archlinux.org/packages/brother-hl2250dn/) |
| HL-2270DW | [brother-hl2270dw](https://aur.archlinux.org/packages/brother-hl2270dw/) |
| HL-2280DW | [brother-hl2280dw](https://aur.archlinux.org/packages/brother-hl2280dw/) |
| HL-3045CN | Install Brother's driver. |
| HL-3150CDW | [brother-hl3150cdw](https://aur.archlinux.org/packages/brother-hl3150cdw/) |
| HL-3170CDW | [brother-cups-wrapper-ac](https://aur.archlinux.org/packages/brother-cups-wrapper-ac/) | Use BRScript3 Driver for HL-4070CDW |
| HL-5140 | [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) | Or Brother's driver. |
| MFC-420CN | [brother-mfc-420cn](https://aur.archlinux.org/packages/brother-mfc-420cn/) |
| MFC-440CN | [brother-mfc-440cn](https://aur.archlinux.org/packages/brother-mfc-440cn/) |
| MFC-465CN | [brother-mfc-465cn](https://aur.archlinux.org/packages/brother-mfc-465cn/) |
| MFC-7360N | Install Brother's driver. |
| MFC-9320CW | Install Brother's driver. |
| MFC-9840CDW | [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) | Or Brother's driver. This printer also works with the generic PCL-6 driver from the [gutenprint](https://www.archlinux.org/packages/?name=gutenprint) package. Use **pcl_p1** for the printer's address when using the PCL-6 driver. |
| MFC-J470DW | [brother-mfc-j470dw](https://aur.archlinux.org/packages/brother-mfc-j470dw/) |
| MFC-J5910DW | [brother-mfc-j5910dw](https://aur.archlinux.org/packages/brother-mfc-j5910dw/) |
| MFC-J650DW | Install Brother's driver. |
| Printer | Driver/filter | Notes |

### Network printers

For network printers, use `ipp://**printer_ip**/ipp/port1` as printer address. For some older printers, this might not work. If not, try `lpd://**printer_ip**/BINARY_P1` instead.

Some printers use the socket protocol. For these printers, use `socket:**printer_ip**:9100`. For http, use `http://**printer_ip**/POSTSCRIPT_P1`.

### Custom drivers

Brother provides custom drivers on their website, either in source tarball, rpm, or deb form. [Packaging Brother printer drivers](/index.php/Packaging_Brother_printer_drivers "Packaging Brother printer drivers") covers creating [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") from the existing RPM packages.

**Note:** The source packages might be a better alternative to the rpm packages, provided they contain all the needed files.

#### Manually installing from the RPM packages

**Warning:** This should ideally be automated in a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")

[Install](/index.php/Install "Install") the [rpmextract](https://www.archlinux.org/packages/?name=rpmextract) package, and extract both rpm packages using `rpmextract.sh`. Extracting both files will create a var and a usr directory - move the contents of both directories into the corresponding root directories.

Run the cups wrapper file in `/usr/local/Brother/cupswrapper`. This should automatically install and configure your brother printer.

## Canon

| Driver | Description |
| [cndrvcups-lb](https://aur.archlinux.org/packages/cndrvcups-lb/) | Canon UFR II /LIPSLX Printer Driver build from source for LBP, iR & MF printers |
| [cndrvcups-lb-bin](https://aur.archlinux.org/packages/cndrvcups-lb-bin/) | Canon UFR II/UFR II LT Printer Driver (including Canon imageCLASS MF4720w) |
| [cnijfilter-mg4200](https://aur.archlinux.org/packages/cnijfilter-mg4200/) | Canon IJ Printer Driver (for mg4200 series) |
| [capt-src](https://aur.archlinux.org/packages/capt-src/) | Canon CAPT Printer Driver (for Canon i-Sensys printers) |
| [cups-bjnp](https://aur.archlinux.org/packages/cups-bjnp/) | CUPS back-end for the canon printers using the proprietary USB over IP BJNP protocol |

| Printer | Driver/filter | Notes |
| iP4300 | [gutenprint](https://www.archlinux.org/packages/?name=gutenprint) | Or use Canon's [cnijfilter-ip4300](https://aur.archlinux.org/packages/cnijfilter-ip4300/) driver, or the [TurboPrint](http://www.turboprint.info/) driver. |
| LBP810 | [capt-src](https://aur.archlinux.org/packages/capt-src/) |
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
| Printer | Driver/filter | Notes |

Some Canon printers will use a similar setup to the iP4300, so consider modifying the [cnijfilter-ip4300](https://aur.archlinux.org/packages/cnijfilter-ip4300/) package for other, similar printers.

### CARPS

Some of Canon's printers use Canon's proprietary Canon Advanced Raster Printing System (CARPS) driver. [Rainbow Software](http://www.rainbow-software.org/2014/01/23/cups-driver-for-canon-carps-printers/) have managed to reverse engineer the CARPS data format and have successfully created a CARPS CUPS driver, which is available as [carps-cups](https://aur.archlinux.org/packages/carps-cups/). The project's [GitHub](https://github.com/ondrej-zary/carps-cups) page includes a list of working printers.

### CAPT

See [Canon CAPT](/index.php/Canon_CAPT "Canon CAPT").

## Dell

| Printer | Driver/filter | Notes |
| 1250C | [foo2zjs](https://aur.archlinux.org/packages/foo2zjs/) | See [http://cybercom.net/~dcoffin/hbpl](http://cybercom.net/~dcoffin/hbpl), the patch has been merged into upstream. The printer may also work with the [Xerox Phaser 6000B driver](#Xerox_Phaser_6000B). |
| Printer | Driver/filter | Notes |

### Custom drivers

#### Xerox Phaser 6000B

[Install](/index.php/Install "Install") the [xerox-phaser-6010](https://github.com/aur-archive/xerox-phaser-6010) package (archived from the AUR). The driver may require older versions of [nettle](https://www.archlinux.org/packages/?name=nettle) and [gnutls](https://www.archlinux.org/packages/?name=gnutls) to be installed, since the binary blob linked against older versions of the shared libraries provided by those packages. The oldest known-good versions are `nettle-2.7.1-1` and `gnutls-3.3.13-1`.

## Epson

[epson-inkjet-printer-escpr](https://aur.archlinux.org/packages/epson-inkjet-printer-escpr/) is a driver for the Epson Inkjet Printer Driver (ESC/P-R) for Linux.

There is a large selection of printer drivers/filters available in the [AUR](/index.php/AUR "AUR").

| Printer | Driver/filter | Notes |
| AcuLaser CX11(NF) | [epson-alcx11-filter](https://aur.archlinux.org/packages/epson-alcx11-filter/) |
| AcuLaser C900 | This printer uses Epson's driver, with a device URI of '**usb://EPSON/AL-C900'**, and may need the pipsplus service to be running. |
| TX125 | [epson-inkjet-printer-n10-nx127](https://aur.archlinux.org/packages/epson-inkjet-printer-n10-nx127/) |
| LP-S5000 | This printer requires a [custom driver from Avasys](#Avasys). |
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

## FujiXerox

| Printer | Driver/filter | Notes |
| DocuPrint 203A | [hplip](https://www.archlinux.org/packages/?name=hplip) | Using the **DocuPrint P8e(hpijs)** driver, or the Brother driver on FujiXerox's website (see [#Brother](#Brother) for more information on how to install custom Brother drivers). |
|  ? | [fxlinuxprint](https://aur.archlinux.org/packages/fxlinuxprint/) |
| Printer | Driver/filter | Notes |

## HP

Most HP printers will use [hplip](https://www.archlinux.org/packages/?name=hplip), but some may use [hpoj](https://aur.archlinux.org/packages/hpoj/).

| Printer | Driver/filter | Notes |
| Photosmart 2575 | [hplip](https://www.archlinux.org/packages/?name=hplip) | Or use the hpijs driver in [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db). |
| DeskJet 710C | [pnm2ppa](https://aur.archlinux.org/packages/pnm2ppa/) |
| DeskJet 712C | [pnm2ppa](https://aur.archlinux.org/packages/pnm2ppa/) |
| DeskJet 720C | [pnm2ppa](https://aur.archlinux.org/packages/pnm2ppa/) |
| DeskJet 722C | [pnm2ppa](https://aur.archlinux.org/packages/pnm2ppa/) |
| DeskJet 820se | [pnm2ppa](https://aur.archlinux.org/packages/pnm2ppa/) |
| DeskJet 820Cxi | [pnm2ppa](https://aur.archlinux.org/packages/pnm2ppa/) |
| DeskJet 1000Cse | [pnm2ppa](https://aur.archlinux.org/packages/pnm2ppa/) |
| DeskJet 1000Cxi | [pnm2ppa](https://aur.archlinux.org/packages/pnm2ppa/) |
| Printer | Driver/filter | Notes |

###### HPLIP Driver

[hplip](https://www.archlinux.org/packages/?name=hplip) provides drivers for HP DeskJet, OfficeJet, Photosmart, Business Inkjet and some LaserJet printers.

To run with qt frontend:

```
# hp-setup -u

```

To run with command line:

```
# hp-setup -i

```

To run systray spool manager:

```
$ hp-systray

```

PPD files are in `/usr/share/ppd/HP/`.

For printers that require the proprietary HP plugin (like the Laserjet Pro P1102w or 1020), install the [hplip-plugin](https://aur.archlinux.org/packages/hplip-plugin/) package from [AUR](/index.php/AUR "AUR").

**Note:**

[hplip](https://www.archlinux.org/packages/?name=hplip) depends on [foomatic-db-engine](https://www.archlinux.org/packages/?name=foomatic-db-engine) which prevents the drivers list from appearing when a printer is added to CUPS via the web user interface (following error : "Unable to get list of printer drivers"). Possible workarounds:

*   **Either:** Install [hplip](https://www.archlinux.org/packages/?name=hplip) first, then retrieve the PPD file that matches your printer from `/usr/share/ppd/HP/`. Next, remove [hplip](https://www.archlinux.org/packages/?name=hplip) entirely as well as any unnecessary dependencies. Finally, install the printer manually using the CUPS web UI, selecting the PPD file you retrieved, and then re-install [hplip](https://www.archlinux.org/packages/?name=hplip). After a reboot, you should have a fully working printer.
*   **Or:** Remove [hplip](https://www.archlinux.org/packages/?name=hplip), [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) and [foomatic-db-engine](https://www.archlinux.org/packages/?name=foomatic-db-engine) along with any unnecessary dependencies. Reinstall [hplip](https://www.archlinux.org/packages/?name=hplip) and restart CUPS. Install your printer using the CUPS web UI, which should now be able to find the drivers automatically. No reboot needed.

## Konica

| Printer | Driver/filter | Notes |
| Minolta Magicolor 1600W | [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) |
| Minolta Magicolor 1680MF | [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) |
| Minolta Magicolor 1690MF | [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) |
| Minolta Magicolor 2480MF | [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) |
| Minolta Magicolor 2490MF | [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) |
| Minolta Magicolor 2530DL | [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) |
| Minolta Magicolor 4690MF | [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) |
| Printer | Driver/filter | Notes |

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
| C110 | [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) |
| MC561 | [foomatic-db-nonfree](https://www.archlinux.org/packages/?name=foomatic-db-nonfree) |
| Printer | Driver/filter | Notes |

## Samsung

For printers requiring the _cnijfilter_ drivers, search for the correct driver [in the AUR](https://aur.archlinux.org/packages.php?K=cnijfilter)

| Printer | Driver/filter | Notes |
| ML-2010 | [splix](https://www.archlinux.org/packages/?name=splix) |
| Newer printers? | [samsung-unified-driver](https://aur.archlinux.org/packages/samsung-unified-driver/) |
| Printer | Driver/filter | Notes |

## Xerox

| Printer | Driver/filter | Notes |
| Phaser 3100MFP | Install Xerox's driver | See [#Phaser 3100MFP](#Phaser_3100MFP) for more instructions. |
| Phaser 6115MFP | [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) |
| Phaser 6121MFP | [foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db) |
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

Retrieved from "[https://wiki.archlinux.org/index.php?title=CUPS/Printer-specific_problems&oldid=419459](https://wiki.archlinux.org/index.php?title=CUPS/Printer-specific_problems&oldid=419459)"