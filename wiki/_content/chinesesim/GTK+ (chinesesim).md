相关文章

*   [统一QT和GTK程序的外观](/index.php/Uniform_Look_for_QT_and_GTK_Applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Uniform Look for QT and GTK Applications (简体中文)")
*   [Qt](/index.php/Qt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Qt (简体中文)")
*   [GNU Project](/index.php/GNU_Project "GNU Project")

**翻译状态：** 本文是英文页面 [GTK+](/index.php/GTK%2B "GTK+") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-02-18，点击[这里](https://wiki.archlinux.org/index.php?title=GTK%2B&diff=0&oldid=247172)可以查看翻译后英文页面的改动。

摘自[GTK+ 官方网站](http://www.gtk.org)：

	*GTK+，或称 GIMP Toolkit，是一个跨平台的图形界面开发库。该库提供各式各样的窗口部件，小到一次性使用的程序、大到大型应用，GTK+ 都能满足你的需求。*

GTK+，或称 GIMP Toolkit，最初由[GNU项目](/index.php/GNU_Project "GNU Project")为图像编辑软件[GIMP](/index.php/GIMP "GIMP")开发，但现在它已经被广泛地应用在各种语言的图形界面编程中。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 配置工具](#配置工具)
*   [2 主题](#主题)
    *   [2.1 GTK+ 1.x](#GTK+_1.x)
    *   [2.2 GTK+ 2.x](#GTK+_2.x)
    *   [2.3 GTK+ 3.x](#GTK+_3.x)
    *   [2.4 GTK+ 与 QT](#GTK+_与_QT)
*   [3 配置文件](#配置文件)
    *   [3.1 使用自定义键盘快捷键](#使用自定义键盘快捷键)
    *   [3.2 加速 GNOME 菜单显示](#加速_GNOME_菜单显示)
    *   [3.3 缩小窗口部件](#缩小窗口部件)
*   [4 开发](#开发)
    *   [4.1 编写简单的对话框](#编写简单的对话框)
        *   [4.1.1 Bash](#Bash)
        *   [4.1.2 Boo](#Boo)
        *   [4.1.3 C](#C)
        *   [4.1.4 C++](#C++)
        *   [4.1.5 C#](#C#)
        *   [4.1.6 Genie](#Genie)
        *   [4.1.7 Java](#Java)
        *   [4.1.8 JavaScript](#JavaScript)
        *   [4.1.9 Perl](#Perl)
        *   [4.1.10 Python](#Python)
        *   [4.1.11 Vala](#Vala)
        *   [4.1.12 Visual Basic .NET](#Visual_Basic_.NET)
*   [5 相关资源](#相关资源)

## 配置工具

使用下列GUI（图形界面）程序，可以调整GTK+程序主题、字体等设置。其基本原理是修改`~/.gtkrc-2.0`文件。

*   [lxappearance](https://www.archlinux.org/packages/?name=lxappearance)：来自[LXDE](/index.php/LXDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LXDE (简体中文)")的配置工具，不过不依赖任何LXDE或其他桌面环境组件。比起其他配置工具，可定制性更强。
*   [gtk-chtheme](https://www.archlinux.org/packages/?name=gtk-chtheme)
*   [gtk-theme-switch2](https://www.archlinux.org/packages/?name=gtk-theme-switch2)
*   [gtk2_prefs](https://aur.archlinux.org/packages/gtk2_prefs/)

安装，以[gtk-theme-switch2](https://www.archlinux.org/packages/?name=gtk-theme-switch2)为例：

```
# pacman -S gtk-theme-switch2

```

另见：[为不同图形库分别设置外观](/index.php/Uniform_look_for_Qt_and_GTK_applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#怎样为每一个工具设置风格? "Uniform look for Qt and GTK applications (简体中文)")。

## 主题

### GTK+ 1.x

古老的GTK+1程序（如xmms）默认主题很难看。改进方法：

1.  下载并安装一些好看的主题
2.  修改主题

[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")上有不错的主题：[gtk-smooth-engine](https://aur.archlinux.org/packages/gtk-smooth-engine/)

可以使用*gtk-theme-switch2*修改主题。

### GTK+ 2.x

多数[桌面环境](/index.php/Desktop_environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop environment (简体中文)")都会提供配置GTK+主题、图标、字体的工具。此外，下面提到的这些工具也很不错。

建议同时安装一些好看的GTK+2主题，比如*Clearlooks*（包含在[gtk-engines](https://www.archlinux.org/packages/?name=gtk-engines)软件包）：

```
# pacman -S gtk-engines

```

[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")上还有更多主题：

*   [https://aur.archlinux.org/packages.php?O=0&K=gtk2-theme&do_Search=Go](https://aur.archlinux.org/packages.php?O=0&K=gtk2-theme&do_Search=Go)
*   [https://aur.archlinux.org/packages.php?O=0&K=gtk-theme&do_Search=Go](https://aur.archlinux.org/packages.php?O=0&K=gtk-theme&do_Search=Go)

可以手动修改配置文件`~/.gtkrc-2.0`来配置GTK+。[GNOME图书馆](http://library.gnome.org/devel/gtk/stable/GtkSettings.html)提供了各种设置的清单。下面给出了配置GTK+主题、图标、字体和字体大小的示范：

 `~/.gtkrc-2.0` 
```
gtk-icon-theme-name = "[图标主题名称]"
gtk-theme-name = "[主题名称]"
gtk-font-name = "[字体名] [大小]"
```

例如：

 `~/.gtkrc-2.0` 
```
gtk-icon-theme-name = "Tango"
gtk-theme-name = "Murrine-Gray"
gtk-font-name = "DejaVu Sans 8"
```

{{注意|使用上述配置，需要安装软件包[ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)、[tangerine-icon-theme](https://www.archlinux.org/packages/?name=tangerine-icon-theme)、[gtk-engine-murrine](https://www.archlinux.org/packages/?name=gtk-engine-murrine)以及[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")中的[gtk-theme-murrine-collection](https://aur.archlinux.org/packages/gtk-theme-murrine-collection/).

### GTK+ 3.x

如果使用 GNOME 3，可以使用[gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool)配置主题。安装：

```
# pacman -S gnome-tweak-tool

```

如果不想用[gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool)，需要自己编辑`{XDG_CONFIG_HOME}/gtk-3.0/settings.ini`（通常为`~/.config/gtk-3.0/settings.ini`）设置主题。文件示例：

 `{XDG_CONFIG_HOME}/gtk-3.0/settings.ini` 
```
[Settings]
gtk-application-prefer-dark-theme = false
gtk-theme-name = Zukitwo
gtk-icon-theme-name = gnome
```

如果还是不起作用，那么删除旧的`{XDG_CONFIG_HOME}/gtk-3.0`目录，并从主题路径复制新的`gtk-3.0`目录。例如：

```
rm -r ~/.config/gtk-3.0/
cp -r /usr/share/themes/Zukitwo/gtk-3.0/ ~/.config/  

```

然后，你需要在桌面环境的外观配置工具中使用相同主题。只有少数几款主题同时提供了外观统一的GTK+3和GTK+2版本：

1.  Adwaita (part of [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard))
2.  Newlooks for GTK+ 3 and Clearlooks for GTK+ 2
3.  Zukitwo
4.  Elegant Brit
5.  Atolm
6.  Hope

**注意:** 有些主题需要[librsvg](https://www.archlinux.org/packages/?name=librsvg)才能正常显示，如果出现主题界面不正常，可以尝试安装它。

**注意:** 未来可能还会有其他提供统一外观的跨GTK+版本主题，有些主题在[AUR](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)")中可以找到。此外，其中某些主题在某些情况会出现问题，比如GTK+2面板（浅色底、浅色字），所以最好使用[这里](http://i.imgur.com/QmeyN.png)提供的面板背景。

### GTK+ 与 QT

同时在系统上安装GTK+和QT（通常是[KDE](/index.php/KDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KDE (简体中文)")组件）程序的人都知道，两者的外观并不怎么协调。关于两者外观统一的问题，参见：[协调QT和GTK+程序的外观](/index.php/Uniform_look_for_Qt_and_GTK_applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Uniform look for Qt and GTK applications (简体中文)")。

## 配置文件

**注意:** 参见GTK+编程手册中的[*GtkSettings*设置](http://library.gnome.org/devel/gtk/stable/GtkSettings.html#GtkSettings.properties)部分，以了解所有GTK+配置选项。

本节介绍了许多GTK+设置，可用在`~/.gtkrc-2.0`文件中。

### 使用自定义键盘快捷键

有个秘密技巧：把鼠标放在某个菜单项，然后按下某个按键组合，即可修改该项目的快捷键。不过，该功能默认是关闭的。启用方法是使用以下配置：

```
gtk-can-change-accels = 1

```

### 加速 GNOME 菜单显示

鼠标指向菜单与菜单显示之间有一个延迟，以下设置就是该延迟时间（应该是以毫秒为单位）：

```
gtk-menu-popup-delay = 0

```

### 缩小窗口部件

如果屏幕很小，不喜欢过大的图标和窗口部件，可以调整其尺寸。

工具栏仅显示图标：

```
gtk-toolbar-style = GTK_TOOLBAR_ICONS

```

显示小图标：

```
gtk-icon-sizes = "panel-menu=16,16:panel=16,16:gtk-menu=16,16:gtk-large-toolbar=16,16\
:gtk-small-toolbar=16,16:gtk-button=16,16"

```

按钮上不显示图标：

```
gtk-button-images = 0

```

菜单不显示图标：

```
gtk-menu-images = 0

```

更多gtkrc优化配置参见[此文](http://martin.ankerl.com/2008/10/10/how-to-make-a-compact-gnome-theme/)。此外，使用[该主题](http://gnome-look.org/content/show.php/Simple+eGTK?content=119812)即可搞定上面所有配置。

## 开发

使用gcc编译C语言的GTK+3程序时，需要添加一些CFLAGS（编译开关）：

```
gcc -g -Wall `pkg-config --cflags --libs gtk+-3.0` -o base base.c

```

-g 和 -Wall 是可选的，程序调试时会用到。

官方提供了一个示范程序：[Hello World](http://developer.gnome.org/gtk-tutorial/stable/c39.html#SEC-HELLOWORLD)。

### 编写简单的对话框

通过GObject-Introspection或语言接口，可以轻松地使用各种语言编写GTK+3程序，甚至bash也可以。

下列示例程序会在屏幕上显示一个信息对话框，上面写有“Hello world”。

#### Bash

*   依赖：[zenity](https://www.archlinux.org/packages/?name=zenity)

 `hello_world.sh` 
```
#!/bin/bash
zenity --info --title='Hello world!' --text='This is an example dialog.'
```

#### Boo

*   依赖： [gtk-sharp-git](https://aur.archlinux.org/packages/gtk-sharp-git/) 来自 AUR ([boo](https://aur.archlinux.org/packages/boo/))
*   编译依赖： [boo](https://aur.archlinux.org/packages/boo/)
*   编译： `booc hello_world.boo`
*   运行： `mono hello_world.exe` (or `booi hello_world.boo`)

 `hello_world.boo` 
```
import Gtk from "gtk-sharp"
Application.Init()
Hello = MessageDialog(null, DialogFlags.Modal, MessageType.Info, ButtonsType.Close, "Hello world!")
Hello.SecondaryText = "This is an example dialog."
Hello.Run()
```

#### C

*   依赖：[gtk3](https://www.archlinux.org/packages/?name=gtk3)
*   编译：`gcc -o hello_world `pkg-config --cflags --libs gtk+-3.0` hello_world.c`

 `hello_world.c` 
```
#include <gtk/gtk.h>
void main (int argc, char *argv[]) {
	gtk_init (&argc, &argv);
        GtkWidget *hello = gtk_message_dialog_new (NULL, GTK_DIALOG_MODAL, GTK_MESSAGE_INFO, GTK_BUTTONS_OK, "Hello world!");
	gtk_message_dialog_format_secondary_text (GTK_MESSAGE_DIALOG (hello), "This is an example dialog.");
        gtk_dialog_run(GTK_DIALOG (hello));
}
```

#### C++

*   依赖：[gtkmm3](https://www.archlinux.org/packages/?name=gtkmm3)
*   编译：`g++ -o hello_world `pkg-config --cflags --libs gtkmm-3.0` hello_world.cc`

 `hello_world.cc` 
```
#include <gtkmm.h>
#include <gtkmm/messagedialog.h>
int main(int argc, char *argv[]) {
	Gtk::Main kit(argc, argv);
	Gtk::MessageDialog Hello("Hello world!", false, Gtk::MESSAGE_INFO, Gtk::BUTTONS_OK);
	Hello.set_secondary_text("This is an example dialog.");
	Hello.run();
}
```

#### C#

*   依赖： [gtk-sharp-git](https://aur.archlinux.org/packages/gtk-sharp-git/) 来自 AUR
*   编译： `mcs -pkg:gtk-sharp-3.0 hello_world.cs`
*   运行： `mono hello_world.exe`

 `hello_world.cs` 
```
using Gtk;
public class HelloWorld {
	static void Main() {
		Application.Init ();
		MessageDialog Hello = new MessageDialog (null, DialogFlags.Modal, MessageType.Info, ButtonsType.Close, "Hello world!");
		Hello.SecondaryText="This is an example dialog.";
		Hello.Run ();
	}
}
```

#### Genie

*   依赖：[gtk3](https://www.archlinux.org/packages/?name=gtk3)
*   编译时依赖：[vala](https://www.archlinux.org/packages/?name=vala)
*   编译：`valac --pkg gtk+-3.0 hello_world.gs`

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

#### Java

*   依赖： [java-gnome](https://aur.archlinux.org/packages/java-gnome/) 来自 AUR
*   编译依赖： java-environment
*   编译： `mkdir HelloWorld && javac -classpath /usr/share/java/gtk.jar -d HelloWorld HelloWorld.java`
*   运行： `java -classpath /usr/share/java/gtk.jar:HelloWorld HelloWorld`

 `HelloWorld.java` 
```
import org.gnome.gtk.Gtk;
import org.gnome.gtk.Dialog;
import org.gnome.gtk.InfoMessageDialog;

public class HelloWorld
{
    public static void main(String[] args) {
        Gtk.init(args);
        Dialog Hello = new InfoMessageDialog(null, "Hello world!", "This is an example dialog.");
        Hello.run();
    }
}
```

#### JavaScript

*   依赖：[gtk3](https://www.archlinux.org/packages/?name=gtk3)，[gjs](https://www.archlinux.org/packages/?name=gjs)（或者[seed](https://www.archlinux.org/packages/?name=seed)）

 `hello_world.js` 
```
#!/usr/bin/gjs
Gtk = imports.gi.Gtk
Gtk.init(null, null)
Hello = new Gtk.MessageDialog({type: Gtk.MessageType.INFO,
                               buttons: Gtk.ButtonsType.OK,
                               text: "Hello world!",
                               "secondary-text": "This is an example dialog."})
Hello.run()
```

#### Perl

*   依赖： [perl-gtk3](https://www.archlinux.org/packages/?name=perl-gtk3) 来自 AUR

 `hello_world.pl` 
```
#!/usr/bin/perl
use Gtk3 -init;
my $hello = Gtk3::MessageDialog->new (undef, 'modal', 'info', 'ok', "Hello world!");
$hello->set ('secondary-text' => 'This is an example dialog.');
$hello->run;
```

#### Python

*   依赖：[gtk3](https://www.archlinux.org/packages/?name=gtk3)，[python-gobject](https://www.archlinux.org/packages/?name=python-gobject)

 `hello_world.py` 
```
#!/usr/bin/python
from gi.repository import Gtk
Gtk.init(None)
Hello=Gtk.MessageDialog(None, Gtk.DialogFlags.MODAL, Gtk.MessageType.INFO, Gtk.ButtonsType.CLOSE, "Hello world!")
Hello.format_secondary_text("This is an example dialog.")
Hello.run()
```

#### Vala

*   依赖：[gtk3](https://www.archlinux.org/packages/?name=gtk3)
*   编译时依赖：[vala](https://www.archlinux.org/packages/?name=vala)
*   编译：`valac --pkg gtk+-3.0 hello_world.vala`

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

#### Visual Basic .NET

*   依赖： [gtk-sharp-git](https://aur.archlinux.org/packages/gtk-sharp-git/) 来自 AUR
*   编译依赖： [mono-basic](https://aur.archlinux.org/packages/mono-basic/)
*   编译： `vbnc -r:/usr/lib/mono/gtk-sharp-3.0/gio-sharp.dll -r:/usr/lib/mono/gtk-sharp-3.0/glib-sharp.dll -r:/usr/lib/mono/gtk-sharp-3.0/gtk-sharp.dll hello_world.vb`
*   运行： `mono hello_world.exe`

 `hello_world.vb` 
```
Imports Gtk
Public Class Hello
	Inherits MessageDialog
	Public Sub New
		MyBase.New(Me, DialogFlags.Modal, MessageType.Info, ButtonsType.Close, "Hello world!")
		Me.SecondaryText = "This is an example dialog."
	End Sub
	Public Shared Sub Main
		Application.Init
		Dim Dialog As New Hello
		Dialog.Run
	End Sub
End Class
```

## 相关资源

*   [GTK+官方网站](http://www.gtk.org/)
*   [维基百科对GTK+的介绍](https://en.wikipedia.org/wiki/GTK%2B "wikipedia:GTK+")
*   [GTK+ 2.0 指南](http://developer.gnome.org/gtk-tutorial/stable/)
*   [GTK+ 3 参考手册](http://developer.gnome.org/gtk3/stable/)
*   [gtkmm 指南](http://developer.gnome.org/gtkmm-tutorial/stable/)
*   [gtkmm 参考手册](http://developer.gnome.org/gtkmm/stable/)