## Contents

*   [1 Easy configuration](#Easy_configuration)
*   [2 Advanced configuration](#Advanced_configuration)
    *   [2.1 Configuration files](#Configuration_files)
        *   [2.1.1 default.pa](#default.pa)
        *   [2.1.2 client.conf](#client.conf)
    *   [2.2 Connection & authentication](#Connection_.26_authentication)
        *   [2.2.1 Environment variables](#Environment_variables)
        *   [2.2.2 X11 properties](#X11_properties)
*   [3 Modules](#Modules)
    *   [3.1 Protocols](#Protocols)
    *   [3.2 ALSA](#ALSA)
    *   [3.3 JACK](#JACK)
    *   [3.4 Filters & Routing](#Filters_.26_Routing)

## Easy configuration

*   [paprefs](https://www.archlinux.org/packages/?name=paprefs)
    *   Simultaneous output to all sound cards
    *   Network device streaming and discovery (requires [Avahi](/index.php/Avahi "Avahi") daemon to be installed and running): play sound on any computer on your network from any computer.

*   [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol)
    *   Per-application volume control
    *   Manage input and output devices volumes and outputs
    *   Sound card configuration to select input/output ports to use and enable/disable devices

**Warning:** Do **not** attempt to change the ALSA configuration files while using the default PulseAudio configuration. The default configuration grabs the hardware devices directly in order to allow all the on-the-fly configurations using the GUIs. Changes to the ALSA configurations will very likely be ignored by PulseAudio and ALSA applications will break randomly while trying to access an ALSA device already used by PulseAudio. If you intend to change the ALSA configurations, also configure PulseAudio manually to output to your own ALSA device and play nice with your configuration.

## Advanced configuration

### Configuration files

#### default.pa

In order to configure the daemon, you will mostly only need the very basic commands:

<caption>Basic PA commands</caption>
| Command | Action |<caption></caption>
| `load-module module-name option1=value1 option2=value2` | Loads a module called `module-name` with two options called `option1` and `option2` |<caption></caption>
| `unload-module 42` or `unload-module module-alsa-sink` | Unloads a module by its index (returned by the load-module command) or all modules by name. |<caption></caption>
| `.fail` | Allows all commands after this statement to fail without interrupting the script and shutting down the daemon. This is useful when you know some commands could fail and would not affect overall operation, like loading modules for removable devices or network devices that can potentially get unreachable. |<caption></caption>
| `.nofail` | Reverse of .fail: failing commands after this statement will interrupt the script and will cause the daemon to return an error. |

There are plenty more commands available that are useful at runtime to control the daemon, see the `pactl` manpage for more details. Everything that an be made in `pavucontrol` can also be made on the command line, useful for bash scripts.

#### client.conf

<caption>Useful client.conf options</caption>
| Option | Description |<caption></caption>
| autospawn | If enabled, clients will automatically start PulseAudio if it is not already running when a client attempts to connect to it. This can be useful if you do not want PulseAudio to always be running to conserve system resources. Otherwise, you really should have it start with your X11 session. |

### Connection & authentication

Since PulseAudio runs as a daemon as the current user, clients needs to know where to find the daemon socket to connect to it as well as a shared random cookie file clients use to authenticate with it. By default, clients should be able to locate the daemon without problem using environment variables, X11 root window properties and finally by trying the default location (`unix:/run/user/$ID/pulse/native`). However, if you have clients that needs to access PulseAudio outside of your X11 session like [mpd](/index.php/Mpd "Mpd") running as a different user, you will need to tell it how to connect to your PulseAudio instance. See [PulseAudio/Examples#Allowing multiple users to use PulseAudio at the same time](/index.php/PulseAudio/Examples#Allowing_multiple_users_to_use_PulseAudio_at_the_same_time "PulseAudio/Examples") for a complete example. An authentication cookie containing random bytes is enabled by default to ensure audio does not leak from one user to another on a multi-user system. If you already control who can access the server using user/group permissions, you can disable the cookie by passing `auth-cookie-enabled=0` to `module-native-protocol-unix`.

#### Environment variables

These two variables are the important ones in order for libpulse clients to locate PulseAudio if you moved its socket to somewhere else. See [pulseaudio(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pulseaudio.1) for more details and other useful environment variables clients will read.

| Variable | Definition |<caption></caption>
| `PULSE_SERVER` | Defines where the server is. It takes a protocol prefix like `unix:` or `tcp` followed by the path or IP of the server. Example: `unix:/home/pulse/native-sock`. |<caption></caption>
| `PULSE_COOKIE` | Point this to the location of a file that contains the random cookie generated by PulseAudio. This file will be read by clients and its content sent to the server, thus the file has to be readable by all audio clients. It does not need to be the same file, as long as its content matches the one the daemon uses. |

#### X11 properties

PulseAudio also uses window properties on the root window of the X11 server to help find the daemon. Since environment variables cannot be modified after child processes are started, X11 properties are more flexible because they are more easily changed because they are globally shared. As long as applications receive a `DISPLAY=` environment variable, it can read the most up-to-date values. X11 properties can be queried using `xprop -root`, or with `pax11publish -d` to read pulse-specific properties. `pax11publish` can also be used to update the properties from environment variables (`pax11publish -e`, or `pax11publish -r` to remove them entirely). If possible, it is recommended to let PulseAudio do it my itself using the module-x11-publish module or the `start-pulseaudio-x11` command. The following table is there only for completeness, you should not ever need to manually set these variables by hand.

| Variable | Definition |<caption></caption>
| `PULSE_SERVER` | String value (`xprop -root -f PULSE_SERVER 8s -set PULSE_SERVER "unix:/tmp/pulse-sock"`), works the same as the environment variable of the same name. |<caption></caption>
| `PULSE_COOKIE` | String value that contains the hexadecimal representation of the authentication cookie. |

## Modules

### Protocols

### ALSA

### JACK

### Filters & Routing