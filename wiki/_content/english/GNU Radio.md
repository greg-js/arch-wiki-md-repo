Related articles

*   [DVB-T](/index.php/DVB-T "DVB-T")
*   [RTL-SDR](/index.php/RTL-SDR "RTL-SDR")

[GNU Radio](http://gnuradio.org/redmine/projects/gnuradio/wiki) is a free & open-source software development toolkit that provides signal processing blocks to implement software radios. It can be used with readily-available low-cost external RF hardware to create software-defined radios, or without hardware in a simulation-like environment. It is widely used in hobbyist, academic and commercial environments to support both wireless communications research and real-world radio systems.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Packages](#Packages)
    *   [1.1 GUI](#GUI)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 GetSize() doesn't work without window](#GetSize()_doesn't_work_without_window)
    *   [2.2 TypeError: in method 'source_sptr_set_gain_mode', argument 2 of type 'bool'](#TypeError:_in_method_'source_sptr_set_gain_mode',_argument_2_of_type_'bool')

## Packages

The latest stable GNU Radio version can be installed with [gnuradio](https://www.archlinux.org/packages/?name=gnuradio) from the [official repositories](/index.php/Official_repositories "Official repositories").

Bleeding edge is [gnuradio-git](https://aur.archlinux.org/packages/gnuradio-git/) in the [AUR](/index.php/AUR "AUR"), and in some cases VOLK may need to be built separately from [libvolk-git](https://aur.archlinux.org/packages/libvolk-git/).

If you want `gnuradio-companion`, just install the [gnuradio-companion](https://www.archlinux.org/packages/?name=gnuradio-companion) package which will install GNU Radio, as well as some additional required packages.

Another popular package is [gnuradio-osmosdr](https://www.archlinux.org/packages/?name=gnuradio-osmosdr) which provides the GRC source blocks for many of the popular SDR devices (Funcube Dongle, [RTL-SDR](/index.php/RTL-SDR "RTL-SDR"), USRP, OsmoSDR, BladeRF and HackRF).

### GUI

The core GNU Radio packages do not support flowgraphs with GUI widgets. For such flowgraphs it is recommended to install QT GUI support via [python2-pyqt4](https://aur.archlinux.org/packages/python2-pyqt4/).

Usage of WX GUI is not recommended since it will be phased out in the 3.8 release of GNU Radio, will also include widget upgrades to QT5.

## Troubleshooting

### GetSize() doesn't work without window

If such errors occur when running flow graphs, make sure that the optional dependency [python2-opengl](https://www.archlinux.org/packages/?name=python2-opengl) is installed.

This should be fixed in the next GNU Radio release. [[1]](https://bbs.archlinux.org/viewtopic.php?id=182732)

### TypeError: in method 'source_sptr_set_gain_mode', argument 2 of type 'bool'

When using an (osmocom) RTL-SDR source, you might see this error. The workaround is to manually set the Gain Mode to `True` or `False`.