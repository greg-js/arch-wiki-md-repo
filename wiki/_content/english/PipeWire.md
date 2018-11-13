From [pipewire.org](http://pipewire.org):

	PipeWire is a project that aims to greatly improve handling of audio and video under Linux. It aims to support the usecases currently handled by both [PulseAudio](/index.php/PulseAudio "PulseAudio") and [Jack](/index.php/Jack "Jack") and at the same time provide same level of powerful handling of Video input and output. It also introduces a security model that makes interacting with audio and video devices from containerized applications easy, with supporting [Flatpak](/index.php/Flatpak "Flatpak") applications being the primary goal. Alongside [Wayland](/index.php/Wayland "Wayland") and [Flatpak](/index.php/Flatpak "Flatpak") we expect PipeWire to provide a core building block for the future of Linux application development. Features include:

*   Capture and playback of audio and video with minimal latency.
*   Real-time Multimedia processing on audio and video.
*   Multiprocess architecture to let applications share multimedia content.
*   GStreamer plugins for easy use and integration in current applications.
*   Sandboxed applications support. See Flatpak for more info.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Video](#Video)
    *   [2.2 Audio (JACK)](#Audio_(JACK))
    *   [2.3 ALSA/Legacy applications](#ALSA/Legacy_applications)
    *   [2.4 Bluetooth](#Bluetooth)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [pipewire](https://www.archlinux.org/packages/?name=pipewire) package from the official repositories or the [pipewire-git](https://aur.archlinux.org/packages/pipewire-git/) package from the [AUR](/index.php/AUR "AUR").

## Usage

### Video

Although the software is not yet production ready, it is safe to play around with. Most application which rely on [GStreamer](/index.php/GStreamer "GStreamer") to handle e.g. video streams should work out-of-the-box due to the PipeWire GStreamer plugin. Applications like e.g. [cheese](https://www.archlinux.org/packages/?name=cheese) are therefore already able to share video input using it.

The GStreamer autoplugging process obviously requires that the PipeWire process is running beforehand. Hence you must start `pipewire` prior to using it.

### Audio (JACK)

Support for the Jack protocol on top of PipeWire is implemented and first applications relying on said interface are working in a test environment. Through that work one is able to achieve the low latency needed for pro-audio with PipeWire.

A detailed description of how to enable and use it can be found [here](https://github.com/PipeWire/pipewire/wiki/JACK).

### ALSA/Legacy applications

Work on ALSA emulation is ongoing but first working code exists.

### Bluetooth

PipeWire provides a bluetooth module which integrates directly into the Bluez Bluetooth framework. Pairing and management hence works the same since it is handled by higher level interfaces.

## See also

*   [Wiki](https://github.com/PipeWire/pipewire/wiki) — PipeWire Wiki on GitHub
*   [Pipewire Update Blog Post](https://blogs.gnome.org/uraeus/2018/01/26/an-update-on-pipewire-the-multimedia-revolution-an-update/) — Blog post from January 2018 outlining the state of PipeWire at the time