Livestreamer is a command-line utility written in [Python](/index.php/Python "Python"), which allows you to watch online video streams in popular video players, such as [VLC](/index.php/VLC "VLC"), [MPlayer](/index.php/MPlayer "MPlayer") or [mpv](/index.php/Mpv "Mpv") The full list of supported media players is available here: [https://livestreamer.readthedocs.org/en/latest/players.html](https://livestreamer.readthedocs.org/en/latest/players.html).

Support of a various streaming services is provided by a plugins, which can be easily added if needed. A lot of popular video streaming services are supported out of the box, including Dailymotion, Livestream, Twitch, UStream, YouTube Live and many more. List of all built-in plugins is available on [http://livestreamer.tanuki.se/en/latest/plugin_matrix.html](http://livestreamer.tanuki.se/en/latest/plugin_matrix.html).

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Twitch](#Twitch)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [livestreamer](https://www.archlinux.org/packages/?name=livestreamer), available from the [official repositories](/index.php/Official_repositories "Official repositories").

## Usage

Package provides a *livestreamer* command-line utility, which is a quite easy to use:

```
$ livestreamer -p *your_player* *url* *stream*

```

*   `your_player` — name of executable of your media player, for example, `vlc`. You can also specify a full path if needed: `/usr/bin/vlc`. By default, VLC will be used if it can be found in its default location.
*   `url` — URL address of a stream. You can omit protocol (`http://`) for HTTP URLs.
*   `stream` — stream to play by given URL. Primarily, you can select the video quality with this option. Use `best` for highest and `worst` for lowest quality available. Specific plugins may have additional quality options.

For example:

```
$ livestreamer -p mpv dailymotion.com/embed/video/x1b1h6o worst

```

See the `livestreamer (1)` [man page](/index.php/Man_page "Man page") for the full list of available options.

### Twitch

```
$ livestreamer -p *player* twitch.tv/*name_of_channel* *quality*

```

For example:

```
 $ livestreamer -p vlc twitch.tv/archlinux medium

```

Available stream qualities are: `source`, `high`, `medium`, `low` and `mobile`.

## See also

*   [Livestreamer repository on GitHub](https://github.com/chrippa/livestreamer)
*   [Livestreamer documentation](http://livestreamer.tanuki.se/en/latest)