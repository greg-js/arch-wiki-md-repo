Desktop notifications are small, passive popup dialogs that notify the user of particular events in an asynchronous manner.

## Contents

*   [1 Libnotify](#Libnotify)
*   [2 Notification servers](#Notification_servers)
    *   [2.1 Built-in](#Built-in)
    *   [2.2 Standalone](#Standalone)
*   [3 Usage in programming](#Usage_in_programming)
*   [4 See also](#See_also)

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

In other desktop environments, the notification server needs to be launched using your WM's/DE's "autostart" option. (It *can* be launched on the first call via DBus, but that's not very desirable as it needs global configuration.)

You can choose one of the following implementations:

*   **[Avant Window Navigator](/index.php/Avant_Window_Navigator "Avant Window Navigator")** — A notification-daemon applet is available for AWN.

	[https://github.com/p12tic/awn-extras](https://github.com/p12tic/awn-extras) || [awn-extras-applets](https://aur.archlinux.org/packages/awn-extras-applets/)

*   **Deepin Notifications** — Notification server for [Deepin](/index.php/Deepin "Deepin").

	[https://github.com/linuxdeepin/deepin-notifications](https://github.com/linuxdeepin/deepin-notifications) || [deepin-notifications](https://www.archlinux.org/packages/?name=deepin-notifications)

*   **[Dunst](/index.php/Dunst "Dunst")** — Minimalistic notification daemon for Linux designed to fit nicely into minimalistic windowmanagers like [dwm](/index.php/Dwm "Dwm").

	[http://www.knopwob.org/dunst/](http://www.knopwob.org/dunst/) || [dunst](https://www.archlinux.org/packages/?name=dunst)

*   **LXQt Notification Daemon** — Notification server for [LXQt](/index.php/LXQt "LXQt").

	[https://github.com/lxde/lxqt-notificationd](https://github.com/lxde/lxqt-notificationd) || [lxqt-notificationd](https://www.archlinux.org/packages/?name=lxqt-notificationd)

*   **Notification Daemon** — The notification server used by [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback").

	[https://github.com/GNOME/notification-daemon](https://github.com/GNOME/notification-daemon) || [notification-daemon](https://www.archlinux.org/packages/?name=notification-daemon)

	You can run it manually using `/usr/lib/notification-daemon-1.0/notification-daemon`.

*   **MATE Notification Daemon** — Notification server for [MATE](/index.php/MATE "MATE").

	[https://github.com/mate-desktop/mate-notification-daemon/](https://github.com/mate-desktop/mate-notification-daemon/) || [mate-notification-daemon](https://www.archlinux.org/packages/?name=mate-notification-daemon)

*   **Notify OSD** — Notification server for [Unity](/index.php/Unity "Unity").

	[https://launchpad.net/notify-osd](https://launchpad.net/notify-osd) || [notify-osd](https://www.archlinux.org/packages/?name=notify-osd)

*   **statnot** — Small, lightweight notification daemon that can output notifications to the root window's title, stdout or FIFO pipes, making it integrate very well with tiling window managers.

	[https://github.com/halhen/statnot](https://github.com/halhen/statnot) || [statnot](https://aur.archlinux.org/packages/statnot/)

*   **twmn** — Notification system for tiling window managers.

	[https://github.com/sboli/twmn](https://github.com/sboli/twmn) || [twmn-git](https://aur.archlinux.org/packages/twmn-git/)

*   **Xfce Notification Daemon** — Notification server for [Xfce](/index.php/Xfce "Xfce").

	[http://goodies.xfce.org/projects/applications/xfce4-notifyd](http://goodies.xfce.org/projects/applications/xfce4-notifyd) || [xfce4-notifyd](https://www.archlinux.org/packages/?name=xfce4-notifyd)

**Tip:** To configure xfce4-notifyd, run the following command: `xfce4-notifyd-config`.

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

**Tip:**

*   An overview on the available icons can be found [here](http://standards.freedesktop.org/icon-naming-spec/icon-naming-spec-latest.html).
*   To send desktop notification from a background script running as root (replace `*X_user*` and `*X_userid*` with the user and userid running X respectively): `# sudo -u *X_user* DISPLAY=:0 DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/*X_userid*/bus notify-send 'Hello world!' 'This is an example notification.'` 

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

*   Dependency: [glib2](https://www.archlinux.org/packages/?name=glib2)
*   Build with: `gcc -o hello_world `pkg-config --cflags --libs gio-2.0` hello_world.c`

 `hello_world.c` 
```
#include <gio/gio.h>
int main() {
	GApplication *application = g_application_new ("hello.world", G_APPLICATION_FLAGS_NONE);
	g_application_register (application, NULL, NULL);
	GNotification *notification = g_notification_new ("Hello world!");
	g_notification_set_body (notification, "This is an example notification.");
	GIcon *icon = g_themed_icon_new ("dialog-information");
	g_notification_set_icon (notification, icon);
	g_application_send_notification (application, NULL, notification);
	g_object_unref (icon);
	g_object_unref (notification);
	g_object_unref (application);
	return 0;
}
```

*   Dependency: [libnotify](https://www.archlinux.org/packages/?name=libnotify)
*   Build with: `gcc -o hello_world `pkg-config --cflags --libs libnotify` hello_world.c`

 `hello_world.c` 
```
#include <libnotify/notify.h>
int main() {
	notify_init ("Hello world!");
	NotifyNotification * Hello = notify_notification_new ("Hello world", "This is an example notification.", "dialog-information");
	notify_notification_show (Hello, NULL);
	g_object_unref(G_OBJECT(Hello));
	notify_uninit();
	return 0;
}
```

**C++**

*   Dependency: [glibmm](https://www.archlinux.org/packages/?name=glibmm)
*   Build with: `g++ -o hello_world `pkg-config --cflags --libs giomm-2.4` hello_world.cc`

 `hello_world.cc` 
```
#include <giomm-2.4/giomm.h>
int main(int argc, char *argv[]) {
	auto Application = Gio::Application::create("hello.world", Gio::APPLICATION_FLAGS_NONE);
	Application->register_application();
	auto Notification = Gio::Notification::create("Hello world");
	Notification->set_body("This is an example notification.");
	auto Icon = Gio::ThemedIcon::create("dialog-information");
	Notification->set_icon (Icon);
	Application->send_notification(Notification);
	return 0;
}
```

*   Dependency: [libnotifymm](https://aur.archlinux.org/packages/libnotifymm/)
*   Build with: `g++ -o hello_world `pkg-config --cflags --libs libnotifymm-1.0` hello_world.cc`

 `hello_world.cc` 
```
#include <libnotifymm.h>
int main(int argc, char *argv[]) {
	Notify::init("Hello world!");
	Notify::Notification Hello("Hello world", "This is an example notification.", "dialog-information");
	Hello.show();
	return 0;
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
*   Makedependency: [cobra](https://aur.archlinux.org/packages/cobra/)
*   Build with: `cobra -c hello_world`
*   Run with: `mono hello_world.exe`

 `hello_world.cobra` 
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
*   Makedependency: [fsharp](https://www.archlinux.org/packages/?name=fsharp)
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

*   Dependency: [glib2](https://www.archlinux.org/packages/?name=glib2)
*   Makedependency: [vala](https://www.archlinux.org/packages/?name=vala)
*   Build with: `valac --pkg gio-2.0 hello_world.gs`

 `hello_world.gs` 
```
uses 
	GLib

init
	var Application = new GLib.Application ("hello.world", GLib.ApplicationFlags.FLAGS_NONE);
	Application.register ();
	var Notification = new GLib.Notification ("Hello world");
	Notification.set_body ("This is an example notification.");
	var Icon = new GLib.ThemedIcon ("dialog-information");
	Notification.set_icon (Icon);
	Application.send_notification (null, Notification);
```

*   Dependency: [libnotify](https://www.archlinux.org/packages/?name=libnotify)
*   Makedependency: [vala](https://www.archlinux.org/packages/?name=vala)
*   Build with: `valac --pkg libnotify hello_world.gs`

 `hello_world.gs` 
```
uses 
	Notify

init
	Notify.init ("Hello world")
	var Hello=new Notify.Notification ("Hello world!","This is an example notification.","dialog-information")
	Hello.show ()
```

**Go**

*   Dependency: [libnotify](https://www.archlinux.org/packages/?name=libnotify)
*   Makedependency: [go-notify-git](https://aur.archlinux.org/packages/go-notify-git/)
*   Build with: `go build hello_world.go`
*   (Or run with: `go run hello_world.go`)

 `hello_world.go` 
```
package main
import ("github.com/mqu/go-notify")

func main() {
	notify.Init("Hello world")
	hello := notify.NotificationNew("Hello World!", "This is an example notification.","dialog-information")
	hello.Show()
}
```

**Groovy**

*   Dependencies: [groovy](https://www.archlinux.org/packages/?name=groovy), [java-gnome](https://aur.archlinux.org/packages/java-gnome/)
*   Build with: `groovyc -cp /usr/share/java/gtk.jar HelloWorld.groovy && jar cfe HelloWorld.jar HelloWorld HelloWorld.class`
*   Run with: `java -cp /usr/share/groovy/embeddable/groovy-all.jar:/usr/share/java/gtk.jar:HelloWorld.jar HelloWorld` or `groovy -cp /usr/share/java/gtk.jar HelloWorld.groovy`

 `HelloWorld.groovy` 
```
import org.gnome.gtk.*
import org.gnome.notify.*

Gtk.init()
Notify.init("Hello world")
def Hello = new Notification("Hello world!", "This is an example notification.", "dialog-information")
Hello.show()
```

**Haskell**

*   Makedependency: [haskell-fdo-notify](https://www.archlinux.org/packages/?name=haskell-fdo-notify)
*   Build with: `ghc hello_world`

 `hello_world.hs` 
```
import DBus.Notify
main = do
         client <- connectSession
         let hello = blankNote { summary="Hello world!",
                                 body=(Just $ Text "This is an example notification."),
                                 appImage=(Just $ Icon "dialog-information") }
         notification <- notify client hello
         return 0
```

**IronPython**

*   Dependencies: [notify-sharp-3](https://www.archlinux.org/packages/?name=notify-sharp-3), [ironpython](https://aur.archlinux.org/packages/ironpython/)
*   Run with: `ipy hello_world.py`

 `hello_world.py` 
```
import clr
clr.AddReference('notify-sharp')
import Notifications
Hello = Notifications.Notification()
Hello.Summary  = "Hello world!"
Hello.Body     = "This is an example notification."
Hello.IconName = "dialog-information"
Hello.Show()
```

**Java**

*   Dependency: [java-gnome](https://aur.archlinux.org/packages/java-gnome/)
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

*   Dependency: [gjs](https://www.archlinux.org/packages/?name=gjs)

 `hello_world.js` 
```
#!/usr/bin/gjs
const Gio = imports.gi.Gio;
var Application = new Gio.Application ({application_id: "hello.world"});
Application.register (null);
var Notification = new Gio.Notification ();
Notification.set_title ("Hello world");
Notification.set_body ("This is an example notification.");
var Icon = new Gio.ThemedIcon ({name: "dialog-information"});
Notification.set_icon (Icon);
Application.send_notification (null, Notification);
```

*   Dependencies: [libnotify](https://www.archlinux.org/packages/?name=libnotify), [gjs](https://www.archlinux.org/packages/?name=gjs)

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

**JRuby**

*   Dependencies: [java-gnome](https://aur.archlinux.org/packages/java-gnome/), [jruby](https://www.archlinux.org/packages/?name=jruby)
*   Build with: `jrubyc hello_world.rb && jar cfe hello_world.jar hello_world hello_world.class`
*   Run with: `java -cp /opt/jruby/lib/jruby.jar:hello_world.jar hello_world` or `jruby hello_world.rb`

 `hello_world.rb` 
```
require '/usr/share/java/gtk.jar'
import Java::OrgGnomeGtk::Gtk
import Java::OrgGnomeNotify::Notify
import Java::OrgGnomeNotify::Notification

Gtk.init(nil)
Notify.init("Hello world")
Hello = Notification.new("Hello world!", "This is an example notification.", "dialog-information")
Hello.show
```

**Jython**

*   Dependencies: [java-gnome](https://aur.archlinux.org/packages/java-gnome/), [jython](https://www.archlinux.org/packages/?name=jython)
*   Run with: `jython -Dpython.path=/usr/share/java/gtk.jar hello_world.py`

 `hello_world.py` 
```
from org.gnome.gtk import Gtk
from org.gnome.notify import Notify, Notification
Gtk.init(None)
Notify.init("Hello world")
Hello=Notification("Hello world!", "This is an example notification.", "dialog-information")
Hello.show()
```

**Lua**

*   Dependency: [lua-lgi](https://www.archlinux.org/packages/?name=lua-lgi)

 `hello_world.lua` 
```
#!/usr/bin/lua
lgi = require 'lgi'
Gio = lgi.require('Gio')
Application = Gio.Application.new("hello.world",Gio.ApplicationFlags.FLAGS_NONE);
Application:register();
Notification = Gio.Notification.new("Hello world");
Notification:set_body("This is an example notification.");
Icon = Gio.ThemedIcon.new("dialog-information");
Notification:set_icon(Icon);
Application:send_notification(nil, Notification);
```

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

**Nemerle**

*   Dependency: [notify-sharp-3](https://www.archlinux.org/packages/?name=notify-sharp-3)
*   Makedependency: [nemerle](https://aur.archlinux.org/packages/nemerle/)
*   Build with: `ncc -pkg:notify-sharp-3.0 -out:hello_world.exe hello_world.n`
*   Run with: `mono hello_world.exe`

 `hello_world.n` 
```
using Notifications;
public class HelloWorld {
	static Main() : void {
		def Hello = Notification();
		Hello.Summary  = "Hello world!";
		Hello.Body     = "This is an example notification.";
		Hello.IconName = "dialog-information";
		Hello.Show();
	}
}
```

**Pascal**

*   Dependency: [libnotify](https://www.archlinux.org/packages/?name=libnotify)
*   Makedependency: [fpc](https://www.archlinux.org/packages/?name=fpc), [libnotify binding](https://github.com/ik5/libnotify-fpc)
*   Build with: `fpc hello_world`

 `hello_world.pas` 
```
program	hello_world;
uses	libnotify;
var	hello : PNotifyNotification;
begin
	notify_init(argv[0]);
	hello := notify_notification_new ('Hello world', 'This is an example notification.', 'dialog-information');
	notify_notification_show (hello, nil);
end.
```

**Perl**

*   Dependencies: [libnotify](https://www.archlinux.org/packages/?name=libnotify), [perl-glib-object-introspection](https://aur.archlinux.org/packages/perl-glib-object-introspection/)

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

*   Dependency: [python-gobject](https://www.archlinux.org/packages/?name=python-gobject) (or [python2-gobject](https://www.archlinux.org/packages/?name=python2-gobject) for Python 2)

 `hello_world.py` 
```
#!/usr/bin/python
import gi
gi.require_version('Gio', '2.0')
from gi.repository import Gio
Application=Gio.Application.new ("hello.world", Gio.ApplicationFlags.FLAGS_NONE);
Application.register ();
Notification=Gio.Notification.new ("Hello world");
Notification.set_body ("This is an example notification.");
Icon=Gio.ThemedIcon.new ("dialog-information");
Notification.set_icon (Icon);
Application.send_notification (None, Notification);
```

*   Dependencies: [libnotify](https://www.archlinux.org/packages/?name=libnotify), [python-gobject](https://www.archlinux.org/packages/?name=python-gobject) (or [python2-gobject](https://www.archlinux.org/packages/?name=python2-gobject) for Python 2)

 `hello_world.py` 
```
#!/usr/bin/python
import gi
gi.require_version('Notify', '0.7')
from gi.repository import Notify
Notify.init("Hello world")
Hello=Notify.Notification.new("Hello world", "This is an example notification.", "dialog-information")
Hello.show()
```

**Ruby**

*   Dependencies: [libnotify](https://www.archlinux.org/packages/?name=libnotify), [ruby-gir_ffi](https://aur.archlinux.org/packages/ruby-gir_ffi/)

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

Using [notify-rust](https://crates.io/crates/notify-rust).

*   Makedependency: [cargo](https://www.archlinux.org/packages/?name=cargo)
*   Build with: `cargo build`
*   Run with: `target/debug/hello_world` or `cargo run`

 `Cargo.toml` 
```
[package]
name = "hello_world"
version = "0.1.0"

[dependencies]
notify-rust = "^3"
```
 `src/main.rs` 
```
extern crate notify_rust;
use notify_rust::Notification;
fn main(){
    Notification::new()
        .summary("Hello world")
        .body("This is an example notification.")
        .icon("dialog-information")
        .show().unwrap();
}
```

**Scala**

*   Dependency: [java-gnome](https://aur.archlinux.org/packages/java-gnome/) (and [scala](https://www.archlinux.org/packages/?name=scala))
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

*   Dependency: [glib2](https://www.archlinux.org/packages/?name=glib2)
*   Makedependency: [vala](https://www.archlinux.org/packages/?name=vala)
*   Build with: `valac --pkg gio-2.0 hello_world.vala`

 `hello_world.vala` 
```
using GLib;
public class HelloWorld {
	static void main () {
		var Application = new GLib.Application ("hello.world", GLib.ApplicationFlags.FLAGS_NONE);
		Application.register ();
		var Notification = new GLib.Notification ("Hello world");
		Notification.set_body ("This is an example notification.");
		var Icon = new GLib.ThemedIcon ("dialog-information");
		Notification.set_icon (Icon);
		Application.send_notification (null, Notification);
	}
}
```

*   Dependency: [libnotify](https://www.archlinux.org/packages/?name=libnotify)
*   Makedependency: [vala](https://www.archlinux.org/packages/?name=vala)
*   Build with: `valac --pkg libnotify hello_world.vala`

 `hello_world.vala` 
```
using Notify;
public class HelloWorld {
	static void main () {
		Notify.init ("Hello world");
		var Hello = new Notify.Notification("Hello world!", "This is an example notification.", "dialog-information");
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