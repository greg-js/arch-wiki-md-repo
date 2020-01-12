Related articles

*   [Bluetooth](/index.php/Bluetooth "Bluetooth")

Currently, Arch Linux supports the A2DP profile (Audio Sink) for remote audio playback with the default installation.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Headset via Bluez5/PulseAudio](#Headset_via_Bluez5/PulseAudio)
    *   [1.1 Configuration via CLI](#Configuration_via_CLI)
        *   [1.1.1 Setting up auto connection](#Setting_up_auto_connection)
        *   [1.1.2 Media controls](#Media_controls)
    *   [1.2 Configuration via GNOME Bluetooth](#Configuration_via_GNOME_Bluetooth)
    *   [1.3 LDAC/aptX](#LDAC/aptX)
    *   [1.4 Troubleshooting](#Troubleshooting)
        *   [1.4.1 Bad sound / Static noise / "Muddy" sound](#Bad_sound_/_Static_noise_/_"Muddy"_sound)
        *   [1.4.2 Selected audio profile, but headset inactive and audio cannot be redirected](#Selected_audio_profile,_but_headset_inactive_and_audio_cannot_be_redirected)
        *   [1.4.3 Pairing fails with AuthenticationFailed](#Pairing_fails_with_AuthenticationFailed)
        *   [1.4.4 Pairing works, but connecting does not](#Pairing_works,_but_connecting_does_not)
        *   [1.4.5 Connecting works, but there are sound glitches all the time](#Connecting_works,_but_there_are_sound_glitches_all_the_time)
        *   [1.4.6 Connecting works, but I cannot play sound](#Connecting_works,_but_I_cannot_play_sound)
        *   [1.4.7 Connecting works, sound plays fine until headphones become idle, then stutters](#Connecting_works,_sound_plays_fine_until_headphones_become_idle,_then_stutters)
        *   [1.4.8 UUIDs has unsupported type](#UUIDs_has_unsupported_type)
        *   [1.4.9 PC shows device as paired, but is not recognized by device](#PC_shows_device_as_paired,_but_is_not_recognized_by_device)
        *   [1.4.10 Device connects, then disconnects after a few moments](#Device_connects,_then_disconnects_after_a_few_moments)
        *   [1.4.11 Apple Airpods have low volume](#Apple_Airpods_have_low_volume)
        *   [1.4.12 HSP problem: the bluetooth sink and source are created, but no audio is being transmitted](#HSP_problem:_the_bluetooth_sink_and_source_are_created,_but_no_audio_is_being_transmitted)
*   [2 Headset via Bluez5/bluez-alsa](#Headset_via_Bluez5/bluez-alsa)
*   [3 Legacy documentation: ALSA, bluez5 and PulseAudio method](#Legacy_documentation:_ALSA,_bluez5_and_PulseAudio_method)
    *   [3.1 Install Software Packages](#Install_Software_Packages)
        *   [3.1.1 Install ALSA and associated libraries](#Install_ALSA_and_associated_libraries)
        *   [3.1.2 Install Bluez5](#Install_Bluez5)
        *   [3.1.3 Install Audacious](#Install_Audacious)
    *   [3.2 Procedure](#Procedure)
        *   [3.2.1 Miscellaneous configuration files](#Miscellaneous_configuration_files)
            *   [3.2.1.1 ALSA /etc/asound.conf](#ALSA_/etc/asound.conf)
            *   [3.2.1.2 /etc/dbus-1/system.d/bluetooth.conf](#/etc/dbus-1/system.d/bluetooth.conf)
            *   [3.2.1.3 Tested applications](#Tested_applications)
*   [4 Switch between HSP/HFP and A2DP setting](#Switch_between_HSP/HFP_and_A2DP_setting)
    *   [4.1 A2DP not working with PulseAudio](#A2DP_not_working_with_PulseAudio)
        *   [4.1.1 Socket interface problem](#Socket_interface_problem)
        *   [4.1.2 A2DP sink profile is unavailable](#A2DP_sink_profile_is_unavailable)
        *   [4.1.3 Gnome with GDM](#Gnome_with_GDM)
*   [5 See also](#See_also)

## Headset via Bluez5/PulseAudio

[Install](/index.php/Install "Install") [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa), [pulseaudio-bluetooth](https://www.archlinux.org/packages/?name=pulseaudio-bluetooth) and [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) providing the `bluetoothctl` utility.

**Note:** Before continuing, ensure that the bluetooth device is not blocked by [rfkill](/index.php/Rfkill "Rfkill").

### Configuration via CLI

[Start](/index.php/Start "Start") the `bluetooth.service` systemd unit.

Now we can use the *bluetoothctl* command line utility to pair and connect. For troubleshooting and more detailed explanations of *bluetoothctl* see the [Bluetooth](/index.php/Bluetooth "Bluetooth") article. Run

```
$ bluetoothctl

```

to be greeted by its internal command prompt. Then enter:

```
[bluetooth]# power on
[bluetooth]# agent on
[bluetooth]# default-agent
[bluetooth]# scan on

```

Now make sure that your headset is in pairing mode. It should be discovered shortly. For example,

```
[NEW] Device 00:1D:43:6D:03:26 Lasmex LBT10

```

shows a device that calls itself *"Lasmex LBT10"* and has MAC address *"00:1D:43:6D:03:26"*. We will now use that MAC address to initiate the pairing:

```
[bluetooth]# pair 00:1D:43:6D:03:26

```

After pairing, you also need to explicitly connect the device (every time?):

```
[bluetooth]# connect 00:1D:43:6D:03:26

```

If you are getting a connection error `org.bluez.Error.Failed` retry by killing existing PulseAudio daemon first:

```
$ pulseaudio -k
[bluetooth]# connect 00:1D:43:6D:03:26

```

If everything works correctly, you now have a separate output device in [PulseAudio](/index.php/PulseAudio "PulseAudio").

**Note:** The device may be off by default. Select its audio profile (`OFF`, `A2DP`, `HFP`) in the "Configuration" tab of [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol).

You can now redirect any audio through that device using the "Playback" and "Recording" tabs of [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol).

You can now disable scanning again and exit the program:

```
[bluetooth]# scan off
[bluetooth]# exit

```

#### Setting up auto connection

To make your headset auto connect you need to enable PulseAudio's switch-on-connect module. Do this by adding the following lines to `/etc/pulse/default.pa`:

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

#### Media controls

To use the media controls they may be forwarded to [MPRIS2](https://specifications.freedesktop.org/mpris-spec/latest/), where they can be picked up by media players that support mpris for external control. Install [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) and run

```
$ mpris-proxy

```

In order to start up mpris-proxy in the background and/or when your system starts, you may create a systemd user script

 `~/.config/systemd/user/mpris-proxy.service` 
```
[Unit]
Description=Forward bluetooth midi controls via mpris2 so they are picked up by supporting media players

[Service]
Type=simple
ExecStart=/usr/bin/mpris-proxy

[Install]
WantedBy=default.target

```

Then start it

```
$ systemctl --user start mpris-proxy

```

and enable it to start at login

```
$ systemctl --user enable mpris-proxy

```

### Configuration via GNOME Bluetooth

**Note:** The A2DP profile will not activate using this method with pulseaudio 9/10 due to an ongoing bug, leading to possible low quality mono sound. See [#A2DP not working with PulseAudio](#A2DP_not_working_with_PulseAudio) for a possible solution.

You can use [GNOME Bluetooth](/index.php/Bluetooth#Graphical "Bluetooth") graphical front-end to easily configure your bluetooth headset.

First, you need to be sure that `bluetooth.service` systemd unit is running.

Open GNOME Bluetooth and activate the bluetooth. After scanning for devices, you can connect to your headset selecting it on the device list. You can directly access to sound configuration panel from the device menu. On the sound panel, a new sink should appear when your device is connected.

### LDAC/aptX

[LDAC](https://en.wikipedia.org/wiki/LDAC_(codec) "wikipedia:LDAC (codec)")/[aptX](https://en.wikipedia.org/wiki/aptX "wikipedia:aptX") codec support can be enabled by installing [pulseaudio-modules-bt-git](https://aur.archlinux.org/packages/pulseaudio-modules-bt-git/) and [libldac](https://aur.archlinux.org/packages/libldac/). See its [project page](https://github.com/EHfive/pulseaudio-modules-bt) for configuration tips.

### Troubleshooting

**Note:** Many users report frustration with getting A2DP/Bluetooth Headsets to work. see [#Switch between HSP/HFP and A2DP setting](#Switch_between_HSP/HFP_and_A2DP_setting) for additional information.

#### Bad sound / Static noise / "Muddy" sound

If you experience bad sound quality with your headset, it could in all likelihood be because your headset is not set to the correct profile. See [#Switch between HSP/HFP and A2DP setting](#Switch_between_HSP/HFP_and_A2DP_setting) to solve the problem.

#### Selected audio profile, but headset inactive and audio cannot be redirected

Deceptively, this menu is available before the device has been connected; annoyingly it will have no effect. The menu seems to be created as soon as the receiver recognizes the device.

Make sure to run bluetoothctl (with sudo/as root) and connect the device manually. There may be configuration options to remove the need to do this each time, but neither pairing nor trusting induce automatic connecting for me.

#### Pairing fails with AuthenticationFailed

If pairing fails, you can try enabling or [disabling SSPMode](https://stackoverflow.com/questions/12888589/linux-command-line-howto-accept-pairing-for-bluetooth-device-without-pin) with:

```
# btmgmt ssp off

```

or

```
# btmgmt ssp on

```

You may need to turn off BlueTooth while you run this command.

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

It can also be due to permission, especially if starting pulseaudio as root allows you to connect. Add your user to the *lp* group, then restart pulseaudio. See `/etc/dbus-1/system.d/bluetooth.conf` for reference.

If the issue is not due to the missing package, the problem in this case is that PulseAudio is not catching up. A common solution to this problem is to restart PulseAudio. Note that it is perfectly fine to run *bluetoothctl* as root while PulseAudio runs as user. After restarting PulseAudio, retry to connect. It is not necessary to repeat the pairing.

If restarting PulseAudio does not work, you need to load module-bluetooth-discover.

```
# pactl load-module module-bluetooth-discover

```

The same load-module command can be added to `/etc/pulse/default.pa`.

If that still does not work, or you are using PulseAudio's system-wide mode, also load the following PulseAudio modules (again these can be loaded via your `default.pa` or `system.pa`):

```
module-bluetooth-policy
module-bluez5-device
module-bluez5-discover

```

It's also possible there are no write permissions for the owner of /var/lib/bluetooth. If this is the case, you may get the device to work by removing and re-pairing it, but the issue will return after rebooting. Restoring write permissions fixes this issue:

```
chmod -R u+w /var/lib/bluetooth

```

#### Connecting works, but there are sound glitches all the time

This is very likely to occur when the Bluetooth and the WiFi share the same chip as they share the same physical antenna and possibly band range (2.4GHz). Although this works seamlessly on Windows, this is not the case on Linux.

A possible solution is to move your WiFi network to 5GHz so that there will be no interference. If your card/router does not support this, you can upgrade your WiFi drivers/firmware. This approach works on Realtek 8723BE and latest rtl drivers for this chip from AUR.

If nothing of the previous is possible, a less effective mitigation is to tweak the fragment size and the latency on PulseAudio output port, trying to compensate interference. Reasonable values must be chosen, because these settings can make the audio out of sync (e.g. when playing videos). To change the latency of the bluetooth headset's port (e.g. to 125000 microseconds in the following example):

```
$ pactl set-port-latency-offset <bluez_card> headset-output **125000**

```

where the identifier of the card can be found with

```
$ pacmd list-sinks | egrep -o 'bluez_card[^>]*'

```

The fragment size can be set in the config file `/etc/pulse/daemon.conf` and takes effect after a restart of PulseAudio (for more details please see [PulseAudio/Troubleshooting#Setting the default fragment number and buffer size in PulseAudio](/index.php/PulseAudio/Troubleshooting#Setting_the_default_fragment_number_and_buffer_size_in_PulseAudio "PulseAudio/Troubleshooting")).

Perhaps it will help to add "options ath9k btcoex_enable = 1" to the `/etc/modprobe.d/ath9k.conf` (with the appropriate bluetooth adapter):

 `/etc/modprobe.d/ath9k.conf` 
```
# possibly fix for sound glitches
options ath9k btcoex_enable = 1
```

Then restart.

#### Connecting works, but I cannot play sound

Make sure that you see the following messages in your system log:

```
bluetoothd[5556]: Endpoint registered: sender=:1.83 path=/MediaEndpoint/A2DPSource
bluetoothd[5556]: Endpoint registered: sender=:1.83 path=/MediaEndpoint/A2DPSink

```

If you see a message similar to this, you can go on and investigate your PulseAudio configuration. Otherwise, go back and ensure the connection is successful.

When using [GDM](/index.php/GDM "GDM"), another instance of PulseAudio is started, which "captures" your bluetooth device connection. This can be prevented by [masking](/index.php/Mask "Mask") the pulseaudio socket for the GDM user by doing the following:

```
# mkdir -p  /var/lib/gdm/.config/systemd/user
# ln -s /dev/null  /var/lib/gdm/.config/systemd/user/pulseaudio.socket

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

#### Connecting works, sound plays fine until headphones become idle, then stutters

If the headphones play sound correctly until they become idle and then stutter on resume (e.g. because the sound is paused, or because no sound is played for a while), try disabling PulseAudio's automatic sink/source suspension on idle.

See [PulseAudio/Troubleshooting#Bluetooth headset replay problems](/index.php/PulseAudio/Troubleshooting#Bluetooth_headset_replay_problems "PulseAudio/Troubleshooting") for steps.

#### UUIDs has unsupported type

During pairing you might see this output in *bluetoothctl*:

```
[CHG] Device 00:1D:43:6D:03:26 UUIDs has unsupported type

```

This message is a very common one and can be ignored.

#### PC shows device as paired, but is not recognized by device

This might be due to the device not supporting bluetooth LE for pairing.

Try setting `ControllerMode = bredr` in `/etc/bluetooth/main.conf`. See [[2]](http://unix.stackexchange.com/questions/292189/pairing-bose-qc-35-over-bluetooth-on-fedora).

#### Device connects, then disconnects after a few moments

If you see messages like the following in `journalctl` output, and your device fails to connect or disconnects shortly after connecting:

```
bluetoothd: Unable to get connect data for Headset Voice gateway: getpeername: Transport endpoint is not connected (107)
bluetoothd: connect error: Connection refused (111)

```

This may be because you have already paired the device with another operating system using the same bluetooth adapter (e.g., dual-booting). Some devices cannot handle multiple pairings associated with the same MAC address (i.e., bluetooth adapter). You can fix this by re-pairing the device. Start by removing the device:

```
$ bluetoothctl
[bluetooth]# devices
Device XX:XX:XX:XX:XX:XX My Device
[bluetooth]# remove XX:XX:XX:XX:XX:XX

```

Then [restart](/index.php/Restart "Restart") `bluetooth.service`, turn on your bluetooth adapter, make your device discoverable, re-scan for devices, and re-pair your device. Depending on your bluetooth manager, you may need to perform a full reboot in order to re-discover the device.

#### Apple Airpods have low volume

Edit `bluetooth.service` by running `systemctl edit --full bluetooth.service` and change the line:

```
ExecStart=/usr/lib/bluetooth/bluetoothd

```

to:

```
ExecStart=/usr/lib/bluetooth/bluetoothd --noplugin=avrcp

```

Finally [restart](/index.php/Restart "Restart") `bluetooth.service`, [reload](/index.php/Reload "Reload") systemd manager configuration

Reconnect your headset.

#### HSP problem: the bluetooth sink and source are created, but no audio is being transmitted

You may be missing firmware or the SCO (audio protocol of HSP and HFP) routing might be wrong. See [[3]](https://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Bluetooth/#index10h3) - the firmware for BCM20702 can be installed via [bcm20702a1-firmware](https://aur.archlinux.org/packages/bcm20702a1-firmware/) or [bcm20702b0-firmware](https://aur.archlinux.org/packages/bcm20702b0-firmware/).

## Headset via Bluez5/bluez-alsa

**Note:** Bluez5 has dropped direct integration for [ALSA](/index.php/ALSA "ALSA") and supports [PulseAudio](/index.php/PulseAudio "PulseAudio") only. Follow the instructions below if you cannot or do not want to use PulseAudio.

First, ensure that your headset is correctly paired and connected to the system (see for example `bluetoothctl`).

Then, install [bluez-alsa-git](https://aur.archlinux.org/packages/bluez-alsa-git/), start (and enable) the `bluealsa` service, and add your user to the `audio` group.

Run the following command to check if everything is working as intended (replace MAC and FILE below):

```
$ aplay -D bluealsa:HCI=hci0,DEV=MAC,PROFILE=a2dp FILE.wav

```

Finally, add the following lines to your .asoundrc:

 `.asoundrc` 
```
defaults.bluealsa {
    interface "hci0"
    device "MAC"
    profile "a2dp"
}

```

You can now use the bluealsa device to reach your headset. Volume management is conducted normally via `alsamixer`.

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

[Start](/index.php/Start "Start") the bluetooth service as root.

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

## Switch between HSP/HFP and A2DP setting

This can easily be achieved by the following command where the `*card_number*` can be obtained by running `pacmd list-cards`.

```
$ pacmd set-card-profile *card_number* a2dp_sink

```

For enabling automatic profile switching from A2DP to HSP when a recording stream appears without any role set, you can append `auto_switch=2` to `load-module module-bluetooth-policy` in `/etc/pulse/default.pa`.

For more information about PulseAudio profiles, see [PulseAudio Documentation](https://freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Bluetooth/#index1h2).

### A2DP not working with PulseAudio

#### Socket interface problem

If PulseAudio fails when changing the profile to A2DP with bluez 4.1+ and PulseAudio 3.0+, you can try disabling the Socket interface from `/etc/bluetooth/audio.conf` by removing the line `Enable=Socket` and adding line `Disable=Socket`.

#### A2DP sink profile is unavailable

When the A2DP sink profile is unavailable it will not be possible to switch to the A2DP sink (output) with a PulseAudio front-end and the A2DP sink will not even be listed. This can be confirmed with `pactl`.

```
 $ pactl list | grep -C2 A2DP
      Profiles:
              headset_head_unit: Headset Head Unit (HSP/HFP) (sinks: 1, sources: 1, priority: 30, available: yes)
              a2dp_sink: High Fidelity Playback (A2DP Sink) (sinks: 1, sources: 0, priority: 40, available: no)
              off: Off (sinks: 0, sources: 0, priority: 0, available: yes)
         Active Profile: headset_head_unit

```

Trying to manually set the card profile with `pacmd` will fail.

```
 $ pacmd set-card-profile bluez_card.C4_45_67_09_12_00 a2dp_sink
 Failed to set card profile to 'a2dp_sink'.

```

This is known to happen from version 10.0 of Pulseaudio when connecting to Bluetooth headphones via Bluedevil or another BlueZ front-end. See [related bug report.](https://gitlab.freedesktop.org/pulseaudio/pulseaudio/issues/525)

This issue also appears after initial pairing of Headphones with some Bluetooth controllers (e.g. `0a12:0001, Cambridge Silicon Radio`) which might default to the `Handsfree` or `Headset - HS` service and will not allow switching to the A2DP PulseAudio sink that requires the `AudioSink` service.

Possible solutions:

*   For some headsets, using the headset's volume or play/pause controls while connected can trigger the A2DP profile to become available.

*   It is possible that connecting to a headset via `bluetoothctl` from [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) will make the A2DP sink profile available. There is an automation for this every time a bluetooth device is connected: [fix-bt-a2dp](https://aur.archlinux.org/packages/fix-bt-a2dp/) ([detailed usage](https://github.com/pastleo/fix-bt-a2dp#usage))

```
[bluetooth]# connect *[headset MAC here]*

```

*   Manually switching to Bluetooth's `AudioSink` service which would make the A2DP profile and its A2DP PulseAudio sink available. This can be done with blueman-manager which included in [blueman](https://www.archlinux.org/packages/?name=blueman) or by registering the UUID of the AudioSink service with `bluetoothctl` .

```
 $ bluetoothctl
 [bluetooth]# menu gatt
 [bluetooth]# register-service 0000110b-0000-1000-8000-00805f9b34fb
 [bluetooth]# quit

```

#### Gnome with GDM

The instructions below were tested on Gnome 3.24.2 and PulseAudio 10.0 however they may still be applicable and useful for other versions.

If PulseAudio fails when changing the profile to A2DP while using GNOME with GDM, you need to prevent GDM from starting its own instance of PulseAudio:

*   Prevent Pulseaudio clients from automatically starting a server if one is not running by adding the following:

 `/var/lib/gdm/.config/pulse/client.conf` 
```
autospawn = no
daemon-binary = /bin/true

```

*   Prevent systemd from starting Pulseaudio anyway with socket activation:

```
$ sudo -ugdm mkdir -p /var/lib/gdm/.config/systemd/user
$ sudo -ugdm ln -s /dev/null /var/lib/gdm/.config/systemd/user/pulseaudio.socket

```

*   Restart, and check that there is no PulseAudio process for the `gdm` user using:

```
 $ pgrep -u gdm pulseaudio

```

Further discussion about this problem and alternative fixes can be found [here](https://bbs.archlinux.org/viewtopic.php?id=194006) and [here](https://bbs.archlinux.org/viewtopic.php?id=196689).

## See also

Using the same device on Windows and Linux without pairing the device over and over again

*   [Dual booting with a Bluetooth keyboard](http://ubuntuforums.org/showthread.php?p=9363229#post9363229)