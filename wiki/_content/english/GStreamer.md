[GStreamer](https://en.wikipedia.org/wiki/GStreamer "wikipedia:GStreamer") is a pipeline-based multimedia framework written in the C programming language with the type system based on GObject.

GStreamer allows a programmer to create a variety of media-handling components, including simple audio playback, audio and video playback, recording, streaming and editing. The pipeline design serves as a base to create many types of multimedia applications such as video editors, streaming media broadcasters, and media players.

Designed to be cross-platform, it is known to work on Linux (x86, PowerPC and ARM), Solaris (Intel and SPARC), macOS, Microsoft Windows and OS/400\. GStreamer has bindings for programming-languages like [Python](/index.php/Python "Python"), C++, Perl, GNU Guile ([guile](https://www.archlinux.org/packages/?name=guile)), and [Ruby](/index.php/Ruby "Ruby"). GStreamer is free software, licensed under the GNU Lesser General Public License.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Integration](#Integration)
    *   [2.1 PulseAudio](#PulseAudio)
    *   [2.2 KDE / Phonon integration](#KDE_/_Phonon_integration)
    *   [2.3 Hardware video acceleration](#Hardware_video_acceleration)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [gstreamer](https://www.archlinux.org/packages/?name=gstreamer) package.

To make GStreamer useful, install the plugins packages you require. See [official documentation](https://gstreamer.freedesktop.org/documentation/plugins.html) for list of features in each plugin.

*   [gst-libav](https://www.archlinux.org/packages/?name=gst-libav) - Libav-based plugin containing many decoders and encoders.
*   [gst-plugins-bad](https://www.archlinux.org/packages/?name=gst-plugins-bad) - Plugins that need more quality, testing or documentation.
*   [gst-plugins-base](https://www.archlinux.org/packages/?name=gst-plugins-base) - Essential exemplary set of elements.
*   [gst-plugins-good](https://www.archlinux.org/packages/?name=gst-plugins-good) - Good-quality plugins under LGPL license.
*   [gst-plugins-ugly](https://www.archlinux.org/packages/?name=gst-plugins-ugly) - Good-quality plugins that might pose distribution problems.
*   [gst-plugin-libde265](https://aur.archlinux.org/packages/gst-plugin-libde265/) - [libde265](https://www.archlinux.org/packages/?name=libde265) plugin (an open h.265 video codec implementation) for gstreamer.

## Integration

### PulseAudio

[PulseAudio](/index.php/PulseAudio "PulseAudio") support is provided by the [gst-plugins-good](https://www.archlinux.org/packages/?name=gst-plugins-good) package.

### KDE / Phonon integration

See [Phonon](/index.php/Phonon "Phonon").

### Hardware video acceleration

See [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

GStreamer will automatically detect and use the correct API [[1]](https://gstreamer.freedesktop.org/documentation/tutorials/playback/hardware-accelerated-video-decoding.html). Depending on your system you can [install](/index.php/Install "Install"):

*   [gstreamer-vaapi](https://www.archlinux.org/packages/?name=gstreamer-vaapi) for VA-API support.
*   [gst-plugins-bad](https://www.archlinux.org/packages/?name=gst-plugins-bad) for VDPAU and NVDEC support. (NVDEC is currently broken, [fixed](https://gitlab.freedesktop.org/gstreamer/gst-plugins-bad/commit/4e314d6f80515501906599f548e88e2e4f2d9452) in GStreamer 1.15)

## See also

*   [Sound system](/index.php/Sound_system "Sound system")
*   [website](https://gstreamer.freedesktop.org/)