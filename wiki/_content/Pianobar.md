# Pianobar

[Pianobar](http://6xq.net/projects/pianobar/) is a free/open-source, console-based client for the personalized online radio [Pandora](http://www.pandora.com/).

_**Features**_

*   _play and manage (create, add more music, delete, rename, ...) stations_
*   _rate songs and explain why they have been selected_
*   _upcoming songs/song history_
*   _customize keybindings and text output_
*   _remote control and eventcmd interface (send tracks to last.fm, for example)_
*   _proxy support for listeners outside the USA_

**Tip:** Since Pianobar is a command line interface based program it can be placed in a different vterm than your desktop and be left to run.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Troubleshooting](#Troubleshooting)
*   [4 See also](#See_also)

## Installation

Pianobar can be installed from the [Official repositories](/index.php/Official_repositories "Official repositories") with the package [pianobar](https://www.archlinux.org/packages/?name=pianobar).

## Configuration

First, you need to create a configuration file for Pianobar. This should be located at `$XDG_CONFIG_HOME/pianobar/config` or `~/.config/pianobar/config`

 `$ man pianobar` 

```
CONFIGURATION
       The  configuration file consists of simple key = value lines, each ter‐
       minated with a newline (\n) character. Note that keys  and  values  are
       both  case  sensitive, and there must be exactly one space on each side
       of the equals sign.

       act_* keys control pianobar's key-bindings.  Every  one-byte  character
       except for \x00 and the special value disabled are allowed here.
```

Here is an example configuration file. See `man pianobar` for more configuration options.

 `$ ~/.config/pianobar/config` 

```
audio_quality = {high, medium, low}
autostart_station = stationid

password = plaintext_password
user = your@user.name
```

## Troubleshooting

If you are experiencing sound/quality issues when running pianobar, and you are currently using [ALSA](/index.php/ALSA "ALSA") as your sound driver, the following fixes may be useful.

**Warning:** The provided fixes may affect other applications that use audio as the default driver is being changed.

1.  Install [alsa-oss](https://www.archlinux.org/packages/?name=alsa-oss). See the [ALSA](/index.php/ALSA "ALSA") page for more information.
    *   Change the default libao driver from alsa to oss.
    *   ```
        # /etc/libao.conf
        default_driver=oss
        ```

    *   Now run pianobar
        *   `$ aoss pianobar` 
2.  Alternatively, you can use pulseaudio.
    *   ```
        # /etc/libao.conf
        default_driver=pulse
        ```

**Note:** Be sure to remove the dev=default option of the alsa driver or adjust it to specify a specific Pulse sink name or number.

## See also

*   [Project's homepage](http://6xq.net/projects/pianobar/)
*   [Project's GitHub](https://github.com/PromyLOPh/pianobar/)
*   [http://ketan.lithiumfox.com/doku.php/pianobar](http://ketan.lithiumfox.com/doku.php/pianobar)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Pianobar&oldid=389812](https://wiki.archlinux.org/index.php?title=Pianobar&oldid=389812)"