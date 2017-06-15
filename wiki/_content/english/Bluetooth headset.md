Currently, Arch Linux supports the A2DP profile (Audio Sink) for remote audio playback with the default installation.

**Note:** Bluez5 dropped the direct integration for [ALSA](/index.php/ALSA "ALSA") and supports [PulseAudio](/index.php/PulseAudio "PulseAudio"). If you do not want to use PulseAudio, you have to use use [bluez-alsa-git](https://aur.archlinux.org/packages/bluez-alsa-git/), as ALSA plugin.

## Contents

*   [1 Headset via Bluez5/PulseAudio](#Headset_via_Bluez5.2FPulseAudio)
    *   [1.1 Configuration via CLI](#Configuration_via_CLI)
        *   [1.1.1 Setting up auto connection](#Setting_up_auto_connection)
    *   [1.2 Configuration via GNOME Bluetooth](#Configuration_via_GNOME_Bluetooth)
    *   [1.3 Troubleshooting](#Troubleshooting)
        *   [1.3.1 Selected audio profile, but headset inactive and audio cannot be redirected](#Selected_audio_profile.2C_but_headset_inactive_and_audio_cannot_be_redirected)
        *   [1.3.2 Pairing fails with AuthenticationFailed](#Pairing_fails_with_AuthenticationFailed)
        *   [1.3.3 Pairing works, but connecting does not](#Pairing_works.2C_but_connecting_does_not)
        *   [1.3.4 Connecting works, but there're sound glitches all the time](#Connecting_works.2C_but_there.27re_sound_glitches_all_the_time)
        *   [1.3.5 Connecting works, but I cannot play sound](#Connecting_works.2C_but_I_cannot_play_sound)
        *   [1.3.6 UUIDs has unsupported type](#UUIDs_has_unsupported_type)
        *   [1.3.7 PC shows device as paired, but is not recognized by device](#PC_shows_device_as_paired.2C_but_is_not_recognized_by_device)
*   [2 Legacy method: ALSA-BTSCO](#Legacy_method:_ALSA-BTSCO)
    *   [2.1 Connecting the headset](#Connecting_the_headset)
        *   [2.1.1 Pairing the headset with your computer](#Pairing_the_headset_with_your_computer)
            *   [2.1.1.1 Using *bluez-gnome*](#Using_bluez-gnome)
            *   [2.1.1.2 Using *passkey-agent*](#Using_passkey-agent)
    *   [2.2 Headset and ALSA Devices](#Headset_and_ALSA_Devices)
    *   [2.3 Headset's multimedia buttons](#Headset.27s_multimedia_buttons)
*   [3 Legacy method: PulseAudio](#Legacy_method:_PulseAudio)
    *   [3.1 Troubleshooting](#Troubleshooting_2)
        *   [3.1.1 Audio sink fails](#Audio_sink_fails)
        *   [3.1.2 Page timeout issue](#Page_timeout_issue)
*   [4 Legacy documentation: ALSA, bluez5 and PulseAudio method](#Legacy_documentation:_ALSA.2C_bluez5_and_PulseAudio_method)
    *   [4.1 Install Software Packages](#Install_Software_Packages)
        *   [4.1.1 Install ALSA and associated libraries](#Install_ALSA_and_associated_libraries)
        *   [4.1.2 Install Bluez5](#Install_Bluez5)
        *   [4.1.3 Install Audacious](#Install_Audacious)
    *   [4.2 Procedure](#Procedure)
        *   [4.2.1 Miscellaneous configuration files](#Miscellaneous_configuration_files)
            *   [4.2.1.1 ALSA /etc/asound.conf](#ALSA_.2Fetc.2Fasound.conf)
            *   [4.2.1.2 /etc/dbus-1/system.d/bluetooth.conf](#.2Fetc.2Fdbus-1.2Fsystem.d.2Fbluetooth.conf)
            *   [4.2.1.3 Tested applications](#Tested_applications)
*   [5 Switch between HSV and A2DP setting](#Switch_between_HSV_and_A2DP_setting)
    *   [5.1 A2DP not working with PulseAudio](#A2DP_not_working_with_PulseAudio)
        *   [5.1.1 Socket interface problem](#Socket_interface_problem)
        *   [5.1.2 A2DP profile is unavailable](#A2DP_profile_is_unavailable)
        *   [5.1.3 Gnome with GDM](#Gnome_with_GDM)
*   [6 Headset via Bluez5/bluez-alsa](#Headset_via_Bluez5.2Fbluez-alsa)
*   [7 See also](#See_also)

## Headset via Bluez5/PulseAudio

PulseAudio 5.x supports A2DP per default. Make sure the following packages are [installed](/index.php/Install "Install"): [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa), [pulseaudio-bluetooth](https://www.archlinux.org/packages/?name=pulseaudio-bluetooth), [bluez](https://www.archlinux.org/packages/?name=bluez), [bluez-libs](https://www.archlinux.org/packages/?name=bluez-libs), [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils). Without [pulseaudio-bluetooth](https://www.archlinux.org/packages/?name=pulseaudio-bluetooth) you will not be able to connect after the next pairing and you will not get any usable error messages.

### Configuration via CLI

[Start](/index.php/Start "Start") the `bluetooth.service` systemd unit.

Now we can use the *bluetoothctl* command line utility to pair and connect. For troubleshooting and more detailed explanations of *bluetoothctl* see the [Bluetooth](/index.php/Bluetooth "Bluetooth") article. Run

```
# bluetoothctl

```

to be greeted by its internal command prompt. Then enter:

```
# power on
# agent on
# default-agent
# scan on

```

Now make sure that your headset is in pairing mode. It should be discovered shortly. For example,

```
[NEW] Device 00:1D:43:6D:03:26 Lasmex LBT10

```

shows a device that calls itself "Lasmex LBT10" and has MAC address *00:1D:43:6D:03:26*. We will now use that MAC address to initiate the pairing:

```
# pair 00:1D:43:6D:03:26

```

After pairing, you also need to explicitly connect the device (every time?):

```
# connect 00:1D:43:6D:03:26

```

If everything works correctly, you now have a separate output device in [PulseAudio](/index.php/PulseAudio "PulseAudio").

**Note:** The device may be off by default. Select its audio profile (*OFF*, A2DP, HFP) in the "Configuration" tab of [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol).

You can now redirect any audio through that device using the "Playback" and "Recording" tabs of [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol).

You can now disable scanning again and exit the program:

```
# scan off
# exit

```

#### Setting up auto connection

To make your headset auto connect you need to enable PulseAudio's switch-on-connect module. Do this by adding the following lines to your the following to your `/etc/pulse/default.pa`:

 `/etc/pulse/default.pa` 
```
# automatically switch to newly-connected devices
load-module module-switch-on-connect

```

Now make *bluetoothctl* trust your Bluetooth headset by running *trust 00:1D:43:6D:03:26* inside the *bluetoothctl* console to prevent errors similar to:

```
bluetoothd[487]: Authentication attempt without agent
bluetoothd[487]: Access denied: org.bluez.Error.Rejected

```

```
[bluetooth]# trust 00:1D:43:6D:03:26

```

By default, your Bluetooth adapter will not power on after a reboot. The former method by using `hciconfig hci0 up` is deprecated, see the [release note](http://www.bluez.org/release-of-bluez-5-35/). Now you just need to add the line `AutoEnable=true` in `/etc/bluetooth/main.conf` at the bottom in the `[Policy]` section:

 `/etc/bluetooth/main.conf` 
```
[Policy]
AutoEnable=true
```

### Configuration via GNOME Bluetooth

**Note:** The A2DP profile will not activate using this method with pulseaudio 9/10 due to an ongoing bug, leading to possible low quality mono sound. see [#A2DP not working with PulseAudio](#A2DP_not_working_with_PulseAudio)

You can use [GNOME Bluetooth](/index.php/Bluetooth#GNOME_Bluetooth "Bluetooth") graphical front-end to easily configure your bluetooth headset.

First, you need to be sure that `bluetooth.service` systemd unit is running.

Open GNOME Bluetooth and activate the bluetooth. After scanning for devices, you can connect to your headset selecting it on the device list. You can directly access to sound configuration panel from the device menu. On the sound panel, a new sink should appear when your device is connected.

### Troubleshooting

**Note:** Many users report frustration with getting A2DP/Bluetooth Headsets to work. see [#Switch between HSV and A2DP setting](#Switch_between_HSV_and_A2DP_setting) for additional information.

#### Selected audio profile, but headset inactive and audio cannot be redirected

Deceptively, this menu is available before the device has been connected; annoyingly it will have no effect. The menu seems to be created as soon as the receiver recognizes the device.

Make sure to run bluetoothctl (with sudo/as root) and connect the device manually. There may be configuration options to remove the need to do this each time, but neither pairing nor trusting induce automatic connecting for me.

#### Pairing fails with AuthenticationFailed

If pairing fails, you can try [disabling SSPMode](https://stackoverflow.com/questions/12888589/linux-command-line-howto-accept-pairing-for-bluetooth-device-without-pin) with:

```
# hciconfig hci0 sspmode 0

```

#### Pairing works, but connecting does not

You might see the following error in *bluetoothctl*:

```
[bluetooth]# connect 00:1D:43:6D:03:26
Attempting to connect to 00:1D:43:6D:03:26
Failed to connect: org.bluez.Error.Failed

```

To further investigate, have a look at the log via one of the following commands:

```
# systemctl status bluetooth
# journalctl -n 20

```

You might see a message like this:

```
bluetoothd[5556]: a2dp-sink profile connect failed for 00:1D:43:6D:03:26: Protocol not available

```

This may be due to the [pulseaudio-bluetooth](https://www.archlinux.org/packages/?name=pulseaudio-bluetooth) package not being installed. Install it if it missing, then restart pulseaudio.

It can also be due to permission, especially if starting pulseaudio as root allows you to connect. Add your user is part of the *lp* group, then restart pulseaudio. See `/etc/dbus-1/system.d/bluetooth.conf` for reference.

If the issue is not due to the missing package, the problem in this case is that PulseAudio is not catching up. A common solution to this problem is to restart PulseAudio. Note that it is perfectly fine to run *bluetoothctl* as root while PulseAudio runs as user. After restarting PulseAudio, retry to connect. It is not necessary to repeat the pairing.

If restarting PulseAudio does not work, you need to load module-bluetooth-discover.

```
# pactl load-module module-bluetooth-discover

```

The same load-module command can be added to `/etc/pulse/default.pa`.

If that still does not work, or you are using PulseAudio's system-wide mode, also load the following PulseAudio modules (again these can be loaded via your default.pa or system.pa):

```
module-bluetooth-policy
module-bluez5-device
module-bluez5-discover

```

#### Connecting works, but there're sound glitches all the time

This is very likely to occur when the bluetooth and the wifi share the same chip as they share the same physical anthena and possibly band range (2.4GHz). Although this works seamlessly on windows, this is not the case on linux. One possible solution is to move your wifi network to 5GHz so that there will be no interference. If your card/router doesn't support this, you can upgrade your wifi drivers/firmware. This approach works on Realtek 8723BE and latest rtl drivers for this chip from AUR.

#### Connecting works, but I cannot play sound

Make sure that you see the following messages in your system log:

```
bluetoothd[5556]: Endpoint registered: sender=:1.83 path=/MediaEndpoint/A2DPSource
bluetoothd[5556]: Endpoint registered: sender=:1.83 path=/MediaEndpoint/A2DPSink

```

If you see a message similar to this, you can go on and investigate your PulseAudio configuration. Otherwise, go back and ensure the connection is successful.

When using [GDM](/index.php/GDM "GDM"), another instance of PulseAudio is started, which "captures" your bluetooth device connection. This can be prevented by [masking](/index.php/Mask "Mask") the pulseaudio socket for the GDM user by doing the following:

```
# mkdir -p ~gdm/.config/systemd/user
# ln -s /dev/null ~gdm/.config/systemd/user/pulseaudio.socket

```

On next reboot the second instance of PulseAudio will not be started.

It may happen that bluez wrongly considers an headset as not a2dp capable. In this case, search the index of the bluetooth device with

```
$ pacmd ls

```

Among the output there should be a section related to the bluetooth headset, containing something similar to

 `pacmd ls` 
```
index: 2
        name: <bluez_card.XX_XX_XX_XX_XX_XX>
        driver: <module-bluez5-device.c>
        owner module: 27
        properties:
                device.description = "SONY MDR-100ABN"
                device.string = "XX:XX:XX:XX:XX:XX"
                device.api = "bluez"
                device.class = "sound"
                ...
```

To manually set the profile, run

```
$ pacmd set-card-profile 2 a2dp_sink

```

where 2 is the index of the device retrieved through `pacmd ls`.

#### UUIDs has unsupported type

During pairing you might see this output in *bluetoothctl*:

```
[CHG] Device 00:1D:43:6D:03:26 UUIDs has unsupported type

```

This message is a very common one and can be ignored.

#### PC shows device as paired, but is not recognized by device

This might be due to the device not supporting bluetooth LE for pairing.

Try setting `ControllerMode = bredr` in `/etc/bluetooth/main.conf`. See [[2]](http://unix.stackexchange.com/questions/292189/pairing-bose-qc-35-over-bluetooth-on-fedora).

## Legacy method: ALSA-BTSCO

It is much easier to set up your bluetooth headset today, with bluez >= 3.16\. You may want to try the out-of-box python script in [this blog](http://fosswire.com/2008/01/11/a2dp-stereo-linux/) (you need edit the script to work with gconftool-2). There is also a piece of equivalent bash script [here](http://lymanrb.blogspot.com/2008/05/linux.html).

You need your headset's bdaddr. It is of the form *12:34:56:78:9A:BC*. Either find it in the documentation of your headset, on the headset itself or with the **hcitool scan** command.

Install [btsco](https://aur.archlinux.org/packages/btsco/).

To load the kernel module, type:

```
# modprobe snd-bt-sco

```

There will now be an extra audio device. Use `alsamixer -cN` (where N is most likely 1) to set the volume. You can access the device with any alsa-capable application by choosing the device *BT headset*, or with any OSS application by using `/dev/dspN` as the audio device.

But to actually get any sound, you have to connect your headset to the computer first.

### Connecting the headset

If you connect your headset for the first time, read the section about pairing first. To connect to your headset to the computer, use the command

```
$ btsco -f <bdaddr>

```

for example

```
$ btsco -f 12:34:56:78:9A:BC

```

#### Pairing the headset with your computer

The first time you connect the headset, you have to pair it with the computer. To do this, you need your headset's PIN. Depending on your headset you may have to reset the headset and repeat the pairing everytime you used the headset with another bluetooth device.

There are two ways to pair your headset with the computer:

##### Using *bluez-gnome*

Install the *bluez-gnome* package from the community repository. Then start the **bt-applet** program. Once you try to connect to the headset, a window will open and ask for the PIN.

##### Using *passkey-agent*

Before connecting to the headset, enter the command

```
$ passkey-agent --default <pin>

```

where *<pin>* is your headset's PIN. Then try to connect to the headset.

### Headset and ALSA Devices

1\. First if you have not already, [install](/index.php/Install "Install") the [bluez](https://www.archlinux.org/packages/?name=bluez) package.

2\. Scan for your device

```
$ hcitool (-i <optional hci#>***) scan

```

3\. Pair your headset with your device:

```
$ bluez-simple-agent (optional hci# ***) XX:XX:XX:XX:XX:XX

```

and put in your pin (0000 or 1234, etc)

4\. Make sure your `/etc/bluetooth/audio.conf` allows A2DP Audio Sinks. Place this line just bellow the [General] heading:

```
Enable=Source,Sink,Media,Socket

```

5\. Add this to your `/etc/asound.conf` file:

```
#/etc/asound.conf

pcm.btheadset {
   type plug
   slave {
       pcm {
           type bluetooth
           device XX:XX:XX:XX:XX:XX 
           profile "auto"
       }   
   }   
   hint {
       show on
       description "BT Headset"
   }   
}
ctl.btheadset {
  type bluetooth
}  

```

6\. Check to see if it has been added to alsa devices

```
$ aplay -L

```

7\. Now play with aplay:

```
$ aplay -D btheadset /path/to/audio/file

```

or Mplayer:

```
$ mplayer -ao alsa:device=btheadset /path/to/audio/or/video/file

```

**Tip:** To find hci# for a usb dongle, type in
```
$ hcitool dev

```

### Headset's multimedia buttons

In order to get your bluetooth headset's multimedia buttons (play, pause, next, previous) working you need to create `/etc/modules-load.d/uinput.conf` containing `uinput`.

## Legacy method: PulseAudio

This one is much easier and more elegant. PulseAudio will seamlessly switch between output devices when the headset is turned on. If you have ALSA as the sound server, you need the following packages installed: [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) and [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa).

Now, to configure the audio output to use bluetooth, just install [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) and run it to configure the audio output:

```
$ pavucontrol

```

Make sure to take a look at the [PulseAudio](/index.php/PulseAudio "PulseAudio") wiki entry for setting up PulseAudio, especially if you are running KDE.

### Troubleshooting

#### Audio sink fails

Bluetooth headset is connected, but ALSA/PulseAudio fails to pick up the connected device. You will get "Audio sink fails". According to [gentoo wiki](http://wiki.gentoo.org/wiki/Bluetooth_Headset), you have to verify than in `/etc/bluetooth/audio.conf` there is `Enable=Socket` under the `[General]` section heading.

Just do a `# systemctl restart bluetooth` to apply it.

#### Page timeout issue

If you receive this error whilst trying to pair your headset with your system using bluez-simple-agent, then you can try to restart your system and use the graphical bluez applet of your desktop environment.

## Legacy documentation: ALSA, bluez5 and PulseAudio method

[ALSA](/index.php/ALSA "ALSA"), [bluez5](/index.php/Bluez "Bluez"), and [PulseAudio](/index.php/PulseAudio "PulseAudio") work together to allow a wireless [Bluetooth](/index.php/Bluetooth "Bluetooth") headset to play audio. The following method works with a Lenovo T61p laptop and SoundBot SB220 wireless bluetooth headset. The required software stack is extensive and failure to include all components can produce errors which are difficult to understand. The following list of software packages might not be the minimum required set and needs to be examined more closely.

Bluez5 has a regression causing HSP/HFP Telephone profile to not be available. This regression is documented in the [draft release notes for Pulseaudio 5.0](http://www.freedesktop.org/wiki/Software/PulseAudio/Notes/5.0/) which say (in "Notes for packagers"): "PulseAudio now supports BlueZ 5, but only the A2DP profile. BlueZ 4 is still the only way to make HSP/HFP work." ([from here](https://fedoraproject.org/wiki/Common_F20_bugs#bluez5-profile))

### Install Software Packages

The core software components are [ALSA](/index.php/ALSA "ALSA"), Bluez5, [PulseAudio](/index.php/PulseAudio "PulseAudio"). However there are additional libraries which are required. As well as a player which can play audio files. The following section lists the software packages installed in order to connect the headset and play audio over the headset.

#### Install ALSA and associated libraries

[ALSA](/index.php/ALSA "ALSA") works with the linux kernel to provide audio services to user mode software. The following packages are used with the [Bluetooth](/index.php/Bluetooth "Bluetooth") headset: [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils), [alsa-plugins](https://www.archlinux.org/packages/?name=alsa-plugins), [alsa-tools](https://www.archlinux.org/packages/?name=alsa-tools).

#### Install Bluez5

Bluez5 is the latest [Bluetooth](/index.php/Bluetooth "Bluetooth") stack. It is required for [PulseAudio](/index.php/PulseAudio "PulseAudio") to interface with wireless headsets. Required packages: [bluez](https://www.archlinux.org/packages/?name=bluez), [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils), [bluez-libs](https://www.archlinux.org/packages/?name=bluez-libs).

#### Install Audacious

[Audacious](/index.php/Audacious "Audacious") is a program which plays audio files. It can work directly with [ALSA](/index.php/ALSA "ALSA") or with [PulseAudio](/index.php/PulseAudio "PulseAudio"). Required packages: [audacious](https://www.archlinux.org/packages/?name=audacious), [audacious-plugins](https://www.archlinux.org/packages/?name=audacious-plugins).

### Procedure

Once the required packages are installed, use this procedure to play audio with a bluetooth headset. The high level overview of the procedure is to pair the headset, connect the headset, configure the player and pulse audio controller and then play audio.

Start the bluetooth service as root:

```
# systemctl start bluetooth

```

Verify Bluetooth is started

```
# systemctl status bluetooth
bluetooth.service - Bluetooth service
  Loaded: loaded (/usr/lib/systemd/system/bluetooth.service; disabled)
  Active: active (running) since Sat 2013-12-07 12:31:14 PST; 12s ago
    Docs: man:bluetoothd(8)
Main PID: 3136 (bluetoothd)
  Status: "Running"
  CGroup: /system.slice/bluetooth.service
          └─3136 /usr/lib/bluetooth/bluetoothd

Dec 07 12:31:14 t61p systemd[1]: Starting Bluetooth service...
Dec 07 12:31:14 t61p bluetoothd[3136]: Bluetooth daemon 5.11
Dec 07 12:31:14 t61p systemd[1]: Started Bluetooth service.
Dec 07 12:31:14 t61p bluetoothd[3136]: Starting SDP server
Dec 07 12:31:14 t61p bluetoothd[3136]: Bluetooth management interface 1.3 i...ed
Hint: Some lines were ellipsized, use -l to show in full.

```

Start the PulseAudio daemon. This must be done after X windows is started and as a normal user.

```
$ pulseaudio -D

```

Verify the PulseAudio daemon is running.

```
$ pulseaudio --check -v
I: [pulseaudio] main.c: Daemon running as PID 3186

```

Start up bluetoothctl as root and pair and connect your headset. As a regular user, bluetoothctl will pair but not connect. Perhaps this is related to the config file (shown below) which is setup for what appears to be the root user. Note: the procedure shown below is for an initial pair and connect of the headphone. If the headset is already paired, then the procedure below can be shortened to: power on, agent on, default-agent, connect <mac address>. The mac address can be seen from the devices command output.

```
 $ bluetoothctl 
 [NEW] Controller 00:1E:4C:F4:98:5B t61p-0 [default]
 [NEW] Device 00:1A:7D:12:36:B9 SoundBot SB220
 [bluetooth]# show
 Controller 00:1E:4C:F4:98:5B
       Name: t61p
       Alias: t61p-0
       Class: 0x000000
       Powered: no
       Discoverable: no
       Pairable: yes
       UUID: PnP Information           (00001200-0000-1000-8000-00805f9b34fb)
       UUID: Generic Access Profile    (00001800-0000-1000-8000-00805f9b34fb)
       UUID: Generic Attribute Profile (00001801-0000-1000-8000-00805f9b34fb)
       UUID: A/V Remote Control        (0000110e-0000-1000-8000-00805f9b34fb)
       UUID: A/V Remote Control Target (0000110c-0000-1000-8000-00805f9b34fb)
       UUID: Audio Source              (0000110a-0000-1000-8000-00805f9b34fb)
       UUID: Audio Sink                (0000110b-0000-1000-8000-00805f9b34fb)
       Modalias: usb:v1D6Bp0246d050B
       Discovering: no
 [bluetooth]# power on
 [CHG] Controller 00:1E:4C:F4:98:5B Class: 0x0c010c
 Changing power on succeeded
 [CHG] Controller 00:1E:4C:F4:98:5B Powered: yes
 [bluetooth]# agent on
 Agent registered
 [bluetooth]# default-agent
 Default agent request successful

```

<power on your headset in pairing mode. Eventually you will see what appears to be a mac address.>

```
 [bluetooth]# scan on
 Discovery started
 [CHG] Controller 00:1E:4C:F4:98:5B Discovering: yes
 [CHG] Device 00:1A:7D:12:36:B9 RSSI: -61
 [bluetooth]# pair 00:1A:7D:12:36:B9
 Attempting to pair with 00:1A:7D:12:36:B9
 [CHG] Device 00:1A:7D:12:36:B9 Connected: yes
 [CHG] Device 00:1A:7D:12:36:B9 UUIDs has unsupported type
 [CHG] Device 00:1A:7D:12:36:B9 Paired: yes
 Pairing successful
 [bluetooth]# connect 00:1A:7D:12:36:B9
 [CHG] Device 00:1A:7D:12:36:B9 Connected: yes
 Connection successful
 [bluetooth]# info 00:1A:7D:12:36:B9
 Device 00:1A:7D:12:36:B9
       Name: SoundBot SB220
       Alias: SoundBot SB220
       Class: 0x240404
       Icon: audio-card
       Paired: yes
       Trusted: no
       Blocked: no
       Connected: yes
       LegacyPairing: yes
       UUID: Headset                   (00001108-0000-1000-8000-00805f9b34fb)
       UUID: Audio Sink                (0000110b-0000-1000-8000-00805f9b34fb)
       UUID: A/V Remote Control Target (0000110c-0000-1000-8000-00805f9b34fb)
       UUID: A/V Remote Control        (0000110e-0000-1000-8000-00805f9b34fb)
       UUID: Handsfree                 (0000111e-0000-1000-8000-00805f9b34fb)

```

Start up alsamixer, for simplicity un-mute all your outputs. Oddly enough some can be muted though. The ones I had muted during playback were:

*   Headphones
*   SPIDF

Start up audacious. Use the menu to select PulseAudio as your output. Somewhere I read that bluez5 requires pulseaudio-git and this jives with my experience.

Start up pavucontrol in a terminal. In the Outputs tab select the bluetooth headset.

[screenshot of application settings](http://netskink.blogspot.com/2013/12/pulseaudio-pavucontrol-and-audacious.html)

#### Miscellaneous configuration files

For reference, these settings were also done.

##### ALSA /etc/asound.conf

The settings shown at the top of this page was used, but the additional modification for Intel laptop sound cards.

```
pcm.btheadset {
  type plug
  slave {
    pcm {
      type bluetooth
      device 00:1A:7D:12:36:B9
      profile "auto"
    }
  }
  hint {
    show on
    description "BT Headset"
  }
}
ctl.btheadset {
  type bluetooth
}
options snd-hda-intel model=laptop

```

##### /etc/dbus-1/system.d/bluetooth.conf

The settings here seem to be enabled for root only. See the policy user="root" section. However, if a regular user is specified here, the system fails to start. Someone with more knowledge could explain why.

 `/etc/dbus-1/system.d/bluetooth.conf` 
```
<!-- This configuration file specifies the required security policies for Bluetooth core daemon to work. -->

<!DOCTYPE busconfig PUBLIC "-//freedesktop//DTD D-BUS Bus Configuration 1.0//EN"
  "http://www.freedesktop.org/standards/dbus/1.0/busconfig.dtd">
<busconfig>

  <!-- ../system.conf have denied everything, so we just punch some holes -->

  <policy user="root">
    <allow own="org.bluez"/>
    <allow send_destination="org.bluez"/>
    <allow send_interface="org.bluez.Agent1"/>
    <allow send_interface="org.bluez.MediaEndpoint1"/>
    <allow send_interface="org.bluez.MediaPlayer1"/>
    <allow send_interface="org.bluez.ThermometerWatcher1"/>
    <allow send_interface="org.bluez.AlertAgent1"/>
    <allow send_interface="org.bluez.Profile1"/>
    <allow send_interface="org.bluez.HeartRateWatcher1"/>
    <allow send_interface="org.bluez.CyclingSpeedWatcher1"/>
  </policy>

  <policy at_console="true">
    <allow send_destination="org.bluez"/>
  </policy>

  <!-- allow users of lp group (printing subsystem) to communicate with bluetoothd -->
  <policy group="lp">
    <allow send_destination="org.bluez"/>
  </policy>

  <policy context="default">
    <deny send_destination="org.bluez"/>
  </policy>

</busconfig>

```

##### Tested applications

As noted above this will work easily with audacious. YouTube videos with Chromium and Flash Player will work on some videos. If the video has ads it will not work, but if the video does not have ads it will work. Just make sure that after audacious is working with Bluetooth headset, start Chromium, and navigate to YouTube. Find a video without leading ads, and it should play the audio. If the settings icon has the a menu with two drop-down combo boxes for Speed and Quality it will play.

## Switch between HSV and A2DP setting

This can easily be achieved by the following command where 2 needs to be changed with the correct device number.

```
pacmd set-card-profile 2 a2dp_sink

```

### A2DP not working with PulseAudio

#### Socket interface problem

If PulseAudio fails when changing the profile to A2DP with bluez 4.1+ and PulseAudio 3.0+, you can try disabling the Socket interface from `/etc/bluetooth/audio.conf` by removing the line `Enable=Socket` and adding line `Disable=Socket`.

#### A2DP profile is unavailable

As of Pulseaudio 10.0, when connecting to headset via Bluedevil or similar, A2DP profile is unavailable. As mentioned in [bug 92102](https://bugs.freedesktop.org/show_bug.cgi?id=92102) discussion, a workaround is connecting to a headset via bluetoothctl

```
bluetoothctl
connect [headset MAC here]

```

#### Gnome with GDM

**Note:** Below was tested with Gnome 3.22.1 and PulseAudio 10.0

If PulseAudio fails when changing the profile to A2DP while using GNOME with GDM, you need to prevent GDM from starting its own instance of PulseAudio :

*   Prevent Pulseaudio clients from automatically starting a server if one is not running by adding the following lines to `/var/lib/gdm/.config/pulse/client.conf` :

```
autospawn = no
daemon-binary = /bin/true
```

*   Prevent systemd from starting Pulseaudio anyway with socket activation :

```
sudo -ugdm mkdir -p /var/lib/gdm/.config/systemd/user
sudo -ugdm ln -s /dev/null /var/lib/gdm/.config/systemd/user/pulseaudio.socket

```

*   Restart, and check that there is no Pulseaudio process for the `gdm` user.

**Note:** Discussion about this problem can be found [here](https://bbs.archlinux.org/viewtopic.php?id=194006) and [here](https://bbs.archlinux.org/viewtopic.php?id=196689)

## Headset via Bluez5/bluez-alsa

This approach should be used only if you cannot or do not want to use PulseAudio that is the status quo.

First of all ensure your headset is correctly paired and connected to the system, this implies the same steps that using PulseAudio, for example using `bluetoothctl`.

Install [bluez-alsa-git](https://aur.archlinux.org/packages/bluez-alsa-git/), start and possibly enable the `bluealsa` service.

Edit the file `/etc/dbus-1/system.d/bluetooth.conf` and add this lines to the bottom, just before the closing `</busconfig>`.

```
<policy user="bluealsa">
  <allow send_destination="org.bluez"/>
</policy>

```

Finally to let the `bluealsa` work your user must be part of the `audio` group.

You can now test if everything works fine, replace your MAC as necessary:

```
 aplay -D bluealsa:HCI=hci0,DEV=00:1D:43:6D:03:26,PROFILE=a2dp ./testme.wav

```

If it does you can set up HCI, DEV, and PROFILE as default. Add this lines to your `.asoundrc`:

```
defaults.bluealsa {
    interface "hci0"
    device "00:1D:43:6D:03:26"
    profile "a2dp"
}

```

You can now use the device bluealsa to reach your headset. You can also use `alsamixer` to setup the volumes, as `alsamixer -D bluealsa`.

## See also

Using the same device on Windows and Linux without pairing the device over and over again

*   [Dual booting with a Bluetooth keyboard](http://ubuntuforums.org/showthread.php?p=9363229#post9363229)