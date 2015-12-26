# Desktop notifications

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [GTK+](/index.php/GTK%2B "GTK+")
*   [Libcanberra](/index.php/Libcanberra "Libcanberra")

Desktop notifications are small, passive popup dialogs that notify the user of particular events in an asynchronous manner.

## Contents

*   [1 Libnotify](#Libnotify)
*   [2 Notification servers](#Notification_servers)
    *   [2.1 Built-in](#Built-in)
    *   [2.2 Standalone](#Standalone)
*   [3 Tips and Tricks](#Tips_and_Tricks)
*   [4 Usage in programming](#Usage_in_programming)
*   [5 See also](#See_also)

## Libnotify

Libnotify is an implementation of the [Desktop Notifications Specification](http://developer.gnome.org/notification-spec/) which provides support for [GTK+](/index.php/GTK%2B "GTK+") and [Qt](/index.php/Qt "Qt") applications and is desktop independent: it is already used by many open source apps like [Evolution](/index.php/Evolution "Evolution") and [Pidgin](/index.php/Pidgin "Pidgin"). Libnotify can be installed with the [libnotify](https://www.archlinux.org/packages/?name=libnotify) package.

In order to use libnotify, you have to install a [notification server](#Notification_servers).

## Notification servers

### Built-in

The following desktop environments use their own implementations to display notifications, and you cannot replace them. Their notification servers are started automatically on login to receive notifications from applications via DBus.

*   [Cinnamon](/index.php/Cinnamon "Cinnamon") provides a notification server itself. Notifications are displayed at the top right corner of the screen.
*   [Enlightenment](/index.php/Enlightenment "Enlightenment") provides a notification server through its Notification extension. Notification options [are configurable](/index.php/Enlightenment#Notifications "Enlightenment").
*   [GNOME](/index.php/GNOME "GNOME") provides a notification server itself. Notifications are displayed at the top of the screen.
*   [KDE Plasma](/index.php/KDE_Plasma "KDE Plasma") provides a notification server itself. Notifications are displayed at the bottom right corner of the screen.

### Standalone

In other desktop environments, the notification server needs to be launched using your WM's/DE's "autostart" option. (It _can_ be launched on the first call via DBus, but that's not very desirable as it needs global configuration.)

You can choose one of the following implementations:

*   **[Avant Window Navigator](/index.php/Avant_Window_Navigator "Avant Window Navigator")** — A notification-daemon applet is available for AWN.

[https://github.com/p12tic/awn-extras](https://github.com/p12tic/awn-extras) || [awn-extras-applets](https://aur.archlinux.org/packages/awn-extras-applets/)<sup><small>AUR</small></sup>

*   **Deepin Notifications** — Notification server for [Deepin](/index.php/Deepin_Desktop_Environment "Deepin Desktop Environment").

[https://github.com/linuxdeepin/deepin-notifications](https://github.com/linuxdeepin/deepin-notifications) || [deepin-notifications](https://www.archlinux.org/packages/?name=deepin-notifications)

*   **Dunst** — Minimalistic notification daemon for Linux designed to fit nicely into minimalistic windowmanagers like [dwm](/index.php/Dwm "Dwm").

[http://www.knopwob.org/dunst/](http://www.knopwob.org/dunst/) || [dunst](https://www.archlinux.org/packages/?name=dunst)

*   **LXQt Notification Daemon** — Notification server for [LXQt](/index.php/LXQt "LXQt").

[https://github.com/lxde/lxqt-notificationd](https://github.com/lxde/lxqt-notificationd) || [lxqt-notificationd](https://www.archlinux.org/packages/?name=lxqt-notificationd)

*   **Notification Daemon** — The notification server used by [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback").

[https://github.com/GNOME/notification-daemon](https://github.com/GNOME/notification-daemon) || [notification-daemon](https://www.archlinux.org/packages/?name=notification-daemon)

You can run it manually using `/usr/lib/notification-daemon-1.0/notification-daemon`.

*   **MATE Notification Daemon** — Notification server for [MATE](/index.php/MATE "MATE").

[https://github.com/mate-desktop/mate-notification-daemon/](https://github.com/mate-desktop/mate-notification-daemon/) || GTK+ 2: [mate-notification-daemon](https://www.archlinux.org/packages/?name=mate-notification-daemon), GTK+ 3 (experimental): [mate-notification-daemon-gtk3](https://www.archlinux.org/packages/?name=mate-notification-daemon-gtk3)

*   **Notify OSD** — Notification server for [Unity](/index.php/Unity "Unity").

[https://launchpad.net/notify-osd](https://launchpad.net/notify-osd) || [notify-osd](https://www.archlinux.org/packages/?name=notify-osd)

*   **statnot** — Small, lightweight notification daemon that can output notifications to the root window's title, stdout or FIFO pipes, making it integrate very well with tiling window managers.

[https://github.com/halhen/statnot](https://github.com/halhen/statnot) || [statnot](https://aur.archlinux.org/packages/statnot/)<sup><small>AUR</small></sup>

*   **twmn** — Notification system for tiling window managers.

[https://github.com/sboli/twmn](https://github.com/sboli/twmn) || [twmn-git](https://aur.archlinux.org/packages/twmn-git/)<sup><small>AUR</small></sup>

*   **Xfce Notification Daemon** — Notification server for [Xfce](/index.php/Xfce "Xfce").

[http://goodies.xfce.org/projects/applications/xfce4-notifyd](http://goodies.xfce.org/projects/applications/xfce4-notifyd) || [xfce4-notifyd](https://www.archlinux.org/packages/?name=xfce4-notifyd)

**Tip:** To configure xfce4-notifyd, run the following command: `xfce4-notifyd-config`.

## Tips and Tricks

Send desktop notification from background script (replace foobar with user running X)

```
  sudo -u foobar DISPLAY=:0 DBUS_SESSION_BUS_ADDRESS="unix:path=/run/user/$(id -u foobar)/bus" notify-send -t 3000 "Backup" "starting..."

```

## Usage in programming

You can write your own libnotify display messages easily in many programming languages through GObject-Introspection or bindings, or you can simply use bash.

The following examples display simple a "Hello world" notification.

**Bash**

*   Dependency: [libnotify](https://www.archlinux.org/packages/?name=libnotify)

 `hello_world.sh` 

```
#!/bin/bash
notify-send 'Hello world!' 'This is an example notification.' --icon=dialog-information
```

**Tip:** An overview on the available icons can be found [here](http://standards.freedesktop.org/icon-naming-spec/icon-naming-spec-latest.html).

**Boo**

*   Dependency: [notify-sharp-3](https://www.archlinux.org/packages/?name=notify-sharp-3) ([boo](https://www.archlinux.org/packages/?name=boo))
*   Makedependency: [boo](https://www.archlinux.org/packages/?name=boo)
*   Build with: `booc hello_world.boo`
*   Run with: `mono hello_world.exe` (or `booi hello_world.boo`)

 `hello_world.boo` 

```
import Notifications from "notify-sharp"
Hello = Notification()
Hello.Summary  = "Hello world!"
Hello.Body     = "This is an example notification."
Hello.IconName = "dialog-information"
Hello.Show()
```

**C**

*   Dependency: [libnotify](https://www.archlinux.org/packages/?name=libnotify)
*   Build with: `gcc -o hello_world `pkg-config --cflags --libs libnotify` hello_world.c`

 `hello_world.c` 

```
#include <libnotify/notify.h>
void main () {
	notify_init ("Hello world!");
	NotifyNotification * Hello = notify_notification_new ("Hello world", "This is an example notification.", "dialog-information");
	notify_notification_show (Hello, NULL);
	g_object_unref(G_OBJECT(Hello));
	notify_uninit();
}
```

**C++**

*   Dependency: [libnotifymm](https://aur.archlinux.org/packages/libnotifymm/)<sup><small>AUR</small></sup>
*   Build with: `g++ -o hello_world `pkg-config --cflags --libs libnotifymm-1.0` hello_world.cc`

 `hello_world.cc` 

```
#include <libnotifymm.h>
int main(int argc, char *argv[]) {
	Notify::init("Hello world!");
	Notify::Notification Hello("Hello world", "This is an example notification.", "dialog-information");
        Hello.show();
}
```

**C#**

*   Dependency: [notify-sharp-3](https://www.archlinux.org/packages/?name=notify-sharp-3)
*   Build with: `mcs -pkg:notify-sharp-3.0 hello_world.cs`
*   Run with: `mono hello_world.exe`

 `hello_world.cs` 

```
using Notifications;
public class HelloWorld {
	static void Main() {
		var Hello = new Notification();
		Hello.Summary  = "Hello world!";
		Hello.Body     = "This is an example notification.";
		Hello.IconName = "dialog-information";
		Hello.Show();
	}
}
```

**Cobra**

*   Dependency: [notify-sharp-3](https://www.archlinux.org/packages/?name=notify-sharp-3)
*   Makedependency: [cobra](https://aur.archlinux.org/packages/cobra/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/cobra)]</sup>
*   Build with: `cobra -c hello_world`
*   Run with: `mono hello_world.exe`

 `hello_world.cs` 

```
@args -pkg:notify-sharp-3.0
use Notifications
class HelloWorld
    def main
        hello = Notification()
        hello.summary  = "Hello world!"
        hello.body     = "This is an example notification."
        hello.iconName = "dialog-information"
        hello.show
```

**F#**

*   Dependency: [notify-sharp-3](https://www.archlinux.org/packages/?name=notify-sharp-3)
*   Makedependency: [fsharp](https://aur.archlinux.org/packages/fsharp/)<sup><small>AUR</small></sup>
*   Build with: `fsharpc -r:notify-sharp.dll -I:/usr/lib/mono/notify-sharp-3.0/ -I:/usr/lib/mono/gtk-sharp-3.0/ hello_world.fs`
*   Run with: `mono hello_world.exe`

 `hello_world.fs` 

```
open Notifications
let Hello = new Notification()
Hello.Summary  <- "Hello world!"
Hello.Body     <- "This is an example notification."
Hello.IconName <- "dialog-information"
Hello.Show()
```

**Genie**

*   Dependency: [libnotify](https://www.archlinux.org/packages/?name=libnotify)
*   Makedependency: [vala](https://www.archlinux.org/packages/?name=vala)
*   Build with: `valac --pkg libnotify hello_world.gs`

 `hello_world.gs` 

```
uses 
	Notify

init
	Notify.init ("Hello world")
	var Hello=new Notification ("Hello world!","This is an example notification.","dialog-information")
	Hello.show ()
```

**Groovy**

*   Dependencies: [groovy](https://www.archlinux.org/packages/?name=groovy), [java-gnome](https://aur.archlinux.org/packages/java-gnome/)<sup><small>AUR</small></sup>
*   Build with: `groovyc -cp /usr/share/java/gtk.jar HelloWorld.groovy && jar cfe HelloWorld.jar HelloWorld HelloWorld.class`
*   Run with: `java -cp /usr/share/groovy/embeddable/groovy-all.jar:/usr/share/java/gtk.jar:HelloWorld.jar HelloWorld` (or `groovy -cp /usr/share/java/gtk.jar HelloWorld.groovy`)

 `HelloWorld.groovy` 

```
import org.gnome.gtk.*
import org.gnome.notify.*

Gtk.init()
Notify.init("Hello world")
def Hello = new Notification("Hello world!", "This is an example notification.", "dialog-information")
Hello.show()
```

**Java**

*   Dependency: [java-gnome](https://aur.archlinux.org/packages/java-gnome/)<sup><small>AUR</small></sup>
*   Makedependency: java-environment
*   Build with: `javac -cp /usr/share/java/gtk.jar HelloWorld.java && jar cfe HelloWorld.jar HelloWorld HelloWorld.class`
*   Run with: `java -cp /usr/share/java/gtk.jar:HelloWorld.jar HelloWorld`

 `HelloWorld.java` 

```
import org.gnome.gtk.Gtk;
import org.gnome.notify.Notify;
import org.gnome.notify.Notification;

public class HelloWorld
{
    public static void main(String[] args) {
        Gtk.init(args);
        Notify.init("Hello world");
        Notification Hello = new Notification("Hello world!", "This is an example notification.", "dialog-information");
        Hello.show();
    }
}
```

**JavaScript**

*   Dependencies: [libnotify](https://www.archlinux.org/packages/?name=libnotify), [gjs](https://www.archlinux.org/packages/?name=gjs) (works also with [seed](https://www.archlinux.org/packages/?name=seed))

 `hello_world.js` 

```
#!/usr/bin/gjs
const Notify = imports.gi.Notify;
Notify.init ("Hello world");
var Hello=new Notify.Notification ({summary: "Hello world!",
                                    body: "This is an example notification.",
                                    "icon-name": "dialog-information"});
Hello.show ();
```

**Lua**

*   Dependencies: [libnotify](https://www.archlinux.org/packages/?name=libnotify), [lua-lgi](https://www.archlinux.org/packages/?name=lua-lgi)

 `hello_world.lua` 

```
#!/usr/bin/lua
lgi = require 'lgi'
Notify = lgi.require('Notify')
Notify.init("Hello world")
Hello=Notify.Notification.new("Hello world","This is an example notification.","dialog-information")
Hello:show()
```

**Perl**

*   Dependencies: [libnotify](https://www.archlinux.org/packages/?name=libnotify), [perl-glib-object-introspection](https://aur.archlinux.org/packages/perl-glib-object-introspection/)<sup><small>AUR</small></sup>

 `hello_world.pl` 

```
#!/usr/bin/perl
use Glib::Object::Introspection;
Glib::Object::Introspection->setup (
	basename => 'Notify',
	version => '0.7',
	package => 'Notify');
Notify->init;
my $hello = Notify::Notification->new("Hello world!", "This is an example notification.", "dialog-information");
$hello->show;
```

**Python**

*   Dependencies: [libnotify](https://www.archlinux.org/packages/?name=libnotify), [python-gobject](https://www.archlinux.org/packages/?name=python-gobject) (or [python2-gobject](https://www.archlinux.org/packages/?name=python2-gobject) for Python 2)

 `hello_world.py` 

```
#!/usr/bin/python
from gi.repository import Notify
Notify.init("Hello world")
Hello=Notify.Notification.new("Hello world", "This is an example notification.", "dialog-information")
Hello.show()
```

**Ruby**

*   Dependencies: [libnotify](https://www.archlinux.org/packages/?name=libnotify), [ruby-gir_ffi](https://aur.archlinux.org/packages/ruby-gir_ffi/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ruby-gir_ffi)]</sup>

 `hello_world.rb` 

```
#!/usr/bin/ruby
require 'gir_ffi'
GirFFI.setup :Notify
Notify.init("Hello world")
Hello = Notify::Notification.new("Hello world!", "This is an example notification.", "dialog-information")
Hello.show
```

**Rust**

*   Dependencies: [rust](https://www.archlinux.org/packages/?name=rust) and [cargo-bin](https://aur.archlinux.org/packages/cargo-bin/)<sup><small>AUR</small></sup> (or just [multirust](https://aur.archlinux.org/packages/multirust/)<sup><small>AUR</small></sup>)
*   notification crate: [notify-rust](https://crates.io/crates/notify-rust)

 `hello_world.rs` 

```
extern crate notify_rust;
use notify_rust::Notification;
fn main(){
    Notification::new()
        .summary("Hello world")
        .body("This is an example notification")
        .icon("dialog-information")
        .show();
}
```

**Scala**

*   Dependency: [java-gnome](https://aur.archlinux.org/packages/java-gnome/)<sup><small>AUR</small></sup> (and [scala](https://www.archlinux.org/packages/?name=scala))
*   Makedependency: [scala](https://www.archlinux.org/packages/?name=scala)
*   Build with: `scalac -cp /usr/share/java/gtk.jar -d HelloWorld.jar HelloWorld.scala`
*   Run with: `java -cp /usr/share/java/gtk.jar:HelloWorld.jar HelloWorld` (or `scala -cp /usr/share/java/gtk.jar HelloWorld.scala`)

 `HelloWorld.scala` 

```
import org.gnome.gtk._
import org.gnome.notify._

object HelloWorld {
  def main(args: Array[String]) {
    Gtk.init(args)
    Notify.init("Hello world")
    var Hello = new Notification("Hello world!", "This is an example notification.", "dialog-information")
    Hello.show()
  }
}
```

**Vala**

*   Dependency: [libnotify](https://www.archlinux.org/packages/?name=libnotify)
*   Makedependency: [vala](https://www.archlinux.org/packages/?name=vala)
*   Build with: `valac --pkg libnotify hello_world.vala`

 `hello_world.vala` 

```
using Notify;
public class HelloWorld {
	static void main () {
		Notify.init ("Hello world");
		var Hello = new Notification("Hello world!", "This is an example notification.", "dialog-information");
		Hello.show ();
	}
}
```

**Visual Basic .NET**

*   Dependency: [notify-sharp-3](https://www.archlinux.org/packages/?name=notify-sharp-3)
*   Makedependency: [mono-basic](https://www.archlinux.org/packages/?name=mono-basic)
*   Build with: `vbnc -r:/usr/lib/mono/notify-sharp-3.0/notify-sharp.dll hello_world.vb`
*   Run with: `mono hello_world.exe`

 `hello_world.vb` 

```
Imports Notifications
Public Class Hello
	Public Shared Sub Main
		Dim Hello As New Notification
		Hello.Summary  = "Hello world!"
		Hello.Body     = "This is an example notification."
		Hello.IconName = "dialog-information"
		Hello.Show
	End Sub
End Class
```

## See also

*   [Libnotify Reference Manual](http://developer.gnome.org/libnotify/)
*   [C example](http://milky.manishsinha.net/2009/03/29/working-with-libnotify/)
*   [Python example](http://hashbang.fr/tutoriel-notify.html) (french article)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Desktop_notifications&oldid=413404](https://wiki.archlinux.org/index.php?title=Desktop_notifications&oldid=413404)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [X server](/index.php/Category:X_server "Category:X server")
*   [Development](/index.php/Category:Development "Category:Development")