# Hauppauge Nova-T Stick

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

The Hauppauge Nova-T Stick is an USB2.0 DVB-T tuner with an additional antenna port.

## Contents

*   [1 Features](#Features)
*   [2 Installation](#Installation)
*   [3 Configuration](#Configuration)
    *   [3.1 User permissions](#User_permissions)
    *   [3.2 Getting channels](#Getting_channels)
    *   [3.3 Watch TV](#Watch_TV)
*   [4 External Links](#External_Links)

# Features

*   Microtune MT2060 tuner
*   Dibcom DVB-T demodulator
*   USB 2.0 controller
*   Remote control

# Installation

Since kernel 2.6.19 nearly all Nova-T sticks are recognized correctly. So if you just plug in your Nova-T Stick and run _dmesg_ you should see something like this:

```
usb 2-3: new high speed USB device using ehci_hcd and address 5
usb 2-3: configuration #1 chosen from 1 choice
dvb-usb: found a 'Hauppauge Nova-T Stick' in cold state, will try to load a firmware
dvb-usb: did not find the firmware file. (dvb-usb-dib0700-01.fw) Please see linux/Documentation/dvb/ for more details on firmware-problems. (-2)

```

As you see the stick has been recognized but it's not working yet because the firmware was missing. Download the [dvb-usb-dib0700-03-pre1.fw firmware file](http://www.wi-bw.tfh-wildau.de/~pboettch/home/linux-dvb-firmware/dvb-usb-dib0700-03-pre1.fw) and copy it to _/lib/firmware_.

Depending on your box number (e.g 293) or device no. (e.g 70009) the kernel may require the firmware version to be _dvb-usb-dib0700-01.fw_. So either you just rename the firmware linked above or put a link. That's up to you. Both seem to work fine.

If this is done just plug in the usb stick again and see what happens. The output of _dmesg_ is supposed to look like that.

```
usb 2-3: new high speed USB device using ehci_hcd and address 7
usb 2-3: configuration #1 chosen from 1 choice
dvb-usb: found a 'Hauppauge Nova-T Stick' in cold state, will try to load a firmware
dvb-usb: downloading firmware from file 'dvb-usb-dib0700-01.fw'
dib0700: firmware started successfully.
dvb-usb: found a 'Hauppauge Nova-T Stick' in warm state.
dvb-usb: will pass the complete MPEG2 transport stream to the software demuxer.
DVB: registering new adapter (Hauppauge Nova-T Stick).
DVB: registering frontend 0 (DiBcom 7000PC)...
MT2060: successfully identified (IF1 = 1220)
dvb-usb: Hauppauge Nova-T Stick successfully initialized and connected.

```

Perfect! Our usb stick is now ready to do its service.

# Configuration

## User permissions

In order to have access to our usb stick as a normal user you'll have to add you to the _video_ group. Run this command as root:

```
gpasswd -a USER video

```

Replace USER with the name of the user which you want to grant access. Afterwards either reboot or relogin.

## Getting channels

Now that we have setup our usb stick and it's working fine, let's scan for channels. Therefore I recommend the linuxtv-dvb-apps package which you can find in the community repository.

```
pacman -S linuxtv-dvb-apps

```

Also we need a so called _initial scan file_. This file is needed for _scan_ to work properly. It provides a frequency that _scan_ is going to use as a starting point from which it'll proceed with its scan. These files are specific to your geographic location and have the form of cc-Ttttt, where cc is a two-letter country abbreviation, and Ttttt is the name of the location of the transmitter. You'll find a lot of scan files in the official [dvb-apps repository](http://linuxtv.org/hg/dvb-apps/file/4bca5d49c9bd/util/scan/dvb-t/).

If you can't find a suitable initial scan file then you can build your own with [w_scan](http://free.pages.at/wirbel4vdr/w_scan/index2.html) ([AUR](https://aur.archlinux.org/packages.php?do_Details=1&ID=12028)).

```
 w_scan -x > cc-Ttttt

```

So for example in Leipzig, Germany, you'd look for a file called de-Leipzig.

```
scan de-Leipzig > leipzig.conf

```

After a few seconds the scan has finished and all found channels have been written into our _leipzig.conf_.

## Watch TV

Now there are a lot of ways to watch TV, for example with [Kaffeine](http://kaffeine.sourceforge.net/), xine, mplayer, [VLC](http://www.videolan.org/vlc) and so on. Also some of these programs provide EPG, Time shafting and things like that.

A fast way is to just open your _leipzig.conf_ with VLC and enjoy watching!

# External Links

*   [Official LinuxTV site](http://linuxtv.org/)
*   [Hauppauge Germany product page](http://www.hauppauge.de/pages/products/data_novatstick.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Hauppauge_Nova-T_Stick&oldid=389739](https://wiki.archlinux.org/index.php?title=Hauppauge_Nova-T_Stick&oldid=389739)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [TV cards](/index.php/Category:TV_cards "Category:TV cards")