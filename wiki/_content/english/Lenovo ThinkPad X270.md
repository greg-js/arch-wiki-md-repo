<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Fingerprint](#Fingerprint)
*   [2 No audio over HDMI](#No_audio_over_HDMI)
*   [3 Thinkpad X270, model 20HN](#Thinkpad_X270,_model_20HN)
    *   [3.1 lsusb](#lsusb)
    *   [3.2 lspci](#lspci)

### Fingerprint

Some X270's come with vfs (Validity Sensors) fingerprint readers. The fingerprint reader included with this model is `138a:0097 Validity Sensors, Inc`. There's a patched libfprint which adds partial support for 138a:0097\. [libfprint-vfs0097-git](https://aur.archlinux.org/packages/libfprint-vfs0097-git/) It allows fingerprint authentication, but only if fingers are previously enrolled on the device from Windows.

### No audio over HDMI

Use "aplay -l" to list all audio devices. Use speaker-test to find the correct device-id for HDMI audio, e.g.

```
speaker-test -c 2 -r 48000 -D hw:0,7

```

Once you have identified the correct audio device id, add the device at the end of your /etc/pulse/default.pa:

 `/etc/pulse/default.pa`  `load-module module-alsa-sink device=hw:0,7 channels=2 rate=48000 sink_properties=device.description=HDMI` 

Finally:

```
killall pulseaudio
pulseaudio --check

```

### Thinkpad X270, model 20HN

#### lsusb

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 005: ID 138a:0097 Validity Sensors, Inc. 
Bus 001 Device 004: ID 04f2:b5ab Chicony Electronics Co., Ltd 
Bus 001 Device 002: ID 058f:9540 Alcor Micro Corp. AU9540 Smartcard Reader
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

#### lspci

```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v6/7th Gen Core Processor Host Bridge/DRAM Registers (rev 02)
00:02.0 VGA compatible controller: Intel Corporation HD Graphics 620 (rev 02)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:15.0 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #0 (rev 21)
00:15.1 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #1 (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:17.0 SATA controller: Intel Corporation Sunrise Point-LP SATA Controller [AHCI mode] (rev 21)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #1 (rev f1)
00:1c.2 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #3 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-LP LPC Controller (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (4) I219-V (rev 21)
02:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS522A PCI Express Card Reader (rev 01)
03:00.0 Network controller: Intel Corporation Wireless 8265 / 8275 (rev 78)

```