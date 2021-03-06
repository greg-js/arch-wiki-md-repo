[Tvheadend](https://tvheadend.org/) is a TV streaming server and recorder. Tvheadend supports DVB-S/S2, DVB-C/C2, DVB-T, ATSC, ISDB-T, IPTV, SAT>IP and HDHomeRun as input sources.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 HDHomeRun](#HDHomeRun)
    *   [1.2 Playback Clients](#Playback_Clients)
*   [2 Usage](#Usage)
*   [3 Configuration](#Configuration)
*   [4 XMLTV](#XMLTV)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Create M3U compatible playlist file](#Create_M3U_compatible_playlist_file)
    *   [5.2 Use hardware video acceleration](#Use_hardware_video_acceleration)
        *   [5.2.1 Enable VA-API support transcoding](#Enable_VA-API_support_transcoding)
    *   [5.3 Use CAPMT (Linux Network DVBAPI) with OSCam](#Use_CAPMT_(Linux_Network_DVBAPI)_with_OSCam)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Unable to authenticate/play stream](#Unable_to_authenticate/play_stream)
    *   [6.2 DVB-T2 HD in Germany](#DVB-T2_HD_in_Germany)

## Installation

Tvheadend is available from the [AUR](/index.php/AUR "AUR") as [tvheadend](https://aur.archlinux.org/packages/tvheadend/) or [tvheadend-git](https://aur.archlinux.org/packages/tvheadend-git/) (development branch).

### HDHomeRun

HDHomeRun support should be working out-of-the-box in the [tvheadend-git](https://aur.archlinux.org/packages/tvheadend-git/) package.

The [tvheadend](https://aur.archlinux.org/packages/tvheadend/) package does not have HDHomeRun support enabled. To enable you will need to edit the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") and add `libhdhomerun` ([libhdhomerun](https://aur.archlinux.org/packages/libhdhomerun/)) to the [depends](/index.php/PKGBUILD#depends "PKGBUILD") list. Finally, add `--enable-hdhomerun_client` in the *configure array*.

### Playback Clients

*   [VLC](/index.php/VLC "VLC") — [vlc-htsp-plugin-git](https://aur.archlinux.org/packages/vlc-htsp-plugin-git/)
*   [Kodi](/index.php/Kodi "Kodi") — [kodi-addon-hts-pvrmanager](https://aur.archlinux.org/packages/kodi-addon-hts-pvrmanager/), [kodi-addon-pvr-hts](https://aur.archlinux.org/packages/kodi-addon-pvr-hts/) or [kodi-addon-pvr-hts-git](https://aur.archlinux.org/packages/kodi-addon-pvr-hts-git/)

## Usage

Once Tvheadend is installed [start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") the `tvheadend.service`.

## Configuration

Once the service is running, configuration of Tvheadend is done through a web interface on [localhost:9981](http://localhost:9981).

The service should automatically generate Tvheadend username and passwords that are the same as your system. You can log in as root with your system's root password. If Tvheadend is unable to generate an username/password, one should simple login **without** providing credentials.

## XMLTV

If you want to obtain schedule data from an outside source like Schedules Direct, then you should also install [xmltv](https://aur.archlinux.org/packages/xmltv/).

## Tips and tricks

### Create M3U compatible playlist file

To export all channels as a M3U playlist file, one may want to use the following URL [[1]](https://tvheadend.org/boards/5/topics/21366):

```
http://<user>:<pass>@<ip>:9981/playlist/channels.m3u?profile=<profile>

```

### Use hardware video acceleration

When using [tvheadend-git](https://aur.archlinux.org/packages/tvheadend-git/) it is possible to enable [hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

Support depends on selected the codec and capabilities of the video device in use.

To enable hardware acceleration, check *Hardware acceleration* for a codec profile on the *Codec Profiles* page.

#### Enable VA-API support transcoding

It is possible to use [VA-API](/index.php/VA-API "VA-API") for transcoding streams when using [tvheadend-git](https://aur.archlinux.org/packages/tvheadend-git/), support depends on capabilities of the video device and the selected codec.

To enable VA-API create a new *Codec Profile* and select a codec with *VAAPI* on the *Codec Profiles* page. On the next screen check *Hardware acceleration*, select the correct *Device Name*, e.g. `i915 v1.6.0 (/dev/dri/renderD128)` and click on *Create*.

Finally, create a *Stream Profile* and select the previously created *Codec Profile* as *Video codec profile*. The *Audio codec profile* and *Subtitle codec profile* depend on the user preferences and as stated support by the video device.

To test the newly created profile, you may want to use the following URL:

```
http://<user>:<pass>@<ip>:9981/stream/channelnumber/<channel>?profile=<stream-profile>

```

Use [journalctl](/index.php/Journalctl "Journalctl") to check for Tvheadend debug info. The error *tvheadend[..]: transcode: no AVHWAccel* indicates the stream profile doesn't use hardware acceleration and one should adjust the codec configuration.

### Use CAPMT (Linux Network DVBAPI) with OSCam

[Install](/index.php/Install "Install") [oscam-git](https://aur.archlinux.org/packages/oscam-git/) or [oscam-svn](https://aur.archlinux.org/packages/oscam-svn/) to provide a softcam for Tvheadend.

The following settings may be used when using DVB-API as Conditional Access Client (CAs):

| Parameter | Value |
| Client name | OSCam |
| Mode | OSCam net protocol (rev >= 10389) |
| IP Address (TCP mode) | localhost *or* 127.0.0.1 *or* hostname |
| Connect port | 9000 |
| CW Mode | Standard / auto |

**Note:** See the official [Tvheadend docs](https://docs.tvheadend.org/webui/config_caclient/) about CAs for details.

In OSCam create a user named *vdr* with *vdr* as password and set the *DVB Api* configuration to use at least the following parameters:

| Parameter | Value |
| Boxtype | pc |
| User | vdr |
| PMT Mode | 4 |
| Listen port | 9000 |

[Restart](/index.php/Restart "Restart") `oscam.service` and `tvheadend.service` to apply the changes.

## Troubleshooting

### Unable to authenticate/play stream

Authentication issues can occur when using *digest* as *Authentication type*.

Change this to *Both plain and digest* to allow browsers/players that don't support the digest protocol.

### DVB-T2 HD in Germany

The German broadcast of DVB-T2 HD is a deviation of the official standard inasmuch as it is using the more modern H.265 codec. Somehow, tvheadend doesn’t detect the channels automatically. You first need to run the configuration wizard, choose no pre-defined muxes, just *--Generic--: auto-Default*. After the search run, save and go to *Configuration*, *DVB Inputs*, *Muxes*. Select all listed muxes (might be on two pages, batch selection via shift key possible) and edit them from *DVB-T* to *DVB-T2* – you need to check the *Delivery system* checkmark in the edit dialog. Then go to *Network*, select the DVB-T entry and click *Force scan*. Observe the rescan via the *Muxes* tab as many of the former "FAIL" results become "OK". This will get you the channels under *Services* which you can use to create an actual channels list of the unencrypted TV channels.