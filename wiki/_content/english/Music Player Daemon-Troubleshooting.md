Go back to [Music Player Daemon](/index.php/Music_Player_Daemon "Music Player Daemon").

## Contents

*   [1 Troubleshooting](#Troubleshooting)
    *   [1.1 Autodetection failed](#Autodetection_failed)
    *   [1.2 MPD hangs on first startup](#MPD_hangs_on_first_startup)
        *   [1.2.1 Easy Tag](#Easy_Tag)
        *   [1.2.2 Kid3](#Kid3)
    *   [1.3 Cannot connect to mpd: host "localhost" not found: Temporary failure in name resolution](#Cannot_connect_to_mpd:_host_.22localhost.22_not_found:_Temporary_failure_in_name_resolution)
    *   [1.4 Other issues when attempting to connect to mpd with a client](#Other_issues_when_attempting_to_connect_to_mpd_with_a_client)
        *   [1.4.1 First fix](#First_fix)
        *   [1.4.2 Second fix](#Second_fix)
    *   [1.5 Binding to IPV6 before IPV4](#Binding_to_IPV6_before_IPV4)
    *   [1.6 daemon: cannot setgid for user "mpd": Operation not permitted](#daemon:_cannot_setgid_for_user_.22mpd.22:_Operation_not_permitted)
    *   [1.7 daemon: fatal_error: Failed to set group NN: Operation not permitted](#daemon:_fatal_error:_Failed_to_set_group_NN:_Operation_not_permitted)
        *   [1.7.1 First fix](#First_fix_2)
        *   [1.7.2 Second fix](#Second_fix_2)
        *   [1.7.3 Third fix](#Third_fix)
    *   [1.8 MPD & ALSA](#MPD_.26_ALSA)
        *   [1.8.1 High CPU usage with ALSA](#High_CPU_usage_with_ALSA)
        *   [1.8.2 Playing audio files with different rate (works for EMU 0202/0204/0404)](#Playing_audio_files_with_different_rate_.28works_for_EMU_0202.2F0204.2F0404.29)

## Troubleshooting

### Autodetection failed

During the start of MPD, it tries to autodetect your set-up and configure output and volume control accordingly. Though this mostly goes well, it will fail for some systems. It may help to tell MPD specifically what to use as output and mixer control. If you copied `/etc/mpd.conf` over from `/etc/mpd.conf.example` as mentioned above, you can simply uncomment:

Example for alsa output type and alsa mixer:

```
audio_output {
	type			"alsa"
	name			"My ALSA Device"
	device			"hw:0,0"	# optional
	format			"44100:16:2"	# optional
	mixer_type		"hardware"
	mixer_device		"default"
	mixer_control		"PCM"
}

```

**Note:** in case of permission problems when using ESD with MPD run this as root:

```
# chsh -s /bin/true mpd

```

### MPD hangs on first startup

This is a common error that's caused by corrupt mp3 tags. Here is an experimental way to solve this issue. Requirements:

*   kid3
*   easytag

This method is very tedious, especially with a huge database. Just as a baseline it took 2.5h to fix a 16GB database.

#### Easy Tag

The purpose of [easytag](https://www.archlinux.org/packages/?name=easytag) here is that easytag detects the error in the tags, but like MPD it hangs and dies. The trick here is that easy tags actually tells you what file is causing the problem on the status bar. Before starting easytag make sure to have a terminal close to be ready to kill easy tag to avoid a hang. Once you are ready, on the tree view select the directory where all your music is located. By default easytag starts to search all subdirectories for mp3 files. Once you notice that easytag stopped scanning for songs, make note of the culprit and kill easytag.

**Note:** This task can also be achieved by editing mpd's config file and setting "log_level" from "default" to "verbose". restart mpd and look up the last entry in mpd's log file after mpd hangs. It is recommended to set "log_level" back to "default" after debugging, since the log file grows fast.

#### Kid3

Here's where [kid3](https://www.archlinux.org/packages/?name=kid3) comes in handy. With kid3 go to the offending song and rewrite one of the tags. then save the file. This should force kid3 to rewrite the whole tag again fixing the problem with MPD and easy tag hanging.

Repeat this procedure until your music library is done.

### Cannot connect to mpd: host "localhost" not found: Temporary failure in name resolution

Cannot connect to MPD (with ncmpcpp), if you are disconnected from network. Solution is [disable IPv6](/index.php/IPv6_-_Disabling_the_Module "IPv6 - Disabling the Module") or add line to /etc/hosts

```
::1 localhost.localdomain localhost

```

### Other issues when attempting to connect to mpd with a client

Some have reported being unable to access mpd with various clients, for example seeing errors like these:

```
$ ncmpcpp
Cannot connect to mpd: Connection closed by the server
$ sonata
2011-02-13 18:33:05  Connection lost while reading MPD hello
2011-02-13 18:33:05  Not connected
2011-02-13 18:33:05  Not connected

```

Please see posts on ncmpcpp on the Arch Forums [HERE](https://bbs.archlinux.org/viewtopic.php?id=109962) and [HERE](https://bbs.archlinux.org/viewtopic.php?id=113493). Also see [FS#22071](https://bugs.archlinux.org/task/22071).

#### First fix

Check `mpd.conf` for a line like `mpd.error` and remove it. The mpd error file is deprecated and has been removed.

#### Second fix

**Note:** I'm not so sure this is a good idea. There is a warning about changing the address to bind to in the default mpd.conf. If this does not help, you might want to comment out the changes.

If that doesn't help, add the following to `mpd.conf`:

```
 bind_to_address "127.0.0.1"
 port "6600"

```

Afterwards, instruct your client to connect via 127.0.0.1\. For example, add the following to the ncmpcpp config file:

```
 mpd_host "127.0.0.1"
 mpd_port "6600"

```

### Binding to IPV6 before IPV4

If on startup, mpd displays the following message:

```
listen: bind to '0.0.0.0:6600' failed: Address already in use (continuing anyway, because binding to '[::]:6600' succeeded)

```

MPD is attempting to bind to the ipv6 interface before binding to ipv4\. If you want to use your ipv4 interface, hardcode it in mpd.conf, like so:

```
bind_to_address "127.0.0.1"

```

Several binds can also be specified, for example, to have MPD listen on localhost and the external IP of your network card:

```
bind_to_address "127.0.0.1"
bind_to_address "192.168.1.13"

```

### daemon: cannot setgid for user "mpd": Operation not permitted

The error is stating that the user starting the process does not have permissions to become another user (mpd) which the configuration has told the process to run as.

To solve the issue, simply start mpd as root.

 `# systemctl start mpd` 

### daemon: fatal_error: Failed to set group NN: Operation not permitted

The error is stating that mpd can't set the group. This is if you have set any other group in `/etc/mpd.conf` than the default: mpd. This is because of the default `mpd.service` file. It starts mpd as user mpd (and if no group specified with the default group of this user as stated in your `/etc/passwd`) and therefore mpd does not have any rights to change his group.

#### First fix

In `/etc/mpd.conf` comment out the `group=` part or change it to `group=mpd`

#### Second fix

Create a custom `mpd.service` file in `/etc/systemd/system/` and add your desired group. E. g. run mpd with the group "audio":

 `/etc/systemd/system/mpd.service` 
```
.include /usr/lib/systemd/system/mpd.service
    [Service]
    Group=audio
```

#### Third fix

Change the default group of the user mpd in your `/etc/passwd`.

### MPD & ALSA

Sometimes, when using other audio outputs, e.g: some web pages containing Flash applets, MPD is rendered unable to play (until it is restarted). The error comes up in mpd's log:

```
Error opening alsa device "hw:0,0": Device or resource busy

```

Reasons for this may be:

*   The sound card does not support hardware mixing (uses **dmix** plugin)
*   An application does not work with ALSA's default settings

For a detailed description, it is recommended to take a look at [this](http://mpd.wikia.com/wiki/Alsa) link.

This problem may be solved by adding the following lines to `mpd.conf`:

 `mpd.conf` 
```
audio_output {
        type                    "alsa"
        name                    "Sound Card"
        options                 "dev=dmixer"
        device                  "plug:dmix"
}
```

To make the changes have effect, restart mpd (e.g. `systemctl restart mpd`, if it is a global configuration).

#### High CPU usage with ALSA

When using MPD with ALSA, users may experience MPD taking up lots of CPU (around 20-30%). This is caused by most sound cards supporting 48kHz and most music being 44.1kHz, thus forcing MPD to resample it. This operation takes lots of CPU cycles and results into high usage.

For most users the problem should be solved by telling MPD not to use resampling by adding `auto_resample "no"` into audio_output-part of `/etc/mpd.conf`.

 `mpd.conf` 
```
audio_output {
   type			"alsa"
   name			"My ALSA Device"
   auto_resample	"no"
}
```

Although it may not give as drastic a speedup, enabling mmap may still speed things up:

 `mpd.conf` 
```
audio_output {
   type			"alsa"
   name			"My ALSA Device"
   use_mmap		"yes"
}
```

Some users might also want to tell dmix to use 44kHz as well. More info about tuning performance of your MPD can be found on the [MPD wiki](http://mpd.wikia.com/wiki/Tuning)

#### Playing audio files with different rate (works for EMU 0202/0204/0404)

To play audio files of different rate with automatic card rate change install pulseaudio and pulseaudio-alsa and keep using ALSA as output:

 `mpd.conf` 
```
audio_output {
    type          "alsa"
    name          "Emu 0202 USB"
    device        "hw:2,0"
}
```