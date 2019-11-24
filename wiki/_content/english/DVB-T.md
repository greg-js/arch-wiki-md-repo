Related articles

*   [DVB-S](/index.php/DVB-S "DVB-S")
*   [LIRC](/index.php/LIRC "LIRC")
*   [RTL-SDR](/index.php/RTL-SDR "RTL-SDR")

[DVB-T](https://en.wikipedia.org/wiki/DVB-T "wikipedia:DVB-T") is a standard for transmitting terrestrial digital video broadcast, which is used in the majority of Africa, Asia, Australia and Europe. It is possible to receive DVB-T using several different hardware setups, however this article will focus on DVB-T USB dongles based on the RTL2832U chipset (which are also very popular as cheap software defined radios using [RTL-SDR](/index.php/RTL-SDR "RTL-SDR")).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Driver](#Driver)
*   [2 Utilities](#Utilities)
    *   [2.1 Scanning](#Scanning)
*   [3 Clients](#Clients)
    *   [3.1 Kaffeine](#Kaffeine)
    *   [3.2 VLC](#VLC)
    *   [3.3 MPlayer / mpv](#MPlayer_/_mpv)
        *   [3.3.1 Channel selector](#Channel_selector)
    *   [3.4 ffmpeg](#ffmpeg)
    *   [3.5 dvbjet](#dvbjet)
*   [4 Troubleshooting](#Troubleshooting)

## Driver

The main driver in use is `dvb_usb_rtl28xxu`, and exists in the latest kernels. If it is not [loaded](/index.php/Kernel_modules "Kernel modules"), do so manually:

```
# modprobe dvb_usb_rtl28xxu

```

You might also need to load `rtl2832` or `rtl2830`:

```
# modprobe rtl2830
# modprobe rtl2832

```

**Note:** If you have [RTL-SDR](/index.php/RTL-SDR "RTL-SDR") installed, note that it conflicts with this driver, and therefore blacklists it. Make sure to remove any necessary blacklists before loading the driver. The default location for the blacklist file is in `/etc/modprobe.d/rtlsdr.conf`.

After plugging the device in, `dmesg` should show something like this:

```
[ 4009.326338] usb 7-5: new high-speed USB device number 4 using ehci-pci
[ 4009.466712] usb 7-5: dvb_usb_v2: found a 'Realtek RTL2832U reference design' in warm state
[ 4009.531594] usb 7-5: dvb_usb_v2: will pass the complete MPEG2 transport stream to the software demuxer
[ 4009.531613] DVB: registering new adapter (Realtek RTL2832U reference design)
[ 4009.534554] usb 7-5: DVB: registering adapter 0 frontend 0 (Realtek RTL2832 (DVB-T))...
[ 4009.534627] r820t 4-001a: creating new instance
[ 4009.546177] r820t 4-001a: Rafael Micro r820t successfully identified
[ 4009.552681] Registered IR keymap rc-empty
[ 4009.552783] input: Realtek RTL2832U reference design as /devices/pci0000:00/0000:00:1d.7/usb7/7-5/rc/rc1/input20
[ 4009.552854] rc1: Realtek RTL2832U reference design as /devices/pci0000:00/0000:00:1d.7/usb7/7-5/rc/rc1
[ 4009.553275] input: MCE IR Keyboard/Mouse (dvb_usb_rtl28xxu) as /devices/virtual/input/input21
[ 4009.554466] rc rc1: lirc_dev: driver ir-lirc-codec (dvb_usb_rtl28xxu) registered at minor = 0
[ 4009.554474] usb 7-5: dvb_usb_v2: schedule remote query interval to 400 msecs
[ 4009.565930] usb 7-5: dvb_usb_v2: 'Realtek RTL2832U reference design' successfully initialized and connected

```

**Note:** in this case we see that the dongle has a R820T tuner, but there are several other popular tuners that you might run into. Also note the IR sensor device that was recognized that, properly configured, can be used with the device remote control. See [LIRC](/index.php/LIRC "LIRC") for more information.

Additionally, you should now see the adapter device under `/dev/dvb/adapter0`. Some cards need additional firmwares that are not distributed for various reasons. Usually you will find an explicit message about that in dmesg. Look for the name of the file(s) you see with your favorite search engine, and once you have them, put the required firmware(s) in /usr/lib/firmware. Possibly a package might exist in the AUR.

## Utilities

Various DVB utilities can be found in the [linuxtv-dvb-apps](https://aur.archlinux.org/packages/linuxtv-dvb-apps/) package.

### Scanning

[w_scan](https://aur.archlinux.org/packages/w_scan/) allows for automatic scanning of channels without configuration. Install it then issue:

```
# w_scan -ft -c [country_code] > ~/channels.conf

```

If you do not know your country code, enter the following to get a list of codes.

```
# w_scan -c "?"

```

Note that country code is optional is some cases (see [w_scan(1)](http://dev.man-online.org/man2/w_scan/) for details). More advanced scanning options can be found under [DVB-S#Scanning channels](/index.php/DVB-S#Scanning_channels "DVB-S"). See also *w_scan'*s [w_scan(1)](http://dev.man-online.org/man2/w_scan/) and [wscan's documentation on LinuxTVWiki](http://linuxtv.org/wiki/index.php/W_scan).

When `w_scan` fails to find all expected channels you could try `w_scan2`. It is a fork of the original *w_scan* and can be found on [GitHub](https://github.com/stefantalpalaru/w_scan2).

## Clients

See also [how to disable screensaver when playing video/TV](/index.php/XScreenSaver "XScreenSaver") by using configuration files or use `xset` command before and after player starts to enable/disable it. If you have installed [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver) then you will need to use `xscreensaver-command` instead of `xset` to activate/deactivate screensaver from command line.

### Kaffeine

DVB-T works out-of-the box in [Kaffeine](/index.php/Kaffeine "Kaffeine"), including management of multpile DVB-T devices, channel tuning, channel selection, EPG and recording. No external playlist generation is needed. Multiple DVB-T devices can be used at once (e.g. for recording from a multiplex while watching another one). Many single-tuner DVB-T devices can even provice two different TV channels, as long as they share the same multiplex; this feature is also readily available in Kaffeine.

### VLC

The simplest way to watch DVB-T channels with [VLC](/index.php/VLC "VLC") is to first generate a playlist:

```
$ w_scan -ft -c [country_code] -L > dvb.xspf
$ vlc dvb.xspf

```

You can also specify the frequency and programs by hand. This can be done using:

```
$ vlc dvb://frequency=543000000

```

where the frequency is set in Hz, and should match the base frequency for the transmissions in your area. You can also explicitly specify which demodulation you would like to use, so instead of `dvb` you can use `dvb-t`, `dvb-t2`, etc.

VLC also accepts various command line arguments, for example if you want to tune into a different program:

```
$ vlc dvb://frequency=543000000 :program=3

```

### MPlayer / mpv

For DVB streaming, [MPlayer](/index.php/MPlayer "MPlayer") (or [mpv](/index.php/Mpv "Mpv")) requires a channels configuration file at `~/.mplayer/channels.conf`. Follow [#Scanning](#Scanning) for instructions on how to generate it, but make sure to use the `-M` flag to generate the proper format for MPlayer, if you are using `w_scan`:

```
$ w_scan -ft -c [country_code] -M > ~/.mplayer/channels.conf

```

For *mpv*, use:

```
$ w_scan -ft -c [country_code] -M > ~/.config/mpv/channels.conf

```

Try the configuration with `mplayer dvb://`, which should start to play the first channel. If it does not, you might need to use `-demuxer lavf` or `-demuxer mpegts` in order to properly receive the stream.

If the configuration works, you can simply run:

```
$ mplayer dvb://"STREAM NAME"

```

with a valid `STREAM NAME` from the channels configuration file.

**Note:** MPlayer cannot handle and play channels from a command line that contains some of Linux special symbols like `/` in their names, but you can manually rename them by editing `~/.mplayer/channels.conf`.

#### Channel selector

Here is a [lstv](https://aur.archlinux.org/packages/lstv/) script that will show a numbered list of channels by reading data from a `~/.mplayer/channels.conf` file. You will be able to watch a channel by using a number associated to it by the script instead of having to type the whole channel name on the command line, e.g. `lstv 3`. The channel number associated by the script equals to the line number with tuning configuration for it. The script disables display power saving and a screen saver before starting *mplayer* and enables both again after you close it to disable screensaver management in this script remove `xset ...;` before and after [MPlayer](/index.php/MPlayer "MPlayer").

 `/usr/local/bin/lstv` 
```
#!/bin/bash
if [ "$1" ];then
CC='^[0-9]+$';
  if ! [[ "$@" =~ $CC ]];then echo Is not a channel number!;
   else
##
    awk -F':' -v AA="$1" '//{ZZ++;
     if(AA == ZZ)system("xset -dpms s off;mplayer dvb://""\""$1"\";xset +dpms s on")}
     END{if(AA > ZZ)printf "The highest channel number is: "ZZ"
"}' "$HOME/.mplayer/channels.conf"
##
  fi;
else
awk -F':' '// { ZZ++; printf  ZZ " | " $1 "
"}' "$HOME/.mplayer/channels.conf"
fi;

```

**Note:**

*   It is assumed that the `channels.conf` file has been created with: `w_scan -ft -c *country_code* -C UTF-8 -M -E 0 -O 0 > ~/.mplayer/channels.conf`
*   If the list of channels is too long then you can use something like `lstv | less` and search for channels name by pressing `/` and writing its name. When found press `q` for exiting of [less](http://unixhelp.ed.ac.uk/CGI/man-cgi?less) and use the channel associated number with [lstv](https://aur.archlinux.org/packages/lstv/).
*   If you have a problem with playing of video see [Arch Linux Forum](https://bbs.archlinux.org/viewtopic.php?id=57650).

**Warning:** If there is more than one channel with the same name, *mplayer* will play only the closest one in the list.

### ffmpeg

[FFmpeg](/index.php/FFmpeg "FFmpeg") can take DVB-T MPEG streams as input, but requires `tzap` to do so.

**Note:** This might not necessarily be the case, if a better method is known, please update.

First, generate a tzap-compatible `channels.conf` file, using `w_scan`:

```
$ w_scan -ft -A1 -X > ~/.tzap/channels.conf

```

Then, you can run:

```
$ tzap -r "CHANNEL NAME"

```

which, if setup correctly should yield an output similar to:

```
using '/dev/dvb/adapter0/frontend0' and '/dev/dvb/adapter0/demux0'
reading channels from file '/home/user/.tzap/channels.conf'
Version: 5.10  	 FE_CAN { DVB-T }
tuning to 506000000 Hz
video pid 0x0a21, audio pid 0x0a22
status 00 | signal 0000 | snr 0000 | ber 0000ffff | unc 00007fbd | 
status 1f | signal 0000 | snr 0126 | ber 00000000 | unc 00007fbd | FE_HAS_LOCK
status 1f | signal 0000 | snr 0129 | ber 0000000f | unc 00007fbd | FE_HAS_LOCK
status 1f | signal 0000 | snr 0120 | ber 00000003 | unc 00007fbd | FE_HAS_LOCK
status 1f | signal 0000 | snr 0125 | ber 00000011 | unc 00007fbd | FE_HAS_LOCK
# ....

```

More information on `tzap` is available on the [zap wiki page](http://www.linuxtv.org/wiki/index.php/Zap).

Once `tzap` is encoding the stream, `/dev/dvb/adapter0/dvr0` should be available to `ffmpeg` (or any other program).

A simple command to stream a program, without addditional encoding might look like so:

```
$ ffmpeg -f mpegts -i /dev/dvb/adapter0/dvr0 out.mp4

```

(Note: the above command will not generate output if the card requires to setup the frontend and/or the demuxer).

### dvbjet

DVB cards receive several simultaneous programs multiplexed. The command-line [dvbjet](https://github.com/lightful/DVBdirect/) standalone tool (has no dependencies) tunes the TV card by selecting the frequency, as with a radio, and saves the *full MPEG-TS stream*. To play or extract a separate program from it (with all its audio, video and subtitle tracks) its companion python script lists the programs and invokes ffmpeg.

## Troubleshooting

If you bump into problems, try these tools to help debug:

*   [dvbsnoop](https://aur.archlinux.org/packages/dvbsnoop/) is an advanced tool that can show all the necessary data regarding the bandwidth, signal, frontend, etc.
*   `femon -H` shows signal statistics