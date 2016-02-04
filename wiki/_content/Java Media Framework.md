# Java Media Framework

From [Sun JMF site](http://java.sun.com/products/java-media/jmf/): "The Java Media Framework API (JMF) enables audio, video and other time-based media to be added to applications and applets built on Java technology. This optional package, which can capture, playback, stream, and transcode multiple media formats, extends the Java 2 Platform, Standard Edition (J2SE) for multimedia developers by providing a powerful toolkit to develop scalable, cross-platform technology."

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 JMFRegistry](#JMFRegistry)
*   [3 Adding audio/video codecs support to JMF](#Adding_audio.2Fvideo_codecs_support_to_JMF)
    *   [3.1 Sun MP3 Plugin](#Sun_MP3_Plugin)
    *   [3.2 JFFMpeg](#JFFMpeg)
        *   [3.2.1 Reinstalling JMF and JffMpeg](#Reinstalling_JMF_and_JffMpeg)
*   [4 Testing JMF capabilities](#Testing_JMF_capabilities)
*   [5 Adding media support to OpenOffice.org](#Adding_media_support_to_OpenOffice.org)
    *   [5.1 Testing media capabilities in OpenOffice.org](#Testing_media_capabilities_in_OpenOffice.org)

## Installation

Install [jmf](https://aur.archlinux.org/packages/jmf/) from [AUR](/index.php/AUR "AUR").

## Configuration

In order to setup JMF for the first time (to recognize audio and capture devices) you will need to **run as root**:

```
jmfinit

```

_(An active X11 session is needed)_

### JMFRegistry

You can manually setup JMF (GUI) running as root:

```
jmfregistry

```

[JMFRegistry User's Guide](http://java.sun.com/products/java-media/jmf/2.1.1/jmfregistry/jmfregistry.html)

## Adding audio/video codecs support to JMF

### Sun MP3 Plugin

[Sun MP3 Plugin](http://java.sun.com/products/java-media/jmf/mp3/download.html) is included in the JMF package and **installed by default** with it.

If there is any trouble you can **reinstall** the MP3Plugin **running as root**:

```
jmfRegisterMp3Plugin

```

### JFFMpeg

"[Jffmpeg](http://jffmpeg.sourceforge.net/) is a plugin that allows the playback of a number of common audio and video formats. It is based around a Java port of parts of the FFMPEG project, supporting a number of codecs in pure Java code. Where codecs have not yet been ported, a JNI wrapper allows calls directly into the full FFMPEG code."

Install [jffmpeg](https://aur.archlinux.org/packages/jffmpeg/) from [AUR](/index.php/AUR "AUR").

The install script will register the plugins and associate the mimetypes in the JMF registry and the uninstall script will unregister the plugins from the JMF registry.

#### Reinstalling JMF and JffMpeg

If you reinstall JMF you will have to **run as root**:

```
jmfRegisterJffmpegPlugin

```

in order to register again all the jffmpeg plugins in the JMF registry

## Testing JMF capabilities

A demo player is available to test JMF audio/video playback capabilities.

```
java JMStudio

```

You can also check if JMF is properly installed in: [http://ku-prism.org/virtualprism/explorations/JavaTest/javatestpage.html](http://ku-prism.org/virtualprism/explorations/JavaTest/javatestpage.html) (it currently works on Firefox2/3 and Opera)

If your JMF installation is OK you should get something like:

```
JMF Version... 2.1.1e
All Java Build
Native Libraries Found

```

## Adding media support to OpenOffice.org

If you want to be able to use sound and video in [OpenOffice.org](/index.php/OpenOffice.org "OpenOffice.org") documents and presentations, you must:

1.  Start OpenOffice.org
2.  Go to Tools/Options - Java Section
    1.  Make sure Java support in OpenOffice.org is **enabled**
3.  Select "Class Path"
4.  Select "Add Folder"
5.  Add "**/opt/java/jre/lib/ext/**" (without quotes)
6.  Select "Add Folder"
7.  Add "**/opt/java/jre/lib/**" (without quotes)
8.  Save changes
9.  Restart OpenOffice.org

### Testing media capabilities in OpenOffice.org

1.  Start OpenOffice.org
2.  Go to Tools/Gallery
3.  Select "Sounds"
4.  Double click any sound file - A media player will open and the sound will be played

Retrieved from "[https://wiki.archlinux.org/index.php?title=Java_Media_Framework&oldid=392295](https://wiki.archlinux.org/index.php?title=Java_Media_Framework&oldid=392295)"