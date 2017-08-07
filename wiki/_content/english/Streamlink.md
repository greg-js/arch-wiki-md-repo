[Streamlink](https://github.com/streamlink/streamlink) is a command-line utility written in [Python](/index.php/Python "Python") which allows you to watch online video streams in popular video players, such as [VLC](/index.php/VLC "VLC"), [MPlayer](/index.php/MPlayer "MPlayer") or [mpv](/index.php/Mpv "Mpv"); see [Player compatibility](https://streamlink.github.io/players.html#player-compatibility) for the full list.

This project was forked from [Livestreamer](/index.php/Livestreamer "Livestreamer"), which is no longer maintained.

Support for various streaming services is provided by plugins, which can be easily added if needed. A lot of popular video streaming services are supported out of the box, including Dailymotion, Livestream, Twitch, UStream, YouTube Live and many more; see [Plugins](https://streamlink.github.io/plugin_matrix.html) for the full list.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Twitch](#Twitch)
        *   [2.1.1 Authenticating With OAuth](#Authenticating_With_OAuth)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [streamlink](https://www.archlinux.org/packages/?name=streamlink) package or [streamlink-git](https://aur.archlinux.org/packages/streamlink-git/).

## Usage

The package provides a *streamlink* command-line utility, which is quite easy to use:

```
$ streamlink -p *your_player* *url* *stream*

```

*   `your_player` — name of executable of your media player, for example, `vlc`. You can also specify a full path if needed: `/usr/bin/vlc`. By default, VLC will be used if it can be found in its default location.
*   `url` — URL address of a stream. You can omit protocol (`http://`) for HTTP URLs.
*   `stream` — stream to play by given URL. Primarily, you can select the video quality with this option. Use `best` for highest and `worst` for lowest quality available. Specific plugins may have additional quality options.

For example:

```
$ streamlink -p mpv dailymotion.com/embed/video/x1b1h6o worst

```

See the `streamlink (1)` [man page](/index.php/Man_page "Man page") for the full list of available options.

### Twitch

```
$ streamlink -p *player* twitch.tv/*name_of_channel* *quality*

```

For example:

```
 $ streamlink -p vlc twitch.tv/archlinux medium

```

Available stream qualities are: `source`, `high`, `medium`, `low` and `mobile`.

#### Authenticating With OAuth

```
 $ streamlink --twitch-oauth-authenticate

```

This command will open a web browser with further instructions on authenticating with twitch.

The instructions only offer documentation for a configuration file, if you prefer not to use a configuration file, you can use:

```
 $ streamlink twitch.tv/*channel* --twitch-oauth-token *YourOAuthToken*

```

Where *YourOAuthToken* is the OAuth token you received in the previous step.

## See also

*   [Streamlink repository on GitHub](https://github.com/streamlink/streamlink)
*   [Streamlink documentation](https://streamlink.github.io/)