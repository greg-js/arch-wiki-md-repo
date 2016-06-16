[RTL-SDR](http://sdr.osmocom.org/trac/wiki/rtl-sdr) is a set of tools that enables [DVB-T](/index.php/DVB-T "DVB-T") USB dongles based on the Realtek RTL2832U chipset to be used as cheap software defined radios, given that the chip allows transferring raw I/Q samples from the tuner straight to the host device.

See the [RTL-SDR wiki](http://sdr.osmocom.org/trac/wiki/rtl-sdr) for exact technical specifications.

## Packages

The latest stable RTL-SDR version can be installed from [rtl-sdr](https://www.archlinux.org/packages/?name=rtl-sdr) in the [official repositories](/index.php/Official_repositories "Official repositories").

Bleeding edge is on [rtl-sdr-git](https://aur.archlinux.org/packages/rtl-sdr-git/) in the [AUR](/index.php/AUR "AUR").

**Note:** RTL-SDR conflicts with existing [DVB-T](/index.php/DVB-T "DVB-T") drivers in the kernel, and upon installation blacklists the relevant drivers as can be seen in `/etc/modprobe.d/rtlsdr.conf`. To use the dongle with the original DVB-T drivers, it is required to manually load them, see [DVB-T#Driver](/index.php/DVB-T#Driver "DVB-T").

udev rules are installed at `/usr/lib/udev/rules.d/10-rtl-sdr.rules` and set the proper permissions such that non-root users can access the device.

## Usage

Performing a simple test, and make sure the dongle works and that there are no lost samples:

```
$ rtl_test

```

Raw samples can be captured directly to file (or fifo), for example to tune to 123.4MHz and capture 1.8M samples/sec:

```
$ rtl_sdr capture.bin -s 1.8e6 -f 123.4e6

```

Tune to your favorite radio station and pipe to [sox](/index.php/PulseAudio "PulseAudio") for audio:

```
$ rtl_fm -f 102.7e6 -M wbfm -s 200000 -r 48000 - | aplay -r 48000 -f S16_LE

```

## Applications

Some popular applications that use RTL-SDR:

*   [dump1090-git](https://aur.archlinux.org/packages/dump1090-git/) - a lightweight ModeS (1090Mhz) decoder
*   [multimon-ng-git](https://aur.archlinux.org/packages/multimon-ng-git/) - a decoder for various digital modes
*   [gqrx](https://www.archlinux.org/packages/?name=gqrx) - A popular sdr radio reciver for linux, see [gqrx](/index.php/Gqrx "Gqrx")