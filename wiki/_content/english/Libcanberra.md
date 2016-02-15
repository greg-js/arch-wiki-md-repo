**Libcanberra** is a simple abstract interface for playing event sounds. It implements the [XDG Sound Theme and Naming Specifications](http://freedesktop.org/wiki/Specifications/sound-theme-spec) for generating event sounds on free desktops, such as GNOME. Further description [here](http://0pointer.de/lennart/projects/libcanberra/)

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Systemd](#Systemd)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Write your own canberra app](#Write_your_own_canberra_app)
*   [5 See also](#See_also)

## Installation

Libcanberra can be installed with the package [libcanberra](https://www.archlinux.org/packages/?name=libcanberra), available in the [Official repositories](/index.php/Official_repositories "Official repositories"). It contains the library and a GTK+ module.

You have to choose a backend to play sounds:

*   [ALSA](/index.php/ALSA "ALSA") backend is included in [libcanberra](https://www.archlinux.org/packages/?name=libcanberra) package
*   [GStreamer](/index.php/GStreamer "GStreamer") backend can be installed with package [libcanberra-gstreamer](https://www.archlinux.org/packages/?name=libcanberra-gstreamer), available in the [Official repositories](/index.php/Official_repositories "Official repositories").
*   [PulseAudio](/index.php/PulseAudio "PulseAudio") backend can be installed with package [libcanberra-pulse](https://www.archlinux.org/packages/?name=libcanberra-pulse), available in the [Official repositories](/index.php/Official_repositories "Official repositories").

Also, you have to install a sound theme in order to hear any event sound:

*   The default sound theme is 'freedesktop', which can be installed with the package [sound-theme-freedesktop](https://www.archlinux.org/packages/?name=sound-theme-freedesktop), available in the [Official repositories](/index.php/Official_repositories "Official repositories").
*   Alternatively, you can install [ubuntu-sounds](https://aur.archlinux.org/packages/ubuntu-sounds/), available in the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

## Configuration

By default, the GTK+ module is loaded automatically, when a GTK+ application launched. You can overwrite default settings in user's GtkSettings file:

 `$HOME/.gtkrc-2.0 and $XDG_CONFIG_HOME/gtk-3.0/settings.ini` 

```
gtk-enable-event-sounds=true
gtk-enable-input-feedback-sounds=true
gtk-sound-theme-name=freedesktop
```

In GNOME, these settings are managed by gnome-settings-daemon, and the configuration is available in GSettings under org.gnome.desktop.sound schema.

## Systemd

To enable bootup, shutdown and reboot sounds using canberra, [enable](/index.php/Enable "Enable") `canberra-system-bootup` service.

## Tips and tricks

### Write your own canberra app

You can write your own libcanberra sound events easily in some programming languages, or you can simply use bash.

**Bash**

*   Dependency: [libcanberra](https://www.archlinux.org/packages/?name=libcanberra)

 `hello_world.sh` 

```
#!/bin/bash
canberra-gtk-play -i phone-incoming-call -d "hello world"
```

**C**

*   Dependency: [libcanberra](https://www.archlinux.org/packages/?name=libcanberra)
*   Build with: `gcc hello_world.c -o hello_world `pkg-config --cflags --libs glib-2.0 libcanberra``

 `hello_world.c` 

```
#include <glib.h>
#include <canberra.h>
void main () {
	ca_context * hello;
	ca_context_create (&hello);
	ca_context_play (hello, 0,
		CA_PROP_EVENT_ID, "phone-incoming-call",
		CA_PROP_EVENT_DESCRIPTION, "hello world",
		NULL);
	g_usleep (2000000);
}
```

**Genie**

*   Dependency: [libcanberra](https://www.archlinux.org/packages/?name=libcanberra)
*   Makedependency: [vala](https://www.archlinux.org/packages/?name=vala)
*   Build with: `valac --pkg libcanberra hello_world.gs`

 `hello_world.gs` 

```
uses
	Canberra
init
	hello: Context
	Context.create(out hello)
	hello.play (0,
		PROP_EVENT_ID, "phone-incoming-call",
		PROP_EVENT_DESCRIPTION, "hello world")
	Thread.usleep (2000000)
```

**Vala**

*   Dependency: [libcanberra](https://www.archlinux.org/packages/?name=libcanberra)
*   Makedependency: [vala](https://www.archlinux.org/packages/?name=vala)
*   Build with: `valac --pkg libcanberra hello_world.vala`

 `hello_world.vala` 

```
using Canberra;
public class HelloWorld {
	static void main () {
	Context hello;
	Context.create(out hello);
	hello.play (0,
		PROP_EVENT_ID, "phone-incoming-call",
		PROP_EVENT_DESCRIPTION, "hello world");
	Thread.usleep (2000000);
	}
}
```

## See also

*   [Libcanberra Reference Manual](http://0pointer.de/lennart/projects/libcanberra/gtkdoc/)