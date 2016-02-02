# Packaging Brother printer drivers

Brother supplies Linux drivers for its printers, however they are not in an easily packaged format. This article explains what adjustments to the contents of the RPM packages supplied by Brother will need to be made to create a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") for the printer driver. Additional example PKGBUILDs for Brother printers can be found by searching in the [AUR](/index.php/AUR "AUR").

## Contents

*   [1 Really short overview of CUPS](#Really_short_overview_of_CUPS)
*   [2 About Brother drivers](#About_Brother_drivers)
*   [3 Preparing a PKGBUILD](#Preparing_a_PKGBUILD)
    *   [3.1 Other changes](#Other_changes)
*   [4 x86_64](#x86_64)

## Really short overview of CUPS

[CUPS](/index.php/CUPS "CUPS") handles printers using a `.ppd` file and a filter binary. Once those two files are installed, the printer can be [registered](/index.php/CUPS#Local_printers "CUPS") in CUPS. A simple example PKGBUILD that does this is [samsung2010p](https://aur.archlinux.org/packages/samsung2010p/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/samsung2010p)]</sup>.

## About Brother drivers

Unfortunately, Brother's drivers have some issues:

*   The CUPS driver is built on top of the lpr driver.
*   The CUPS driver package contains a single installation shell script with an embedded ppd and filter. It is executed by rpm during installation. It extracts the ppd and filter, and performs some installation procedures in a Red Hat-specific way.
*   The CUPS driver package uses paths that are not compliant with the [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards").

## Preparing a PKGBUILD

These issues can be worked around.

*   The lpr driver does not need to be installed, so the PKGBUILD can just extract the files in the lpr driver's RPM package.
*   The CUPS driver's RPM should contain a single shell script. For instance, for the [brother-hl2030](https://aur.archlinux.org/packages/brother-hl2030/)<sup><small>AUR</small></sup> package, the PKGBUILD changes three things:
    1.  The paths are changed.
    2.  All commands are disabled except "`cat <<EOF`" or "`echo > ...`" or whatever there is that emits *.ppd or filter to separate file. It was done by wrapping irrelevant instructions by `if false; then ... fi`.
    3.  The target file names for the ppd and filter are changed so they are installed into the same directory as the PKGBUILD. Note that paths to the embedded filter where also changed.
*   To fix the paths to conform to the [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards"), [sed](https://www.archlinux.org/packages/?name=sed) or similar can be used on all text files unpacked from both the lpr and CUPS drivers. Look at the patch in the [brother-hl2030](https://aur.archlinux.org/packages/brother-hl2030/)<sup><small>AUR</small></sup> package to check which files are affected.

Effectively after the changes described above the script will just output a ppd and a filter to some known location. The PKGBUILD will then copy them to the proper directories in `$pkgdir`:

```
 install -m 644 -D ppd "${pkgdir}/usr/share/cups/model/HL2030.ppd"
 install -m 755 -D filter  "${pkgdir}/usr/lib/cups/filter/brlpdwrapperHL2030"

```

The lpr driver files will also need to be copied into `$pkgdir`!

### Other changes

Edit the installation script:

```
 -#PSTOPSFILTER=`which pstops`
 +PSTOPSFILTER='/usr/lib/cups/filter/pstops'

```

As pstops is not installed in a standard location, the path will need to be hard-coded.

This may also need to be added.

```
 +[psconvert2]
 +pstops=/usr/lib/cups/filter/pstops

```

## x86_64

Because some of the supplied binaries are 32 bit only, on an x86_64 system some additional [multilib](/index.php/Multilib "Multilib") packages such as a 32 bit version of glibc ([lib32-glibc](https://www.archlinux.org/packages/?name=lib32-glibc)) may need to be installed.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Packaging_Brother_printer_drivers&oldid=409433](https://wiki.archlinux.org/index.php?title=Packaging_Brother_printer_drivers&oldid=409433)"