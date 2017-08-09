Deze pagina behandelt het decoderen van digitenne (DVB-T) in Nederland.

## Contents

*   [1 Omgeving](#Omgeving)
    *   [1.1 Je hebt kernel <= 2.6.36 of kernel>=2.6.38 nodig](#Je_hebt_kernel_.3C.3D_2.6.36_of_kernel.3E.3D2.6.38_nodig)
*   [2 Gebruikte hardware](#Gebruikte_hardware)
*   [3 DVB-T ontvanger testen](#DVB-T_ontvanger_testen)
    *   [3.1 Controle device nodes](#Controle_device_nodes)
    *   [3.2 DVB-T ontvanger testen met vlc](#DVB-T_ontvanger_testen_met_vlc)
    *   [3.3 DVB-T ontvanger testen met tzap en mplayer](#DVB-T_ontvanger_testen_met_tzap_en_mplayer)
*   [4 Cardreader](#Cardreader)
    *   [4.1 Insteken cardreader](#Insteken_cardreader)
    *   [4.2 Installeer oscam via aur](#Installeer_oscam_via_aur)
    *   [4.3 Oscam configuratie](#Oscam_configuratie)
        *   [4.3.1 /etc/oscam/oscam.conf](#.2Fetc.2Foscam.2Foscam.conf)
        *   [4.3.2 /etc/oscam/oscam.server](#.2Fetc.2Foscam.2Foscam.server)
        *   [4.3.3 /etc/oscam/oscam.services](#.2Fetc.2Foscam.2Foscam.services)
        *   [4.3.4 /etc/oscam/oscam.user](#.2Fetc.2Foscam.2Foscam.user)
    *   [4.4 Oscam starten](#Oscam_starten)
*   [5 Softcam (sasc-ng)](#Softcam_.28sasc-ng.29)
    *   [5.1 sasc-ng installeren via aur](#sasc-ng_installeren_via_aur)
    *   [5.2 Sasc-ng configureren](#Sasc-ng_configureren)
        *   [5.2.1 /etc/conf.d/sasc-ng](#.2Fetc.2Fconf.d.2Fsasc-ng)
        *   [5.2.2 /etc/camdir/cardclient.conf](#.2Fetc.2Fcamdir.2Fcardclient.conf)
        *   [5.2.3 /etc/rc.d/sasc-ng](#.2Fetc.2Frc.d.2Fsasc-ng)
    *   [5.3 Sasc-ng starten](#Sasc-ng_starten)
    *   [5.4 Softcam testen met tzap en mplayer](#Softcam_testen_met_tzap_en_mplayer)
*   [6 Integratie met mythtv](#Integratie_met_mythtv)
    *   [6.1 Mythtv-setup](#Mythtv-setup)
        *   [6.1.1 1\. Algemeen](#1._Algemeen)
        *   [6.1.2 2\. TV kaarten](#2._TV_kaarten)
        *   [6.1.3 3\. Videobronnen](#3._Videobronnen)
        *   [6.1.4 4\. Ingang verbindingen](#4._Ingang_verbindingen)
        *   [6.1.5 5\. Kanaal bewerker](#5._Kanaal_bewerker)
        *   [6.1.6 6\. Opslagmappen](#6._Opslagmappen)
        *   [6.1.7 7\. System events](#7._System_events)
    *   [6.2 Starten mythtv](#Starten_mythtv)
*   [7 Referenties](#Referenties)

## Omgeving

#### Je hebt kernel <= 2.6.36 of kernel>=2.6.38 nodig

**Note:** core/kernel26 is nieuw genoeg (zowel i686 als x86_64). Gewoon pacman -Syu draaien en herstarten.

Met kernel 2.6.37 zal sasc-ng vastlopen ,met de volgende meldingen in dmesg:

```
INFO: task sasc-ng:4563 blocked for more than 120 seconds.
"echo 0 > /proc/sys/kernel/hung_task_timeout_secs" disables this message.
sasc-ng D f0adbdac 0 4563 1 0x00000000
f0adbdbc 00000082 00000002 f0adbdac 00000213 4ee701f2 0004a040 00000000
00000000 f6006340 f0adbd34 c100a208 f0adbd88 c1068173 d03da3f7 c14b6340
f0f97810 c14b6340 c14b6340 f0f979d4 c14b6340 c14b6340 f6206340 f0f97810
Call Trace:
[<c100a208>] ? sched_clock+0x8/0x10
[<c1068173>] ? sched_clock_local+0xd3/0x1c0
[<c103dca2>] ? enqueue_entity+0x102/0x170
[<c131439d>] __mutex_lock_slowpath+0x10d/0x2b0
[<c131454b>] mutex_lock+0xb/0x20
[<fa348119>] dvb_device_open+0x19/0x290 [dvb_core]
[<c110717f>] chrdev_open+0x13f/0x240
[<c1101979>] __dentry_open+0xe9/0x310
[<c1102b2e>] nameidata_to_filp+0x5e/0x70
[<c1107040>] ? chrdev_open+0x0/0x240
[<c110f5df>] do_last+0x3ff/0x630
[<c110f9e4>] do_filp_open+0x1d4/0x510
[<c1102b95>] do_sys_open+0x55/0xf0
[<f80bca30>] ? dvblb_read+0x0/0x340 [dvbloopback]
[<c1102c59>] sys_open+0x29/0x40
[<c100391f>] sysenter_do_call+0x12/0x28
INFO: task sasc-ng:4563 blocked for more than 120 seconds.
"echo 0 > /proc/sys/kernel/hung_task_timeout_secs" disables this message.
sasc-ng D f0adbdac 0 4563 1 0x00000000
f0adbdbc 00000082 00000002 f0adbdac 00000213 4ee701f2 0004a040 00000000
00000000 f6006340 f0adbd34 c100a208 f0adbd88 c1068173 d03da3f7 c14b6340
f0f97810 c14b6340 c14b6340 f0f979d4 c14b6340 c14b6340 f6206340 f0f97810
Call Trace:
[<c100a208>] ? sched_clock+0x8/0x10
[<c1068173>] ? sched_clock_local+0xd3/0x1c0
[<c103dca2>] ? enqueue_entity+0x102/0x170
[<c131439d>] __mutex_lock_slowpath+0x10d/0x2b0
[<c131454b>] mutex_lock+0xb/0x20
[<fa348119>] dvb_device_open+0x19/0x290 [dvb_core]
[<c110717f>] chrdev_open+0x13f/0x240
[<c1101979>] __dentry_open+0xe9/0x310
[<c1102b2e>] nameidata_to_filp+0x5e/0x70
[<c1107040>] ? chrdev_open+0x0/0x240
[<c110f5df>] do_last+0x3ff/0x630
[<c110f9e4>] do_filp_open+0x1d4/0x510
[<c1102b95>] do_sys_open+0x55/0xf0
[<f80bca30>] ? dvblb_read+0x0/0x340 [dvbloopback]
[<c1102c59>] sys_open+0x29/0x40
[<c100391f>] sysenter_do_call+0x12/0x28

```

## Gebruikte hardware

Ik gebruik de volgende hardware:

*   PCTV NanoStick 73e SE (solo) [http://linuxtv.org/wiki/index.php/Pinnacle_PCTV_nano_Stick_%2873e%29](http://linuxtv.org/wiki/index.php/Pinnacle_PCTV_nano_Stick_%2873e%29)
*   smargo smartreader + [https://www.cardwriter.nl/nl/pd1184675949.htm](https://www.cardwriter.nl/nl/pd1184675949.htm)
*   Digitenne smartcard

## DVB-T ontvanger testen

### Controle device nodes

Kijk eerst of er een DVB ontvanger aanwezig is. Onder /dev hoort de map dvb aanwezig te zijn:

```
$ ls -l /dev/dvb/adapter0/*
crw-rw---- 1 root video 212, 4 May 15 10:21 /dev/dvb/adapter0/demux0
crw-rw---- 1 root video 212, 5 May 15 10:21 /dev/dvb/adapter0/dvr0
crw-rw---- 1 root video 212, 3 May 15 10:21 /dev/dvb/adapter0/frontend0
crw-rw---- 1 root video 212, 7 May 15 10:21 /dev/dvb/adapter0/net0

```

### DVB-T ontvanger testen met vlc

Gebruik nu vlc om de ontvanger te testen:

```
# pacman -S vlc

```

```
$vlc
Media -> Open Capture device,
Capture mode : DVB
Adapter card to tune: /dev/dvb/adapter0
DVB type: DVB-T
Transponder / multiplex frequency: 722000
Bandwidth: auto => play

```

Nu zal vlc alle kanalen scannnen, en na ongeveer 10 minuten het eerste beeld en/of geluid geven.

Als de permisies van /dev/dvb/adapter0 verkeerd staan zal vlc de volgende melding geven:

```
dvb access error: FrontEndOpen: opening device failed (Permission denied)
main input error: open of `dvb://frequency=0000' failed: (null)

```

Voeg dan jezelf toe aan de groep "video":

```
# usermod -a -G video yourusername

```

### DVB-T ontvanger testen met tzap en mplayer

Installeer mplayer en tzap (onderdeel van linuxtv-dvb-apps)

```
# pacman -S linuxtv-dvb-apps mplayer

```

Scan nu naar de digitenne kanalen in nederland:

```
$ mkdir ~/.tzap
$ scan /usr/share/dvb/dvb-t/nl-All -o zap | tee ~/.tzap/channels.conf
scanning /usr/share/dvb/dvb-t/nl-All
using '/dev/dvb/adapter0/frontend0' and '/dev/dvb/adapter0/demux0'
initial transponder 474000000 0 1 9 3 1 3 0
initial transponder 474000000 0 2 9 3 1 3 0
>>> tune to: 474000000:INVERSION_AUTO:BANDWIDTH_8_MHZ:FEC_1_2:FEC_AUTO:QAM_64:TRANSMISSION_MODE_8K:GUARD_INTERVAL_1_4:HIERARCHY_NONE
0x0000 0x044d: pmt_pid 0x1b62 Digitenne -- Nederland 1 (running)
0x0000 0x044e: pmt_pid 0x1b6c Digitenne -- Nederland 2 (running)
0x0000 0x044f: pmt_pid 0x1b76 Digitenne -- Nederland 3 (running)
0x0000 0x0450: pmt_pid 0x1b80 Digitenne -- TV Rijnmond (running)
0x0000 0x0457: pmt_pid 0x1bc6 Digitenne -- Radio Rijnmond (running)
0x0000 0x0458: pmt_pid 0x1bd0 Digitenne -- Radio 1 (running)
0x0000 0x0459: pmt_pid 0x1bda Digitenne -- Radio 2 (running)
0x0000 0x045a: pmt_pid 0x1be4 Digitenne -- 3FM (running)
0x0000 0x045b: pmt_pid 0x1bee Digitenne -- Radio 4 (running)
0x0000 0x045c: pmt_pid 0x1bf8 Digitenne -- Radio 5 (running)
0x0000 0x045d: pmt_pid 0x1c02 Digitenne -- Radio 6 (running)
0x0000 0x045f: pmt_pid 0x1c16 Digitenne -- FunX (running)
Network Name 'Digitenne'
>>> tune to: 482000000:INVERSION_AUTO:BANDWIDTH_8_MHZ:FEC_1_2:FEC_AUTO:QAM_64:TRANSMISSION_MODE_8K:GUARD_INTERVAL_1_4:HIERARCHY_NONE
WARNING: >>> tuning failed!!!
...

```

Dit levert het bestand ~/.tzap/channels.conf op. Hierin is te zien dat Nederland 1,2 en 3 op 474 MHz zitten, en dat Discovery channel op 498MHz zit. De frekwenties zijn afhankelijk van uw locatie.

```
Nederland 1:474000000:INVERSION_AUTO:BANDWIDTH_8_MHZ:FEC_1_2:FEC_1_2:QAM_64:TRANSMISSION_MODE_8K:GUARD_INTERVAL_1_4:HIERARCHY_NONE:7011:7012:1101
Nederland 2:474000000:INVERSION_AUTO:BANDWIDTH_8_MHZ:FEC_1_2:FEC_1_2:QAM_64:TRANSMISSION_MODE_8K:GUARD_INTERVAL_1_4:HIERARCHY_NONE:7021:7022:1102
Nederland 3:474000000:INVERSION_AUTO:BANDWIDTH_8_MHZ:FEC_1_2:FEC_1_2:QAM_64:TRANSMISSION_MODE_8K:GUARD_INTERVAL_1_4:HIERARCHY_NONE:7031:7032:1103
...
Nickelodeon:498000000:INVERSION_AUTO:BANDWIDTH_8_MHZ:FEC_2_3:FEC_AUTO:QAM_64:TRANSMISSION_MODE_8K:GUARD_INTERVAL_1_4:HIERARCHY_NONE:3051:3052:35
Discovery Channel:498000000:INVERSION_AUTO:BANDWIDTH_8_MHZ:FEC_2_3:FEC_AUTO:QAM_64:TRANSMISSION_MODE_8K:GUARD_INTERVAL_1_4:HIERARCHY_NONE:3061:3062:36
Eurosport 1:498000000:INVERSION_AUTO:BANDWIDTH_8_MHZ:FEC_2_3:FEC_AUTO:QAM_64:TRANSMISSION_MODE_8K:GUARD_INTERVAL_1_4:HIERARCHY_NONE:3071:3072:37

```

Nu kan de tuner afgestemd worden op bijvoorbeeld Nederland 1

```
$ tzap -a 0 -r 'Nederland 1'
using '/dev/dvb/adapter0/frontend0' and '/dev/dvb/adapter0/demux0'
reading channels from file '/home/cedric/.tzap/channels.conf'
tuning to 474000000 Hz
video pid 0x1b63, audio pid 0x1b64
status 1b | signal 0dbd | snr 0062 | ber 001fffff | unc 00000000 | FE_HAS_LOCK
status 1b | signal 0d83 | snr 0063 | ber 00000000 | unc 00001e81 | FE_HAS_LOCK
status 1b | signal 0d17 | snr 0069 | ber 00000000 | unc 00001ef6 | FE_HAS_LOCK

```

Gebruik een andere terminal om mplayer te starten. Nu moet na enkele seconden Nederland 1 op het scherm verschijnen.

```
$ mplayer /dev/dvb/adapter0/dvr0 
MPlayer SVN-r33159-4.5.2 (C) 2000-2011 MPlayer Team
162 audio & 359 video codecs
mplayer: could not connect to socket
mplayer: No such file or directory
Failed to open LIRC support. You will not be able to use your remote control.

Playing /dev/dvb/adapter0/dvr0.
TS file format detected.
VIDEO MPEG2(pid=7021) AUDIO MPA(pid=7022) NO SUBS (yet)!  PROGRAM N. 0
VIDEO:  MPEG2  704x576  (aspect 3)  25.000 fps  15000.0 kbps (1875.0 kbyte/s)
Load subtitles in /dev/dvb/adapter0/
==========================================================================
Opening video decoder: [ffmpeg] FFmpeg's libavcodec codec family
Selected video codec: [ffmpeg2] vfm: ffmpeg (FFmpeg MPEG-2)
==========================================================================
==========================================================================
Opening audio decoder: [mp3lib] MPEG layer-2, layer-3
AUDIO: 48000 Hz, 2 ch, s16le, 160.0 kbit/10.42% (ratio: 20000->192000)
Selected audio codec: [mp3] afm: mp3lib (mp3lib MPEG layer-2, layer-3)
==========================================================================
AO: [oss] 48000Hz 2ch s16le (2 bytes per sample)
Starting playback...
Unsupported PixelFormat 61
Unsupported PixelFormat 53
Movie-Aspect is 1.78:1 - prescaling to correct movie aspect.
VO: [vdpau] 704x576 => 1024x576 Planar YV12 
A:22383.9 V:22383.9 A-V:  0.052 ct: -0.257 569/569  4%  3% 24.6% 3 0

```

## Cardreader

### Insteken cardreader

Nadat de Smargo smartreader + in de PC wordt gestoken zal dmesg laten zien dat er een nieuwe seriële poort (ttyUSB0) is toegevoegd:

```
$ dmesg
[18014.724903] usb 2-1: new full speed USB device using uhci_hcd and address 4
[18014.887673] ftdi_sio 2-1:1.0: FTDI USB Serial Device converter detected
[18014.887788] usb 2-1: Detected FT232BM
[18014.887794] usb 2-1: Number of endpoints 2
[18014.887799] usb 2-1: Endpoint 1 MaxPacketSize 64
[18014.887804] usb 2-1: Endpoint 2 MaxPacketSize 64
[18014.887808] usb 2-1: Setting MaxPacketSize 64
[18014.889396] ftdi_sio ttyUSB0: Unable to read latency timer: -32
[18014.890893] usb 2-1: FTDI USB Serial Device converter now attached to ttyUSB0

```

### Installeer oscam via aur

[https://aur.archlinux.org/packages.php?ID=45646](https://aur.archlinux.org/packages.php?ID=45646)

```
$ wget [https://aur.archlinux.org/packages/oscam/oscam.tar.gz](https://aur.archlinux.org/packages/oscam/oscam.tar.gz)
$ tar -xf oscam.tar.gz 
$ cd oscam
$ makepkg
# pacman -U oscam-1.00-1-i686.pkg.tar.xz

```

### Oscam configuratie

Oscam gebruikt de volgende configuratiebestanden:

#### /etc/oscam/oscam.conf

```
# main configuration
[global]
nice	      = -1
WaitForCards  = 1

# logging
pidfile	      = /var/run/oscam.pid
logfile	      = /var/log/oscam/oscam.log
usrfile	      = /var/log/oscam/oscamuser.log
cwlogdir      = /var/log/oscam/cw

# monitor
[monitor]
port	      = 8988
aulow	      = 120
monlevel      = 1

# web interface
[webif]
httpport       = 8888
httpuser       = myusername
httppwd        = mypassword
httpallowed    = 192.168.31.201

# protocols

[newcamd]
key            = 000102030405060708090A0B0C0D
port           = 15050@0B00:0E030

```

#### /etc/oscam/oscam.server

```
# reader configuration

[reader]
label    = reader1
protocol = mouse
detect   = CD
device   = /dev/ttyUSB0
group    = 1
emmcache = 1,3,2
services = services1
caid     = 0B00
mhz      = 500
cardmhz  = 500

```

#### /etc/oscam/oscam.services

```
# definition of services 
#
# format:
# [name]
# caid=CAID[,CAID]...
# provid = provider ID[,provider ID]...
# srvid = service ID[,service ID]...

[services1]
caid=0B00
provid=0E030
srvid=

```

#### /etc/oscam/oscam.user

```
# user configuration

[account]
user       = user1
pwd        = password1
monlevel   = 0
uniq       = 0
group      = 1
au         = 1
ident 	   = 0B00:0E030
caid       = 0B00

# user for group 2 with monitor access, AU enabled

#[account]
user       = user2
pwd        = password2
monlevel   = 0
uniq       = 0
group      = 1
au         = 1
ident 	   = 0B00:0E030
caid       = 0B00

```

Maak de directory aan waar oscam zijn logbestanden kwijt kan

```
# mkdir /var/log/oscam

```

### Oscam starten

```
# /etc/rc.d/oscam start

```

Dit levert de volgende meldingen op in /var/log/oscam.log

```
-------------------------------------------------------------------------------
>> OSCam <<  cardserver started at Thu May 19 19:08:47 2011
-------------------------------------------------------------------------------
2011/05/19 19:08:47   1556 s   version=0.99.4svn, build #3146, system=i686-pc-linux, nice=-1
2011/05/19 19:08:47   1556 s   max. clients=509, client max. idle=120 sec
2011/05/19 19:08:47   1556 s   max. logsize=unlimited
2011/05/19 19:08:47   1556 s   client timeout=5000 ms, fallback timeout=2500 ms, cache delay=0 ms
2011/05/19 19:08:47   1556 s   shared memory initialized (size=4340618, id=229378)
2011/05/19 19:08:47   1556 s   auth size=4772
2011/05/19 19:08:47   1556 s   services reloaded: 0 services freed, 1 services loaded
2011/05/19 19:08:47   1556 s   userdb reloaded: 0 accounts freed, 1 accounts loaded, 0 expired, 0 disabled
2011/05/19 19:08:47   1556 s   signal handling initialized (type=sysv)
2011/05/19 19:08:47   1556 s   can't open file "/etc/oscam/oscam.srvid" (err=2), no service-id's loaded
2011/05/19 19:08:47   1556 s   can't open file "/etc/oscam/oscam.tiers" (err=2), no tier-id's loaded
2011/05/19 19:08:47   1556 s   can't open file "/etc/oscam/oscam.provid" (err=2), no provids's loaded
2011/05/19 19:08:47   1557 s   monitor: initialized (fd=7, port=8988)
2011/05/19 19:08:47   1557 s   camd 3.3x: disabled
2011/05/19 19:08:47   1557 s   camd 3.5x: disabled
2011/05/19 19:08:47   1557 s   cs378x: disabled
2011/05/19 19:08:47   1557 s   newcamd: initialized (fd=8, port=15050, crypted)
2011/05/19 19:08:47   1557 s   CAID: 0B00
2011/05/19 19:08:47   1557 s   provid #0: 00E030
2011/05/19 19:08:47   1557 s   cccam: disabled
2011/05/19 19:08:47   1557 s   radegast: disabled
2011/05/19 19:08:47   1557 s   logger started (pid=1558)
2011/05/19 19:08:47   1557 s   http started (pid=1559)
2011/05/19 19:08:47   1559 h   HTTP Server listening on port 8888
2011/05/19 19:08:47   1557 s   reader started (pid=1560, device=/dev/ttyUSB0, detect=cd, mhz=500, cardmhz=500)
2011/05/19 19:08:47   1557 s   waiting for local card init
2011/05/19 19:08:51   1557 s   init for all local cards done
2011/05/19 19:08:51   1557 s   anti cascading disabled
2011/05/19 19:08:51   1557 s   dvbapi: dvbapi disabled

```

Steek nu de digitenne kaart in de cardreader. Dit levert de volgende meldingen op in /var/log/oscam/oscam.log:

```
2011/05/19 19:13:25   1560 r02 card detected
2011/05/19 19:13:29   1560 r02 ATR: 3B 24 00 30 42 30 30 
2011/05/19 19:13:30   1560 r02 Maximum frequency for this card is formally 5 Mhz, clocking it to 5.00 Mhz
2011/05/19 19:13:32   1560 r02 type: Conax, caid: 0B00, serial: 1428098758, hex serial: 551f0ec6, card: v64
2011/05/19 19:13:32   1560 r02 Providers: 1
2011/05/19 19:13:32   1560 r02 Provider: 1  Provider-Id: 000000
2011/05/19 19:13:32   1560 r02 Provider: 1  SharedAddress: 002A8F87
2011/05/19 19:13:32   1560 r02 Package: 1, id: 1010, date: 2011/03/01 - 2011/03/31, name: Digitenne
2011/05/19 19:13:32   1560 r02 [conax-reader] ready for requests

```

## Softcam (sasc-ng)

### sasc-ng installeren via aur

[https://aur.archlinux.org/packages.php?ID=48512](https://aur.archlinux.org/packages.php?ID=48512) [https://aur.archlinux.org/packages.php?ID=27885](https://aur.archlinux.org/packages.php?ID=27885)

```
# pacman -S mercurial
$ wget [https://aur.archlinux.org/packages/open-sasc-ng/open-sasc-ng.tar.gz](https://aur.archlinux.org/packages/open-sasc-ng/open-sasc-ng.tar.gz)
$ tar -xf open-sasc-ng.tar.gz
$ cd open-sasc-ng
$ makepkg
# pacman -U open-sasc-ng-560-4-i686.pkg.tar.xz

```

### Sasc-ng configureren

#### /etc/conf.d/sasc-ng

```
# Use -j <real>:<virtual> to link adapters

```

```
SASCNG_ARGS="-j 0:1"
DVBLOOPBACK_ARGS="num_adapters=1"
LOGDIR="/var/log/"
CAMDIR=/etc/camdir

```

#### /etc/camdir/cardclient.conf

```
# Comment lines can start with # or ;
#
# every client line starts with the client name, followed by some arguments:
# 'hostname' is the name of the server
# 'port'     is the port on the server
# 'emm'      is a flag to allow EMM transfers to the server
#            (0=disabled 1=enabled)
# 'caid'     (optional) caid on which this client should work
# 'mask'     (optional) mask for caid e.g. caid=1700 mask=FF00 would allow
#            anything between 1700 & 17FF.
#            Default is 1700 & FF00\. If only caid is given mask is FFFF.
#            You may give multiple caid/mask values comma separated
#            (e.g. 1702,1722,0d0c/ff00).
# 'username' is the login username
# 'password' is the login password
#
# newcamd client
# 'cfgkey' is the config key (28bytes)
newcamd:localhost:15050:1/0B00/FF00:user2:password2:000102030405060708090A0B0C0D

```

#### /etc/rc.d/sasc-ng

Als de ingebouwde logging gebruikt wordt, dan komt het op minder snelle systemen voor dat sasc-ng continue 100% CPU gebruikt, en alleen met killall -s 16 sasc-ng te stoppen is. Pas daarom /etc/rc.d/sasc-ng op de volgende manier aan:

```
 #!/bin/bash

 . /etc/rc.conf
 . /etc/rc.d/functions

 [ -f /etc/conf.d/sasc-ng ] && . /etc/conf.d/sasc-ng

 PID=$(pidof -o %PPID /usr/sbin/sasc-ng)

 case $1 in
 start)
         stat_busy "Loading dvbloopback kernel module"

         [[ -z $DVBLOOPBACK_ARGS ]] && stat_die 1

         modprobe dvbloopback $DVBLOOPBACK_ARGS
         sleep 1

         stat_done

         stat_busy "Starting SASC-NG daemon"

         [[ -z $SASCNG_ARGS ]] && stat_die 2
         [[ -z $CAMDIR ]] && stat_die 3
         [[ -z $LOGDIR ]] && stat_die 4

         #[[ -z $PID ]] && /usr/sbin/sasc-ng -D $SASCNG_ARGS --cam-dir=$CAMDIR -l $LOGDIR/sasc-ng.log
 	[[ -z $PID ]] && /usr/sbin/sasc-ng -D $SASCNG_ARGS --cam-dir=$CAMDIR >> $LOGDIR/sasc-ng.log 2>&1
         if [ $? -gt 0 ]; then
                 stat_die 5
         else
                 add_daemon sasc-ng
                 stat_done
         fi
         ;;
 stop)
         stat_busy "Stoping SASC-NG daemon"
         [[ ! -z $PID ]] && kill $PID &> /dev/null

         if [ $? -gt 0 ]; then
                 stat_die 6
         else
                 rm_daemon sasc-ng
                 stat_done
         fi

         stat_busy "Unloading dvbloopback kernel module"

         sleep 2
         modprobe -r dvbloopback

         stat_done
         ;;

 restart)
         $0 stop
         sleep 1
         $0 start
         ;;

 *)
         echo "usage: $0 {start|stop|restart}" >&2
         exit 1
 esac

```

### Sasc-ng starten

```
# /etc/rc.d/sasc-ng start

```

Meldingen in dmesg:

```
[ 8130.913490] /home/cedric/open-sasc-ng/src/sc-build/contrib/sasc-ng/dvbloopback/module/dvb_loopback.c: frontend loopback driver v0.0.1
[ 8130.913502] dvbloopback: registering 1 adapters
[ 8130.913627] DVB: registering new adapter (DVB-LOOPBACK)

```

Meldingen in /var/log/oscam.log

```
May 19 20:51:50.858 : Version: 0.0.2-61975953edd0+
May 19 20:51:50.995 CAM: initializing plugin: SoftCam (1.0.0pre-HG-61975953edd0+): A software emulated CAM
May 19 20:51:51.051 CAM(general.info): SC version 1.0.0pre-HG-61975953edd0+ initializing (VDR 1.6.0)
May 19 20:51:51.107 CAM: starting plugin:
May 19 20:51:51.164 CAM(general.info): SC version 1.0.0pre-HG-61975953edd0+ starting (VDR 1.6.0)
May 19 20:51:51.220 CAM(core.load): ** Plugin config:
May 19 20:51:51.276 CAM(core.load): ** Key updates (AU) are enabled (active CAIDs) (no prestart)
May 19 20:51:51.334 CAM(core.load): ** Local systems DON'T take priority over cached remote
May 19 20:51:51.383 CAM(core.load): ** Concurrent FF recordings are NOT allowed
May 19 20:51:51.439 CAM(core.load): ** Force transfermode with digital audio
May 19 20:51:51.496 CAM(core.load): ** ECM cache is set to enabled
May 19 20:51:51.552 CAM(core.load): ** ScCaps are 1 2 0 0 0 0 0 0 0 0
May 19 20:51:51.620 CAM(general.info): loading cardclient config from /etc/camdir/cardclient.conf
May 19 20:51:51.687 CAM(cardclient.newcamd): now using protocol version 525 (cdLen=8)
May 19 20:51:51.744 CAM(cardclient.core): hostname=localhost port=15050 emm=1 emmCaids 0b00/ff00
May 19 20:51:51.789 CAM(cardclient.core): Newcamd: username=user2 password=password2 key=000102030405060708090A0B0C0D
May 19 20:51:51.846 CAM(cardclient.core): client 'Newcamd' ready
May 19 20:51:51.945 CAM(core.net): connecting to localhost:15050/tcp (127.0.0.1)
May 19 20:51:52.204 CAM(cardclient.login): Newcamd: CaID=0b00 admin=1 srvUA=00000000551F0EC6 provider 00E030/0000000000000000000000/00000000002A8F87
May 19 20:51:52.376 CAM(general.error): failed open /etc/camdir/SoftCam.Key: No such file or directory
May 19 20:51:52.511 CAM(general.error): failed open /etc/camdir/smartcard.conf: No such file or directory
May 19 20:51:52.556 CAM(general.error): failed open /etc/camdir/cardslot.conf: No such file or directory
May 19 20:51:52.601 CAM(general.error): failed open /etc/camdir/override.conf: No such file or directory
May 19 20:51:52.647 CAM(general.error): no keys loaded for softcam!
May 19 20:51:52.692 CAM(core.load): ** registered systems:
May 19 20:51:52.737 CAM(core.load): ** Cardclient        (pri -15)
May 19 20:51:52.794 CAM(core.load): ** Conax             (pri -10)
May 19 20:51:52.850 CAM(core.load): ** ConstCW           (pri -20)
May 19 20:51:52.907 CAM(core.load): ** Cryptoworks       (pri -10)
May 19 20:51:52.963 CAM(core.load): ** Irdeto            (pri -10)
May 19 20:51:53.035 CAM(core.load): ** Irdeto2           (pri  -8)
May 19 20:51:53.080 CAM(core.load): ** Nagra             (pri -10)
May 19 20:51:53.126 CAM(core.load): ** Nagra2            (pri -10)
May 19 20:51:53.182 CAM(core.load): ** Fake-NDS          (pri -12)
May 19 20:51:53.239 CAM(core.load): ** SC-Conax          (pri  -5)
May 19 20:51:53.295 CAM(core.load): ** SC-Cryptoworks    (pri  -5)
May 19 20:51:53.352 CAM(core.load): ** SC-Irdeto         (pri  -5)
May 19 20:51:53.408 CAM(core.load): ** SC-Nagra          (pri  -5)
May 19 20:51:53.465 CAM(core.load): ** SC-Seca           (pri  -5)
May 19 20:51:53.521 CAM(core.load): ** SC-Viaccess       (pri  -5)
May 19 20:51:53.577 CAM(core.load): ** SC-VideoGuard2    (pri  -5)
May 19 20:51:53.623 CAM(core.load): ** Seca              (pri -10)
May 19 20:51:53.684 CAM(core.load): ** @SHL              (pri -10)
May 19 20:51:53.740 CAM(core.load): ** Viaccess          (pri -10)
May 19 20:51:54.817 frontend: Starting thread on /dev/dvb/adapter1/frontend1
The thread scheduling parameters indicate:
policy = 0
priority = 0
May 19 20:51:54.818 dvr: Starting thread on /dev/dvb/adapter1/dvr1
The thread scheduling parameters indicate:
policy = 1
priority = 99
May 19 20:51:54.818 demux: Starting thread on /dev/dvb/adapter1/demux1
The thread scheduling parameters indicate:
policy = 0
priority = 0
May 19 20:51:54.988 : Listening on port 5456
May 19 20:53:53.011 CAM(core.net): idle timeout, disconnected localhost:15050

```

Meldingen in /var/log/oscam/oscam.log:

```
2011/05/19 20:51:52   1557 s   client(1) connect from 127.0.0.1 (pid=7297, pipfd=14)
2011/05/19 20:51:52   7297 c01 encrypted newcamd:15050-client 127.0.0.1 granted (user2, au(auto)=reader1)
2011/05/19 20:51:52   7297 c01 user user2 authenticated successfully (generic)
2011/05/19 20:51:52   7297 c01 AU enabled for user user2 on reader reader1

```

### Softcam testen met tzap en mplayer

Geef de volgende opdrachten in 3 verschillende terminals:

```
$ tzap -a 1 -r 'Discovery Channel'
$ cat /dev/dvb/adapter1/dvr0 >test.ts
$ mplayer test.ts

```

Nu moet na enkele seconden discovery channel op het scherm verschijnen. Meldingen in /var/log/oscam/oscam.log:

```
2011/05/19 20:53:53   7297 c01 Connection closed to client
2011/05/19 20:53:53   7297 c01 user2 disconnected  from 127.0.0.1
2011/05/19 20:59:38   1557 s   client(1) connect from 127.0.0.1 (pid=7315, pipfd=14)
2011/05/19 20:59:38   7315 c01 encrypted newcamd:15050-client 127.0.0.1 granted (user2, au(auto)=reader1)
2011/05/19 20:59:38   7315 c01 user user2 authenticated successfully (generic)
2011/05/19 20:59:38   7315 c01 AU enabled for user user2 on reader reader1
2011/05/19 20:59:38   7315 c01 user2 (0B00&00E030/0024/47:4A33): found (290 ms) by reader1
2011/05/19 20:59:43   7315 c01 user2 (0B00&00E030/0024/47:FEE2): found (265 ms) by reader1

```

Meldingen in /var/log/sasc-ng.log:

```
May 19 20:59:37.396 CAM(core.ecm): 0.1: is no longer idle
May 19 20:59:37.453 MSG: Got unprocessed message type: 1
May 19 20:59:37.515 CAM(core.ecm): 0.1: triggered SID -1/36 idx -1/1 mode -1/0 -
May 19 20:59:37.611 CAM(core.ecm): 0.1: new caDescr: 09 04 0B 00 EB FD
May 19 20:59:37.656 CAM(core.ecm): 0.1: CA descriptors for SID 36 (len=6)
May 19 20:59:37.706 CAM(core.ecm): 0.1: descriptor 0b 00 eb fd
May 19 20:59:37.762 CAM(core.ecm): 0.1: found 0b00(0000) (Conax) id 0000 with ecm bfd/80 (new)
May 19 20:59:37.819 CAM(core.ecm): 0.1: try system Conax (0b00) id 0000 with ecm bfd (pri=-10)
May 19 20:59:37.838 CAM(core.au): 0: chain caid 0b00 -> Cardclient(-15) [00b6-82/ff/00]
May 19 20:59:37.955 CAM(conax.key): missing 20 E key
May 19 20:59:38.111 CAM(core.ecm): system: no key found for C 20 M
May 19 20:59:38.156 CAM(conax.key): missing 20 E key
May 19 20:59:38.202 CAM(core.ecm): 0.1: try system Cardclient (0b00) id 0000 with ecm bfd (pri=-15)
May 19 20:59:38.247 CAM(cardclient.core): cc-loop
May 19 20:59:38.303 CAM(cardclient.core): now trying client Newcamd (localhost:15050)
May 19 20:59:38.360 CAM(core.net): connecting to localhost:15050/tcp (127.0.0.1)
May 19 20:59:38.066 CAM(core.au): 0: starting chain 0b00
May 19 20:59:38.432 CAM(cardclient.login): Newcamd: CaID=0b00 admin=1 srvUA=00000000551F0EC6 provider 00E030/0000000000000000000000/00000000002A8F87
Called cSascDvbDevice::SetCaDescr
May 19 20:59:38.936 CSA: Got command(1): E idx: 1 pid: 0 key: 67b4...1a
Called cSascDvbDevice::SetCaDescr
May 19 20:59:39.106 CSA: Got command(1): O idx: 1 pid: 0 key: 170e...77
May 19 20:59:39.162 CAM(core.ecm): cache add prgId=36 source=1 transponder=0 ecm=bfd/80
May 19 20:59:39.218 CAM(core.ecm): 0.1: correct key found
Called cSascDvbDevice::SetCaDescr
May 19 20:59:41.436 CSA: Got command(1): E idx: 1 pid: 0 key: 67b4...1a
Called cSascDvbDevice::SetCaDescr
May 19 20:59:41.461 CAM(core.load): saved ecm cache to /etc/camdir/ecm.cache
May 19 20:59:41.651 CSA: Got command(1): O idx: 1 pid: 0 key: 170e...77
Called cSascDvbDevice::SetCaDescr
May 19 20:59:43.932 CSA: Got command(1): E idx: 1 pid: 0 key: 23b4...20
Called cSascDvbDevice::SetCaDescr
May 19 20:59:53.968 CSA: Got command(1): O idx: 1 pid: 0 key: 60b5...3e
Buffer has room, reading 32900 bytes
May 19 20:59:54.285 CSA: Creating csa for rb: 1
Buffer has room, reading 188 bytes
Buffer has room, reading 188 bytes
Returning 32768
Buffer has room, reading 32900 bytes
Buffer has room, reading 188 bytes
Buffer has room, reading 188 bytes
Returning 32768
Buffer has room, reading 32900 bytes
Buffer has room, reading 188 bytes
Returning 32768
Buffer has room, reading 32900 bytes
Buffer has room, reading 188 bytes
Returning 32768
Called cSascDvbDevice::SetCaDescr
May 19 21:00:04.069 CSA: Got command(1): E idx: 1 pid: 0 key: 461b...cd
Called cSascDvbDevice::SetCaDescr
May 19 21:00:13.931 CSA: Got command(1): O idx: 1 pid: 0 key: 12bf...2d
Called cSascDvbDevice::SetCaDescr
May 19 21:00:23.936 CSA: Got command(1): E idx: 1 pid: 0 key: bc12...41
Called cSascDvbDevice::SetCaDescr

```

## Integratie met mythtv

Installeer mythtv zoals hier beschreven: [MythTV HOWTO](/index.php/MythTV_HOWTO "MythTV HOWTO")

### Mythtv-setup

Zorg ervoor dat mysql, oscam en sasc-ng gestart zijn:

```
# /etc/rc.d/mysqld start
# /etc/rc.d/oscam start
# /etc/rc.d/sasc-ng start

```

Start vervolgens mythtv-setup, en stel daarna de volgende pagina's in:

```
$mythtv-setup

```

#### 1\. Algemeen

In dit menu zijn geen instellingen die invloed hebben op digitenne.

#### 2\. TV kaarten

```
Kaarttype: DVB DVT TV-kaart (v3.x)
DVB apparaatnummer: /dev/dvb/adapter1/frontend0
Frontendnaam: DiBcom 7000PC Subtype: DVB-T
Signal Timeout (ms): 1000
Tuning Timeout (ms): 3000
Maximum # opnames: 5
[niet] op SEQ start header wachten
[niet] DVB-kaart op vraag openen
[wel ] Use DVB card for active EIT scan
DVB tuning delay (ms): 0

```

#### 3\. Videobronnen

```
Naam videobron: digitenne_eit
TV-gids grabber: Enkel de meegezonden programmagids (EIT)
kanaalfrequentie-tabel: europe-west

```

#### 4\. Ingang verbindingen

```
[DVB : /dev/adapter1/frontend0 ] (DVBInput) -> digitenne_eit 
TV-Kaart: [DVB:/dev/dvb/adapter1/frontend0 ]
Ingang: DVBInput
Displaynaam: digitenne
Videobron: digitenne_eit
Snel afstemmen gebruiken: nooit
[niet] Use DishNet long-term EIT data
Zoeken naar zenders
 video bron: digitenne_eit
 Ingang: [DVB : /dev/adapter1/frontend0 ] (DVBInput)
 Gewenste diensten: TV
 [niet] enkel onversleuteld
 [niet] Test Decryptability
 Scan type: Volledige Scan
 Land: Duitsland (Nederland bestaat niet)  
Zender waarmee gestart wordt: 10
Ingangsprioriteit: 0
Ingangsgroep 1: DVB_/dev/dvb/adapter0/frontend0
Ingangsgroep 2: Generieke

```

#### 5\. Kanaal bewerker

Hier horen de kanalen te zien zijn die in scherm 4 (Ingang verbindingen) gevonden zijn.

#### 6\. Opslagmappen

In dit menu zijn geen instellingen die invloed hebben op digitenne.

#### 7\. System events

In dit menu zijn geen instellingen die invloed hebben op digitenne.

### Starten mythtv

Zorg ervoor dat mysqld, oscam, sasc-ng gestart zijn:

```
# /etc/rc.d/mysqld start
# /etc/rc.d/oscam start
# /etc/rc.d/sasc-ng start

```

Start dan mythbackend:

```
$ mythbackend

```

En in een andere terminal mythfrontend:

```
$ mythfrontend

```

Nu moet het mogelijk zijn om via TV -> TV kijken naar digitenne te kijken. Het kan enige tijd duren voordat afgestemd is op het juiste kanaal, en dat de juiste sleutel opgehaald is. Zappen duurt best lang, zeker als de zender waar je naar toe gaat in een andere transport (frequentie) zit.

Het beste werkt het om de programma's op te laten nemen, en vervolgens te kijken. Dan gebeurt al het decoderen in de achtergrond.

## Referenties

Sat4All forum: [http://www.sat4all.com/forums/ubbthreads.php/topics/1967886/digitenne_kijken_via_oscam_en_#Post1967886](http://www.sat4all.com/forums/ubbthreads.php/topics/1967886/digitenne_kijken_via_oscam_en_#Post1967886)