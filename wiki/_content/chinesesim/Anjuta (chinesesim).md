Anjuta DevStudio[[1]](http://www.anjuta.org/)是一个全功能集成开发环境。包括工程管理，应用程序创建向导，交互式调试器，源码编辑器，版本控制，GUI设计器，性能分析器和其他更多的可扩展工具。它提供简单和易用的用户界面，同时又强大的高效开发环境。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 功能](#.E5.8A.9F.E8.83.BD)
    *   [2.1 用户界面](#.E7.94.A8.E6.88.B7.E7.95.8C.E9.9D.A2)
    *   [2.2 插件系统](#.E6.8F.92.E4.BB.B6.E7.B3.BB.E7.BB.9F)
    *   [2.3 文件管理器](#.E6.96.87.E4.BB.B6.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [2.4 工程管理器](#.E5.B7.A5.E7.A8.8B.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [2.5 工程向导](#.E5.B7.A5.E7.A8.8B.E5.90.91.E5.AF.BC)
    *   [2.6 源代码编辑器](#.E6.BA.90.E4.BB.A3.E7.A0.81.E7.BC.96.E8.BE.91.E5.99.A8)
    *   [2.7 集成Glade UI设计器](#.E9.9B.86.E6.88.90Glade_UI.E8.AE.BE.E8.AE.A1.E5.99.A8)
    *   [2.8 集成调试器](#.E9.9B.86.E6.88.90.E8.B0.83.E8.AF.95.E5.99.A8)
    *   [2.9 集成 Devhelp API 帮助查看器](#.E9.9B.86.E6.88.90_Devhelp_API_.E5.B8.AE.E5.8A.A9.E6.9F.A5.E7.9C.8B.E5.99.A8)
    *   [2.10 符号查看与导航](#.E7.AC.A6.E5.8F.B7.E6.9F.A5.E7.9C.8B.E4.B8.8E.E5.AF.BC.E8.88.AA)
    *   [2.11 类生成器和文件向导](#.E7.B1.BB.E7.94.9F.E6.88.90.E5.99.A8.E5.92.8C.E6.96.87.E4.BB.B6.E5.90.91.E5.AF.BC)

## 安装

[anjuta](https://www.archlinux.org/packages/?name=anjuta) 包可以在[extra]库中找到，使用[pacman](/index.php/Pacman "Pacman")安装:

```
# pacman -S anjuta

```

一些插件可以在[anjuta-extras](https://www.archlinux.org/packages/?name=anjuta-extras)包里找到

```
# pacman -S anjuta-extras

```

## 功能

### 用户界面

Anjuta has a flexible and advanced docking system that allows you to lay out all views in whatever way you like. You can drag and drop the views using drag bars and rearrange the layout. The layouts are persistent for each project so you can maintain different layouts for different projects. All dock views are minimizable to avoid clutter in the main window. Minimized views appear as icons on the left side of the main window. You can configure all menu actions either by typing when the cursor is over a menu item (the usual GNOME way) or through a dedicated shortcut configuration user interface.

### 插件系统

Anjuta通过插件，使其具有非常高的扩展性。Anjuta中的几乎所有的功能都是通过可以动态启用或禁用的插件来实现的。 你可以选择哪些插件在你的工程模式中激活或者在默认模式（无工程打开模式）中激活。像UI布局一样，Anjuta会为每个工程持久保存激活插件集，这也通过使用不同的插件集来使项目工作变得容易些。 通过使用插件，你可以为Anjuta扩展你想要的功能。由于Anjuta使用C语言写的，插件框架和API也是使用C来完成的。然而，C++和Python绑定也在活跃的开发中。在不久，也可以通过C++和Python来写Anjuta插件。 所有的插件都可以轻易的被实现类似功能的不同插件来替换掉。这允许你，比如，从多个不同的编辑器中选择你喜欢的（目前，我们只有Scintilla和GtkSourceView编辑器可用）或者实现一个符合你的要求的新编辑器（比如Vim/Emacs）。这对任何插件都是一样的。如果Anjuta发现多个可用的插件实现同样的功能，它会提醒用户选择一个并记住选择。

### 文件管理器

集成的文件管理器插件多少很像典型的树形文件管理器。 它会列出当前工程的所有目录和文件（或者预先配置的目录，如果没有打开工程的话）。你可以选择不显示隐藏文件和被版本控制系统忽略的文件。

在任何文件上的默认操作（双击）会打开文件，不管是通过Anjuta中可以处理该文件类型的插件或者是标准桌面中配置的外部应用程序。文件也可以在上下文菜单中用其他应用程序或者插件打开。可用的程序和插件会在上下文菜单中列出。

In addition, the file manager context menu also lists actions associated with other plugins, such as build actions (associated with the build system plugin), CVS/Subversion actions (associated with version control system plugins) and project actions (associated with the project manager plugin). This allows you to conveniently perform all actions from within the file manager.

### 工程管理器

Anjuta has a powerful project manager plugin which can open pretty much any automake/autoconf based project on the planet. It might fail on some oddly configured projects, but as long as the project uses automake/autoconf in a typical way, it should work.

The neat thing is that Anjuta does not store any project information beyond what is already available in the project structure. That is, there is no separate project data maintained by Anjuta and all project processing is done directly within the project structure. This allows a project to be maintained or developed outside Anjuta without any need to convert to or from an Anjuta-specific format. Since technically Anjuta projects are just automake projects, mixed development (with both Anjuta and non-Anjuta users) or switching back and forth between Anjuta and other tools is quite possible without any hindrance.

The project manager window displays the project's automake hierarchy organized into groups of targets. Groups correspond to directories in your project and targets correspond to normal automake targets (not to be confused with make targets). The project manager window actually has two parts: the lower part shows the complete project hierarchy and the upper part lists important targets directly. Important targets include executable and library targets; the view makes these easily accessible. This is particularly useful in large projects where the hierarchy can be deep and hard to navigate from the tree alone. Targets are, in turn, composed of source files.

Each project group and target is configurable in the standard automake way. You can set compiler and linker flags directly for each target, or set configure variables. Groups allow you to set an installation destination for their targets.

Just like the file manager, the project manager view also has convenience actions (accessible from the context menu) for source files and targets.

### 工程向导

The project wizard plugin uses a powerful template processing engine called autogen. All new projects are created from templates that are written in autogen syntax. The project wizard lets you create new projects from a selection of project templates. The selection includes simple generic, flat (no subdirectory), GTK+, GNOME, Java, Python projects and more. New templates can be easily downloaded and installed since each template is just a collection of text files.

### 源代码编辑器

There are two editors currently available in Anjuta; the Scintilla-based (classic) editor and the new GtkSourceView-based editor. Except for some minor differences, both are equally functional and can be used interchangeably. Depending on your taste in editing, you can choose either one. Editor features include:

1.  语法高亮: The editor supports syntax highlighting for almost all common programing languages. Syntax highlighting for new languages can be easily added by adding a properties file, a lexer parser (for the Scintilla editor) or lang files (for the GtkSourceView editor).

1.  智能缩进: Code is automatically indented as you type based on the language and your indentation settings. (Smart indentation is currently only available for C and C++; for other languages, Anjuta performs only basic indentation.)

1.  Autoindentation: The editor can indent the current line or a selection of lines according to your indentation settings.

1.  自动代码格式化(仅C和C++可用): The editor can reformat source code using the indent program. The full range of indent options is available.

1.  代码折叠/隐藏: You can fold code blocks and functions to hide them hierarchically, and can unfold them to unhide them.

1.  行号和标记号显示: The editor has left margins which display line numbers, markers and fold points.

1.  文本缩放: You can zoom (change the editor font size) using either the scroll wheel or menu commands.

1.  代码自动完成: The editor can autocomplete known symbols, and provides type-ahead suggestions to choose for completion.

1.  函数原型的调用提示: When you are typing a function call, the editor provides a helpful tip showing the parameters from the function's prototype.

1.  缩进指导: The editor has guides to make it easier to see indentation levels.

1.  书签: You can set or unset bookmarks for convieniently navigating to frequent destinations in your source code.

1.  多重分割视图: The editor provides multiple views for the same file (split inside the same editor). This allows you to enter text in a file while referring to the same file at another location, or to copy/paste within the same file at different locations without having to scroll back and forth.

1.  渐进式搜索: The editor can search instantly as you type a search string in the search box. This is useful when you want to avoid typing a full search string when the first few characters are enough to reach the desired location.

Powerful search and replace: The editor supports searching for strings and regular expressions, searching in files or searching all files in your project.

1.  行号跳转: You can instantly jump to any line number in a source file.

1.  构建信息高亮: Error/warning/information messages are indicated in the editor with helpful (and appropriately colored) underlines. This lets you navigate through a source file correcting all build errors without having to use the build output to jump to errors individually.

1.  Tab页面重排序: You can reorder editor tabs as you like.

1.  文件改变通知: Anjuta notifies you when a file is modified outside Anjuta while it is open in Anjuta.

### 集成Glade UI设计器

Glade is the GTK+/GNOME WYSIWYG graphical user interface designer which lets you create user interfaces (dialogs and windows) for your application visualy. Glade files can be directly edited within Anjuta. When a Glade file is opened or created, the Glade plugin is started and brings up the designer view, palettes, properties editor and widgets view. The project can have any number of Glade files and, conveniently, more than one can be opened simultaneously (however, only one can be edited at a time).

### 集成调试器

Anjuta provides a full source-level debugger (currently backed by gdb, but there will be other debugger backends soon). The debugger provides everything that can be expected from a typical source debugger including breakpoints, watches, source navigation, stack traces, threads, a disassembly view, registers, local variables, and memory dumps. You can also set up breakpoints and watches without first having the debugger running. They are saved in your session so that the next debugging session will still have them.

You can control program execution under the debugger in various ways: you can single step, step over, step out, continue execution, run to the cursor, pause the program, or attach to a running process. All programs in a project can be started in a terminal window and can be provided arguments. When a program links shared libraries within a project, the debugger starts the program correctly using libtool to ensure that non-installed libraries are picked up rather than installed ones.

### 集成 Devhelp API 帮助查看器

Devhelp is the GTK+/GNOME developer's help browser. It is conveniently integrated into Anjuta to give instant API help. Press Shift+F1 to jump to the API documentation of the symbol at the editor cursor. Make sure you have enabled the Devhelp plugin for the project. In Devhelp, you can browse all installed help documents from the tree view and can search for symbols in the search view.

### 符号查看与导航

The symbol db plugin shows all symbols in your project organized by type. There are three views in the symbol browser: one showing the global symbol tree, another showing symbols in the current file and a third view for searching symbols. You can navigate to any symbol's definition or declaration.

When Anjuta is started for the first time, it also indexes symbols from all installed libraries for autocompletion and calltips. This provides an instant reference to library functions used in the project. The libraries that should be referenced can be selected from the symbol db preferences or will be read from the project configuration automatically.

### 类生成器和文件向导

With the class generator plugin, you can create C++ and GObject classes easily and add them to your projects. Similarly, the file wizard can create templates for new source files.