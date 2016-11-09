See [Advanced Linux Sound Architecture](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture") for the main article.

## Contents

*   [1 Volume](#Volume)
    *   [1.1 Output is muted after reboot](#Output_is_muted_after_reboot)
    *   [1.2 Volume is too low](#Volume_is_too_low)
    *   [1.3 Low Sound Volume](#Low_Sound_Volume)
    *   [1.4 Random lack of sound on startup](#Random_lack_of_sound_on_startup)
*   [2 Microphone](#Microphone)
    *   [2.1 No microphone input](#No_microphone_input)
    *   [2.2 Setting the default microphone/capture device](#Setting_the_default_microphone.2Fcapture_device)
    *   [2.3 Internal microphone not working](#Internal_microphone_not_working)
    *   [2.4 Crackling microphone](#Crackling_microphone)
*   [3 Audio Quality](#Audio_Quality)
    *   [3.1 Crackling sound through mini-jack (headphones connector)](#Crackling_sound_through_mini-jack_.28headphones_connector.29)
    *   [3.2 Popping sound after resuming from suspension](#Popping_sound_after_resuming_from_suspension)
    *   [3.3 Sound skipping during playback](#Sound_skipping_during_playback)
    *   [3.4 Poor sound quality or clipping](#Poor_sound_quality_or_clipping)
    *   [3.5 Pops when starting and stopping playback](#Pops_when_starting_and_stopping_playback)
    *   [3.6 Sound skipping while using dynamic CPU frequency scaling](#Sound_skipping_while_using_dynamic_CPU_frequency_scaling)
*   [4 Hardware and Cards](#Hardware_and_Cards)
    *   [4.1 Verifying output parameters](#Verifying_output_parameters)
    *   [4.2 Error 'Unknown hardware' appears after kernel update](#Error_.27Unknown_hardware.27_appears_after_kernel_update)
    *   [4.3 Fix wrong audio pin mapping](#Fix_wrong_audio_pin_mapping)
    *   [4.4 S/PDIF output does not work](#S.2FPDIF_output_does_not_work)
    *   [4.5 Conflicting PC speaker](#Conflicting_PC_speaker)
    *   [4.6 HP TX2500](#HP_TX2500)
    *   [4.7 No sound when S/PDIF video card is installed](#No_sound_when_S.2FPDIF_video_card_is_installed)
    *   [4.8 Wrong sound card model type](#Wrong_sound_card_model_type)
    *   [4.9 Intel onboard sound](#Intel_onboard_sound)
        *   [4.9.1 No sound with onboard Intel sound card](#No_sound_with_onboard_Intel_sound_card)
        *   [4.9.2 No headphone sound with onboard intel sound card](#No_headphone_sound_with_onboard_intel_sound_card)
    *   [4.10 HDMI](#HDMI)
        *   [4.10.1 HDMI Output does not work](#HDMI_Output_does_not_work)
        *   [4.10.2 PCM through HDMI does not work (Intel Gfx)](#PCM_through_HDMI_does_not_work_.28Intel_Gfx.29)
        *   [4.10.3 HDMI 5.1 sound goes to wrong speakers](#HDMI_5.1_sound_goes_to_wrong_speakers)
*   [5 Applications](#Applications)
    *   [5.1 SDL: No sound with SDL applications](#SDL:_No_sound_with_SDL_applications)
    *   [5.2 OpenAL: No sound in applications that use OpenAL](#OpenAL:_No_sound_in_applications_that_use_OpenAL)
    *   [5.3 VirtualBox: Virtual machine has no sound](#VirtualBox:_Virtual_machine_has_no_sound)
    *   [5.4 Others: General application problems](#Others:_General_application_problems)
*   [6 Other Issues](#Other_Issues)
    *   [6.1 Simultaneous playback problems](#Simultaneous_playback_problems)
    *   [6.2 Removing old ALSA state file (asound.state)](#Removing_old_ALSA_state_file_.28asound.state.29)
    *   [6.3 Problems with availability to only one user at a time](#Problems_with_availability_to_only_one_user_at_a_time)

## Volume

### Output is muted after reboot

Run the following command:

```
# alsactl restore

```

If the problem persists, verify that the `Auto-Mute` option in *alsamixer* is set to `Disabled`.

### Volume is too low

Run *alsamixer* and try to increase the value of the sliders, unmuting channels if necessary. Note that if you have many sliders, you may have to scroll to the right to see any missing sliders.

If all the sliders are maxed out, and the volume is still too low, you can try running the following [script](http://www.alsa-project.org/hda-analyzer.py) to reset your codec settings:

```
$ wget [http://www.alsa-project.org/hda-analyzer.py](http://www.alsa-project.org/hda-analyzer.py)
$ su -c 'python2 hda-analyzer.py'

```

The script assumes that `/usr/bin/python` refers to Python 2, which is incorrect on Arch by default. To avoid this issue run the following command:

```
$ sed -i 's/python %s/python2 %s/' hda-analyzer.py

```

Close the analyzer, and when prompted as to whether you want to reset the codecs, say "yes".

If the volume is *still* too low, run *alsamixer* again: resetting the codecs may have caused new sliders to become enabled and some of them may be set to a low value.

### Low Sound Volume

If you are facing low sound even after maxing out your speakers/headphones, you can give the softvol plugin a try. Add the following to `/etc/asound.conf`.

```
pcm.!default {
    type plug
    slave.pcm "softvol"
}

pcm.softvol {
    type softvol
    slave {
        pcm "dmix"
    }
    control {
        name "Pre-Amp"
        card 0
    }
    min_dB -5.0
    max_dB 20.0
    resolution 6
}
```

**Note:** You will probably have to restart the computer, as restarting the alsa daemon did not load the new configuration for me. Also, if the configuration does not work even after restarting, try changing `plug` with `hw` in the above configuration.

After the changes are loaded successfully, you will see a `Pre-Amp` section in alsamixer. You can adjust the levels there.

**Note:**

*   Setting a high value for `Pre-Amp` can cause sound distortion, so adjust it according to the level that suits you.
*   Some audio codecs may need to have settings adjusted in the HDA Analyzer (see [#Volume is too low](#Volume_is_too_low)) in order to achieve proper volume without distortion. Checking the HP option under widget control in the Playback Switch (Node[0x14] PIN in the ALC892 codec, for instance) can sometimes improve audio quality and volume significantly.

### Random lack of sound on startup

You can quickly test sound by running `speaker-test`. If there is no sound, the error message might look something like

```
 ALSA lib pcm_dmix.c:1022:(snd_pcm_dmix_open) unable to open slave
 Playback open error: -16
 Device or resource busy

```

If you have no sound on startup, this may be because your system has multiple sound cards, and their order may sometimes change on startup. If this is the case, try [setting the default sound card](/index.php/ALSA#Set_the_default_sound_card "ALSA").

If you use mpd and the configuration tips above do not work for you, try [reading this](http://mpd.wikia.com/wiki/Configuration#ALSA_MPD_software_volume_control) instead.

## Microphone

### No microphone input

In alsamixer, make sure that all the volume levels are up under recording, and that CAPTURE is toggled active on the microphone (e.g. Mic, Internal Mic) and/or on Capture (in alsamixer, select these items and press space). Try making positive Mic Boost and raising Capture and Digital levels higher; this make make static or distortion, but then you can adjust them back down once you are hearing *something* when you record

As the pulseaudio wrapper is shown as "default" in alsamixer, you may have to press F6 to select your actual soundcard first. You may also need to enable and increase the volume of Line-in in the Playback section.

To test the microphone, run these commands (see arecord's man page for further information):

```
$ arecord -d 5 -f dat test-mic.wav
$ aplay test-mic.wav

```

Alternatively, you can run this command:

```
$ arecord -vv -f dat /dev/null

```

alongside alsamixer to easily identify channel which you should select and unmute.

If all fails, you may want to eliminate hardware failure by testing the microphone with a different device.

For at least some computers, muting a microphone (MM) simply means its input does not go immediately to the speakers. It still receives input.

Many Dell laptops need "-dmic" to be appended to the model name in `/etc/modprobe.d/modprobe.conf`:

```
options snd-hda-intel model=dell-m6-dmic

```

Some programs use try to use OSS as the main input software. If you have enabled the `snd_pcm_oss`, `snd_mixer_oss` or `snd_seq_oss` [kernel modules](/index.php/Kernel_modules "Kernel modules") previously (they are not loaded by default), try unloading them.

See also:

*   [http://www.alsa-project.org/main/index.php/SoundcardTesting](http://www.alsa-project.org/main/index.php/SoundcardTesting)
*   [http://alsa.opensrc.org/Record_from_mic](http://alsa.opensrc.org/Record_from_mic)

### Setting the default microphone/capture device

Some applications (Pidgin, Adobe Flash) do not provide an option to change the capture device. It becomes a problem if your microphone is on a separate device (e.g. USB webcam or microphone) than your internal sound card. To change only the default capture device, leaving the default playback device as is, you can modify your `~/.asoundrc` file to include the following:

```
pcm.usb
{
    type hw
    card U0x46d0x81d
}

pcm.!default
{
    type asym
    playback.pcm
    {
        type plug
        slave.pcm "dmix"
    }
    capture.pcm
    {
        type plug
        slave.pcm "usb"
    }
}

```

Replace "U0x46d0x81d" with your capture device's card name in ALSA. You can use `arecord -L` to list all the capture devices detected by ALSA.

### Internal microphone not working

First make sure the volume is enabled under the `Capture` view in *alsamixer*. In some case, the "Internal Microphone" is not displayed in the capture list available when pressing F4\. If so, specifying the card number given by `aplay -l` to start *alsamixer* (for example `alsamixer -c 0` ) can make it appear.

Then add the following to `/etc/modprobe.d/snd-hda-intel.conf`:

```
options snd-hda-intel enable_msi=1

```

Then reload the module:

```
# rmmod snd-hda-intel && modprobe snd-hda-intel

```

Now there should be an additional input under the previously mentioned `Capture` view.

### Crackling microphone

If you are getting a crackling or popping from your microphone that cannot be resolved with ALSA settings or cleaning your microphone jack, try adding the following line to `/etc/modprobe.d/modprobe.conf`:

```
options snd-hda-intel model=MODEL position_fix=3

```

This option will fix crackling on pure ALSA, but will cause issues to pulseaudio. To let Pulse use these settings effectively, edit `/etc/pulse/default.pa` and find this line:

```
load-module module-udev-detect

```

And change it to this:

```
load-module module-udev-detect tsched=0

```

See the DMA-Position Problem in the kernel docs.

*   [HD-audio Kernel Docs](https://www.kernel.org/doc/Documentation/sound/alsa/HD-Audio.txt)

## Audio Quality

### Crackling sound through mini-jack (headphones connector)

Whether you followed [simultaneous output tip](/index.php/Advanced_Linux_Sound_Architecture#Simultaneous_output "Advanced Linux Sound Architecture") or managed to get it done on your own, you might get crackling sound through headphones or external speakers. This can be fixed by muting **or** setting volume to 0% on item **Mic**. Use `alsamixer` or `amixer`:

```
$ amixer sset "Mic" 0%
$ amixer sset "Mic" mute

```

### Popping sound after resuming from suspension

You might hear a popping sound after resuming the computer from suspension. This can be fixed by editing `/etc/pm/sleep.d/90alsa` and removing the line that says `aplay -d 1 /dev/zero`

### Sound skipping during playback

Run *alsamixer*, and if channels exist for nonexistent output devices then disable them (e.g. *alsamixer* showing a center speaker but you not having one).

### Poor sound quality or clipping

If you experience poor sound quality, try setting the PCM volume (in alsamixer) to a level such that gain is 0.

If snd-usb-audio driver has been loaded, you could try to enable `softvol` in `/etc/asound.conf` file. Example configuration for the first audio device:

```
pcm.!default {
    type plug
    slave.pcm "softvol"
}
pcm.dmixer {
    type dmix
    ipc_key 1024
    slave {
        pcm "hw:0"
        period_size 4096
        buffer_size 131072
        rate 50000
    }
    bindings {
        0 0
        1 1
    }
}
pcm.dsnooper {
    type dsnoop
    ipc_key 1024
    slave {
        pcm "hw:0"
        channels 2
        period_size 4096
        buffer_size 131072
        rate 50000
    }
    bindings {
        0 0
        1 1
        }
}
pcm.softvol {
  type softvol
  slave { pcm "dmixer" }
  control {
    name "Master"
    card 0
  }
}
ctl.!default {
  type hw
  card 0
}
ctl.softvol {
  type hw
  card 0
}
ctl.dmixer {
  type hw
  card 0
}
```

### Pops when starting and stopping playback

Some modules (e.g. snd_ac97_codec and snd_hda_intel) can power off your sound card when not in use. This can make an audible noise (like a crack/pop/scratch) when turning on/off your sound card. Sometimes even when move the slider volume, or open and close windows (KDE4). If you find this annoying try `modinfo snd_MY_MODULE`, and look for a module option that adjusts or disables this feature.

*Example*: disable the power saving mode and solve cracking sound trough speakers problem, using snd_hda_intel add in `/etc/modprobe.d/modprobe.conf`:

```
options snd_hda_intel power_save=0

```

or:

```
options snd_hda_intel power_save=0 power_save_controller=N

```

You can also try it with `modprobe snd_hda_intel power_save=0` before.

You may also have to unmute the 'Line' ALSA channel for this to work. Any value will do (other than '0' or something too high).

*Example:* on an onboard VIA VT1708S (using the snd_hda_intel module) these cracks occured even though 'power_save' was set to 0\. Unmuting the 'Line' channel and setting a value of '1' solved the problem.

Source: [https://www.kernel.org/doc/Documentation/sound/alsa/powersave.txt](https://www.kernel.org/doc/Documentation/sound/alsa/powersave.txt)

If you use a laptop, pm-utils will change `power_save` back to 1 when you go onto battery power even if you disable power saving in `/etc/modprobe.d`. Disable this for pm-utils by disabling the script that makes the change (see [Disabling a hook](/index.php/Pm-utils#Disabling_a_hook "Pm-utils") for more information):

```
# touch /etc/pm/power.d/intel-audio-powersave

```

### Sound skipping while using dynamic CPU frequency scaling

Some combinations of ALSA drivers and chipsets may cause audio from all sources to skip when used in combination with a dynamic frequency scaling governor such as `ondemand` or `conservative`. Currently, the solution is to switch back to the `performance` governor.

Refer to the [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") for more information.

## Hardware and Cards

### Verifying output parameters

Check the contents of `/proc/asound/cardX/pcmYp/subZ/hw_params`, where `X`, `Y`, and `Z` are system dependent. In order to find this file, execute the following command while outputting anything via ALSA:

```
$ find /proc/asound/ -name hw_params | xargs -I FILE grep -v -l "closed" FILE | grep '/proc/asound/card./pcm.p/sub./hw_params'

```

If nothing is playing there should be no results.

Here is an example output for audio with a [bit depth](https://en.wikipedia.org/wiki/Audio_bit_depth "wikipedia:Audio bit depth") of 24 bits and a [sampling frequency](https://en.wikipedia.org/wiki/Sampling_frequency "wikipedia:Sampling frequency") of 44.1 kilohertz:

 `cat /proc/asound/card1/pcm0p/sub0/hw_params` 
```
access: RW_INTERLEAVED
format: S24_3LE
subformat: STD
channels: 2
rate: 44100 (44100/1)
period_size: 5513
buffer_size: 22050

```

More info is available in the [ALSA documentation](http://alsa.opensrc.org/Proc_asound_documentation).

### Error 'Unknown hardware' appears after kernel update

The following messages may be displayed during ALSA's initialization:

```
Unknown hardware "foo" "bar" ...
Hardware is initialized using a guess method
/usr/bin/alsactl: set_control:nnnn:failed to obtain info for control #mm (No such file or directory)

```

or:

```
Found hardware: "HDA-Intel" "VIA VT1705" "HDA:11064397,18490397,00100000" "0x1849" "0x0397"
Hardware is initialized using a generic method
/usr/bin/alsactl: set_control:1328: failed to obtain info for control #1 (No such file or directory)
/usr/bin/alsactl: set_control:1328: failed to obtain info for control #2 (No such file or directory)
/usr/bin/alsactl: set_control:1328: failed to obtain info for control #25 (No such file or directory)
/usr/bin/alsactl: set_control:1328: failed to obtain info for control #26 (No such file or directory)

```

Simply store ALSA mixer settings again:

```
# alsactl -f /var/lib/alsa/asound.state store

```

It may be necessary configure ALSA again with alsamixer

### Fix wrong audio pin mapping

If the mappings to your audio pins(plugs) do not correspond but ALSA works fine, you could try HDA Analyzer -- a pyGTK2 GUI for HD-audio control can be found [at the ALSA wiki](http://www.alsa-project.org/main/index.php/HDA_Analyzer). Try tweaking the Widget Control section of the PIN nodes, to make microphones IN and headphone jacks OUT. Referring to the Config Defaults heading is a good idea.

**Note:** The script is incompatible with Python 3, which is the default Python implementation on Arch Linux. In order to use the script, replace all occurrences of `python` in the `run.py` file with `python2` to point the script to the Python 2 version. Then make the script [executable](/index.php/Chmod "Chmod") and run it.

### S/PDIF output does not work

If the optical/coaxial digital output of your motherboard/sound card is not working or stopped working, and have already enabled and unmuted it in alsamixer, try running the following:

```
$ iecset audio on

```

You can also put this command in an enabled [systemd](/index.php/Systemd "Systemd") service as it sometimes it may stop working after a reboot.

### Conflicting PC speaker

If you are sure nothing is muted, that your drivers are installed correctly, and that your volume is right, but you still do not hear anything, then try adding the following line to `/etc/modprobe.d/modprobe.conf`:

```
options snd-NAME-OF-MODULE ac97_quirk=0

```

The above fix has been observed to work with `via82xx`

```
options snd-NAME-OF-MODULE ac97_quirk=1

```

The above fix has been reported to work with `snd-intel8x0`

### HP TX2500

Add these 2 lines into `/etc/modprobe.d/modprobe.conf`:

```
options snd-cmipci mpu_port=0x330 fm_port=0x388
options snd-hda-intel index=0 model=toshiba position_fix=1
options snd-hda-intel model=hp (works for tx2000cto)

```

### No sound when S/PDIF video card is installed

Discover available modules and their order:

 `$ cat /proc/asound/modules` 
```
 0 snd_hda_intel
 1 snd_ca0106

```

Disable the undesired video card audio codec in `/etc/modprobe.d/modprobe.conf`:

 `/etc/modprobe.d/modprobe.conf` 
```
install snd_hda_intel /bin/false

```

If both devices use the same module then we can use the `enable` parameter from snd_hda_intel module; it is an array of booleans that can enable/disable the desired sound card.

```
options snd_hda_intel enable=1,0

```

### Wrong sound card model type

Although ALSA detects your soundcard through the BIOS, at times ALSA may not be able to recognize your [model type](http://www.kernel.org/doc/Documentation/sound/alsa/HD-Audio-Models.txt). The soundcard chip can be found in `alsamixer` (e.g. ALC662) and the model can be set in `/etc/modprobe.d/modprobe.conf` or `/etc/modprobe.d/sound.conf`. For example:

```
options snd-hda-intel model=MODEL

```

There are other model settings too. For most cases ALSA defaults will do. If you want to look at more specific settings for your soundcard take a look at the [ALSA Soundcard List](http://bugtrack.alsa-project.org/main/index.php/Matrix:Main) find your model, then Details, then look at the "Setting up modprobe..." section. Enter these values in `/etc/modprobe.d/modprobe.conf`. For example, for an Intel AC97 audio:

```
# ALSA portion
alias char-major-116 snd
alias snd-card-0 snd-intel8x0
# module options should go here

# OSS/Free portion
alias char-major-14 soundcore
alias sound-slot-0 snd-card-0

# card #1
alias sound-service-0-0 snd-mixer-oss
alias sound-service-0-1 snd-seq-oss
alias sound-service-0-3 snd-pcm-oss
alias sound-service-0-8 snd-seq-oss
alias sound-service-0-12 snd-pcm-oss

```

### Intel onboard sound

#### No sound with onboard Intel sound card

There may be a problem with two conflicting modules loaded, namely `snd-intel8x0` and `snd-intel8x0m`. In this case, blacklist `snd-intel8x0m`:

 `/etc/modprobe.d/modprobe.conf`  `blacklist snd-intel8x0m` 

*Muting* the "External Amplifier" in `alsamixer` or `amixer` may also help. See [the ALSA wiki](http://alsa.opensrc.org/Intel8x0#Dell_Inspiron_8600_.28and_probably_others.29).

Unmuting the "Mix" setting in the mixer might help, also.

#### No headphone sound with onboard intel sound card

With **Intel Corporation 82801 I (ICH9 Family) HD Audio Controller** on laptop, you may need to add this line to modprobe or sound.conf:

```
options snd-hda-intel model=*model*

```

Where *model* is any one of the following:

*   dell-m6
*   dell-vostro
*   generic
*   laptop
*   laptop-hpsense
*   olpc-xo-1_5

**Note:** It may be necessary to put this "options" line below (after) any "alias" lines about your card.

You can see all the available models in the kernel documentation. For example [here](http://git.kernel.org/cgit/linux/kernel/git/stable/linux-stable.git/tree/Documentation/sound/alsa/HD-Audio-Models.txt), but check that it is the correct version of that document for your kernel version.

A list of available models is also available [here](http://www.mjmwired.net/kernel/Documentation/sound/alsa/HD-Audio-Models.txt). To know your chip name type the following command (with * being corrected to match your files). Note that some chips could have been renamed and do not directly match the available ones in the file.

```
$ grep Codec /proc/asound/card*/codec*

```

Note that there is a high chance none of the input devices (all internal and external mics) will work if you choose to do this, so it is either your headphones or your mic. Please report to ALSA if you are affected by this bug.

And also, if you have problems getting beeps to work (pcspkr):

```
options snd-hda-intel model=$model enable=1 index=0

```

### HDMI

#### HDMI Output does not work

The procedure described below can be used to test HDMI audio. Before proceeding, make sure you have enabled and unmuted the output with `alsamixer`.

**Note:** If you are using an AMD card a necessary kernel module is disabled by default. See [ATI#HDMI audio](/index.php/ATI#HDMI_audio "ATI").

Connect your PC to the Display via HDMI cable and enable the display with [xrandr](/index.php/Xrandr "Xrandr").

Use `aplay -l` to get the discover the card and device number. For example:

 `$ aplay -l` 
```
**** List of PLAYBACK Hardware Devices ****
card 0: SB [HDA ATI SB], device 0: ALC892 Analog [ALC892 Analog]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 0: SB [HDA ATI SB], device 1: ALC892 Digital [ALC892 Digital]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
**card 1**: Generic [HD-Audio Generic], **device 3**: HDMI 0 [HDMI 0]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
```

Send sound to the device. Following the example in the previous step, you would send sound to `**card 1**`, `**device 3**`:

```
$ aplay -D plughw:1,3 /usr/share/sounds/alsa/Front_Center.wav

```

If aplay does not output any errors, but still no sound is heard, "reboot" the receiver, monitor or tv set. Since the HDMI interface executes a handshake on connection, it might have noticed before that there was no audio stream embedded, and disabled audio decoding. If you are using a standalone window manager, you may need to have sound playing while plugging in the HDMI cable.

mplay and other application could be configured to use special HDMI device as audio output. But flashplugin could only use default device. The following method is used to override default device. But you need to change it back when your TV is disconnected from HDMI port.

If the test is successful, create or edit your `~/.asoundrc` file to set HDMI as the default audio device.

 `~/.asoundrc` 
```
pcm.!default {
    type hw
    card 1
    device 3
}

```

Or if the above configuration does not work try:

 `~/.asoundrc` 
```
defaults.pcm.card 1
defaults.pcm.device 3
defaults.ctl.card 1

```

#### PCM through HDMI does not work (Intel Gfx)

As of Linux 3.1 multi-channel PCM output through HDMI with a Intel card (Intel Eaglelake, IbexPeak/Ironlake,SandyBridge/CougarPoint and IvyBridge/PantherPoint) is not yet supported. Support for it has been recently added and expected to be available in Linux 3.2\. To make it work in Linux 3.1 you need to apply the following patches:

*   [drm: support routines for HDMI/DP ELD](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=patch;h=76adaa34db407f174dd06370cb60f6029c33b465)
*   [drm/i915: pass ELD to HDMI/DP audio driver](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=patch;h=e0dac65ed45e72fe34cc7ccc76de0ba220bd38bb)

#### HDMI 5.1 sound goes to wrong speakers

Sound can be redirected to the intended speakers using ALSA's `remap` function. To do so, add the following to `/etc/asound.conf`:

```
pcm.!hdmi-remap {
    type asym
    playback.pcm {
        type plug
        slave.pcm "remap-surround51"
    }
}

pcm.!remap-surround51 {
    type route
    slave.pcm "hw:0,3"
    ttable {
        0.0= 1
        1.1= 1
        2.4= 1
        3.5= 1
        4.2= 1
        5.3= 1
    }
}
```

## Applications

### SDL: No sound with SDL applications

If you get no sound using SDL based applications, try setting the [environment variable](/index.php/Environment_variable "Environment variable") `SDL_AUDIODRIVER` to `alsa`.

### OpenAL: No sound in applications that use OpenAL

Openal defaults to pulseaudio, to change the order, add the following configuration to `/etc/openal/alsoft.conf`:

 `drivers=alsa,pulse` 

### VirtualBox: Virtual machine has no sound

If you experience problems with VirtualBox, the following command might be helpful:

 `$ alsactl init` 
```
Found hardware: "ICH" "SigmaTel STAC9700,83,84" "AC97a:83847600" "0x8086" "0x0000"
Hardware is initialized using a generic method
```

You might need to activate the ALSA output in your audio software as well. You might also try selecting different sound devices in your virtual machine settings to find one that works.

### Others: General application problems

For other applications who insist on their own audio setup, e.g., XMMS or MPlayer, you would need to set their specific options.

For [MPlayer](/index.php/MPlayer "MPlayer") or [mpv](/index.php/Mpv "Mpv"), add the following line to the respective configuration file:

```
ao=alsa

```

Eg. for XMMS2, go into their options and make sure the sound driver is set to ALSA, not oss.

To do this in XMMS:

*   Open XMMS
    *   Options > Preferences.
    *   Choose the ALSA output plugin.

For applications which do not provide a ALSA output, you can use aoss from the alsa-oss package. To use aoss, when you run the program, prefix it with `aoss`, e.g.:

```
aoss realplay

```

pcm.!default{ ... } doesnt work for me anymore. but this does:

```
pcm.default pcm.dmixer

```

## Other Issues

### Simultaneous playback problems

If you are having problems with simultaneous playback, and if [PulseAudio](/index.php/PulseAudio "PulseAudio") is installed, its default configuration is set to "hijack" the soundcard. Some users of ALSA may not want to use [PulseAudio](/index.php/PulseAudio "PulseAudio") and are quite content with their current ALSA settings. One fix is to edit `/etc/asound.conf` and comment out the following lines:

```
# Use PulseAudio by default
pcm.!default {
    type pulse
    fallback "sysdefault"
    hint {
        show on
        description "Default ALSA Output (currently PulseAudio Sound Server)"
    }
}
```

Commenting the following out also may help:

```
ctl.!default {
    type pulse
    fallback "sysdefault"
}
```

This may be a much simpler solution than completely uninstalling [PulseAudio](/index.php/PulseAudio "PulseAudio").

Effectively, here is an example of a working `/etc/asound.conf`:

```
pcm.dmixer {
    type dmix
    ipc_key 1024
    ipc_key_add_uid 0
    ipc_perm 0660
}
pcm.dsp {
    type plug
    slave.pcm "dmix"
}
```

**Note:** This `/etc/asound.conf` file was intended for and used successfully with a global [MPD](/index.php/MPD "MPD") configuration. See [#Problems with availability to only one user at a time](#Problems_with_availability_to_only_one_user_at_a_time).

### Removing old ALSA state file (asound.state)

The [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) package provides `alsa-store.service` which automatically stores the current ALSA state to `/var/lib/alsa/asound.state` upon system shutdown. This can be problematic for users who are trying to reset their current ALSA state as the `asound.state` file will be recreated with the current state upon every shutdown (e.g., attempting to remove user-defined channels from the mixer). The `alsa-store.service` service may be temporarily disabled by creating the following empty file:

```
# mkdir -p /etc/alsa
# touch /etc/alsa/state-daemon.conf

```

The presence of `state-daemon.conf` prevents `alsa-store.service` from saving `asound.state` during shutdown. After disabling this service, the `asound.state` file may be removed as such:

```
# rm /var/lib/alsa/asound.state

```

After rebooting, the previous ALSA state should be lost and the current state should be reset to defaults. Re-enable `alsa-store.service` by deleting the condition file we created:

```
# rm /etc/alsa/state-daemon.conf

```

On the next shutdown, the `asound.state` file should be recreated with ALSA defaults. The file may also be generated immediately using:

```
# alsactl store

```

### Problems with availability to only one user at a time

You might find that only one user can use the dmixer at a time. This is probably ok for most, but for those who run [mpd](/index.php/Mpd "Mpd") as a separate user this poses a problem. When mpd is playing a normal user cannot play sounds though the dmixer. While it is quite possible to just run mpd under a user's login account, another solution has been found. Adding the line `ipc_key_add_uid 0` to the `pcm.dmixer` block disables this locking. The following is a snippet from `asound.conf`, the rest is the same as above.

```
...
pcm.dmixer {
    type dmix
    ipc_key 1024
    ipc_key_add_uid 0
    ipc_perm 0660
slave {
 ...
```