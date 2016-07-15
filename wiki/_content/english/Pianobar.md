[Pianobar](http://6xq.net/projects/pianobar/) is a free/open-source, console-based client for the personalized online radio [Pandora](http://www.pandora.com/).

***Features***

*   *play and manage (create, add more music, delete, rename, ...) stations*
*   *rate songs and explain why they have been selected*
*   *upcoming songs/song history*
*   *customize keybindings and text output*
*   *remote control and eventcmd interface (send tracks to last.fm, for example)*
*   *proxy support for listeners outside the USA*

**Tip:** Since Pianobar is a command line interface based program it can be placed in a different vterm than your desktop and be left to run.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Sound Quality Issues](#Sound_Quality_Issues)
    *   [3.2 Network Error](#Network_Error)
*   [4 See also](#See_also)

## Installation

Pianobar can be installed from the [Official repositories](/index.php/Official_repositories "Official repositories") with the package [pianobar](https://www.archlinux.org/packages/?name=pianobar).

## Configuration

First, you need to create a configuration file for Pianobar. This should be located at `$XDG_CONFIG_HOME/pianobar/config` or `~/.config/pianobar/config`

 `$ man pianobar` 
```
CONFIGURATION
       The  configuration file consists of simple key = value lines, each ter‐
       minated with a newline (
) character. Note that keys  and  values  are
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

### Sound Quality Issues

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

### Network Error

If you are receiving the "Network error: TLS fingerprint mismatch" error when running pianobar the following fixes may be useful.

1.  obtain the current tls_fingerprint by running the following command:
     `# openssl s_client -connect tuner.pandora.com:443 < /dev/null 2> /dev/null | openssl x509 -noout -fingerprint | tr -d ':' | cut -d'=' -f2` 
2.  add this output to ~/.config/pianobar/config:

    ```
    ~/.config/pianobar/config

    audio_quality = high
    password = password
    user = email address
    tls_fingerprint = 13CC51AC0C31CD96C55015C76914360F7AC41A00
    ```

## See also

*   [Project's homepage](http://6xq.net/projects/pianobar/)
*   [Project's GitHub](https://github.com/PromyLOPh/pianobar/)
*   [https://wiki.k2patel.in/pianobar](https://wiki.k2patel.in/pianobar)