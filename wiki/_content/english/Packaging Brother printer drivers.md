Brother supplies Linux drivers for its printers, however they are provided as .RPM and/or .DEB packages only. This article explains what adjustments to the contents of the DEB and RPM packages supplied by Brother will need to be made to create a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") for the printer driver. Additional example PKGBUILDs for Brother printers can be found by searching in the [AUR](/index.php/AUR "AUR").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Really short overview of CUPS](#Really_short_overview_of_CUPS)
*   [2 Preparing a PKGBUILD for .DEB](#Preparing_a_PKGBUILD_for_.DEB)
*   [3 Preparing a PKGBUILD for .RPM](#Preparing_a_PKGBUILD_for_.RPM)
    *   [3.1 Other changes](#Other_changes)
*   [4 x86_64](#x86_64)

## Really short overview of CUPS

[CUPS](/index.php/CUPS "CUPS") handles printers using a `.ppd` file and a filter binary. Once those two files are installed, the printer can be [added](/index.php/CUPS#Usage "CUPS") in CUPS. A simple example PKGBUILD that does this is [samsung2010p](https://aur.archlinux.org/packages/samsung2010p/).

## Preparing a PKGBUILD for .DEB

Brother is offering a "Driver Install Tool" as well as two .DEB packages, one being the LPR driver and the other one being a cups wrapper (running on top of lpr driver). Both can be found on brothers "Support & Downloads" page, e.g. for HL-L9200CDW this would be [https://support.brother.com/g/b/producttop.aspx?c=ca&lang=en&prod=hll9200cdw_us_as_cn](https://support.brother.com/g/b/producttop.aspx?c=ca&lang=en&prod=hll9200cdw_us_as_cn) . It is possible to create a PKGBUILD file that will automatically download and install the .DEB packages directly from the URL provided by brother. Therefore you will need to obtain the direct download links for both .DEB packages from brothers website, e.g. for HL-L9200CDW these would be: [https://download.brother.com/welcome/dlf101047/hll9200cdwlpr-1.1.2-1.i386.deb](https://download.brother.com/welcome/dlf101047/hll9200cdwlpr-1.1.2-1.i386.deb) and [https://download.brother.com/welcome/dlf101045/hll9200cdwcupswrapper-1.1.3-1.i386.deb](https://download.brother.com/welcome/dlf101045/hll9200cdwcupswrapper-1.1.3-1.i386.deb)

Once you have obtained the download URLs for both .DEB packages, use existing PKGBUILD files from [brother-hll8360cdw-lpr-bin](https://aur.archlinux.org/packages/brother-hll8360cdw-lpr-bin/) and [brother-hll8360cdw-cups-bin](https://aur.archlinux.org/packages/brother-hll8360cdw-cups-bin/) as templates. You will need to adjust the package name, probably to a new name for your specific printer model. Change url= to the URL of brothers support page for your specific printer model (for HL-L9200CDW this would be [https://support.brother.com/g/b/producttop.aspx?c=ca&lang=en&prod=hll9200cdw_us_as_cn](https://support.brother.com/g/b/producttop.aspx?c=ca&lang=en&prod=hll9200cdw_us_as_cn) ), source= needs to be adjusted to the URL of the .DEB package. The following PKGBUILD example has been based on [brother-hll8360cdw-cups-bin](https://aur.archlinux.org/packages/brother-hll8360cdw-cups-bin/) but has been adjusted for HL-L9200CDW lpr printer driver:

```
# Maintainer: *John Doe <joe@example.com>*
pkgname=*brother-hll9200cdw-lpr-bin*
pkgver=*1.1.2*
pkgrel=1
pkgdesc="*LPR driver for Brother HL-L9200CDW(T) printer*"
arch=("i686" "x86_64")
url="*[https://support.brother.com/g/b/producttop.aspx?c=ca&lang=en&prod=hll9200cdw_us_as_cn](https://support.brother.com/g/b/producttop.aspx?c=ca&lang=en&prod=hll9200cdw_us_as_cn)*"
license=("EULA")
groups=("base-devel")
source=("*[http://www.brother.com/pub/bsc/linux/packages/hll9200cdwlpr-1.1.2-1.i386.deb](http://www.brother.com/pub/bsc/linux/packages/hll9200cdwlpr-1.1.2-1.i386.deb)*")
md5sums=("*30124df7d49362906a2a118eff3c710e*")
package() {
        tar -xf data.tar.gz -C "${pkgdir}"
}

```

Don't forget to update the md5sum and pkgver version should be the same version as brother's printer drivers (please note versions might differ for lpr and cups wrapper). Create the PKGBUILD file for the cups wrapper, too:

```
# Maintainer: *John Doe <joe@example.com>*
pkgname=*brother-hll9200cdw-cups-bin*
pkgver=*1.1.3*
pkgrel=1
pkgdesc="*CUPS wrapper for Brother HL-L9200CDW(T) printer*"
arch=("i686" "x86_64")
url="*[https://support.brother.com/g/b/producttop.aspx?c=ca&lang=en&prod=hll9200cdw_us_as_cn](https://support.brother.com/g/b/producttop.aspx?c=ca&lang=en&prod=hll9200cdw_us_as_cn)*"
license=("EULA")
groups=("base-devel")
source=("*[http://www.brother.com/pub/bsc/linux/packages/hll9200cdwcupswrapper-1.1.3-1.i386.deb](http://www.brother.com/pub/bsc/linux/packages/hll9200cdwcupswrapper-1.1.3-1.i386.deb)*")
md5sums=("*0a802088aac7236a3c309b2b46b37f11*")
package() {
       tar -xf data.tar.gz -C "${pkgdir}"
}

```

Finally, use [makepkg](/index.php/Makepkg "Makepkg") to test/install your newly created PKGBUILD file(s). If everything works, don't forget to push your new driver to AUR. In order to create a new AUR repository for your printer driver, register an account with [https://aur.archlinux.org](https://aur.archlinux.org) then git clone a new non-existing repo that matches your newly chosen package names, e.g.:

```
git clone *[https://aur.archlinux.org/](https://aur.archlinux.org/)*brother-hll9200cdw-lpr-bin.git
git clone *[https://aur.archlinux.org/](https://aur.archlinux.org/)*brother-hll9200cdw-cups-bin.git

```

Put your previously created PKGBUILD file into the according folder. To submit your driver to AUR, finally run:

```
cd *brother-hll9200cdw-cups-bin*
makepkg --printsrcinfo > .SRCINFO
git add PKGBUILD .SRCINFO
git commit -a -m "Updating the package"
git push -f origin master
cd ..

```

```
cd *brother-hll9200cdw-lpr-bin*
makepkg --printsrcinfo > .SRCINFO
git add PKGBUILD .SRCINFO
git commit -a -m "Updating the package"
git push -f origin master
cd ..

```

## Preparing a PKGBUILD for .RPM

Unfortunately, Brother's drivers have some issues:

*   The CUPS driver is built on top of the lpr driver.
*   The CUPS driver package contains a single installation shell script with an embedded ppd and filter. It is executed by rpm during installation. It extracts the ppd and filter, and performs some installation procedures in a Red Hat-specific way.
*   The CUPS driver package uses paths that are not compliant with the [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards").

These issues can be worked around.

*   The lpr driver does not need to be installed, so the PKGBUILD can just extract the files in the lpr driver's RPM package.
*   The CUPS driver's RPM should contain a single shell script. For instance, for the [brother-hl2030](https://aur.archlinux.org/packages/brother-hl2030/) package, the PKGBUILD changes three things:
    1.  The paths are changed.
    2.  All commands are disabled except "`cat <<EOF`" or "`echo > ...`" or whatever there is that emits *.ppd or filter to separate file. It was done by wrapping irrelevant instructions by `if false; then ... fi`.
    3.  The target file names for the ppd and filter are changed so they are installed into the same directory as the PKGBUILD. Note that paths to the embedded filter where also changed.
*   To fix the paths to conform to the [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards"), [sed](https://www.archlinux.org/packages/?name=sed) or similar can be used on all text files unpacked from both the lpr and CUPS drivers. Look at the patch in the [brother-hl2030](https://aur.archlinux.org/packages/brother-hl2030/) package to check which files are affected.

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