# GTK+/Development

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Contents

*   [1 Write a simple message dialog app](#Write_a_simple_message_dialog_app)
    *   [1.1 Ada](#Ada)
    *   [1.2 Bash](#Bash)
    *   [1.3 Boo](#Boo)
    *   [1.4 C](#C)
    *   [1.5 C++](#C.2B.2B)
    *   [1.6 C#](#C.23)
    *   [1.7 Cobra](#Cobra)
    *   [1.8 D](#D)
    *   [1.9 F#](#F.23)
    *   [1.10 Fortran](#Fortran)
    *   [1.11 Genie](#Genie)
    *   [1.12 Go](#Go)
    *   [1.13 Groovy](#Groovy)
    *   [1.14 Haskell](#Haskell)
    *   [1.15 Java](#Java)
    *   [1.16 JavaScript](#JavaScript)
    *   [1.17 Lua](#Lua)
    *   [1.18 Pascal](#Pascal)
    *   [1.19 Perl](#Perl)
    *   [1.20 Python](#Python)
    *   [1.21 Ruby](#Ruby)
    *   [1.22 Scala](#Scala)
    *   [1.23 Vala](#Vala)
    *   [1.24 Visual Basic .NET](#Visual_Basic_.NET)

## Write a simple message dialog app

You can write your own GTK+ 3 message dialog easily in many programming languages through GObject-Introspection or bindings, or you can simply use bash.

The following examples display a simple "Hello world" in a message dialog.

### Ada

*   Dependency: [gtkada](https://aur.archlinux.org/packages/gtkada/)<sup><small>AUR</small></sup> from AUR
*   Makedependency: [gcc-ada](https://www.archlinux.org/packages/?name=gcc-ada)
*   Build with: `gnatmake hello_world `gtkada-config``

 `hello_world.adb` 

```
with Gtk.Main;
with Gtk.Dialog;           use Gtk.Dialog;
with Gtk.Message_Dialog;   use Gtk.Message_Dialog;

procedure hello_world is
  Dialog   : Gtk_Message_Dialog;
  Response : Gtk_Response_Type;
begin
  Gtk.Main.Init;
  Gtk_New (Dialog   => Dialog,
           Parent   => null,
           Flags    => 0,
           The_Type => Message_Info,
           Buttons  => Buttons_OK,
           Message  => "Hello world!");
  Format_Secondary_Markup (Dialog, "This is an example dialog.");
  Response := Run (Dialog);
end hello_world;
```

### Bash

*   Dependency: [zenity](https://www.archlinux.org/packages/?name=zenity)

 `hello_world.sh` 

```
#!/bin/bash
zenity --info --title='Hello world!' --text='This is an example dialog.'
```

### Boo

*   Dependency: [gtk-sharp-3](https://www.archlinux.org/packages/?name=gtk-sharp-3) (and [boo](https://www.archlinux.org/packages/?name=boo))
*   Makedependency: [boo](https://www.archlinux.org/packages/?name=boo)
*   Build with: `booc hello_world.boo`
*   Run with: `mono hello_world.exe` (or `booi hello_world.boo`)

 `hello_world.boo` 

```
import Gtk from "gtk-sharp"
Application.Init()
Hello = MessageDialog(null, DialogFlags.Modal, MessageType.Info, ButtonsType.Ok, "Hello world!")
Hello.SecondaryText = "This is an example dialog."
Hello.Run()
```

### C

*   Dependency: [gtk3](https://www.archlinux.org/packages/?name=gtk3)
*   Build with: `gcc -o hello_world $(pkg-config --cflags --libs gtk+-3.0) hello_world.c`

 `hello_world.c` 

```
#include <gtk/gtk.h>
int main (int argc, char *argv[]) {
	gtk_init (&argc, &argv);
        GtkWidget *hello = gtk_message_dialog_new (NULL, GTK_DIALOG_MODAL, GTK_MESSAGE_INFO, GTK_BUTTONS_OK, "Hello world!");
	gtk_message_dialog_format_secondary_text (GTK_MESSAGE_DIALOG (hello), "This is an example dialog.");
        gtk_dialog_run(GTK_DIALOG (hello));
        return 0;
}
```

### C++

*   Dependency: [gtkmm3](https://www.archlinux.org/packages/?name=gtkmm3)
*   Build with: `g++ -o hello_world $(pkg-config --cflags --libs gtkmm-3.0) hello_world.cc`

 `hello_world.cc` 

```
#include <gtkmm/main.h>
#include <gtkmm/messagedialog.h>
int main(int argc, char *argv[]) {
	Gtk::Main kit(argc, argv);
	Gtk::MessageDialog Hello("Hello world!", false, Gtk::MESSAGE_INFO, Gtk::BUTTONS_OK);
	Hello.set_secondary_text("This is an example dialog.");
	Hello.run();
}
```

### C#

*   Dependency: [gtk-sharp-3](https://www.archlinux.org/packages/?name=gtk-sharp-3)
*   Build with: `mcs -pkg:gtk-sharp-3.0 hello_world.cs`
*   Run with: `mono hello_world.exe`

 `hello_world.cs` 

```
using Gtk;
public class HelloWorld {
	static void Main() {
		Application.Init ();
		MessageDialog Hello = new MessageDialog (null, DialogFlags.Modal, MessageType.Info, ButtonsType.Ok, "Hello world!");
		Hello.SecondaryText="This is an example dialog.";
		Hello.Run ();
	}
}
```

### Cobra

*   Dependency: [gtk-sharp-3](https://www.archlinux.org/packages/?name=gtk-sharp-3)
*   Makedependency: [cobra](https://aur.archlinux.org/packages/cobra/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/cobra)]</sup> from AUR
*   Build with: `cobra -c hello_world`
*   Run with: `mono hello_world.exe`

 `hello_world.cobra` 

```
@args -pkg:gtk-sharp-3.0
use Gtk

class HelloWorld
    def main
        Application.init
        hello = MessageDialog(nil, DialogFlags.Modal, MessageType.Info, ButtonsType.Ok, "Hello world!")
        hello.secondaryText = "This is an example dialog."
        hello.run
```

### D

*   Dependency: [gtkd](https://aur.archlinux.org/packages/gtkd/)<sup><small>AUR</small></sup> from AUR
*   Makedependency: [dmd](https://www.archlinux.org/packages/?name=dmd)
*   Build with: `dmd hello_world $(pkg-config --cflags --libs gtkd-2)`

 `hello_world.d` 

```
import gtk.Main;
import gtk.MessageDialog;

void main(string[] args)
{
	Main.init(args);
	MessageDialog dialog = new MessageDialog(null, GtkDialogFlags.MODAL, MessageType.INFO, ButtonsType.OK, "Hello world!");
	dialog.run();
}
```

### F#

*   Dependency: [gtk-sharp-3](https://www.archlinux.org/packages/?name=gtk-sharp-3)
*   Makedependency: [fsharp](https://aur.archlinux.org/packages/fsharp/)<sup><small>AUR</small></sup> from AUR
*   Build with: `fsharpc -r:gtk-sharp.dll -I:/usr/lib/mono/gtk-sharp-3.0/`
*   Run with: `mono hello_world.exe`

 `hello_world.fs` 

```
open Gtk
Application.Init()
let Hello = new MessageDialog(null, DialogFlags.Modal, MessageType.Info, ButtonsType.Ok, "Hello world!")
Hello.SecondaryText <- "This is an example dialog."
Hello.Run() |> ignore

```

### Fortran

*   Dependency: [gtk-3-fortran-git](https://aur.archlinux.org/packages/gtk-3-fortran-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gtk-3-fortran-git)]</sup> from AUR
*   Makedependency: [gcc-fortran](https://www.archlinux.org/packages/?name=gcc-fortran)
*   Build with: `gfortran hello_world.f90 -o hello_world $(pkg-config --cflags --libs gtk-3-fortran)`

 `hello_world.f90` 

```
program hello_world
  use gtk_hl
  use gtk, only: gtk_init

  integer(c_int) :: resp
  character(40), dimension(2) :: msg

  call gtk_init()
  msg(1) ="Hello world!"
  msg(2) = "This is an example dialog."
  resp = hl_gtk_message_dialog_show(msg, GTK_BUTTONS_OK, type=GTK_MESSAGE_INFO)
end program hello_world

```

### Genie

*   Dependency: [gtk3](https://www.archlinux.org/packages/?name=gtk3)
*   Makedependency: [vala](https://www.archlinux.org/packages/?name=vala)
*   Build with: `valac --pkg gtk+-3.0 hello_world.gs`

 `hello_world.gs` 

```
uses 
	Gtk
init
	Gtk.init (ref args)
	var Hello=new MessageDialog (null, Gtk.DialogFlags.MODAL, Gtk.MessageType.INFO, Gtk.ButtonsType.OK, "Hello world!")
	Hello.format_secondary_text ("This is an example dialog.")
	Hello.run ()
```

### Go

*   Dependency: [gtk3](https://www.archlinux.org/packages/?name=gtk3)
*   Makedependency: [gotk3-git](https://aur.archlinux.org/packages/gotk3-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gotk3-git)]</sup> from AUR
*   Build with: `go build hello_world.go`
*   (Or run with: `go run hello_world.go`)

 `hello_world.go` 

```
package main
import ("github.com/conformal/gotk3/gtk")

func main() {
	gtk.Init(nil)
	dialog := gtk.MessageDialogNew(nil, gtk.DIALOG_MODAL, gtk.MESSAGE_INFO, gtk.BUTTONS_OK, "Hello world!")
	dialog.FormatSecondaryText("This is an example notification.")
	dialog.Run()
}
```

### Groovy

*   Dependencies: [groovy](https://www.archlinux.org/packages/?name=groovy), [java-gnome](https://aur.archlinux.org/packages/java-gnome/)<sup><small>AUR</small></sup> from AUR
*   Build with: `groovyc -cp /usr/share/java/gtk.jar HelloWorld.groovy && jar cfe HelloWorld.jar HelloWorld HelloWorld.class`
*   Run with: `java -cp /usr/share/groovy/embeddable/groovy-all.jar:/usr/share/java/gtk.jar:HelloWorld.jar HelloWorld` (or `groovy -cp /usr/share/java/gtk.jar HelloWorld.groovy`)

 `HelloWorld.groovy` 

```
import org.gnome.gtk.*
Gtk.init()
def Hello = new InfoMessageDialog(null, "Hello world!", "This is an example dialog.")
Hello.run()
```

### Haskell

*   Dependency: [gtk3](https://www.archlinux.org/packages/?name=gtk3)
*   Makedependency: [haskell-gtk3](https://aur.archlinux.org/packages/haskell-gtk3/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/haskell-gtk3)]</sup> from AUR
*   Build with: `ghc hello_world`

 `hello_world.hs` 

```
import Graphics.UI.Gtk

main = do
	initGUI
	dialog <- messageDialogNew Nothing [DialogModal] MessageInfo ButtonsOk "Hello world!"
	messageDialogSetSecondaryText dialog "This is an example dialog."
	_res <- dialogRun dialog
	return 0
```

### Java

*   Dependency: [java-gnome](https://aur.archlinux.org/packages/java-gnome/)<sup><small>AUR</small></sup> from AUR
*   Makedependency: java-environment
*   Build with: `javac -cp /usr/share/java/gtk.jar HelloWorld.java && jar cfe HelloWorld.jar HelloWorld HelloWorld.class`
*   Run with: `java -cp /usr/share/java/gtk.jar:HelloWorld.jar HelloWorld`

 `HelloWorld.java` 

```
import org.gnome.gtk.Gtk;
import org.gnome.gtk.Dialog;
import org.gnome.gtk.InfoMessageDialog;

public class HelloWorld {
    public static void main(String[] args) {
        Gtk.init(args);
        Dialog Hello = new InfoMessageDialog(null, "Hello world!", "This is an example dialog.");
        Hello.run();
    }
}
```

### JavaScript

*   Dependencies: [gtk3](https://www.archlinux.org/packages/?name=gtk3), [gjs](https://www.archlinux.org/packages/?name=gjs) (works also with [seed](https://www.archlinux.org/packages/?name=seed))

 `hello_world.js` 

```
#!/usr/bin/env gjs
const Gtk = imports.gi.Gtk
Gtk.init(null, null)
var Hello = new Gtk.MessageDialog({type: Gtk.MessageType.INFO,
                                   buttons: Gtk.ButtonsType.OK,
                                   text: "Hello world!",
                                   "secondary-text": "This is an example dialog."})
Hello.run()
```

### Lua

*   Dependencies: [gtk3](https://www.archlinux.org/packages/?name=gtk3), [lua-lgi](https://www.archlinux.org/packages/?name=lua-lgi)

 `hello_world.lua` 

```
#!/usr/bin/env lua
lgi = require 'lgi'
Gtk = lgi.require('Gtk')
Gtk.init()
Hello=Gtk.MessageDialog {message_type = Gtk.MessageType.INFO,
                         buttons = Gtk.ButtonsType.OK,
                         text = "Hello world!",
                         secondary_text = "This is an example dialog."}
Hello:run()
```

### Pascal

*   Dependency: [gtk3](https://www.archlinux.org/packages/?name=gtk3)
*   Makedependencies: [fpc](https://www.archlinux.org/packages/?name=fpc), [Gtk+3.0 bindings](http://wiki.freepascal.org/Gtk+3)
*   Build with: `fpc hello_world`

 `hello_world.pas` 

```
program	hello_world;
uses	Math, Gtk3;
var	dialog: PGtkWidget;
begin
	SetExceptionMask([exInvalidOp, exDenormalized, exZeroDivide, exOverflow, exUnderflow, exPrecision]);
	gtk_init(@argc, @argv);
	dialog := gtk_message_dialog_new(nil, GTK_DIALOG_MODAL, GTK_MESSAGE_INFO, GTK_BUTTONS_OK, '%s', ['Hello world!']);
	gtk_message_dialog_format_secondary_text(PGtkMessageDialog(dialog), '%s', ['This is an example dialog.']);
	gtk_dialog_run(PGtkDialog(dialog));
end.
```

### Perl

*   Dependency: [perl-gtk3](https://aur.archlinux.org/packages/perl-gtk3/)<sup><small>AUR</small></sup> from AUR

 `hello_world.pl` 

```
#!/usr/bin/env perl
use Gtk3 -init;
my $hello = Gtk3::MessageDialog->new (undef, 'modal', 'info', 'ok', "Hello world!");
$hello->set ('secondary-text' => 'This is an example dialog.');
$hello->run;
```

### Python

*   Dependencies: [gtk3](https://www.archlinux.org/packages/?name=gtk3), [python-gobject](https://www.archlinux.org/packages/?name=python-gobject)

 `hello_world.py` 

```
#!/usr/bin/env python
from gi.repository import Gtk
Gtk.init(None)
Hello=Gtk.MessageDialog(None, Gtk.DialogFlags.MODAL, Gtk.MessageType.INFO, Gtk.ButtonsType.OK, "Hello world!")
Hello.format_secondary_text("This is an example dialog.")
Hello.run()
```

### Ruby

*   Dependency: [ruby-gtk3](https://aur.archlinux.org/packages/ruby-gtk3/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ruby-gtk3)]</sup>

 `hello_world.rb` 

```
#!/usr/bin/env ruby
require 'gtk3'
Gtk.init
Hello = Gtk::MessageDialog.new(:type => :info,
                               :buttons_type => :ok,
                               :message => "Hello world!")
Hello.secondary_text = "This is an example dialog."
Hello.run
```

### Scala

*   Dependency: [java-gnome](https://aur.archlinux.org/packages/java-gnome/)<sup><small>AUR</small></sup> from AUR (and [scala](https://www.archlinux.org/packages/?name=scala))
*   Makedependency: [scala](https://www.archlinux.org/packages/?name=scala)
*   Build with: `scalac -cp /usr/share/java/gtk.jar -d HelloWorld.jar HelloWorld.scala`
*   Run with: `java -cp /usr/share/java/gtk.jar:HelloWorld.jar HelloWorld` (or `scala -cp /usr/share/java/gtk.jar HelloWorld.scala`)

 `HelloWorld.scala` 

```
import org.gnome.gtk._

object HelloWorld {
  def main(args: Array[String]) {
    Gtk.init(args)
    var hello = new InfoMessageDialog(null, "Hello world!", "This is an example dialog.")
    hello.run()
  }
}
```

### Vala

*   Dependency: [gtk3](https://www.archlinux.org/packages/?name=gtk3)
*   Makedependency: [vala](https://www.archlinux.org/packages/?name=vala)
*   Build with: `valac --pkg gtk+-3.0 hello_world.vala`

 `hello_world.vala` 

```
using Gtk;
public class HelloWorld {
	static void main (string[] args) {
		Gtk.init (ref args);
		var Hello=new MessageDialog (null, Gtk.DialogFlags.MODAL, Gtk.MessageType.INFO, Gtk.ButtonsType.OK, "Hello world!");
		Hello.format_secondary_text ("This is an example dialog.");
		Hello.run ();
	}
}
```

### Visual Basic .NET

*   Dependency: [gtk-sharp-3](https://www.archlinux.org/packages/?name=gtk-sharp-3)
*   Makedependency: [mono-basic](https://www.archlinux.org/packages/?name=mono-basic)
*   Build with: `vbnc -r:/usr/lib/mono/gtk-sharp-3.0/gio-sharp.dll -r:/usr/lib/mono/gtk-sharp-3.0/glib-sharp.dll -r:/usr/lib/mono/gtk-sharp-3.0/gtk-sharp.dll hello_world.vb`
*   Run with: `mono hello_world.exe`

 `hello_world.vb` 

```
Imports Gtk
Public Class Hello
	Inherits MessageDialog
	Public Sub New
		MyBase.New(Me, DialogFlags.Modal, MessageType.Info, ButtonsType.Ok, "Hello world!")
		Me.SecondaryText = "This is an example dialog."
	End Sub
	Public Shared Sub Main
		Application.Init
		Dim Dialog As New Hello
		Dialog.Run
	End Sub
End Class
```

Retrieved from "[https://wiki.archlinux.org/index.php?title=GTK%2B/Development&oldid=393257](https://wiki.archlinux.org/index.php?title=GTK%2B/Development&oldid=393257)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Widget toolkits](/index.php/Category:Widget_toolkits "Category:Widget toolkits")
*   [Development](/index.php/Category:Development "Category:Development")