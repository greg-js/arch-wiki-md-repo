Go back to [Music Player Daemon](/index.php/Music_Player_Daemon "Music Player Daemon").

## Contents

*   [1 Organizing library](#Organizing_library)
*   [2 Last.fm/Libre.fm scrobbling](#Last.fm.2FLibre.fm_scrobbling)
    *   [2.1 mpdas](#mpdas)
    *   [2.2 mpdcron](#mpdcron)
    *   [2.3 mpdscribble](#mpdscribble)
    *   [2.4 Sonata](#Sonata)
*   [3 Disable resume playback on startup](#Disable_resume_playback_on_startup)
*   [4 Example configuration: Output with 44.1 KHz at e. g. 16 bit depth, multiple programs at once](#Example_configuration:_Output_with_44.1_KHz_at_e._g._16_bit_depth.2C_multiple_programs_at_once)
*   [5 Control MPD with lirc](#Control_MPD_with_lirc)
*   [6 PulseAudio](#PulseAudio)
    *   [6.1 Local (as your own user)](#Local_.28as_your_own_user.29)
    *   [6.2 Local (with separate mpd user)](#Local_.28with_separate_mpd_user.29)
    *   [6.3 Remote](#Remote)
*   [7 Cue Files](#Cue_Files)
*   [8 HTTP streaming](#HTTP_streaming)
    *   [8.1 Configuration](#Configuration)
        *   [8.1.1 Format](#Format)
    *   [8.2 Use](#Use)
*   [9 MPRIS2 Support](#MPRIS2_Support)
    *   [9.1 mpDris2](#mpDris2)
    *   [9.2 mpd-mpris](#mpd-mpris)
*   [10 Adding a separate volume control (ALSA)](#Adding_a_separate_volume_control_.28ALSA.29)

## Organizing library

MPD does not manage your library. Check out [beets](https://www.archlinux.org/packages/?name=beets) or [picard](https://www.archlinux.org/packages/?name=picard) in the [official repositories](/index.php/Official_repositories "Official repositories").

## Last.fm/Libre.fm scrobbling

**Note:** mpd release 0.18 removed Last.fm [support](http://git.musicpd.org/cgit/master/mpd.git/tree/NEWS). However, some clients offer scrobbling independent of mpd.

To scrobble your songs to [Last.fm](http://www.last.fm) or [Libre.fm](http://libre.fm) when using MPD, there are several possibilities.

### mpdas

[mpdas](http://50hz.ws/mpdas/) is an AudioScrobbler client for MPD written in C++. It uses [curl](https://www.archlinux.org/packages/?name=curl) and [libmpd](https://www.archlinux.org/packages/?name=libmpd). mpdas supports the latest AudioScrobbler protocol (2.0) and will also cache unscrobbled plays in `~/.mpdascache` if there is no network connectivity.

[mpdas](https://aur.archlinux.org/packages/mpdas/) is available in the [AUR](/index.php/AUR "AUR").

Configuration of mpdas is very simple, see the official [README](https://github.com/hrkfdn/mpdas/blob/master/README). A very basic example of `/etc/mpdasrc` is also available as `/etc/mpdasrc`.

Your password can also be in the form of an md5hash:

```
$ echo -n 'PASSWORD' | md5sum | cut -f 1 -d " "

```

To autostart *mpdas* along with *mpd*, add an entry for it into the file in which you start *mpd* (e.g. [xinitrc](/index.php/Xinitrc "Xinitrc")):

 `[[ -z $(pgrep -xU $UID mpdas) ]] && mpdas &` 

When *mpd* is started with a [systemd user service](/index.php/Music_Player_Daemon#Autostart_with_systemd "Music Player Daemon"), it is better to start *mpdas* the same way:

```
$ systemctl --user start mpdas.service

```

**Tip:** If you get a failed `mpdas.service` after system startup, consider using [socket activation](/index.php/Music_Player_Daemon#Socket_activation "Music Player Daemon") with `mpd.socket` instead.

### mpdcron

[mpdcron](http://alip.github.io/mpdcron/) is a cron-like daemon for MPD that listens for events and executes user defined actions. It can be extended via modules to show notifications, submit songs to Last.fm or Libre.fm (*scrobbling*), or to collect statistics about played songs.

[mpdcron-git](https://aur.archlinux.org/packages/mpdcron-git/) is available in the [AUR](/index.php/AUR "AUR").

See the official page for information about configuration and modules.

To autostart *mpdcron* along with *mpd*, add an entry for it into the file in which you start *mpd* (e.g. [xinitrc](/index.php/Xinitrc "Xinitrc")):

```
[[ -z $(pgrep -xU $UID mpdcron) ]] && mpdcron &

```

### mpdscribble

[mpdscribble](https://aur.archlinux.org/packages/mpdscribble/) is a daemon available in the [AUR](/index.php/AUR "AUR"). This is arguably the best alternative, because it is the semi-official MPD scrobbler and uses the new "idle" feature in MPD for more accurate scrobbling. Also, you do not need root access to configure it, because it does not need any changes to `/etc` at all. Visit [the official website](https://www.musicpd.org/clients/mpdscribble/) for more information.

Example configuration:

 `~/.mpdscribble/mpdscribble.conf` 
```
[mpdscribble]
host = *your mpd host* # optional, defaults to $MPD_HOST or localhost
port = *your mpd port* # optional, defaults to $MPD_PORT or 6600
log = /home/*YOUR_USERNAME*/.mpdscribble/mpdscribble.log
verbose = 2
proxy = *your proxy* # optional, e. g. [http://your.proxy:8080](http://your.proxy:8080), defaults to none

[last.fm]
# last.fm section, comment if you do not use last.fm
url = [http://post.audioscrobbler.com/](http://post.audioscrobbler.com/)
username = *your last.fm username*
password = *your last.fm password*
journal = /home/*YOUR_USERNAME*/.mpdscribble/lastfm.journal

[libre.fm]
# libre.fm section, comment if you do not use libre.fm
url = [http://turtle.libre.fm/](http://turtle.libre.fm/)
username = *your libre.fm username*
password = *your libre.fm password*
journal = /home/*YOUR_USERNAME*/.mpdscribble/librefm.journal
```

Your password can also be in the form of an md5hash.

```
echo -n "*password*" | md5sum | cut -f 1 -d " "

```

To autostart *mpdscribble* you can use the `mpdscribble.service` under systemd user instance. See [systemd/User](/index.php/Systemd/User "Systemd/User") for details.

Alternatively you can autostart *mpdscribble* along with *mpd*, add an entry for it into the file in which you start *mpd* (e.g. `~/.xinitrc`):

```
[[ -z $(pgrep -xU $UID mpdscribble) ]] && mpdscribble &

```

**Note:** If you get a `[last.fm] handshake failed, username or password incorrect (BADAUTH)` error, make sure your username and password are correct, and that your password is not [32 characters long](http://bugs.musicpd.org/view.php?id=3836).

### Sonata

Sonata has built-in support for scrobbling, although that requires the program to run the whole time. Additionally, Sonata does not cache the songs if they cannot be forwarded to Last.fm at the time of playing, meaning they will not be added to the statistics.

## Disable resume playback on startup

This feature is present in *mpd* after version 0.16.2\. When this feature is enabled, *mpd* will always start in the "paused" state, even if a song was playing when mpd was stopped. Add the line below to your `mpd.conf` to enable this feature.

```
restore_paused "yes"

```

## Example configuration: Output with 44.1 KHz at e. g. 16 bit depth, multiple programs at once

*Why these formats?* Because they are the standard format for CD audio, because ALSA on its own allows more than one program "to sound" only with dmix — which uses an inferior resampling algorithm by default — and because dmix by default resamples anything lower to 48 KHz (or whatever higher format is playing at the time). Also, some get clicking sounds if at least `mpd.conf` is not changed this way.

*What is the downside?* These settings cause *everything* (if necessary) to be resampled to this format, such as material from DVD or TV which usually is at 48 KHz. But there is no known way to have ALSA dynamically change the format, and particularly if you listen to far more CDs than anything else the occasional 48 → 44.1 is not too great a loss.

The following assumes that there are not already other settings which conflict resp. overwrite it. This applies especially to the current user's potential `~/.asoundrc` — which MPD as its own user ignores, therefore the following should go to `/etc/asound.conf`:

 `/etc/asound.conf` 
```
defaults.pcm.dmix.rate 44100 # Force 44.1 KHz
defaults.pcm.dmix.format S16_LE # Force 16 bits

```
 `/etc/mpd.conf` 
```
audio_output {
        type                    "alsa" # Use the ALSA output plugin.
	name			"your_custom_name" # Must be present and does not have to match the actual card name , e.g. what you have in /etc/asound.conf
        options                 "dev=dmixer"
        device                  "plug:dmix" # Both lines cause MPD to output to dmix
	format	        	"44100:16:2" # the actual format
	auto_resample		"no" # This bypasses ALSA's own algorithms, which generally are inferior. See below how to choose a different one.
}
```

**Note:** MPD gives the mp3 format a special treatment at decoding: it is always put out as 24 bit. (The conversion as forced by the *format* line only comes after that.)

If one wants to leave the bit depth decision to ALSA resp. MPD, comment out resp. omit the *dmix.format* line and change the one for mpd with *format* to "44100:*:2".

**Note:** *Crossfading* between files decoded at two different bit depths (say, one mp3 and one 16 bit flac) does not work unless conversion is active.

## Control MPD with lirc

There are already some clients designed for communications between lircd and MPD, however, as far as the practical use, they are not very useful since their functions are limited.

It is recommended to use mpc with irexec. mpc is a command line player which only sends the command to MPD and exits immediately, which is perfect for irexec, the command runner included in lirc. What irexec does is that it runs a specified command once received a remote control button.

First of all, please setup your remotes as referred to the [LIRC](/index.php/LIRC "LIRC") article.

Edit your favored lirc startup configuration file, default location is `~/.lircrc`.

Fill the file with the following pattern:

```
begin
     prog = irexec
     button = <button_name>
     config = <command_to_run>
     repeat = <0 or 1>
end

```

An example:

```
## irexec
begin
     prog = irexec
     button = play_pause
     config = mpc toggle
     repeat = 0
end

begin
     prog = irexec
     button = stop
     config = mpc stop
     repeat = 0
end
begin
     prog = irexec
     button = previous
     config = mpc prev
     repeat = 0
end
begin
     prog = irexec
     button = next
     config = mpc next
     repeat = 0
end
begin
     prog = irexec
     button = volup
     config = mpc volume +2
     repeat = 1
end
begin
     prog = irexec
     button = voldown
     config = mpc volume -2
     repeat = 1
end
begin
     prog = irexec
     button = pbc
     config = mpc random
     repeat = 0
end
begin
     prog = irexec
     button = pdvd
     config = mpc update
     repeat = 0
end
begin
     prog = irexec
     button = right
     config = mpc seek +00:00:05
     repeat = 0
end
begin
     prog = irexec
     button = left
     config = mpc seek -00:00:05
     repeat = 0
end
begin
     prog = irexec
     button = up
     config = mpc seek +1%
     repeat = 0
end
begin
     prog = irexec
     button = down
     config = mpc seek -1%
     repeat = 0
end

```

There are more functions for mpc, run [mpc(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mpc.1) for more info.

## PulseAudio

### Local (as your own user)

No special options are required; just add a pulse output as described in the comments of mpd's config file.

### Local (with separate mpd user)

When run as its own user as per the wiki instructions, mpd will be unable to send sound to another user's pulseaudio server. Rather than setting up pulseaudio as a system-wide daemon, a practice strongly discouraged by upstream, you can instead configure mpd to use pulseaudio's tcp module to send sound to localhost:

First, uncomment the tcp module in `/etc/pulse/default.pa` or `$XDG_CONFIG_HOME/pulse/default.pa` (typically `~/.config/pulse/default.pa`) and set 127.0.0.1 as an allowed IP address; the home directory takes precedence:

```
### Network access (may be configured with paprefs, so leave this commented
### here if you plan to use paprefs)
#load-module module-esound-protocol-tcp
load-module module-native-protocol-tcp auth-ip-acl=127.0.0.1
#load-module module-zeroconf-publish

```

Additional IP ranges in cidr notation may be added using `;` as the separator. Once this is complete, restart pulseaudio:

```
$ pulseaudio --kill
$ pulseaudio --start -or- start-pulseaudio-x11/kde

```

Next, edit `/etc/mpd.conf` and add a new pulse output pointing to 127.0.0.1 as a "remote" server:

```
audio_output {
       type		"pulse"
       name		"Local Music Player Daemon"
       server		"127.0.0.1"
}

```

Once this is added, restart mpd.

Enable the output in mpd; you should now have a working local mpd, usable by all users whose pulseaudio servers allow sound from 127.0.0.1.

### Remote

As with any PulseAudio-enabled program, mpd can send sound over the network. The complete PulseAudio system is not required on the server running mpd; [libpulse](https://www.archlinux.org/packages/?name=libpulse) is the only requirement to act as a source and is already a dependency of mpd.

In order to send audio from mpd to another computer follow the directions above, editing `/etc/mpd.conf` on the server running mpd using the IP address of the target computer and `/etc/pulse/default.pa` or `$XDG_CONFIG_HOME/default.pa` (typically `~/.config/pulse/default.pa`) on the target computer using the IP address of the server.

Once this is done, the server's mpd source should show up on the target computer while playing or paused as a normal source able to be rerouted and controlled as usual; there will be no visible source on the target while mpd is stopped.

## Cue Files

No additional steps are needed for cue support in mpd since 0.17\. MPD has its own integrated parser which works with both external and embedded cuesheets. For example, the command `mpc load albumx/x.cue` loads the file `*music_directory*/albumx/x.cue` as playlist; or in the case of an CUESHEET tag, `mpc load albumx/x.flac`.

Client support of CUE files is a bit limited. Two available programs that do support CUE files are [cantata](https://www.archlinux.org/packages/?name=cantata) and [ncmpcpp](/index.php/Ncmpcpp "Ncmpcpp").

## HTTP streaming

Since version 0.15 there is a built-in HTTP streaming daemon/server that comes with MPD.

### Configuration

To activate this server simply set it as output device in mpd.conf:

```
audio_output {
	type		"httpd"
	name		"My HTTP Stream"
	encoder		"vorbis"		# optional
	port		"8000"
#	quality		"5.0"			# do not define if bitrate is defined
	bitrate		"128"			# do not define if quality is defined
	format		"44100:16:1"
	always_on       "yes"			# prevent MPD from disconnecting all listeners when playback is stopped.
	tags            "yes"			# httpd supports sending tags to listening streams.
}

```

#### Format

MPD supports several encoding formats. See what your MPD supports with:

```
$ mpd --version

```

### Use

Then to listen to this stream simply open the URL of your mpd server (along with the specified port) in your favorite music player. Note: You may have to specify the file format of the stream using an appropriate file extension in the URL. For example, using Winamp 5.5, You would use [http://192.168.1.2:8000/mpd.ogg](http://192.168.1.2:8000/mpd.ogg) rather than [http://192.168.1.2:8000/](http://192.168.1.2:8000/).

To use mpd to connect to the stream from another computer:

```
mpc add [http://192.168.1.2:8000](http://192.168.1.2:8000)

```

## MPRIS2 Support

### mpDris2

**Note:** As of 2017-07-25, there are reports that mpDris2 would break [GDM](/index.php/GDM "GDM") if started as a service.

Install the [mpDris2](https://aur.archlinux.org/packages/mpDris2/) package. It runs in the user session and monitors the mpd server.

Copy the default configuration file from `/usr/share/doc/mpdris2/mpDris2.conf` to `~/.config/mpDris2/mpDris2.conf`. Edit it as needed.

mpDris2 has a `.desktop` file, but it will not show up by default. You can set this to autostart at login. If your desktop environment cannot do this, you can set it manually by making a symlink in `~/.config/autostart/`

```
$ ln -s /usr/share/applications/mpdris2.desktop ~/.config/autostart/

```

It should now be autorun at login.

### mpd-mpris

Install the [mpd-mpris](https://aur.archlinux.org/packages/mpd-mpris/) package.

After installation, you can start or enable the `mpd-mpris.service` user service through [systemd](/index.php/Systemd "Systemd").

By default mpd-mpris listens on `localhost:6600` (which is the default host/port of [mpd](/index.php/Mpd "Mpd")). To change this settings copy `/usr/lib/systemd/user/mpd-mpris.service` to `~/.config/systemd/user/` then edit run parameters as needed.

## Adding a separate volume control (ALSA)

While MPD does not allow you to adjust its own volume by default (`mpc volume` affects global volume), you can easily make a MPD-specific volume slider using the *softvol* [ALSA](/index.php/ALSA "ALSA") module. Just add this to `asound.conf`:

```
pcm.mpd {
    type softvol
    slave.pcm "default"
    control.name "MPD"
    control.card 0
}

```

And link it to MPD:

 `mpd.conf` 
```
audio_output {
    device "mpd"
    mixer_control "MPD"
}

```

Afterwards you will be able to adjust song volume both through `mpc` and `amixer`.