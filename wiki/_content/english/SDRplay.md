Related articles

*   [GNU Radio](/index.php/GNU_Radio "GNU Radio")
*   [RTL-SDR](/index.php/RTL-SDR "RTL-SDR")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Hardware Driver](#Hardware_Driver)
*   [2 SoapySDR](#SoapySDR)
*   [3 GNU Radio](#GNU_Radio)
*   [4 Other Applications](#Other_Applications)
*   [5 See Also](#See_Also)

[SDRplay](https://www.sdrplay.com/) is a manufacturer for a range of Software Defined Radio (SDR) receivers all based on the Mirics Semiconductor [MSi2500](http://www.mirics.com/MSi2500%20Datasheet%20R1P1.pdf) which is used in a variety of applications from DVB-T to AM Radio.

## Hardware Driver

The SDRplay driver is closed source so it is only available in binary format, it can be downloaded from [here](https://www.sdrplay.com/linuxdl.php) or preferably installed from [libsdrplay](https://aur.archlinux.org/packages/libsdrplay/).

## SoapySDR

Not many applications currently support libmirsdrapi-rsp so it is a good idea to install [soapysdr](https://www.archlinux.org/packages/?name=soapysdr) or [soapysdr-git](https://aur.archlinux.org/packages/soapysdr-git/).

The SoapySDRPlay module is also required and is available from [soapysdrplay](https://aur.archlinux.org/packages/soapysdrplay/) or [soapysdrplay-git](https://aur.archlinux.org/packages/soapysdrplay-git/)

## GNU Radio

Users wanting to use the SDRplay with GNU Radio will need to install [gr-osmosdr-nonfree-git](https://aur.archlinux.org/packages/gr-osmosdr-nonfree-git/).

## Other Applications

*   [cubicsdr](https://aur.archlinux.org/packages/cubicsdr/) or [cubicsdr-git](https://aur.archlinux.org/packages/cubicsdr-git/) provides a fully functional and easy to use SDR application.
*   [gqrx](https://www.archlinux.org/packages/?name=gqrx) another easy to use SDR application built on GNU Radio.
*   [sdrangel](https://www.archlinux.org/packages/?name=sdrangel) a versatile tool with a nice looking interface, can also decode digital voice

## See Also

*   [Official Website](https://www.sdrplay.com/)
*   [Official Forum](https://www.sdrplay.com/community/)