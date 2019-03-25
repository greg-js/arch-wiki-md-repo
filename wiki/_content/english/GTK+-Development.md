<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Write a simple message dialog app](#Write_a_simple_message_dialog_app)
    *   [1.1 Ada](#Ada)
    *   [1.2 Bash](#Bash)
    *   [1.3 BASIC](#BASIC)
    *   [1.4 Boo](#Boo)
    *   [1.5 C](#C)
    *   [1.6 C++](#C++)
    *   [1.7 C#](#C#)
    *   [1.8 Cobra](#Cobra)
    *   [1.9 D](#D)
    *   [1.10 F#](#F#)
    *   [1.11 Fortran](#Fortran)
    *   [1.12 Genie](#Genie)
    *   [1.13 Go](#Go)
    *   [1.14 Groovy](#Groovy)
    *   [1.15 Haskell](#Haskell)
    *   [1.16 IronPython](#IronPython)
    *   [1.17 Java](#Java)
    *   [1.18 JavaScript](#JavaScript)
    *   [1.19 JRuby](#JRuby)
    *   [1.20 Jython](#Jython)
    *   [1.21 Lua](#Lua)
    *   [1.22 Nemerle](#Nemerle)
    *   [1.23 Pascal](#Pascal)
    *   [1.24 Perl](#Perl)
    *   [1.25 Prolog](#Prolog)
    *   [1.26 Python](#Python)
    *   [1.27 Ruby](#Ruby)
    *   [1.28 Rust](#Rust)
    *   [1.29 Scala](#Scala)
    *   [1.30 Vala](#Vala)
    *   [1.31 Visual Basic .NET](#Visual_Basic_.NET)
*   [2 See also](#See_also)

## Write a simple message dialog app

You can write your own GTK+ 3 message dialog easily in many programming languages through GObject-Introspection or bindings, or you can simply use bash.

The following examples display a simple "Hello world" in a message dialog.

### Ada

*   Dependency: [gtkada](https://aur.archlinux.org/packages/gtkada/)
*   Makedependency: [gcc-ada](https://www.archlinux.org/packages/?name=gcc-ada)
*   Build with: `gnatmake hello_world `gtkada-config``

 `hello_world.adb` 
```
with Gtk.Main;
with Gtk.Dialog;           use Gtk.Dialog;
with Gtk.Message_Dialog;   use Gtk.Message_Dialog;

procedure hello_world is
  Dialog   : Gtk_Message_Dialog;
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

### BASIC

*   Dependency: [gtk3](https://www.archlinux.org/packages/?name=gtk3)
*   Makedependency: [freebasic-gnomeheaders](https://aur.archlinux.org/packages/freebasic-gnomeheaders/)
*   Build with: `fbc hello_world.bas`

 `hello_world.bas` 
```
#include "Gir/Gtk-3.0.bi"
Dim As GtkWidget Ptr hello
gtk_init (cast(gint ptr, @__fb_argc__), @__fb_argv__)
hello = gtk_message_dialog_new (NULL, GTK_DIALOG_MODAL, GTK_MESSAGE_INFO, GTK_BUTTONS_OK, "Hello world!")
gtk_message_dialog_format_secondary_text (GTK_MESSAGE_DIALOG (hello), "This is an example dialog.")
gtk_dialog_run (GTK_DIALOG (hello))
```

### Boo

*   Dependency: [gtk-sharp-3](https://www.archlinux.org/packages/?name=gtk-sharp-3) (and [boo](https://aur.archlinux.org/packages/boo/))
*   Makedependency: [boo](https://aur.archlinux.org/packages/boo/)
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
        return 0;
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
*   Makedependency: [cobra](https://aur.archlinux.org/packages/cobra/)
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

*   Dependency: [gtkd](https://www.archlinux.org/packages/?name=gtkd)
*   Makedependency: [ldc](https://www.archlinux.org/packages/?name=ldc)
*   Build with: `ldc hello_world $(pkg-config --cflags --libs gtkd-3)`

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
*   Makedependency: [fsharp](https://aur.archlinux.org/packages/fsharp/)
*   Build with: `fsharpc -r:gtk-sharp.dll -I:/usr/lib/mono/gtk-sharp-3.0/ hello_world.fs`
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

*   Dependency: [gtk-3-fortran-git](https://aur.archlinux.org/packages/gtk-3-fortran-git/)
*   Makedependency: [gcc-fortran](https://www.archlinux.org/packages/?name=gcc-fortran)
*   Build with: `gfortran -o hello_world $(pkg-config --cflags --libs gtk-3-fortran) hello_world.f90`

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
*   Makedependency: [gotk3-git](https://aur.archlinux.org/packages/gotk3-git/)
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

*   Dependencies: [groovy](https://www.archlinux.org/packages/?name=groovy), [java-gnome](https://aur.archlinux.org/packages/java-gnome/)
*   Build with: `groovyc -cp /usr/share/java/gtk.jar HelloWorld.groovy && jar cfe HelloWorld.jar HelloWorld HelloWorld.class`
*   Run with: `java -cp /usr/share/groovy/embeddable/groovy-all.jar:/usr/share/java/gtk.jar:HelloWorld.jar HelloWorld` or `groovy -cp /usr/share/java/gtk.jar HelloWorld.groovy`

 `HelloWorld.groovy` 
```
import org.gnome.gtk.*
Gtk.init()
def Hello = new InfoMessageDialog(null, "Hello world!", "This is an example dialog.")
Hello.run()
```

### Haskell

*   Dependency: [gtk3](https://www.archlinux.org/packages/?name=gtk3)
*   Makedependency: [haskell-gtk](https://www.archlinux.org/packages/?name=haskell-gtk)
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

### IronPython

*   Dependencies: [gtk-sharp-3](https://www.archlinux.org/packages/?name=gtk-sharp-3), [ironpython](https://aur.archlinux.org/packages/ironpython/)
*   Run with: `ipy hello_world.py`

 `hello_world.py` 
```
import clr
clr.AddReference('gtk-sharp')
import Gtk
Gtk.Application.Init()
Hello = Gtk.MessageDialog (None, Gtk.DialogFlags.Modal, Gtk.MessageType.Info, Gtk.ButtonsType.Ok, "Hello world!")
Hello.SecondaryText="This is an example dialog."
Hello.Run()
```

### Java

*   Dependency: [java-gnome](https://aur.archlinux.org/packages/java-gnome/)
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

*   Dependencies: [gtk3](https://www.archlinux.org/packages/?name=gtk3), [gjs](https://www.archlinux.org/packages/?name=gjs)

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

### JRuby

*   Dependencies: [java-gnome](https://aur.archlinux.org/packages/java-gnome/), [jruby](https://www.archlinux.org/packages/?name=jruby)
*   Build with: `jrubyc hello_world.rb && jar cfe hello_world.jar hello_world hello_world.class`
*   Run with: `java -cp /opt/jruby/lib/jruby.jar:hello_world.jar hello_world` or `jruby hello_world.rb`

 `hello_world.rb` 
```
require '/usr/share/java/gtk.jar'
import Java::OrgGnomeGtk::Gtk
import Java::OrgGnomeGtk::Dialog
import Java::OrgGnomeGtk::InfoMessageDialog

Gtk.init(nil)
Hello = InfoMessageDialog.new(nil, "Hello world!", "This is an example dialog.")
Hello.run
```

### Jython

*   Dependencies: [java-gnome](https://aur.archlinux.org/packages/java-gnome/), [jython](https://www.archlinux.org/packages/?name=jython)
*   Run with: `jython -Dpython.path=/usr/share/java/gtk.jar hello_world.py`

 `hello_world.py` 
```
from org.gnome.gtk import Gtk, InfoMessageDialog
Gtk.init(None)
Hello=InfoMessageDialog(None, "Hello world!", "This is an example dialog.")
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

### Nemerle

*   Dependency: [gtk-sharp-3](https://www.archlinux.org/packages/?name=gtk-sharp-3)
*   Makedependency: [nemerle](https://aur.archlinux.org/packages/nemerle/)
*   Build with: `ncc -pkg:gtk-sharp-3.0 -out:hello_world.exe hello_world.n`
*   Run with: `mono hello_world.exe`

 `hello_world.n` 
```
using Gtk;
public class HelloWorld {
	static Main() : void {
		Application.Init ();
		def Hello = MessageDialog (null, DialogFlags.Modal, MessageType.Info, ButtonsType.Ok, "Hello world!");
		Hello.SecondaryText = "This is an example dialog.";
		_ = Hello.Run ();
	}
}
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

*   Dependency: [perl-gtk3](https://www.archlinux.org/packages/?name=perl-gtk3)

 `hello_world.pl` 
```
#!/usr/bin/env perl
use Gtk3 -init;
my $hello = Gtk3::MessageDialog->new (undef, 'modal', 'info', 'ok', "Hello world!");
$hello->set ('secondary-text' => 'This is an example dialog.');
$hello->run;
```

### Prolog

*   Dependency: [plgi](https://aur.archlinux.org/packages/plgi/)
*   Run with: `swipl hello_world.pl`

 `hello_world.pl` 
```
:- use_module(library(plgi)).
:- plgi_use_namespace('Gtk').

main :-
	g_object_new('GtkMessageDialog',
	             ['message-type'='GTK_MESSAGE_INFO',
	              'buttons'='GTK_BUTTONS_OK',
	              'text'='Hello world!',
	              'secondary-text'='This is an example dialog.'],
	             Dialog),
	gtk_dialog_run(Dialog, _),
	halt.
:- main.
```

### Python

*   Dependencies: [gtk3](https://www.archlinux.org/packages/?name=gtk3), [python-gobject](https://www.archlinux.org/packages/?name=python-gobject) (or [python2-gobject](https://www.archlinux.org/packages/?name=python2-gobject) for Python 2)

 `hello_world.py` 
```
#!/usr/bin/env python
import gi
gi.require_version('Gtk', '3.0')
from gi.repository import Gtk
Gtk.init(None)
Hello = Gtk.MessageDialog(message_type=Gtk.MessageType.INFO,
                          buttons=Gtk.ButtonsType.OK,
                          text="Hello world!",
                          secondary_text="This is an example dialog.")
Hello.run()
```

### Ruby

*   Dependency: [gtk3](https://www.archlinux.org/packages/?name=gtk3), [ruby-gir_ffi-gtk](https://aur.archlinux.org/packages/ruby-gir_ffi-gtk/)

 `hello_world.rb` 
```
#!/usr/bin/env ruby
require 'gir_ffi-gtk3'
Gtk.init
Hello = Gtk::MessageDialog.new nil, :modal, :info, :ok, "Hello world!"
Hello.secondary_text = "This is an example dialog."
Hello.run
```

*   Dependency: [ruby-gtk3](https://www.archlinux.org/packages/?name=ruby-gtk3)

 `hello_world.rb` 
```
#!/usr/bin/env ruby
require 'gtk3'
Gtk.init
Hello = Gtk::MessageDialog.new(:type => :info,
                               :buttons_type => :ok,
                               :message => "Hello world!")
Hello.secondary_text = "This is an example dialog."
Hello.run
```

### Rust

Using [Gtk-rs](http://gtk-rs.org/).

*   Dependency: [gtk3](https://www.archlinux.org/packages/?name=gtk3)
*   Makedependency: [rust](https://www.archlinux.org/packages/?name=rust)
*   Build with: `cargo build`
*   Run with: `target/debug/hello_world` or `cargo run`

 `Cargo.toml` 
```
[package]
name = "hello_world"
version = "0.1.0"

[dependencies]
gtk = "^0"
```
 `src/main.rs` 
```
extern crate gtk;
use gtk::prelude::*;
use gtk::{ButtonsType, DialogFlags, MessageType, MessageDialog, Window};

fn main() {
    let _ = gtk::init();
    MessageDialog::new(None::<&Window>,
                       DialogFlags::empty(),
                       MessageType::Info,
                       ButtonsType::Ok,
                       "Hello world!").run();
}
```

### Scala

*   Dependency: [java-gnome](https://aur.archlinux.org/packages/java-gnome/) (and [scala](https://www.archlinux.org/packages/?name=scala))
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
*   Makedependency: [mono-basic](https://aur.archlinux.org/packages/mono-basic/)
*   Build with: `vbnc -r:/usr/lib/mono/gtk-sharp-3.0/gtk-sharp.dll hello_world.vb`
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

## See also

*   [GNOME Developer Center](https://developer.gnome.org/)
*   [GTK+ 3 Reference Manual](https://developer.gnome.org/gtk3/stable/)
*   [GTK+ 2.0 Tutorial](https://developer.gnome.org/gtk-tutorial/stable/)
*   [gtkmm 3 Tutorial](https://developer.gnome.org/gtkmm-tutorial/stable/)