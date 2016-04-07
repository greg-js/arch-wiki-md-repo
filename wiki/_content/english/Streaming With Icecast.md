**Icecast** is a program for streaming media such as audio and video across a network. Different types of clients connect to the IceCast server, either to provide a "mount point", control the server, or listen to the audio being cast.

Icecast has support for streaming many audio streams simultaneously - each stream has a "mount point" which a client can access, usually through a network uri, such as:

```
http://server:8000/mpd.ogg.m3u

```

This refers to a mount point called "mpd".

## Contents

*   [1 Setting up Icecast](#Setting_up_Icecast)
*   [2 Icecast paths](#Icecast_paths)
    *   [2.1 Local user](#Local_user)
*   [3 Running icecast](#Running_icecast)
*   [4 Streaming with MPD](#Streaming_with_MPD)
    *   [4.1 Step 1: Set Up MPD and Install a Client](#Step_1:_Set_Up_MPD_and_Install_a_Client)
    *   [4.2 Step 2: Ensure Icecast is running](#Step_2:_Ensure_Icecast_is_running)
    *   [4.3 Step 3: Configure MPD to be an Icecast Source](#Step_3:_Configure_MPD_to_be_an_Icecast_Source)
    *   [4.4 Step 4: Running MPD with Icecast](#Step_4:_Running_MPD_with_Icecast)
    *   [4.5 Step 5: Test / use the stream](#Step_5:_Test_.2F_use_the_stream)
    *   [4.6 mpd](#mpd)
    *   [4.7 Sonata](#Sonata)
    *   [4.8 MPlayer](#MPlayer)
*   [5 Streaming with oggfwd and ffmpeg2theora](#Streaming_with_oggfwd_and_ffmpeg2theora)
*   [6 Playing the stream](#Playing_the_stream)
*   [7 References](#References)

## Setting up Icecast

*   [Install](/index.php/Install "Install") [icecast](https://www.archlinux.org/packages/?name=icecast). Alternatively, you can build and install the [icecast-kh](https://aur.archlinux.org/packages/icecast-kh/) package. Icecast-kh (Karl Heyes) extends on the official release with features that may be (if found to be working out well) merged into next official releases.
*   Edit the configuration file.

Open up /etc/icecast.xml in your text editor. The main section you want to pay attention to is <authentication>. Inside the <authentication> block there are all the passwords that icecast use. **It is strongly recommended** that you change them. Icecast defaults to listening on port 8000, and you may also change that if you wish.

Since icecast 2.3.2-4 the daemon is started as nobody user. Icecast-kh starts as icecast user by default. To change this behavior, pay attention to the <changeowner> section.

## Icecast paths

### Local user

Note that if you are running icecast under a local user (i.e. one that does not use /etc/icecast.xml) then you will need to copy the icecast web xml files from /usr/share otherwise you will get errors about XSLT and the web interface will not work.

```
$ cp -R /usr/share/icecast/web ~/icecast/

```

Also, make sure that the <changeowner> section is commented out, as changing the owner of a process requires root privileges.

## Running icecast

*   Start icecast

You can start icecast as a single user by executing:

```
# icecast -b -c /etc/icecast.xml

```

If you want icecast to remain in the foreground of your terminal, remove the -b flag.

To run icecast as a system daemon, [start](/index.php/Start "Start") the `icecast.service` systemd unit.

To run icecast at system boot, [enable](/index.php/Enable "Enable") the systemd unit.

*   Test it.

Make sure Icecast is running by opening up [http://localhost:8000/](http://localhost:8000/) in your web browser. You should be greeted by an Icecast2 Status page. This indicates everything is running properly.

Or run

```
# systemctl status icecast

```

## Streaming with MPD

MPD is a program for playing music via a daemon process instead of using a client. It also incorporates a music database for quick access, playlists, and a variety of front-end options.

**Note:** MPD has its own <u>built-in</u> HTTP Streaming, and using Icecast+mpd may not be needed. See [Music Player Daemon : HTTP Streaming](/index.php/Music_Player_Daemon/Tips_and_tricks#HTTP_Streaming "Music Player Daemon/Tips and tricks") for more information.

### Step 1: Set Up MPD and Install a Client

Use the [MPD Install Guide](/index.php/Mpd "Mpd") to install and configure MPD and a client.

### Step 2: Ensure Icecast is running

Start Icecast in first, or mpd will not have anything to stream :

```
# systemctl start icecast

```

### Step 3: Configure MPD to be an Icecast Source

Edit /etc/mpd.conf and enable the Icecast audio_output by adding the following:

```
audio_output {
    type        "shout"
    encoding    "ogg"
    name        "my cool stream"
    host        "localhost"
    port        "8000"
    mount       "/mpd.ogg"

# This is the source password in icecast.xml
    password    "hackme"

# Set either quality or bit rate
#   quality     "5.0"
    bitrate     "64"

    format      "44100:16:1"

# Optional Parameters
    user        "source"
#   description "here is my long description"
#   genre       "jazz"
} # end of audio_output

# Need this so that mpd still works if icecast is not running
audio_output {
    type "alsa"
    name "fake out"
    driver "null"
}

```

### Step 4: Running MPD with Icecast

Now you can start mpd :

```
# systemctl start mpd

```

Note that icecast must be started first for the stream to work.

### Step 5: Test / use the stream

Now that you have installed the necessary software you probably want to test/use the stream. Realize that you will need your client to do two things:

1.  Connect to the mpd server so you can control it
2.  Connect to the stream to actually hear the music. Connecting to the mpd server will alter output to the Icecast server but you will not hear it.

Sonata (a graphical mpd client) and mplayer (a command line client) are just two of the available clients. Note that if you use mplayer, you will need another way to control the remote mpd server (for example ssh)

### mpd

You can play an icecast stream from another mpd instance, on another computer, for example.

Use mpc to add the url to mpd's playlist

```
$ mpc add [http://ip.of.server:8000/mpd.ogg.m3u](http://ip.of.server:8000/mpd.ogg.m3u)

```

You can then play the stream as if it was a song belonging to your local mpd instance.

### Sonata

*   [Install](/index.php/Install "Install") the [sonata](https://www.archlinux.org/packages/?name=sonata) package.
*   Start it up and you should be greeted by Sonata's preferences.
*   Set 'Name' to the name of your server.
*   Set 'Host' to the IP address of your server.
*   Set 'Port' to '6600'.
*   Click the '+' and repeat the previous steps but instead about your local computer (i.e. its name and IP).
*   Right-click->'Connections' and select your server. Then click on the 'Library' tab, if all is well, you should see your entire music selection that is on your server. Find a folder, right-click and click 'Add'. Clicking on the 'Current' tab will show you your current playlist, which should have the contents of whatever folder you just chose from the library. Double-click on a song. You should see the text get bold and the progress bar show up, just like it is playing, but you will not hear anything. Fear not.
*   Right-click->'Connections' and select your local computer. Then click the 'Streams' tab. Right-click and click 'New'. Make 'Stream Name' the name from your servers /etc/mpd.conf file's audio_output { } section and make the URL IP.of.server:8000/mpd.ogg.m3u. Double-click on this stream.
*   Click on the 'Current' tab and you will see the URL of the stream as your only item. Double-click on it and after a delay you should hear whatever song you had chosen on the server.

### MPlayer

*   [Install](/index.php/Install "Install") the [mplayer](https://www.archlinux.org/packages/?name=mplayer) package.
*   Start it, telling it to play the playlist that icecast places in the icecast root directory (the playlist redirects mplayer to mpd.ogg)

```
$ mplayer -playlist [http://ip.of.server:8000/mpd.ogg.m3u](http://ip.of.server:8000/mpd.ogg.m3u)

```

To control the remote mpd server, if you have an ssh server on the same machine, you can login and use [ncmpcpp](/index.php/Ncmpcpp "Ncmpcpp")] to control it.

Or, if your mpd server is listening on an accessible interface/port (`$ ss -p -l -t` on the mpd machine will show mpd listening on 0.0.0.0, for example) then you can set the MPD_HOST variable which directs a local client like mpc to the remote server.

```
$ export MPD_HOST=ip.of.server
$ export MPD_PORT=6600      # optional
$ mpc play

```

## Streaming with oggfwd and ffmpeg2theora

If you want to stream a single track, for example, you can use this method instead of changing your mpd setup.

*   [Install](/index.php/Install "Install") the [ffmpeg2theora](https://www.archlinux.org/packages/?name=ffmpeg2theora) and [oggfwd](https://aur.archlinux.org/packages/oggfwd/) packages.

*   Start icecast using a previously setup config file using

```
$ icecast -c path/to/config.xml

```

or [start](/index.php/Start "Start") the systemd unit `icecast` instead.

*   Start ffmpeg2theora, sending its output to oggfwd, which forwards to the icecast server for you.

```
$ ffmpeg2theora --no-skeleton --novideo -o - path/to/audio/file | \
  oggfwd localhost 8000 source_password_here /mountpoint_name_here.ogg

```

Alternatively, you can use this script:

```
#!/bin/sh

if [ $# -eq 1 ] 
then
  music="$1"
else
  echo "Usage: $0 music-file"
  exit 1
fi

pass="source_password"
mountpt="mount_point_name"

set -e
ffmpeg2theora --no-skeleton --novideo -o - "$music" 2> /dev/null | \ 
  oggfwd localhost 8000 "$pass" /"$mountpt".ogg

```

## Playing the stream

The above mentioned sonata and mplayer methods can be used.

## References

*   [MPD Wiki: Configuration](http://mpd.wikia.com/wiki/Configuration)
*   [[1]](http://en.flossmanuals.net/TheoraCookbook/FfmpegStreaming) - oggfwd and ffmpeg2theora howto.