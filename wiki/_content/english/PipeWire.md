[PipeWire](http://pipewire.org) is a rather new multimedia framework by GNOME. The main developer is Wim Taymans.

Because PipeWire supports containers like [Flatpak](/index.php/Flatpak "Flatpak") it doesn't rely on the [user groups](/index.php/User_group "User group") *audio* and *video*, but rather uses a complex PolKit-like security model asking Flatpak or Wayland for permission to record screen or audio.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 WebRTC screen sharing](#WebRTC_screen_sharing)
    *   [2.2 Video](#Video)
    *   [2.3 Audio (JACK)](#Audio_(JACK))
    *   [2.4 ALSA/Legacy applications](#ALSA/Legacy_applications)
    *   [2.5 Bluetooth](#Bluetooth)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [pipewire](https://www.archlinux.org/packages/?name=pipewire) package from the official repositories or the [pipewire-git](https://aur.archlinux.org/packages/pipewire-git/) package from the [AUR](/index.php/AUR "AUR").

The package installs systemd unit files for the service itself and automatic socket activation (which means it will autostart).

```
systemctl --user status pipewire.socket
systemctl --user status pipewire.service

```

## Usage

### WebRTC screen sharing

Most browsers used to rely on X11 for capturing the desktop (or apps) when using WebRTC (e.g. on google Hangouts); because Gnome shell uses Wayland by default on Arch when started by GDM, desktop sharing is basically broken, but pipewire is going to provide support for this usecase under Wayland.

This requires [Pipewire and xdg-desktop-portal to be installed](http://jgrulich.cz/2018/07/04/how-to-enable-and-use-screen-sharing-on-wayland); Firefox 68 [will support PipeWire with a custom patch from fedora](https://bugzilla.mozilla.org/show_bug.cgi?id=1496359), and on Chromium (73+) you need to enable [WebRTC PipeWire support](https://bugs.chromium.org/p/chromium/issues/detail?id=682122) the following url in a chromium tab:

```
chrome://flags/#enable-webrtc-pipewire-capturer

```

Note that the only supported feature is sharing the entire desktop and not a specific app/window due to [missing implementation in xdg-desktop-portal](https://github.com/flatpak/xdg-desktop-portal-gtk/issues/204).

### Video

Although the software is not yet production ready, it is safe to play around with. Most application which rely on [GStreamer](/index.php/GStreamer "GStreamer") to handle e.g. video streams should work out-of-the-box due to the PipeWire GStreamer plugin. Applications like e.g. [cheese](https://www.archlinux.org/packages/?name=cheese) are therefore already able to share video input using it.

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