GStreamer is a pipeline-based multimedia framework written in the C programming language with the type system based on GObject.

GStreamer allows a programmer to create a variety of media-handling components, including simple audio playback, audio and video playback, recording, streaming and editing. The pipeline design serves as a base to create many types of multimedia applications such as video editors, streaming media broadcasters, and media players.

Designed to be cross-platform, it is known to work on Linux (x86, PowerPC and ARM), Solaris (Intel and SPARC), macOS, Microsoft Windows and OS/400\. GStreamer has bindings for programming-languages like [Python](/index.php/Python "Python"), C++, Perl, GNU Guile ([guile](https://www.archlinux.org/packages/?name=guile)), and [Ruby](/index.php/Ruby "Ruby"). GStreamer is free software, licensed under the GNU Lesser General Public License.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Current version plugins](#Current_version_plugins)
    *   [1.2 Legacy version plugins](#Legacy_version_plugins)
*   [2 Integration](#Integration)
    *   [2.1 PulseAudio](#PulseAudio)
    *   [2.2 Lightweight desktops](#Lightweight_desktops)
    *   [2.3 KDE / Phonon integration](#KDE_.2F_Phonon_integration)
    *   [2.4 Hardware acceleration](#Hardware_acceleration)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 assertion 'mini_object->refcount > 0' failed](#assertion_.27mini_object-.3Erefcount_.3E_0.27_failed)
*   [4 See also](#See_also)

## Installation

Install a GStreamer version from the [official repositories](/index.php/Official_repositories "Official repositories"):

*   [gstreamer](https://www.archlinux.org/packages/?name=gstreamer) - Current version.
*   [gstreamer0.10](https://www.archlinux.org/packages/?name=gstreamer0.10) - Legacy version.

To make GStreamer useful, install the plugins packages you require.

### Current version plugins

*   [gst-libav](https://www.archlinux.org/packages/?name=gst-libav) - Libav-based plugin containing many decoders and encoders.
*   [gst-plugins-bad](https://www.archlinux.org/packages/?name=gst-plugins-bad) - Plugins that need more quality, testing or documentation.
*   [gst-plugins-base](https://www.archlinux.org/packages/?name=gst-plugins-base) - Essential exemplary set of elements.
*   [gst-plugins-good](https://www.archlinux.org/packages/?name=gst-plugins-good) - Good-quality plugins under LGPL license.
*   [gst-plugins-ugly](https://www.archlinux.org/packages/?name=gst-plugins-ugly) - Good-quality plugins that might pose distribution problems.
*   [gst-plugin-libde265](https://aur.archlinux.org/packages/gst-plugin-libde265/) - [libde265](https://aur.archlinux.org/packages/libde265/) plugin (an open h.265 video codec implementation) for gstreamer.

### Legacy version plugins

**Tip:** Install all of them at once as [gstreamer0.10-plugins](https://www.archlinux.org/groups/x86_64/gstreamer0.10-plugins/).

*   [gstreamer0.10-bad-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-bad-plugins) - Plugins that need more quality, testing or documentation.
*   [gstreamer0.10-base-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-base-plugins) - Essential exemplary set of elements.
*   [gstreamer0.10-ffmpeg](https://www.archlinux.org/packages/?name=gstreamer0.10-ffmpeg) - Libav-based plugin containing many decoders and encoders.
*   [gstreamer0.10-good-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-good-plugins) - Good-quality plugins under LGPL license.
*   [gstreamer0.10-good-plugins-slim](https://aur.archlinux.org/packages/gstreamer0.10-good-plugins-slim/) - Good-quality plugins under LGPL license. GNOME and ASCII-art dependency removed.
*   [gstreamer0.10-ugly-plugins](https://www.archlinux.org/packages/?name=gstreamer0.10-ugly-plugins) - Good-quality plugins that might pose distribution problems.
*   [gstreamer0.10-plugin-libde265](https://aur.archlinux.org/packages/gstreamer0.10-plugin-libde265/) - [libde265](https://aur.archlinux.org/packages/libde265/) plugin (an open h.265 video codec implementation) for gstreamer0.10.

## Integration

### PulseAudio

[PulseAudio](/index.php/PulseAudio "PulseAudio") support is provided by *good* plugins packages.

### Lightweight desktops

To configure GStreamer, for example to change the audio output device, use *gstreamer-properties* from package [gstreamer-properties](https://aur.archlinux.org/packages/gstreamer-properties/). This can be run by each user or as root for all users. Per-user configuration files are under `$HOME/.gconf/system/gstreamer` and the global files are in `/etc/gconf/gconf.xml.defaults`.

### KDE / Phonon integration

See [Phonon](/index.php/Phonon "Phonon").

### Hardware acceleration

See [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

GStreamer will automatically detect and use the correct API [[1]](http://docs.gstreamer.com/display/GstSDK/Playback+tutorial+8%3A+Hardware-accelerated+video+decoding). Depending on your system you can [install](/index.php/Install "Install"):

*   [gstreamer-vaapi](https://www.archlinux.org/packages/?name=gstreamer-vaapi) for VA-API support.
*   [gst-plugins-bad](https://www.archlinux.org/packages/?name=gst-plugins-bad) for VDPAU support.

## Troubleshooting

### assertion 'mini_object->refcount > 0' failed

If you get an `GStreamer-CRITICAL **: gst_mini_object_unref: assertion 'mini_object->refcount > 0' failed` error (which usually occurs when recording video), you can [install](/index.php/Install "Install") [gstreamer0.10-ffmpeg](https://www.archlinux.org/packages/?name=gstreamer0.10-ffmpeg) to fix it.

## See also

*   [Sound](/index.php/Sound "Sound")
*   [http://gstreamer.freedesktop.org/](http://gstreamer.freedesktop.org/)