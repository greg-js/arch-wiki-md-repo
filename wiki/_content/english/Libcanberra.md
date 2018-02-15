Related articles

*   [GTK+](/index.php/GTK%2B "GTK+")
*   [Desktop notifications](/index.php/Desktop_notifications "Desktop notifications")

**Libcanberra** is a simple abstract interface for playing event sounds. It implements the [XDG Sound Theme and Naming Specifications](http://freedesktop.org/wiki/Specifications/sound-theme-spec) for generating event sounds on free desktops, such as GNOME. Further description [here](http://0pointer.de/lennart/projects/libcanberra/)

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Systemd](#Systemd)
*   [4 Usage in programming](#Usage_in_programming)
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

## Usage in programming

You can write your own libcanberra sound events easily in many programming languages using [GSound](https://wiki.gnome.org/Projects/GSound) through GObject-Introspection, or you can simply use bash.

**Bash**

*   Dependency: [libcanberra](https://www.archlinux.org/packages/?name=libcanberra)

 `hello_world.sh` 
```
#!/bin/bash
canberra-gtk-play -i phone-incoming-call -d "hello world"
```

**C**

*   Dependency: [libcanberra](https://www.archlinux.org/packages/?name=libcanberra)
*   Build with: `gcc -o hello_world `pkg-config --cflags --libs glib-2.0 libcanberra` hello_world.c`

 `hello_world.c` 
```
#include <glib.h>
#include <canberra.h>
int main () {
	ca_context * hello;
	ca_context_create (&hello);
	ca_context_play (hello, 0,
		CA_PROP_EVENT_ID, "phone-incoming-call",
		CA_PROP_EVENT_DESCRIPTION, "hello world",
		NULL);
	g_usleep (2000000);
	return 0;
}
```

*   Dependency: [gsound](https://www.archlinux.org/packages/?name=gsound)
*   Build with: `gcc -o hello_world `pkg-config --cflags --libs glib-2.0 gsound` hello_world.c`

 `hello_world.c` 
```
#include <glib.h>
#include <gsound.h>
int main () {
	GSoundContext *hello = gsound_context_new(NULL, NULL);
	gsound_context_play_simple(hello, NULL, NULL,
		GSOUND_ATTR_EVENT_ID, "phone-incoming-call",
		GSOUND_ATTR_EVENT_DESCRIPTION, "hello world",
		NULL);
	g_usleep (2000000);
	return 0;
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

*   Dependency: [gsound](https://www.archlinux.org/packages/?name=gsound)
*   Makedependency: [vala](https://www.archlinux.org/packages/?name=vala)
*   Build with: `valac --pkg gsound hello_world.gs`

 `hello_world.gs` 
```
uses
	GSound
init
	var hello = new GSound.Context
	hello.init()
	hello.play_simple(null,
		GSound.Attribute.EVENT_ID, "phone-incoming-call",
		GSound.Attribute.EVENT_DESCRIPTION, "hello world")
	Thread.usleep (2000000)
```

**JavaScript**

*   Dependencies: [gsound](https://www.archlinux.org/packages/?name=gsound), [gjs](https://www.archlinux.org/packages/?name=gjs)

 `hello_world.js` 
```
#!/usr/bin/gjs
const GLib = imports.gi.GLib;
const GSound = imports.gi.GSound;

let hello = new GSound.Context();
hello.init(null);
hello.play_simple({ "event.id" : "phone-incoming-call", 
                    "event.description" : "hello world" }, null);
GLib.usleep (2000000);
```

**Lua**

*   Dependencies: [gsound](https://www.archlinux.org/packages/?name=gsound), [lua-lgi](https://www.archlinux.org/packages/?name=lua-lgi)

 `hello_world.lua` 
```
#!/usr/bin/lua
lgi = require 'lgi'
GLib = lgi.require('GLib')
GSound = lgi.require('GSound')

hello = GSound.Context()
hello:play_simple({ [GSound.ATTR_EVENT_ID] = "phone-incoming-call",
                    [GSound.ATTR_EVENT_DESCRIPTION] = "hello world" })
GLib.usleep (2000000)
```

**Perl**

*   Dependencies: [gsound](https://www.archlinux.org/packages/?name=gsound), [perl-glib-object-introspection](https://aur.archlinux.org/packages/perl-glib-object-introspection/)

 `hello_world.pl` 
```
#!/usr/bin/perl
use Glib::Object::Introspection;
Glib::Object::Introspection->setup (
	basename => 'GSound',
	version => '1.0',
	package => 'GSound');
my $hello = GSound::Context->new;
$hello->play_simple({ "event.id" => "phone-incoming-call",
                      "event.description" => "hello world" });
sleep (2);
```

**Python**

*   Dependencies: [gsound](https://www.archlinux.org/packages/?name=gsound), [python-gobject](https://www.archlinux.org/packages/?name=python-gobject)

 `hello_world.py` 
```
#!/usr/bin/python
import gi
gi.require_version('GSound', '1.0')
from gi.repository import GLib, GSound

hello = GSound.Context()
hello.init()
hello.play_simple({GSound.ATTR_EVENT_ID: "phone-incoming-call",
                   GSound.ATTR_EVENT_DESCRIPTION: "hello world"})
GLib.usleep(2000000)
```

**Ruby**

*   Dependencies: [gsound](https://www.archlinux.org/packages/?name=gsound), [ruby-gir_ffi](https://aur.archlinux.org/packages/ruby-gir_ffi/)

 `hello_world.rb` 
```
#!/usr/bin/ruby
require 'gir_ffi'
GirFFI.setup :GSound
Hello = GSound::Context.new
Hello.play_simple("event.id" => "phone-incoming-call", 
                  "event.description" => "hello world")
sleep (2)
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

*   Dependency: [gsound](https://www.archlinux.org/packages/?name=gsound)
*   Makedependency: [vala](https://www.archlinux.org/packages/?name=vala)
*   Build with: `valac --pkg gsound hello_world.vala`

 `hello_world.vala` 
```
using GSound;
public class HelloWorld {
	static void main () {
	var hello = new GSound.Context();
	hello.init();
        hello.play_simple(null,
		GSound.Attribute.EVENT_ID, "phone-incoming-call",
		GSound.Attribute.EVENT_DESCRIPTION, "hello world");
	Thread.usleep (2000000);
	}
}
```

## See also

*   [Libcanberra Reference Manual](http://0pointer.de/lennart/projects/libcanberra/gtkdoc/)
*   [GSound Reference Manual](https://developer.gnome.org/gsound/)