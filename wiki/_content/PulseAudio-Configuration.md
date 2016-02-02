# PulseAudio/Configuration

[PulseAudio](https://en.wikipedia.org/wiki/PulseAudio "wikipedia:PulseAudio") PulseAudio is a general purpose sound server intended to run as a middleware between your applications and your hardware devices, either using [ALSA](/index.php/ALSA "ALSA") or [OSS](/index.php/OSS "OSS"). In its default configuration, PulseAudio attemps to make controlling and routing audio streams to the correct place easier with its own graphical configuration tools and deep integration in some desktop environments, like the sound applet in [GNOME](/index.php/GNOME "GNOME") or veromix in [KDE](/index.php/KDE "KDE"). It also offers easy network streaming accross local devices using [Avahi](/index.php/Avahi "Avahi") if enabled. While its main purpose is to ease audio configuration, its modular design allows more advanced users to configure the daemon precisely to best suit their needs.

## Contents

*   [1 Installation](#Installation)
*   [2 Easy configuration](#Easy_configuration)
    *   [2.1 paprefs](#paprefs)
    *   [2.2 pavucontrol](#pavucontrol)
*   [3 Advanced configuration](#Advanced_configuration)
    *   [3.1 Configuration files](#Configuration_files)
        *   [3.1.1 daemon.conf](#daemon.conf)
        *   [3.1.2 default.pa](#default.pa)
        *   [3.1.3 client.conf](#client.conf)
    *   [3.2 Connection & authentication](#Connection_.26_authentication)
        *   [3.2.1 Environment variables](#Environment_variables)
        *   [3.2.2 X11 properties](#X11_properties)
*   [4 Modules](#Modules)
    *   [4.1 Protocols](#Protocols)
    *   [4.2 ALSA](#ALSA)
    *   [4.3 JACK](#JACK)
    *   [4.4 Filters & Routing](#Filters_.26_Routing)
*   [5 Further resources](#Further_resources)

## Installation

PulseAudio only requires the [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) package to run, but you may also want to install various other tools to help you configure it and integrate better with your desktop environment.

<caption>PulseAudio packages</caption>
| Package | Usage |<caption></caption>
| [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio) (required) | The main daemon, commandline tools and libraries. |<caption></caption>
| [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa) | Provides an `/etc/asound.conf` configuration file that sets the [ALSA](/index.php/ALSA "ALSA") default plugin to pulse, thus redirecting playback and capture to PulseAudio. Highly recommended to avoid conflicts between ALSA applications and PulseAudio if you intend to run PulseAudio all the time and use the default configuration. |<caption></caption>
| [paprefs](https://www.archlinux.org/packages/?name=paprefs) | A GUI for general daemon configuration. |<caption></caption>
| [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) | An advanced volume control GUI: allows to change the volume of individual streams and configure the ports of all sound cards. |<caption></caption>
| [ponymix](https://www.archlinux.org/packages/?name=ponymix) and [pamixer-git](https://aur.archlinux.org/packages/pamixer-git/)<sup><small>AUR</small></sup> | CLI mixers similar to pavucontrol. |<caption></caption>
| [PaWebControl](https://github.com/Siot/PaWebControl) | A web GUI similar to [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) to remotely control volumes (like from a mobile device). |<caption></caption>
| [pasystray-git](https://aur.archlinux.org/packages/pasystray-git/)<sup><small>AUR</small></sup> | A system tray for volume adjustment as well as a few basic operations like switching sinks and sources. |<caption></caption>
| [kdemultimedia-kmix](https://www.archlinux.org/packages/?name=kdemultimedia-kmix) | KDE's default volume control applet with similar functions to pavucontrol. |<caption></caption>
| [kdeplasma-applets-veromix](https://aur.archlinux.org/packages/kdeplasma-applets-veromix/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kdeplasma-applets-veromix)]</sup> | An advanced PulseAudio applet for KDE. |

## Easy configuration

By default, PulseAudio is configured to automatically detect all sound cards and manage them. It takes control of all detected ALSA devices and redirect all audio streams to itself, making the PulseAudio daemon the central configuration point. The daemon should work mostly out of the box, only requiring a few minor tweaks using the GUI configuration tools. All settings are saved in `~/.config/pulse` and automatically restored when the daemon starts. Use the following tools to configure the daemon to your taste:

### [paprefs](https://www.archlinux.org/packages/?name=paprefs)

*   Simultaneous output to all sound cards
*   Network device streaming and discovery (requires [Avahi](/index.php/Avahi "Avahi") daemon to be installed and running): play sound on any computer on your network from any computer.

### [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol)

*   Per-application volume control
*   Manage input and output devices volumes and outputs
*   Sound card configuration to select input/output ports to use and enable/disable devices

**Warning:** Do **not** attempt to change the ALSA configuration files while using the default PulseAudio configuration. The default configuration grabs the hardware devices directly in order to allow all the on-the-fly configurations using the GUIs. Changes to the ALSA configurations will very likely be ignored by PulseAudio and ALSA applications will break randomly while trying to access an ALSA device already used by PulseAudio. If you intend to change the ALSA configurations, also configure PulseAudio manually to output to your own ALSA device and play nice with your configuration.

## Advanced configuration

While PulseAudio usually runs fine out of the box and requires only minimal configuration, advanced users can change almost every aspect of the daemon by either altering the default configuration file to disable modules or writing your own from scratch. PulseAudio runs as a server daemon that can run either system-wide or on per-user basis using a client/server architecture. The daemon by itself does nothing without its modules except to provide an API and host dynamically loaded modules. The audio routing and processing tasks are all handled by various modules, including Pulse's native protocol itself (provided by [module-native-protocol-unix](http://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Modules/#index22h3)). Clients reach the server through one of many protocol modules that will accept audio from external sources, route it through PulseAudio and eventually have it go out through a final other module. The output module does not have to be an actual sound output: it can dump the stream into a file, stream it to a broadcasting server such as [Icecast](/index.php/Icecast "Icecast"), or even just discard it.

### Configuration files

PulseAudio can be configured in multiple ways depending on your needs and uses multiple different configuration files. Configuration files are read from `~/.pulse/` first, then from `/etc/pulse/` for system-wide defaults. People usually change the system-wide version unless they intend to have multiple users with different configurations.

#### `daemon.conf`

This is the main configuration file to configure the daemon itself. It defines base settings like the default sample rates used by modules, resampling methods, realtime scheduling and various other settings related to the server process. These can not be changed at runtime without restarting the PulseAudio daemon. Most defaults make sense here and are self-explaining, see the `pulse-daemon.conf` [man](/index.php/Man "Man") page for additional information. Boolean options accepts any of these: `true`, `yes`, `on` and `1` as well as `false`, `no`, `off` and `0`.

<caption>Notable configuration options</caption>
| Option | Description |<caption></caption>
| system-instance | If set to `yes`, the daemon will run as a system-wide instance. Highly discouraged as it can introduce security issues. Can be used when multiple users will use sound at the same time, either remotely or locally using [Xorg multiseat](/index.php/Xorg_multiseat "Xorg multiseat"). Defaults to `no`. |<caption></caption>
| realtime-scheduling | If your kernel supports realtime scheduling (for instance, [Kernels#-rt](/index.php/Kernels#-rt "Kernels") or [Kernels#-ck](/index.php/Kernels#-ck "Kernels")), set this to `yes` to ensure PulseAudio can deliver low-latency glitch-free playback. You can adjust `realtime-priority` as well to have it use the correct priority, especially when [JACK](/index.php/JACK "JACK") is also running on the system. |<caption></caption>
| exit-idle-time | If you want to run PulseAudio only when needed and use ALSA otherwise, you can set a delay in seconds after which the daemon will automatically shutdown after all clients are disconnected. Set it to -1 to disable this feature. |<caption></caption>
| resample-method | When PulseAudio needs to pass audio from one module to another using incompatible sample-rate (for example, playback at 96kHz to a card that only supports a maximum of 48kHz), specifies which resampler to use. You can use the command `$ pulseaudio --dump-resample-methods` to list all available resamplers and choose the best tradeoff between CPU usage and audio quality for your taste.

**Tip:** One of the major complaint about PulseAudio is its high CPU usage in some use cases. A lot of these cases happens when pulse needs to resample multiple streams (individually). If you intend to mix multiple sample rates often, consider creating an additional sink at the correct sample rate which you can then feed back to your main sink, resampling only once.

 |<caption></caption>
| enable-remixing | When the input and output have a different channel count (for example, outputting a 6 channel movie into a stereo sink), pulse can either remix all the channels (default, `yes`) or just trivially map the channels by their name (left goes to left, right to right, all others ignored) when `no` |<caption></caption>
| flat-volumes | If `yes` (default), all input sources have their volume relative to the maximum volume of the entire sound card. This allows each application to individually adjust their volume so for example, raising your VoIP call volume will raise the hardware volume and adjust your music player volume so it stays where it was, avoiding confusion by having to lower manually the music player then raise the global volume.

**Warning:** Sometimes this can be more confusing than what it solves and some applications unaware of this feature can set their volume at 100% at startup, potentially blowing your speakers or your ears. If unsure, prefer to set this to `no` so pulse will use the classic ALSA behavior instead.

 |<caption></caption>
| default-fragments | Audio samples are splitted into multiple fragments of `default-fragment-size-msec` each. The larger the buffer is, the less likely audio will skip when the system is overloaded, but will also increase the overall latency. Increase this value if you have issues. |<caption></caption>
| default-fragment-size-msec | The size in milliseconds of each fragment. This is the amount of data that will be processed at once by the daemon. TODO: Verify |

#### `default.pa`

This file is a startup script and is used to configure modules. It is actually parsed and read after the daemon has finished initializing and additional commands can be sent at runtime using `$ pactl` or `$ pacmd`. The startup script can also be provided on the command line by starting PulseAudio in a terminal using `$ pulseaudio -nC`. This will make the daemon load the CLI module and will accept the configuration directly from the command line, and output resulting information or error messages on the same terminal. This can be useful when debugging the daemon or just to test various modules before setting them permanently on disk. The manual page is quite self explaining, please consult `man pulse-cli-syntax` for the details of the syntax.

In order to configure the daemon, you will mostly only need the very basic commands:

<caption>Basic PA commands</caption>
| Command | Action |<caption></caption>
| `load-module module-name option1=value1 option2=value2` | Loads a module called `module-name` with two options called `option1` and `option2` |<caption></caption>
| `unload-module 42` or `unload-module module-alsa-sink` | Unloads a module by its index (returned by the load-module command) or all modules by name. |<caption></caption>
| `.fail` | Allows all commands after this statement to fail without interrupting the script and shutting down the daemon. This is useful when you know some commands could fail and would not affect overall operation, like loading modules for removable devices or network devices that can potentially get unreachable. |<caption></caption>
| `.nofail` | Reverse of .fail: failing commands after this statement will interrupt the script and will cause the daemon to return an error. |

There are plenty more commands available that are useful at runtime to control the daemon, see the `pactl` manpage for more details. Everything that an be made in `pavucontrol` can also be made on the command line, useful for bash scripts.

#### `client.conf`

This is the configuration file read by every PulseAudio client applications. It is used to configure runtime options for individual clients. It can be used to set the configure the default sink and source statically as well as allowing (or disallowing) clients to automatically start the server if not currently running.

<caption>Useful client.conf options</caption>
| Option | Description |<caption></caption>
| autospawn | If enabled, clients will automatically start PulseAudio if it is not already running when a client attempts to connect to it. This can be useful if you do not want PulseAudio to always be running to conserve system resources. Otherwise, you really should have it start with your X11 session. |

### Connection & authentication

Since PulseAudio runs as a daemon as the current user, clients needs to know where to find the daemon socket to connect to it as well as a shared random cookie file clients use to authenticate with it. By default, clients should be able to locate the daemon without problem using environment variables, X11 root window properties and finally by trying the default location (`unix:/run/user/$ID/pulse/native`). However, if you have clients that needs to access PulseAudio outside of your X11 session like [mpd](/index.php/Mpd "Mpd") running as a different user, you will need to tell it how to connect to your PulseAudio instance. See [PulseAudio/Examples#TODO](/index.php/PulseAudio/Examples#TODO "PulseAudio/Examples") for a complete example. An authentication cookie containing random bytes is enabled by default to ensure audio does not leak from one user to another on a multi-user system. If you already control who can access the server using user/group permissions, you can disable the cookie by passing `auth-cookie-enabled=0` to `module-native-protocol-unix`.

#### Environment variables

These two variables are the important ones in order for libpulse clients to locate PulseAudio if you moved its socket to somewhere else. See `man pulseaudio` for more details and other useful environment variables clients will read.

| Variable | Definition |<caption></caption>
| `PULSE_SERVER` | Defines where the server is. It takes a protocol prefix like `unix:` or `tcp` followed by the path or IP of the server. Example: `unix:/home/pulse/native-sock`. |<caption></caption>
| `PULSE_COOKIE` | Point this to the location of a file that contains the random cookie generated by PulseAudio. This file will be read by clients and its content sent to the server, thus the file has to be readable by all audio clients. It does not need to be the same file, as long as its content matches the one the daemon uses. |

#### X11 properties

PulseAudio also uses window properties on the root window of the X11 server to help find the daemon. Since environment variables cannot be modified after child processes are started , X11 properties are more flexible because they are more easily changed because they are globally shared. As long as applications receive a `DISPLAY=` environment variable, it can read the most up-to-date values. X11 properties can be queried using `xprop -root`, or with `pax11publish -d` to read pulse-specific properties. `pax11publish` can also be used to update the properties from environment variables (`pax11publish -e` or remove them entirely . If possible, it is recommended to let PulseAudio do it my itself using the module-x11-publish module or the `start-pulseaudio-x11` command. The following table is there only for completeness, you should not ever need to manually set these variables by hand.

| Variable | Definition |<caption></caption>
| `PULSE_SERVER` | String value (`xprop -root -f PULSE_SERVER 8s -set PULSE_SERVER "unix:/tmp/pulse-sock"`), works the same as the environment variable of the same name. |<caption></caption>
| `PULSE_COOKIE` | String value that contains the hexadecimal representation of the authentication cookie. |

## Modules

### Protocols

### ALSA

### JACK

### Filters & Routing

## Further resources

Retrieved from "[https://wiki.archlinux.org/index.php?title=PulseAudio/Configuration&oldid=392594](https://wiki.archlinux.org/index.php?title=PulseAudio/Configuration&oldid=392594)"