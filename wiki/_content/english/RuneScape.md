From [Wikipedia](https://en.wikipedia.org/wiki/RuneScape "wikipedia:RuneScape"):

	RuneScape is a fantasy massively multiplayer online role-playing game (MMORPG) released in January 2001 by Andrew and Paul Gower, and developed and published by Jagex Games Studio. It is a graphical browser game implemented on the client-side in Java or HTML5, and incorporates 3D rendering. The game has had over 200 million accounts created and is recognised by the Guinness World Records as the world's largest free MMORPG and the most-updated game.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Methods to play](#Methods_to_play)
    *   [1.1 RuneScape NXT](#RuneScape_NXT)
    *   [1.2 Rsu-client](#Rsu-client)
    *   [1.3 OSBuddy (Old School RuneScape only)](#OSBuddy_(Old_School_RuneScape_only))
    *   [1.4 RuneLite (Old School RuneScape only)](#RuneLite_(Old_School_RuneScape_only))
        *   [1.4.1 GPU Plugin](#GPU_Plugin)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Audio issues](#Audio_issues)
    *   [2.2 SSL errors](#SSL_errors)

## Methods to play

### RuneScape NXT

Install the official RuneScape NXT client with the [runescape-launcher](https://aur.archlinux.org/packages/runescape-launcher/) package.

### Rsu-client

**Note:** If you are unable to install the client from the AUR because of a problem with [perl-wx](https://aur.archlinux.org/packages/perl-wx/), remove it from the [depends array](/index.php/PKGBUILD#depends "PKGBUILD"). [perl-wx](https://aur.archlinux.org/packages/perl-wx/) is needed for the [GUI](https://en.wikipedia.org/wiki/Graphical_user_interface "wikipedia:Graphical user interface"). The client will work fine without it, but you will not have a [GUI](https://en.wikipedia.org/wiki/Graphical_user_interface "wikipedia:Graphical user interface").

[Rsu-client](https://github.com/HikariKnight/rsu-client) is an unofficial RuneScape Unix/Linux client for RuneScape/Old School RuneScape. It can be installed with the [unix-runescape-client](https://aur.archlinux.org/packages/unix-runescape-client/) package. After installation, to start playing, open either “RuneScape” or “RuneScape OldSchool”, depending on what version you are interested in.

### OSBuddy (Old School RuneScape only)

[OSBuddy](https://rsbuddy.com/osbuddy/) is a third-party toolkit for Old School RuneScape which in addition to a client offers useful features, such as highscores, notes, price checker etc. It's available for installation from the AUR, [osbuddy](https://aur.archlinux.org/packages/osbuddy/).

### RuneLite (Old School RuneScape only)

[RuneLite](https://runelite.net/) is an open-source alternative to other third-party Old School RuneScape clients. It is available on the AUR: [runelite](https://aur.archlinux.org/packages/runelite/).

#### GPU Plugin

To enable the GPU feature within RuneLite, ensure you meet the [requirements](https://github.com/runelite/runelite/wiki/GPU-FAQ) and have updated to the latest version of [mesa](https://www.archlinux.org/packages/?name=mesa).

## Troubleshooting

### Audio issues

The Java client (jagexappletviewer.jar) requires [pulseaudio-alsa](https://www.archlinux.org/packages/?name=pulseaudio-alsa) to be installed for sound to work properly. Otherwise there will be no in-game sound or other applications will not be able to play audio due to the client claiming direct access to `/dev/snd/*` devices. For more details, see [PulseAudio#ALSA](/index.php/PulseAudio#ALSA "PulseAudio").

### SSL errors

If you receive an error like this (with RuneLite or otherwise):

```
javax.net.ssl.SSLHandshakeException: Received fatal alert: handshake_failure

```

This error may be due to Java's new TLSv1.3 implementation. Try adding `-Djdk.tls.client.protocols=TLSv1.2` to your client's launch options. For example:

```
java -Djdk.tls.client.protocols=TLSv1.2 -jar RuneLite.jar

```