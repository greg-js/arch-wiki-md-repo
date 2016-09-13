Twitch.tv is one of the more popular [RTMP](https://en.wikipedia.org/wiki/Real_Time_Messaging_Protocol "wikipedia:Real Time Messaging Protocol") based streaming services offered. As [Steam](/index.php/Steam "Steam") has a Linux client available, some people may be in search of solutions to stream their games or Linux desktop. As there are no well known Linux broadcasting programs just yet, most solutions at this point are CLI based. The info included here should serve as a list of such solutions.

## Contents

*   [1 Twitch streaming Guidelines](#Twitch_streaming_Guidelines)
*   [2 GUI solutions](#GUI_solutions)
*   [3 Ffmpeg solutions](#Ffmpeg_solutions)
    *   [3.1 .bashrc script method](#.bashrc_script_method)

## Twitch streaming Guidelines

*From* [Twitch.tv support](http://help.twitch.tv/customer/portal/articles/1253460-broadcast-requirements):

**Video Requirements**

*   Codec: H.264 (x264)
*   Mode: Strict CBR
*   Keyframe Interval: 2 seconds

**Audio Requirements**

*   Codec: AAC-LC or MP3, Stereo or Mono
*   Maximum bit rate: 160 kbps (AAC), 128 kbps (MP3)
*   Sampling frequency: any (AAC), 44.1 KHz (MP3)

**Other Requirements**

Not listed on their page is a requirement of the [Y'UV420p pixel format](https://en.wikipedia.org/wiki/YUV#Y.27UV420p_.28and_Y.27V12_or_YV12.29_to_RGB888_conversion "wikipedia:YUV"), as Y'UV444 is not widely supported just yet.

## GUI solutions

*   Castawesome ([castawesome](https://aur.archlinux.org/packages/castawesome/) from the [AUR](/index.php/AUR "AUR")) is a Gtk3 frontend for ffmpeg streaming with builtin Twitch.tv support.

*   Open Broadcaster Software ([obs-studio](https://www.archlinux.org/packages/?name=obs-studio)) is a popularly used software on Windows. *Note that the package is **not an official build**.* Alpha Linux builds ([obs-studio-git](https://aur.archlinux.org/packages/obs-studio-git/) from the [AUR](/index.php/AUR "AUR")) are also available for compiling & testing.

*   SimpleScreenRecorder ([lib32-simplescreenrecorder](https://www.archlinux.org/packages/?name=lib32-simplescreenrecorder) from the [official repositories](/index.php/Official_repositories "Official repositories")) can be configured to stream to twitch.
    *   For this to work:
        *   The container needs to be set to FLV
        *   RTMP URL needs to be put in the 'save as' field
        *   make sure 'separeate file per segment' is unchecked
        *   video codec set to libx264 (NOT H.264)
        *   set bitrate to reasonable value, such as 2000 kbps
        *   in the custom option field, enter `preset=fast,minrate=2000,maxrate=2000,bufsize=2000,keyint=60`
        *   Note: The value of 'minrate', 'maxrate' and 'bufsize' should be equal to the bit rate

## Ffmpeg solutions

These solutions revolve around making use of the [FFmpeg](/index.php/FFmpeg "FFmpeg") package:

### .bashrc script method

One method of streaming to twitch using FFMPEG makes use of a simple script that is placed in a user's ~/.bashrc file. this script supports streaming of both desktop and OpenGL elements.

*   Depending on your internet upload speed, you may need to modify the Ffmpeg parameters. use the breakdown list for reference.

The script can be used by typing

```
streaming streamkeyhere

```

into a terminal. While it is running, use **pavucontrol** to edit sound sources. The .bashrc script is as follows:

```
 streaming() {
     INRES="1920x1080" # input resolution
     OUTRES="1920x1080" # output resolution
     FPS="15" # target FPS
     GOP="30" # i-frame interval, should be double of FPS, 
     GOPMIN="15" # min i-frame interval, should be equal to fps, 
     THREADS="2" # max 6
     CBR="1000k" # constant bitrate (should be between 1000k - 3000k)
     QUALITY="ultrafast"  # one of the many FFMPEG preset
     AUDIO_RATE="44100"
     STREAM_KEY="$1" # use the terminal command Streaming streamkeyhere to stream your video to twitch or justin
     SERVER="live-fra" # twitch server in frankfurt, see [http://bashtech.net/twitch/ingest.php](http://bashtech.net/twitch/ingest.php) for list

     ffmpeg -f x11grab -s "$INRES" -r "$FPS" -i :0.0 -f alsa -i pulse -f flv -ac 2 -ar $AUDIO_RATE \
       -vcodec libx264 -g $GOP -keyint_min $GOPMIN -b:v $CBR -minrate $CBR -maxrate $CBR -pix_fmt yuv420p\
       -s $OUTRES -preset $QUALITY -tune film -acodec libmp3lame -threads $THREADS -strict normal \
       -bufsize $CBR "rtmp://$SERVER.twitch.tv/app/$STREAM_KEY"
 }

```

<caption>**Ffmpeg Parameter breakdown**</caption>
| Parameter | Description |
| ffmpeg | The converter |
| -f x11grab | -f forces input to be from x11grab |
| -s $INRES | -s sets a specific image size, relying on the variable $INRES |
| -r $FPS | -r sets framerate to be the value equal to $FPS |
| -i :0.0 | -i gets input, in this case its pulling in screen :0.0 from x11\. Can be adjusted, e.g. -i :0.0+500,100 to start at screenpos 500/100 |
| -b:v $CBR | -b:v specifies that the video bitrate is to be changed. the value of the bitrate is set by $CBR |
| -ab 96k | -ab sets audio bitrate to 96k. **-b:a** is the alternate form of this command |
| -f alsa | forces input(?) to be from alsa |
| -ac 2 | sets audio channels to 2 |
| -i pulse | gets input from pulse |
| -vcodec libx264 | sets video codec to libx264 |
| -crf 23 | sets the ffmpeg constant rate factor to 23 |
| -preset "$QUAL" | sets the preset compression quality and speed |
| -s "1280x720" | specifies size of image to be 720p |
| -acodec libmp3lame | sets audio codec to use libmp3lame |
| -ar 44100 | sets audio rate to 44100 hz |
| -threads 0 | sets cpu threads to start, 0 autostarts threads based on cpu cores |
| -pix_fmt yuv420p | sets pixel format to Y'UV420p. Otherwise by default Y'UV444 is used and is incompatible with twitch |
| -f flv "$URL" | forces format to flv, and outputs to the twitch RTMP url |