Modern Linux systems are more than capable of supporting your (semi-)professional audio needs. Latencies of 5ms down to even as low as 1ms can be achieved with good hardware and proper configuration.

## Contents

*   [1 Getting Started](#Getting_Started)
    *   [1.1 System Configuration](#System_Configuration)
        *   [1.1.1 Checklist](#Checklist)
    *   [1.2 JACK](#JACK)
        *   [1.2.1 FireWire](#FireWire)
        *   [1.2.2 Jack Flash](#Jack_Flash)
        *   [1.2.3 Quickscan JACK script](#Quickscan_JACK_script)
        *   [1.2.4 Desktop Effects vs JACK](#Desktop_Effects_vs_JACK)
        *   [1.2.5 A General Example](#A_General_Example)
*   [2 Realtime Kernel](#Realtime_Kernel)
    *   [2.1 ABS](#ABS)
    *   [2.2 AUR](#AUR)
*   [3 MIDI](#MIDI)
*   [4 Environment Variables](#Environment_Variables)
*   [5 Tips and Tricks](#Tips_and_Tricks)
*   [6 Hardware](#Hardware)
    *   [6.1 M-Audio Delta 1010](#M-Audio_Delta_1010)
    *   [6.2 M-Audio Fast Track Pro](#M-Audio_Fast_Track_Pro)
    *   [6.3 PreSonus Firepod](#PreSonus_Firepod)
    *   [6.4 PreSonus AudioBox USB](#PreSonus_AudioBox_USB)
    *   [6.5 Tascam US-122](#Tascam_US-122)
    *   [6.6 RME Babyface](#RME_Babyface)
*   [7 Restricted Software](#Restricted_Software)
    *   [7.1 Steinberg's SDKs](#Steinberg.27s_SDKs)
*   [8 Arch Linux Pro Audio Project](#Arch_Linux_Pro_Audio_Project)
*   [9 Linux and Arch Linux Pro Audio in the News](#Linux_and_Arch_Linux_Pro_Audio_in_the_News)

## Getting Started

Some of the major pro audio applications are already available from the official and community Arch Linux repositories. For anything which is not, you can either add a binary repository (see further down below) or if you prefer to compile, search the AUR. Nothing stops you from building directly off of upstream releases, but then you might as well run LFS.

Start by installing [JACK](/index.php/JACK "JACK").

The following packages are a good start to build a full-featured pro audio system:

*   [qjackctl](https://www.archlinux.org/packages/?name=qjackctl)
*   [patchage](https://www.archlinux.org/packages/?name=patchage)
*   [ardour](https://www.archlinux.org/packages/?name=ardour)
*   [qtractor](https://www.archlinux.org/packages/?name=qtractor)
*   [hydrogen](https://www.archlinux.org/packages/?name=hydrogen)
*   [musescore](https://www.archlinux.org/packages/?name=musescore)
*   [rosegarden](https://www.archlinux.org/packages/?name=rosegarden)
*   [qsynth](https://www.archlinux.org/packages/?name=qsynth)
*   [jsampler](https://www.archlinux.org/packages/?name=jsampler)
*   [lmms](https://www.archlinux.org/packages/?name=lmms)
*   [calf](https://www.archlinux.org/packages/?name=calf)
*   [dssi](https://www.archlinux.org/packages/?name=dssi)

Other packages you may need that are available from the [AUR](/index.php/AUR "AUR"):

*   [qsampler](https://aur.archlinux.org/packages/qsampler/) (also see [Linuxsampler](/index.php/Linuxsampler "Linuxsampler"))
*   [tal-plugins-vst-bin](https://aur.archlinux.org/packages/tal-plugins-vst-bin/)
*   [mhwaveedit](https://aur.archlinux.org/packages/mhwaveedit/)
*   [carla](https://aur.archlinux.org/packages/carla/)
*   [guitarix-git](https://aur.archlinux.org/packages/guitarix-git/)
*   [fluidsynth-dssi](https://aur.archlinux.org/packages/fluidsynth-dssi/)
*   [rakarrack-git](https://aur.archlinux.org/packages/rakarrack-git/)
*   [XCFA](https://aur.archlinux.org/packages/XCFA/)
*   [yoshimi](https://aur.archlinux.org/packages/yoshimi/)
*   [wineasio](https://aur.archlinux.org/packages/wineasio/)
*   [vst-bridge](https://github.com/abique/vst-bridge)

See also [List of applications#Audio systems](/index.php/List_of_applications#Audio_systems "List of applications") and [List of applications#Sound editing](/index.php/List_of_applications#Sound_editing "List of applications").

### System Configuration

You may want to consider the following often seen system optimizations:

*   Add yourself to the _audio_ [group](/index.php/Group "Group").
*   Add the `threadirqs` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter").

**Warning:** Enabling threadirqs seems to be causing system lockups in conjunction with usb devices in at least some kernel versions starting with 3.13 and including at least 3.14-rc2\. See for example [https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1279081](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1279081) and [http://www.spinics.net/lists/linux-usb/msg102504.html](http://www.spinics.net/lists/linux-usb/msg102504.html) also linked from there.
EDIT: The changelog seems to indicate that this has been fixed in the 3.13.6 vanilla kernel. (Search for threadirqs in [https://www.kernel.org/pub/linux/kernel/v3.x/ChangeLog-3.13.6](https://www.kernel.org/pub/linux/kernel/v3.x/ChangeLog-3.13.6))

*   Install [linux-rt](https://aur.archlinux.org/packages/linux-rt/) kernel.
*   Set the [cpufreq](/index.php/Cpufreq "Cpufreq") governor to _performance_.
*   Add _noatime_ to the [filesystem mount options](/index.php/Fstab "Fstab") (see [Maximizing Performance](/index.php/Maximizing_performance#Mount_options "Maximizing performance")).

Realtime configuration has mostly been automated. There is no longer any need to edit files like `/etc/security/limits.conf` for realtime access. However, if you must change the settings, see `/etc/security/limits.d/99-audio.conf` and `/usr/lib/udev/rules.d/40-hpet-permissions.rules` (these files are provided by [jack](https://www.archlinux.org/packages/?name=jack) or [jack2](https://www.archlinux.org/packages/?name=jack2)). Additionaly, you may want to increase the highest requested RTC interrupt frequency (default is 64 Hz) by [running the following at boot](/index.php/Systemd_FAQ#How_can_I_make_a_script_start_during_the_boot_process.3F "Systemd FAQ"):

```
echo 2048 > /sys/class/rtc/rtc0/max_user_freq
echo 2048 > /proc/sys/dev/hpet/max-user-freq

```

By default, swap frequency defined by "swappiness" is set to 60\. By reducing this number to 10, the system will wait much longer before trying to write to disk. Then, there is _inotify_ which watches for changes to files and reports them to applications requesting this information. When working with lots of audio data, a lot of watches will need to be kept track of, so they will need to be increased. These two settings can be adjusted in `/etc/sysctl.d/99-sysctl.conf`.

```
vm.swappiness = 10
fs.inotify.max_user_watches = 524288

```

You may also want to maximize the PCI latency timer of the PCI sound card and raise the latency timer of all other PCI peripherals (default is 64).

```
$ setpci -v -d *:* latency_timer=**b0**
$ setpci -v -s _$SOUND_CARD_PCI_ID_ latency_timer=**ff** # eg. SOUND_CARD_PCI_ID=03:00.0 (see below)

```

The SOUND_CARD_PCI_ID can be obtained like so:

 `$ lspci ¦ grep -i audio` 

```
**03:00.0** Multimedia audio controller: Creative Labs SB Audigy (rev 03)
**03:01.0** Multimedia audio controller: VIA Technologies Inc. VT1720/24 [Envy24PT/HT] PCI Multi-Channel Audio Controller (rev 01)
```

#### Checklist

The steps below are mostly to double-check that you have a working multimedia system:

*   Have I set up sound properly? See [ALSA](/index.php/ALSA "ALSA") or [OSS](/index.php/OSS "OSS").

```
$ speaker-test

```

*   Am I in the audio group? See [ALSA](/index.php/ALSA "ALSA") or [OSS](/index.php/OSS "OSS").

```
$ groups | grep audio

```

*   Is PulseAudio, OSS or something else grabbing my device?

```
$ lsof +c 0 /dev/snd/pcm* /dev/dsp*

```

-OR-

```
$ fuser -fv /dev/snd/pcm* /dev/dsp*  

```

*   Is PAM-security and realtime working OK?

See: [Realtime for Users#PAM-enabled login](/index.php/Realtime_for_Users#PAM-enabled_login "Realtime for Users") (Pay special attention especially if you do not run KDM, GDM or Slim.)

*   Have I rebooted after having done all that?

### JACK

The aim here is to find the best possible combination of buffer size and periods, given the hardware you have. **Frames/Period = 256** is a sane starter. For onboard and USB devices, try **Periods/Buffer = 3**. Commonly used values are: 256/3, 256/2, 128/3.

Also, the sample rate must match the hardware sample rate. To check what sample and bit rates your device supports:

```
$ cat /proc/asound/card0/codec#0

```

Replace _card0_ and _codec#0_ depending on what you have. You will be looking for **rates** or _VRA_ in **Extended ID**. A common sample rate across many of today's devices is **48000 Hz**. Others common rates include 44100 Hz and 96000 Hz.

Almost always, when recording or sequencing with external gear is concerned, **realtime** is a must. Also, you may like to set maximum priority (at least 10 lower than system limits defined in `/etc/security/limits.d/99-audio.conf`); the highest is for the device itself).

Start jack with the options you just found out:

```
$ /usr/bin/jackd -R -P89 -dalsa -dhw:0 -r48000 -p256 -n3

```

[qjackctl](https://www.archlinux.org/packages/?name=qjackctl), [cadence](https://aur.archlinux.org/packages/cadence/) and [patchage](https://www.archlinux.org/packages/?name=patchage) can all be used to as GUIs to monitor JACK's status and simplify its configuration .

**Note:** Once you set up JACK, try different audio applications to test your configuration results. I spent days trying to troubleshoot JACK xrun issues with LMMS which in the end turned out to be the problem with the latter.

_Further reading: [http://w3.linux-magazine.com/issue/67/JACK_Audio_Server.pdf](http://w3.linux-magazine.com/issue/67/JACK_Audio_Server.pdf)_

#### FireWire

**Note:** Nothing much is needed to be done as most things have been automated, especially with the introduction of the [new FireWire stack](https://ieee1394.wiki.kernel.org/articles/j/u/j/Juju_Migration_e8a6.html), deprecation of HAL and more focus on [udev](/index.php/Udev "Udev"). You should not need to edit device permissions, but if you suspect that your device may not be working due to such issues, see `/lib/udev/rules.d/60-ffado.rules` and if needed, create and put your changes into `/etc/udev/rules.d/60-ffado.rules`. Most often than not, your device will work with the [libffado-svn](https://aur.archlinux.org/packages/libffado-svn/) development version of the driver.

JACK(2) is built against FFADO, you only need to install it with the [libffado](https://www.archlinux.org/packages/?name=libffado) package.

To test whether you have any chances of getting FireWire devices to work:

*   Ensure the proper kernel modules are loaded:

```
# modprobe firewire-core firewire-ohci

```

*   Is my chipset sane enough to initiate a device?

[http://www.ffado.org/?q=node/622](http://www.ffado.org/?q=node/622)

*   Is my chipset sane enough to make a device work to its capacity?

We cannot say for sure, particularly for those based on Ricoh (cross-platform issue). Most of the time, your device will run fine, but on occasion you will be faced with funny quirks. For unlucky ones, you will be facing hell.

**Note:** As stated by Takashi Sakamoto [on the alsa-devel mailing list](http://mailman.alsa-project.org/pipermail/alsa-devel/2014-September/081731.html), if you use the FireWire backend with jackd, the DICE module is incompatible. If you see a line like this :

```
Warning (dice_eap.cpp)[1811] read: No routes found. Base 0x7, offset 0x4000

```

you need to disable the "snd_dice" module.

#### Jack Flash

If after getting jack setup you will find that Flash has no audio.

In order to get flash to work with jack you will need to install [libflashsupport-jack](https://aur.archlinux.org/packages/libflashsupport-jack/) from the [AUR](/index.php/AUR "AUR").

You can also use more flexible method to allow Alsa programs (including Flash) play sound while jack is running:

First you must install the jack plugin for Alsa by installing [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins) from the [official repositories](/index.php/Official_repositories "Official repositories"). Enable it by editing (or creating) `/etc/asound.conf` (system wide settings) to have these lines:

```
# convert alsa API over jack API
# use it with
# % aplay foo.wav

# use this as default
pcm.!default {
    type plug
    slave { pcm "jack" }
}

ctl.mixer0 {
    type hw
    card 1
}

# pcm type jack
pcm.jack {
    type jack
    playback_ports {
        0 system:playback_1
        1 system:playback_2
    }
    capture_ports {
        0 system:capture_1
        1 system:capture_2
    }
}

```

You do not need to restart your computer or anything. Just edit the alsa config files, start up jack.

#### Quickscan JACK script

Most people will probably want to run JACK in realtime mode, there are however a lot of knobs and buttons to press in order for that to happen.

A great way to quickly diagnose your system and find out what it is missing in order to have JACK work properly in real time mode is to run the Quickscan script.

[https://github.com/raboof/realtimeconfigquickscan/blob/master/realTimeConfigQuickScan.pl](https://github.com/raboof/realtimeconfigquickscan/blob/master/realTimeConfigQuickScan.pl)

(or just install [realtimeconfigquickscan](https://aur.archlinux.org/packages/realtimeconfigquickscan/) from the [AUR](/index.php/AUR "AUR"))

The output should tell you where your system is lacking and will point you to places to find more information.

#### Desktop Effects vs JACK

In addition to the factors listed under the System Configuration section above as well as the settings checked by realTimeConfigQuickScan.pl, it is also worth noting that desktop environments can cause xruns and hence JACK audio glitches, especially memory/process intensive ones and those desktops that utilize composited desktop effects. It is recommended you disable desktop effects when using JACK. You are likely to get the least xruns and best performance by running a lightweight desktop or just a window manager instead.

#### A General Example

A general configuration example is [JACK Audio Connection Kit#A Shell-Based Example Setup](/index.php/JACK_Audio_Connection_Kit#A_Shell-Based_Example_Setup "JACK Audio Connection Kit").

## Realtime Kernel

Since a while ago, the stock Linux kernel has proven to be adequate for realtime uses. The stock kernel (with `CONFIG_PREEMPT=y`, default in Arch) can operate with a worst case latency of [upto 10ms](https://rt.wiki.kernel.org/index.php/Frequently_Asked_Questions#What_are_real-time_capabilities_of_the_stock_2.6_linux_kernel.3F) (time between the moment an interrupt occurs in hardware, and the moment the corresponding interrupt-thread gets running), although some device drivers can introduce latency much worse than that. So depending on your hardware and driver (and requirement), you might want a kernel with hard realtime capabilities.

The [RT_PREEPMT](https://rt.wiki.kernel.org/index.php/RT_PREEMPT_HOWTO) patch by Ingo Molnar and Thomas Gleixner is an interesting option for hard and firm realtime applications, reaching from professional audio to industrial control. Most audio-specific distro Linux ships with this patch applied. A realtime-preemptible kernel will also make it possible to tweak priorities of IRQ handling threads and help ensure smooth audio almost regardless of the load.

If you are going to compile your own kernel, remember that removing modules/options does not equate to a "leaner and meaner" kernel. It is true that the size of the kernel image is reduced, but in today's systems it is not as much of an issue as it was back in **1995**.

In any way, you should also ensure that:

*   **Timer Frequency** is set to **1000Hz** (CONFIG_HZ_1000=y; if you do not do _MIDI_ you can ignore this)
*   **APM** is **DISABLED** (CONFIG_APM=n; Troublesome with some hardware - default in x86_64)

If you truly want a slim system, we suggest you go your own way and deploy one with _static /devs_. You should, however, set your CPU architecture. Selecting "Core 2 Duo" for appropriate hardware will allow for a good deal of optimisation, but not so much as you go down the scale.

General issue(s) with (realtime) kernels:

*   Hyperthreading (if you suspect, disable in BIOS)

There are ready-to-run/compile patched kernels available in the ABS and AUR.

**Note:** Before you decide to use a patched kernel, see [http://jackaudio.org/faq/realtime_vs_realtime_kernel.html](http://jackaudio.org/faq/realtime_vs_realtime_kernel.html).

### ABS

You can use [ABS](/index.php/ABS "ABS") to recompile [linux](https://www.archlinux.org/packages/?name=linux) with the patch. However, this is not the most useful of methods since updates will overwrite your custom kernel (at least you should add `IgnorePkg=linux` to `/etc/pacman.conf`).

### AUR

From the [AUR](/index.php/AUR "AUR") itself, you have the following options:

*   [linux-rt](https://aur.archlinux.org/packages/linux-rt/)
*   [linux-rt-lts](https://aur.archlinux.org/packages/linux-rt-lts/) (Long Term Support, stable release)
*   [linux-rt-ice](https://aur.archlinux.org/packages/linux-rt-ice/)

The first two are standard kernels with the CONFIG_PREEMPT_RT patch, while -ice includes patches some may consider to be nasty, while to others are a blessing.

	_See: [Real-Time Linux Wiki](https://rt.wiki.kernel.org/)_

## MIDI

If you want to use any MIDI hardware you need to ensure the ALSA MIDI driver is loaded. You can set the MIDI driver to load at boot by creating the file `/etc/modules-load.d/alsamidi.conf` containing:

```
snd_seq_midi

```

To work with MIDI you can it is highly recommended that you install a2j ([a2jmidid](https://www.archlinux.org/packages/?name=a2jmidid)), a bridge between alsa midi and jack midi. It allows you to connect applications that only communicate with alsa midi to applications that only use jack midi. Laditray can also start/stop a2j.

	_See: [JACK#MIDI](/index.php/JACK#MIDI "JACK")_

## Environment Variables

If you install things to non-standard directories, it is often necessary to set environment path variables so that applications know where to look (for plug-ins and other libraries). This usually affects only VST since users might have a Wine or external Windows location.

We would usually not have Linux plug-ins (LADSPA, LV2, DSSI, LXVST) beyond standard paths, so it is not necessary to export them. But if you do, be sure to include those standard paths as well since Arch does not do anything for _dssi_ or _ladspa_, and some applications like _dssi-vst_ will not look anywhere else if it finds predefined paths.

 `~/.bashrc` 

```
...
export VST_PATH=/usr/lib/vst:/usr/local/lib/vst:~/.vst:/someother/custom/dir
export LXVST_PATH=/usr/lib/lxvst:/usr/local/lib/lxvst:~/.lxvst:/someother/custom/dir
export LADSPA_PATH=/usr/lib/ladspa:/usr/local/lib/ladspa:~/.ladspa:/someother/custom/dir
export LV2_PATH=/usr/lib/lv2:/usr/local/lib/lv2:~/.lv2:/someother/custom/dir
export DSSI_PATH=/usr/lib/dssi:/usr/local/lib/dssi:~/.dssi:/someother/custom/dir
```

## Tips and Tricks

*   Disable WiFi and close any programs that don't need to be open when recording such as browsers. Many have reported disabling WiFi has led to more reliable JACK performance.

*   Some USB audio hardware is known not to work properly when plugged into USB 3 ports so try USB 2/1 ports instead.

*   IRQ issues can occur and cause problems. An example is video hardware reserving the bus, causing needless interrupts in the system I/O path. See discussion at [FFADO IRQ Priorities How-To](http://subversion.ffado.org/wiki/IrqPriorities). If you have a realtime or a recent kernel, you can use [rtirq](https://aur.archlinux.org/packages/rtirq/) to adjust priorities of IRQ handling threads.

*   Do not use the **irqbalance** daemon, or do so carefully [[1]](http://docs.redhat.com/docs/en-US/Red_Hat_Enterprise_MRG/1.3/html/Realtime_Tuning_Guide/sect-Realtime_Tuning_Guide-General_System_Tuning-Interrupt_and_Process_Binding.html).

*   Some daemons/processes can unexpectedly cause **xruns**. If you do not need it - kill it. No questions asked.

```
$ ls /var/run/daemons
$ top # or htop, ps aux, whatever you are comfortable with
$ killall -9 $processname
# systemctl stop $daemonname

```

*   If you are facing a lot of _xruns_ especially with [nvidia](https://www.archlinux.org/packages/?name=nvidia), disable your GPU throttling. This can be done via the card's control applet and for nvidia it is "prefer maximum performance" (thanks to a mail in LAU by Frank Kober).

*   You may like to read more on ALSA: [http://www.volkerschatz.com/noise/alsa.html](http://www.volkerschatz.com/noise/alsa.html)

## Hardware

### M-Audio Delta 1010

The M-Audio Delta series cards are based on the VIA Ice1712 audio chipset. Cards using this chip require that you install the alsa-tools package, because it contains the [envy24control](/index.php/Envy24control "Envy24control") program. [Envy24control](/index.php/Envy24control "Envy24control") is a hardware level mixer/controller. You _can_ use alsa-mixer but you will save yourself some hassle not to try it. Note that this section has no information on MIDI setup or usage.

Open the mixer application:

```
$ envy24control

```

This application can be more than a bit confusing; see [envy24control](/index.php/Envy24control "Envy24control") for guidance on its use. That said, here is a very simple working setup for multitracking with Ardour.

1.  On the "Monitor Inputs" and "Monitor PCMs" tabs, set all monitor inputs and monitor PCM's to around 20.
2.  On the "Patchbay / Router" tab, set all to PCM out.
3.  On the "Hardware Settings" tab, verify that the Master Clock setting matches what is set in Qjackctl. If these do not match you will have xruns out of control!

### M-Audio Fast Track Pro

The M-Audio Fast Track Pro is an USB 4x4 audio interface, working at 24bit/96kHz. Due to limitation of USB 1, this device requires additional setup to get access to all its features. Device works in one of two configuration:

*   Configuration 1, or "Class compliant mode" - with reduced functionality, only 16bit, 48kHz, analogue input (2 channels) and digital/analogue output (4 channels).
*   Configuration 2 - with access to all features of interface.

Currently with stock kernel it runs in configuration 2, but if you want to make sure in what mode you are, you can check kernel log for entries:

```
usb-audio: Fast Track Pro switching to config #2
usb-audio: Fast Track Pro config OK

```

The interface also needs extra step of cofiguration to switch modes. It is done using option `device_setup` during module loading. The recommended way to setup the interface is using file in `modprobe.d`:

 `/etc/modprobe.d/ftp.conf` 

```
options snd_usb_audio vid=0x763 pid=0x2012 device_setup=XXX index=YYY enable=1

```

where `vid` and `pid` are vendor and product id for M-Audio Fast Track Pro, `index` is desired device number and `device_setup` is desired device setup. Possible values for `device_setup` are:

<caption>device modes</caption>
| device_setup value | bit depth | frequency | analog output | digital output | analog input | digital input | IO mode |
| 0x0 | 16 bit | 48kHz | + | + | + | + | 4x4 |
| 0x9 | 24 bit | 48kHz | + | + | + | - | 2x4 |
| 0x13 | 24 bit | 48kHz | + | + | - | + | 2x4 |
| 0x5 | 24 bit | 96kHz | * | * | * | * | 2x0 or 0x2 |

The 24 bit/96kHz mode is special: it provides all input/output, but you can open only one of 4 interfaces at a time. If you for example open output interface and then try to open second output or input interface, you will see error in kernel log:

```
cannot submit datapipe for urb 0, error -28: not enough bandwidth

```

which is perfectly normal, because this is USB 1 device and cannot provide enough bandwidth to support more than single (2 channel) destination/source of that quality at a time.

Depending on the value of `index` it will setup two devices: `hwYYY:0` and `hwYYY:1`, which will contain available inputs and outputs. First device is most likely to contain analog output and digital input, while second one will contain analog input and digital output. To find out which devices are linked where and if they are setup correctly, you can check `/proc/asound/cardYYY/stream{0,1}` . Below is list of important endpoints that will help in correctly identifying card connections (it easy to mistake analog and digital input or output connections before you get used to the device):

```
EP 3 (analgoue output = TRS on back, mirrored on RCA outputs 1 and 2 on back)
EP 4 (digital output = S/PDIF output on back, mirrored on RCA outputs 3 and 4 on back)
EP 5 (analogue input = balanced TRS or XLR microphone, unbalanced TS line on front)
EP 6 (digital input = S/PDIF input on back)

```

This .asoundrc file enables 24-bit IO on the fast-track pro (and I'm sure it could be modified to work with other 3-byte usb devices) within the context of jack's 32-bit interface while routing default alsa traffic to jack outputs on the audio interface. Alsa will be in S24_3BE mode but jack can plug S32_LE data in and out of the interface and other alsa programs will be able to plug almost anything into jack.

```
### ~/.asoundrc
### default alsa config file, for a fast-track pro configured in 24-bit mode as so:
### options snd_usb_audio device_setup=0x9
### invoke jack with: (if you use -r48000, change the rate in the plugs as well)
### $jackd -dalsa -P"hw:Pro" -C"hw:Pro,1" -r44100

## setup input and output plugs so jack can write S24_3BE data to the audio interface

pcm.maud0 {
	type hw
	card Pro
	 }

#jack_out plug makes sure that S32_LE data can be written to hw:Pro
pcm.jack_out{
	type plug
	format S32_LE
	channels 2
	rate 44100
	slave pcm.maud0
}

pcm.maud1 {
	type hw
	card Pro
	device 1
}
## jack_in plug makes sure that hw:Pro,1 can read S32_LE data
pcm.jack_in {
	type plug
	format S32_LE
	channels 2
	rate 44100
	slave pcm.maud1
}
#####
# route default alsa traffic through jack system io

pcm.jack {
    type jack
    playback_ports {
        0 system:playback_1
        1 system:playback_2
    }
    capture_ports {
        0 system:capture_1
        1 system:capture_2
    }
} 
pcm.amix {
	type asym
	playback.pcm "jack"
	capture.pcm "jack"
	}
pcm.!default {
	type plug
	slave.pcm amix
}

```

### PreSonus Firepod

1.  Startup: Either from command line or QjackCtl, the driver is called firewire.
2.  Specs: The card contains 8/8 preamp'ed XLR plus a stereo pair, in total 10 channels.
3.  Linking: Cards can be linked together without any problems.
4.  Hardware Settings: Nothing particular, tweak the settings in QjackCtl to your likings.

Volume levels are hardware and routing can be done through QjackCtl, even with more cards linked together, this is not a problem. The ffadomixer does not work with this card yet, hopefully in the future we can control more aspects of the card through a software interface like that.

### PreSonus AudioBox USB

1.  Startup: It is called "USB" by ALSA.
2.  Specs: Two mono TRS+XLR in, two mono TRS out, MIDI in and out, plus separate stereo headphone jack. Knob controls for both inputs, for main out, and for headphone, four in all.
3.  Hardware: Works very well, audio and MIDI too. No software mixer controls at all.

### Tascam US-122

_**This does not apply to the US-122L**_

1.  Required packages: [alsa-tools](https://www.archlinux.org/packages/?name=alsa-tools) [alsa-firmware](https://www.archlinux.org/packages/?name=alsa-firmware) [fxload](https://aur.archlinux.org/packages/fxload/)
2.  udev rules: create the following rules file, then reload udev rules, [Udev#Loading new rules](/index.php/Udev#Loading_new_rules "Udev")

 `/etc/udev/rules.d/51-tascam-us-122.rules` 

```
SUBSYSTEMS=="usb", ACTION=="add", ATTRS{idProduct}=="8006", ATTRS{idVendor}=="1604", RUN+="/bin/sh -c '/sbin/fxload -D %N -s /usr/share/alsa/firmware/usx2yloader/tascam_loader.ihx -I /usr/share/alsa/firmware/usx2yloader/us122fw.ihx'"
SUBSYSTEMS=="usb", ACTION=="add", ATTRS{idProduct}=="8007", ATTRS{idVendor}=="1604", RUN+="/bin/sh -c '/usr/bin/usx2yloader'"

```

Plug in the unit The device should now be working, there are no software mixer controls

### RME Babyface

It works very well at low latencies (~5ms) with [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils), [jack2](https://www.archlinux.org/packages/?name=jack2) and [linux-rt](https://aur.archlinux.org/packages/linux-rt/). Running on ALSA only with the standard kernel may cause crackling at lower latencies.

To be recognized and work, the firmware version of the Babyface needs to be >= 200, which introduces the Class Compliant Mode. To enter Class Compliant Mode hold the "Select" and "Recall" buttons while connecting the Babyface to the computer via USB. It should now be recognized.

To check if it is recognized:

```
grep -i baby /proc/asound/cards

```

For more info about the Class Compliant Mode visit RME's website, they have PDF which covers all the functionality.

The Babyface does not need any special Jack Settings. But if you want to use the built in MIDI In/Out then you need to set the "MIDI Driver" to "seq" and optionally disable "Enable Alsa Sequencer Support" to use it in combination with other MIDI Devices (a USB Midi Keyboard for example).

## Restricted Software

### Steinberg's SDKs

It is very clear - we can distribute neither the VST nor the ASIO headers in **binary package form**. However, whenever you are building a program which would host Windows _.dll_ VST plug-ins, check for the following hints (that do not require use of any SDK):

*   dssi-vst
*   fst
*   vestige

With that said, if you are building a program which would host native _.so_ VST plug-ins, then there is no escape. For such cases, Arch yet again allows us to maintain a uniform local software database. We can "install" the SDK _system-wide_ - you simply have to download it yourself and place it in the packaging directory.

[Get them from AUR](https://aur.archlinux.org/packages.php?O=0&K=steinberg-&do_Search=Go)

_Note: Steinberg does not forbid redistribution of resulting products, nor dictate what license they can be under. There are many GPL-licensed VST plug-ins. As such, distributing binary packages of software built with these restricted headers is **not** a problem, because the headers are simply **buildtime dependencies**._

## Arch Linux Pro Audio Project

Yes, we have one. Think of "Planet CCRMA" or "Pro Audio Overlay", less the academic connotations of the former: [ArchAudio](http://archaudio.org).

What this means is that the repositories are add-ons, i.e you need to have a running, sane Arch Linux installation.

It is a relatively new effort although the initiative has been around since 2006/2007\.

History: [https://bbs.archlinux.org/viewtopic.php?id=30547](https://bbs.archlinux.org/viewtopic.php?id=30547)

For all your Arch- and ArchAudio-related audio issues hop on to **IRC**: #archaudio @ Freenode

## Linux and Arch Linux Pro Audio in the News

*   [Build a Serious Multimedia Production Workstation with Arch](https://www.linux.com/learn/tutorials/607117-build-a-serious-multimedia-production-workstation-with-arch-linux) - Linux.com article, July 2012

*   [An Arch Tale](http://www.linuxjournal.com/content/arch-tale) - Article by fellow musician and writer Dave Phillips, October 2011

*   [From Windows to Linux: a sound decision](http://www.itwire.com/opinion-and-analysis/open-sauce/36698-from-windows-to-linux-a-sound-decision) - Interview with Geoff "songshop" Beasley, February 2010