[Shairport Sync](https://github.com/mikebrady/shairport-sync) is an [w:AirPlay](https://en.wikipedia.org/wiki/AirPlay "w:AirPlay") audio player — it plays audio streamed from iTunes, iOS devices and third-party AirPlay sources such as ForkedDaapd and others. Audio played by a Shairport Sync-powered device stays synchronised with the source and hence with similar devices playing the same source. In this way, synchronised multi-room audio is possible without difficulty.

Shairport Sync does not support AirPlay video or photo streaming.

Shairport Sync is a fork of the original Shairport which was based on reverse-engineering Apple's key used in its AirPort Express. Be advised that this functionality may be removed at Apple's discretion.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 System service](#System_service)
    *   [3.1 Starting](#Starting)
    *   [3.2 Daemon Setup](#Daemon_Setup)
*   [4 User service](#User_service)

## Installation

[Install](/index.php/Install "Install") the [shairport-sync](https://www.archlinux.org/packages/?name=shairport-sync) package.

**Note:** Shairport Sync requires the avahi-daemon to be running. You can [Start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") `avahi-daemon.service` using systemd.

## Configuration

The configuration file can be found at `/etc/shairport-sync.conf`. It contains useful comments and configuration hints. More documentation is available in the [README](https://github.com/mikebrady/shairport-sync/blob/master/README.md#configuring-shairport-sync) file.

## System service

Will work well only with ALSA backed (maybe with Jack and Sndio too). Also, check list of output devices, e.g. by using tools from [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils): `aplay -L` and look which device is referred by `default` target. If target device is PulseAudio, like:

```
default
    Default ALSA Output (currently PulseAudio Sound Server)

```

you must configure shairport-sync ASLA backend to use another one, like:

```
sysdefault:CARD=PCH
    HDA Intel PCH, ALC269VC Analog
    Default Audio Device

```

Edit `/etc/shairport-sync.conf`:

```
// These are parameters for the "alsa" audio back end.
// For this section to be operative, Shairport Sync must be built with the following configuration flag:
// --with-alsa
alsa =
{
    output_device = "sysdefault";
    ...
}

```

### Starting

[Start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") `shairport-sync.service` using systemd.

### Daemon Setup

If you want to run shairport-sync as a daemon you will need to have a folder created in `/var/run` which is a tempfs by default in Arch Linux. To have a folder created automatically on boot create a tempfiles configuration file, for example

 `/usr/lib/tempfiles.d/shairport-sync.conf`  `d /var/run/shairport-sync 0755 username group` 

you can now use `shairport-sync -d` to run shairport-sync as a daemon, and `shairport-sync -k` to kill the daemon.

## User service

According to the [author](https://github.com/mikebrady/shairport-sync/issues/471#issuecomment-394089069), the PulseAudio backend with the default PulseAudio configuration can only work as a user service.

To run *shairport-sync* as user daemon, you can add it to the desktop environment autostart, or use a systemd service:

```
sudo cp /usr/lib/systemd/system/shairport-sync.service /etc/systemd/user/

```

Next, edit `/etc/systemd/user/shairport-sync.service` and comment out the next lines:

```
[Unit]
...
#Requires=avahi-daemon.service
#After=avahi-daemon.service
...
[Service]
...
#Requires=avahi-daemon.service
#After=avahi-daemon.service
...

```

Now, you are ready to start service as user:

```
systemctl --user enable --now shairport-sync.service

```

To obtain logs:

```
journalctl --user -fu shairport-sync.service

```