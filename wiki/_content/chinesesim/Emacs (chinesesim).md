**翻译状态：** 本文是英文页面 [Emacs](/index.php/Emacs "Emacs") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-12-08，点击[这里](https://wiki.archlinux.org/index.php?title=Emacs&diff=0&oldid=229169)可以查看翻译后英文页面的改动。

[Emacs](https://en.wikipedia.org/wiki/Emacs "wikipedia:Emacs")是一个扩展方便，定制能力强，文档丰富的动态交互编辑器。Emacs的核心构建在[Emacs Lisp](https://en.wikipedia.org/wiki/Emacs_Lisp "wikipedia:Emacs Lisp")解释器之上，其中Emacs Lisp是大部分Emacs的内建函数和拓展模块的实现语言。Emacs可以在命令行界面下(CLI)工作良好，在图形界面系统下，使用GTK作为默认的图形界面构建工具。在文本编辑能力上，Emacs常常拿来和[vim](/index.php/Vim "Vim")比较。

**Note:** 入门建议直接使用starterkit扩展。本文档实际帮助不大

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 运行Emacs](#.E8.BF.90.E8.A1.8CEmacs)
    *   [2.1 没有颜色](#.E6.B2.A1.E6.9C.89.E9.A2.9C.E8.89.B2)
    *   [2.2 作为守护进程](#.E4.BD.9C.E4.B8.BA.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B)
    *   [2.3 作为systemd单元](#.E4.BD.9C.E4.B8.BAsystemd.E5.8D.95.E5.85.83)
*   [3 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [3.1 TRAMP](#TRAMP)
    *   [3.2 键盘宏和寄存器](#.E9.94.AE.E7.9B.98.E5.AE.8F.E5.92.8C.E5.AF.84.E5.AD.98.E5.99.A8)
    *   [3.3 正则表达式](#.E6.AD.A3.E5.88.99.E8.A1.A8.E8.BE.BE.E5.BC.8F)
*   [4 定制](#.E5.AE.9A.E5.88.B6)
    *   [4.1 多种配置](#.E5.A4.9A.E7.A7.8D.E9.85.8D.E7.BD.AE)
    *   [4.2 加载扩展程序](#.E5.8A.A0.E8.BD.BD.E6.89.A9.E5.B1.95.E7.A8.8B.E5.BA.8F)
    *   [4.3 Local and custom variables](#Local_and_custom_variables)
    *   [4.4 Custom colors and theme](#Custom_colors_and_theme)
    *   [4.5 SyncTeX support](#SyncTeX_support)
*   [5 Documentation](#Documentation)
    *   [5.1 Contextual help](#Contextual_help)
    *   [5.2 The manuals](#The_manuals)
*   [6 拓展模块](#.E6.8B.93.E5.B1.95.E6.A8.A1.E5.9D.97)
*   [7 疑难杂症](#.E7.96.91.E9.9A.BE.E6.9D.82.E7.97.87)
    *   [7.1 彩色输出的问题](#.E5.BD.A9.E8.89.B2.E8.BE.93.E5.87.BA.E7.9A.84.E9.97.AE.E9.A2.98)
    *   [7.2 菜单显示为空](#.E8.8F.9C.E5.8D.95.E6.98.BE.E7.A4.BA.E4.B8.BA.E7.A9.BA)
    *   [7.3 X 窗口下的字符显示问题](#X_.E7.AA.97.E5.8F.A3.E4.B8.8B.E7.9A.84.E5.AD.97.E7.AC.A6.E6.98.BE.E7.A4.BA.E9.97.AE.E9.A2.98)
    *   [7.4 启动速度慢](#.E5.90.AF.E5.8A.A8.E9.80.9F.E5.BA.A6.E6.85.A2)
        *   [7.4.1 错误的网络配置](#.E9.94.99.E8.AF.AF.E7.9A.84.E7.BD.91.E7.BB.9C.E9.85.8D.E7.BD.AE)
        *   [7.4.2 初始化文件加载慢](#.E5.88.9D.E5.A7.8B.E5.8C.96.E6.96.87.E4.BB.B6.E5.8A.A0.E8.BD.BD.E6.85.A2)
    *   [7.5 不能打开配置文件: ...](#.E4.B8.8D.E8.83.BD.E6.89.93.E5.BC.80.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6:_...)
    *   [7.6 Dead-accent keys problem: '<dead-acute> is undefined'](#Dead-accent_keys_problem:_.27.3Cdead-acute.3E_is_undefined.27)
    *   [7.7 C-M-% and some other bindings do not work in emacs nox](#C-M-.25_and_some_other_bindings_do_not_work_in_emacs_nox)
    *   [7.8 Emacs client gets stuck when switching back to it](#Emacs_client_gets_stuck_when_switching_back_to_it)
    *   [7.9 Emacs-nox output gets messy](#Emacs-nox_output_gets_messy)
    *   [7.10 Shift + Arrow keys not working in emacs within tmux](#Shift_.2B_Arrow_keys_not_working_in_emacs_within_tmux)
*   [8 替代方案](#.E6.9B.BF.E4.BB.A3.E6.96.B9.E6.A1.88)
    *   [8.1 mg](#mg)
    *   [8.2 zile](#zile)
    *   [8.3 uemacs](#uemacs)
    *   [8.4 remacs](#remacs)
*   [9 资源](#.E8.B5.84.E6.BA.90)

## 安装

Emacs有众多变体发行版本（有时候称作*emacsen*）。 最常见的莫过于 [GNU Emacs](http://www.gnu.org/software/emacs/)，在[Official repositories](/index.php/Official_repositories "Official repositories")可以找到。

在 [official repositories](/index.php/Official_repositories "Official repositories") 中可以安装 [emacs](https://www.archlinux.org/packages/?name=emacs) 。如果你经常使用命令行，你可能更喜欢没有GTK+支持的 [emacs-nox](https://www.archlinux.org/packages/?name=emacs-nox)（也没有声音或其它有趣的东西）。 值得注意的是文字模式的Emacs有一些缺点：它支持更少的颜色和字体设置功能（实时改变字体大小，单文档多字体等等）。而且emacs-nox存在一些高级功能上的缺陷，比如Speedbar和GUD（调试环境），处理复杂的外观（face）的时候速度也会变慢。

如果你想体验Emacs的所有扩展功能而不用装一堆依赖的话，你可以使用PKGBUILD来按你的需求定制Emacs。不使用 `gtk3` 可以让Emacs避免使用gconf。图像和声音的支持也可以去除。在Emacs的源代码目录下运行 `./configure --help` 可以看看有哪些配置选项。

 `PKGBUILD` 
```
# ...
  ./configure --prefix=/usr --sysconfdir=/etc --libexecdir=/usr/lib \
    --localstatedir=/var --with-x-toolkit=gtk2 --with-xft \
    --without-gconf --without-sound
# ...

```

## 运行Emacs

启动Emacs之前，你应该知道怎样关掉它（特别是你在终端里运行时）：使用 `Ctrl+x``Ctrl+c` 。

启动Emacs：

```
$ emacs

```

或者以文字模式启动：

```
$ emacs -nw

```

又或者，快速启动（不解析.emacs文件）并以文字模式启动：

```
$ emacs -Q -nw

```

如果你安装的是nox版本，'emacs' 和 'emacs -nw' 效果是一样的。

可以直接打开文件：

```
$ emacs filename.txt

```

### 没有颜色

默认情况下Emacs启动时会将超链接显示为深蓝色。不使用任何颜色主题：

```
$ emacs -nw --color=no

```

这样一来所有文字都是白色了。

### 作为守护进程

不想让Emacs每次启动都读取一次配置文件的话，可以将Emacs以守护进程运行：

```
$ emacs --daemon

```

连接到守护进程：

```
$ emacsclient -nc

```

这个命令创建一个新的frame `-c`（使用 `-t` 如果你更喜欢文字模式）并且不独占终端 `-n` （`--no-wait`）。有的程序例如Mutt和Git（为了提交信息）会等待编辑器完成编辑，所以不能使用 `-n` 参数。如果你的默认编辑器是Emacs，你需要为那些程序指定一个替代编辑器（比如 `emacsclient -a "" -t`）。

### 作为systemd单元

The old system unit method had some caveats. It gave a limited shell environment which restricted shell calls, so we will be using a user unit, which tends to work a lot better than naively calling *emacs --daemon*.

为Emacs创建一个systemd单元：

**Note:** Such a unit file is planned for inclusion in Emacs 26.1, see [emacs bug 16507](https://debbugs.gnu.org/cgi/bugreport.cgi?bug=16507).
 `~/.config/systemd/user/emacs.service` 
```
[Unit]
Description=Emacs: the extensible, self-documenting text editor

[Service]
Type=forking
ExecStart=/usr/bin/emacs --daemon
ExecStop=/usr/bin/emacsclient --eval "(kill-emacs)"
Restart=always

[Install]
WantedBy=default.target

```

You need to start and enable the unit so that it gets started on every boot (note - DO *NOT* run this as root - we want them for our user, not for the root user):

```
$ systemctl --user enable --now emacs

```

Note that systemd user units do not inherit environment variables from a login shell (like `~/.bash_profile`), so you may want to set the variables in `~/.pam_environment` instead. See [Systemd/User](/index.php/Systemd/User "Systemd/User") for more information.

If you start emacs as a daemon, you may want to set the `VISUAL` and `EDITOR` environment variables to `emacsclient` so that programs that start an editor use emacsclient instead of starting a new full instance of the editor. Programs that use an external editor include email programs (for editing the message), Git (for editing the commit message), and less (the `v` command for editing the displayed file). Do not use the `-n` (`--nowait`) option to emacsclient, since programs typically expect editing to be finished when the editor exits.

It is also recommended to change any GUI start menu entries (or equivalent) for Emacs to point to emacsclient instead of emacs, so that the emacs daemon is used instead of starting a new emacs process.

## 提示和技巧

前面的部分给出了基本编辑命令的概述，没有给出Emacs的一个指示。这个部分讲述一些高级的技巧和功能。

### TRAMP

TRAMP (Transparent Remote Access, Multiple Protocols) ，顾名思义，是一个可以通过很多协议透明访问远程文件的一个扩展。当提示输入一个文件名，输入特定的格式就可以使用TRAMPP。比如：

在打开`/etc/hosts`文件之前提示输入root的密码以获取root权限：

```
C-x C-f /su::/etc/hosts

```

要通过SSH使用'myuser'用户名登录'myhost'主机并打开文件`~/example.txt`：

```
C-x C-f /ssh:myuser@myhost:~/example.txt

```

TRAMP的路径一般是这种格式'/[protocol]:[[user@]host]:<file>'。TRAMP支持的不只上面的两个简单例子。请查看Emacs里面的TRAMPP info手册了解更多的信息。

### 键盘宏和寄存器

这一部分会提供一个实用的指南来使用一些更强大的编辑特性。也就是“键盘宏”和“寄存器”。

我们的目标是产生一个字符列表和它们在这个列表中对应的位置。虽然这可以通过手工格式化来完成，但是这样会很慢而且容易出错。如果我们采用一些Emacs更高级的编辑功能却可以起到四两拨千斤的功效。在介绍这个方法之前，需要先了解一些技术背后的细节。

要介绍的第一个特性就是*寄存器*。寄存器的功能是用来保存和获取各种各样的数据。每个寄存器用一个字母来命名，这个字母就是用来调用这个寄存器的。

另一个要介绍的就是*键盘宏*。一个键盘宏存储了一个命令序列以便以后可以重复使用。下面就一步一步地讲解这个方法。

首先我们从一个包含如下字符的缓冲区开始：

```
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz

```

通过`number-to-register' 命令 (**C-x r n**)我们来准备一个寄存器，把数字'0'存储在寄存器'k'中：

```
C-x r n k

```

当光标在缓冲区开头的时候，开始录制键盘宏 (**C-x (**) 然后开始对字符串进行格式化：

```
C-x ( C-f M-4 .

```

插入 (**C-x r i**) 然后将寄存器'k'加1 (**C-x r +**) 。开头的 (**C-u**) 命令是用来在插入文字之后让光标移到插入的文字后面：

```
C-u C-x r i k C-x r + k

```

最后我们来插入一个回车来结束格式化。Emacs可以重复以上过程，从我们定义键盘宏的位置开始，直到最后一个字符。**C-x e**命令停止宏的录制并开始执行这段宏。开头的 **M-0** 命令是用来让宏在出错的时候停下来，这样在它走到这行的结尾就会停下来。

```
<RET> M-0 C-x e

```

下面是结果：

```
 A....0
 B....1
 C....2
 [...]
 x....49
 y....50
 z....51

```

### 正则表达式

From the Emacs Manual: "A regular expression, or *regexp* for short, is a pattern that denotes a (possibly infinite) set of strings." This section will not go into any detail regarding regular expressions themselves (as there is simply too much to cover). It will however provide a quick demonstration of their power. See [Regular Expressions](http://www.gnu.org/software/emacs/manual/html_node/elisp/Regular-Expressions.html#Regular-Expressions) section in the Emacs Manual for further reading.

Given the same scenario presented above: A list of characters which are to be formatted to represent their respective position in the list. (see [Keyboard macros and registers](/index.php/Emacs#Keyboard_macros_and_registers "Emacs")). Again, starting with a buffer containing.

```
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz

```

At the beginning of the buffer, use **C-M-%** (if the key-sequence is difficult to perform, it may be more comfortable to use **M-x query-replace-regexp**). At the prompt:

```
\(.\)

```

which simply matches one character. Then, when prompted for the replacement:

```
\1....\#^J

```

**Note:** '^J' represents where a newline should be placed, it should not be entered into the prompt. The newline must instead be inserted literally using **C-q C-j**.

The replacement expression reads: "Insert the matched text between the first set of parentheses (in this case, a single character), followed by 4 periods then insert an automatically incremented number followed by a newline.

Finally, press **!** to apply this across the entire buffer. All of the formatting that was performed in the previous section was performed with a single regexp replacement.

## 定制

Emacs能通过~/.emacs或者**M-x customize**来定制。本段落将着眼于手动定制 ~/.emacs，并且提供了一些常用配置的样例。配置命令提供了一个适应的途径，通过它你能够渐渐熟悉Emacs。

这里的所有例子都能在Emacs中奏效。比如，在Emacs中计算表达式： **C-M-x** 同时指到任何需要求值的地方。

或者

**C-x C-e** 指到最后的“）”。

用'y'和'n'来代替频繁地输入'yes’和'no‘是一个好的方法：

```
(defalias 'yes-or-no-p 'y-or-n-p)

```

取消光标闪烁：

```
(blink-cursor-mode -1)

```

类似地，开启上一节提到的列号模式：

```
(column-number-mode 1)

```

它们两者之间的相似不是偶然：光标闪烁模式和列号模式都是'副参模式'，按照规则，'副参模式’能通过正负值来设置。如果参数省略，'副参模式'将被开/关。

这里有其他一些'副参模式'的例子，下面的参数将会关闭滚动栏、菜单栏、工具栏。

```
(scroll-bar-mode -1)
(menu-bar-mode -1)
(tool-bar-mode -1)

```

变量'auto-mode-alist'修改之后能够改变默认的“主参模式”。下面的例子把'.tut'和'.req'修改成了'.text-mode'。

```
(setq auto-mode-alist
  (append
    '(("\\.tut$" . text-mode)
      ("\\.req$" . text-mode))
    auto-mode-alist))

```

Settings can also be applied on a per-mode basis. A common method for this is to add a function to a *hook*. For example, to force indentation to use spaces instead of tabs, but only in text-mode:

```
(add-hook 'text-mode-hook (lambda () (setq indent-tabs-mode nil)))

```

Similarly, to only use spaces for indentation everywhere:

```
(setq-default indent-tabs-mode nil)

```

Keybindings can be adjusted in two ways. The first of which is 'define-key'. 'define-key' creates a keybinding for a command but only in one mode. The example below will make **F8** delete any whitespace from the end of each line of a 'text-mode' buffer:

```
(define-key text-mode-map (kbd "<f8>") 'delete-trailing-whitespace)

```

The other method is 'global-set-key'. This is used to bind a key to a command everywhere. To bind 'query-replace-regexp' (**C-M-%**) to '<f7>'.

```
(global-set-key (kbd "<f7>") 'query-replace-regexp)

```

Binding a command to an alternate key does not replace any existing bindings. Which is to say, 'query-replace-regexp' would be bound to both **F7** and **C-M-%** after the above example.

Almost anything within Emacs can be configured. Browsing through the [Emacs Wiki](http://emacswiki.org/) should give a solid place to start.

### 多种配置

你可以使用少量配置然后告诉Emacs来加载其他配置。

例如，我们来定义两个配置文件。

 `.emacs` 
```
(load "~/.emacs.d/main" nil t)
(load "~/.emacs.d/functions" nil t)
(load "~/.emacs.d/modes" nil t)
(load "~/.emacs.d/plugins" nil t)
(load "~/.emacs.d/theme" nil t)

```

这是我们在后台载入的完整配置。但是plugins文件太大导致载入太慢，如果我们要打开一个新的Emacs窗口，可能就不会使用plugins配置，每次加载它实在是太笨重了。

 `.emacs-light` 
```
(load "~/.emacs.d/main" nil t)
(load "~/.emacs.d/functions" nil t)
(load "~/.emacs.d/modes" nil t)
(load "~/.emacs.d/theme" nil t)

```

现在我们这样来加载Emacs：

```
emacs -q -l ~/.emacs-light

```

你可以为这个命令创建一个别名。

### 加载扩展程序

你能用require来加载扩展程序，例如这样：

```
(require 'mediawiki)

```

如果你试着在一个买有安装mediawiki的机器上使用相同的配置，Emacs会提示错误。并且，所有制定的扩展代码都会失效。

一个小的技巧是测试require的返回值。

```
(if (require 'mediawiki nil t)
    (progn
      (setq mediawiki-site-alist '(
             ("ArchLinux" "[https://wiki.archlinux.org/](https://wiki.archlinux.org/)" "UserName" "" "Main Page")
             )
           )
      (setq mediawiki-mode-hook
            (lambda ()
              (visual-line-mode 1)
              (turn-off-auto-fill)
              ))
 ))

```

### Local and custom variables

You can define variables in your configuration file that can be later one modified locally for a file.

```
(defcustom my-compiler "gcc" "Some documentation")

```

Now in any file you can define local variables in two ways:

*   On the very first line, write

```
// -*- my-compiler:g++; mode:c++ -*-

```

*   If you cannot (or do not want to) write this on the first line, you can put it at the end:

```
// Local Variables:
// my-compiler: g++
// mode: c++
// End:

```

Note that the beginning characters need to be comments for the current language, that's why here we used two backslashes for C++. For Elisp you would use

```
;; -*- mode:emacs-lisp -*-

```

There is two functions that may help you in defining the variables: *add-file-local-variable* and *add-file-local-variable-prop-line*.

Finally, custom variable are considered insecure by default. If you try to open a file that contains local variable redefining insecure custom variables, Emacs will ask you for confirmation.

If you know what you are doing, you can declare the variable as secure, thus removing the Emacs prompt for confirmation. You need to specify a predicate that any new value has to verify so that it can be considered safe.

```
(defcustom my-compiler "gcc" "Some documentation" :safe 'stringp)

```

In the previous example, if you attempt to set anything else than a string, Emacs will consider it insecure.

### Custom colors and theme

Colors can be easily customized using the *face* facility.

```
(set-face-background  'region                 "color-17")
(set-face-foreground  'region                 "white")
(set-face-bold-p      'font-lock-builtin-face t ) 

```

You can have let Emacs tell you the name of the face where the point is. Use the *customize-face* function for that. The facility will show you how to set colors, bold, underline, etc.

Emacs in console can handle 256 colors, but you will have to use an appropriate terminal for that. For instance URxvt has support for 256 colors. You can use the *list-colors-display* for a comprehensive list of supported colors. This is highly terminal-dependent.

### SyncTeX support

Emacs is definitely one of the most powerful LaTeX editor. This is mostly due to the fact you can adapt or create a LaTeX mode to fit your needs best.

Still, there might be some challenges, like SyncTeX support. First you need to make sure your TeX distribution has it. If you installed TeX Live manually, you may need to install the *synctex* package.

```
# umask 022 && tlmgr install synctex

```

SyncTeX support is viewer-dependent. Here we will use Zathura as an example, so the code needs to be adapted if you want to use another PDF viewer.

```
(defcustom tex-my-viewer "zathura --fork -s -x \"emacsclient --eval '(progn (switch-to-buffer  (file-name-nondirectory \"'\"'\"%{input}\"'\"'\")) (goto-line %{line}))'\"" 
  "PDF Viewer for TeX documents. You may want to fork the viewer
so that it detects when the same document is launched twice, and
persists when Emacs gets closed.

Simple command:

  zathura --fork

We can use

  emacsclient --eval '(progn (switch-to-buffer  (file-name-nondirectory \"%{input}\")) (goto-line %{line}))'

to reverse-search a pdf using SyncTeX. Note that the quotes and double-quotes matter and must be escaped appropriately."
:safe 'stringp)

```

Here we define our custom variable. If you are using AucTeX or Emacs default LaTeX-mode, you will have to set the viewer accordingly.

Now open a LaTeX source file with Emacs, compile the document, and launch the viewer. Zathura will spawn. If you press `Ctrl+Left click` Emacs should place the point at the corresponding position.

## Documentation

You may find yourself overwhelmed by the amount of Emacs features. You may find it difficult to know how to use Emacs Lisp to customize your favorite modes, or even to create your own modes / packages. Thankfully Emacs takes a strong point to auto-documenting everything: its internals, current configuration, bindings, etc. Almost everything is documented.

### Contextual help

Emacs is self-documenting by design. As such, a great deal of information is available to determine the name of a specific command or its keybinding, for example. The following is a listing of some of the most helpful of these:

```
**C-h a**        Find a command matching a description.

```

```
**C-h b**        List all active keybindings.

```

```
**C-h f**        Describe the given function.

```

```
**C-h k**        Find which command a key is bound to.

```

```
**C-h m**        Display information regarding the currently active modes.

```

```
**C-h t**        Start the Emacs tutorial.

```

```
**C-h v**        Describe the given variable.

```

```
**C-h w**        Find which key(s) a command is bound to.

```

### The manuals

If you really want to master Emacs, the most recommanded source of documentation remains the official manuals:

*   Emacs: the complete Emacs user manual.
*   Emacs FAQ.
*   Emacs Lisp Intro: if you never used any programming language before.
*   Elisp: if you are already familiar with a programming language.

You can access it as PDFs from [GNU.org](http://www.gnu.org/software/emacs/manual/) or directly from Emacs itself thanks to the embedded 'info' reader: **C-h i**. Press **m** to choose a book.

Some users prefer to read books using 'info' because of its convenient shortcuts, its paragraphs adapting to window width and the font adapted to current screen resolution. Some find it less irritating to the eyes. Finally you can easily copy content from the book to any Emacs buffer, and you can even execute Lisp code snippets directly from the examples.

You may want to read the **Info** book to know more about it: **C-h i m info <RET>**. Press **?** while in info mode for a quick list of shortcuts.

## 拓展模块

虽然Emacs包含了成百上千种模式(mode)，库和其它扩展，还有更多的扩展来增强Emacs。大多数扩展会详细说明安装它的时候要对~/.emacs作什么改动。这些说明一般会在一个elisp源文件开头的注释中，或者在一个README中（如果这个扩展包含了多个源文件）。

在'community'仓库中有很多流行的扩展，更多的扩展还放在了[AUR](/index.php/AUR "AUR")。这些软件包的名字有一个'emacs-'前缀（比如emacs-lua-mode）。在很多情况下，在安装的过程会显示怎样修改~/.emacs以安装该扩展到Emacs中。

想知道怎样激活一个不在上面提到的地方的扩展，查看[Emacs Wiki](http://emacswiki.org/)中的相应页面，一般会提供一个配置的例子。Emacs Wiki也是一个寻找扩展的优秀资源。

你也可以使用[Emacs Lisp Package Archive (ELPA)](http://tromey.com/elpa/) 来自动安装软件包。打开那个网站看说明。ELPA已经包括在了Emacs24中;它已经作为Emacs生态系统中的一部分了。

## 疑难杂症

### 彩色输出的问题

Emacs默认使用原生的转义串来输出颜色。也就是说，它会在要显示颜色的地方显示奇怪的字符。

在`~/.emacs`中加入下面的代码解决这个问题：

```
(add-hook 'shell-mode-hook 'ansi-color-for-comint-mode-on)

```

### 菜单显示为空

一些菜单显示为空，这是GNU Emacs 23.1的一个bug（使用GTK toolkit的时候）。好像在Emacs的CVS trunk中已经修复了。对应的[Debian bug report](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=550541) 有一个应对措施。

### X 窗口下的字符显示问题

当你使用X窗口启动emacs时，如果发现主窗口中的所有字符都是黑框白块（就像你没有安装正确的字体看到的字符一样），那么你需要安装 [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi) 或者 [xorg-fonts-100dpi](https://www.archlinux.org/packages/?name=xorg-fonts-100dpi) 并且重启X窗口。

### 启动速度慢

启动速度慢经常是由下面两种情况引起的。

要确定是哪种情况，这样打开Emacs：

```
$ emacs -q

```

如果Emacs还是启动很慢，则是[错误的网络配置](/index.php/Emacs#Incorrect_network_configuration "Emacs")。如果不是，则可以确定是[.emacs的问题](/index.php/Emacs#Init_file_loads_slowly "Emacs")。

#### 错误的网络配置

当启动Emacs的时候，一些错误，特别是在/etc/hosts中的，经常会导致5秒以上的延迟。在网络配置指南中查看'[set the hostname](/index.php/Configuring_network#Set_the_hostname "Configuring network")' 了解更多内容。

#### 初始化文件加载慢

一个很简单的方法查找原因是注释掉（比如在行开头使用';'）你的~/.emacs（或者~/.emacs.d/init.el）里面可疑的地方，然后再启动Emacs，看速度是否有改善。记住，使用"require"和"load"会减慢启动速度，特别是用在很大的插件上。一般来说，他们应该用在当目标是Emacs启动的时候就需要或者提供仅仅是一个扩展的"autoloads"。否则，直接使用'autoload'函数。比如，不是这样：

```
(require 'anything)

```

你应该这样:

```
(autoload 'anything "anything" "Select anything" t)

```

### 不能打开配置文件: ...

这个错误最常见的原因是'load-path'变量没有包含某些插件的目录。要解决这个问题，在加载插件前，把需要加载的插件目录加入到要搜索的list中：

```
 (add-to-list 'load-path "/path/to/directory/")

```

当尝试使用一个插件的包，而这个包又被Emacs加上了非'/usr'的前缀时，load-path需要更新。把下面的代码放到使用这个插件的包的代码的前面：

```
 (add-to-list 'load-path "/usr/share/emacs/site-lisp")

```

如果手动编译Emacs，记住默认的前缀是'/usr/local'。

### Dead-accent keys problem: '<dead-acute> is undefined'

Searching about this bug on Google, we find this link: [http://lists.gnu.org/archive/html/help-gnu-emacs/2009-05/msg00167.html](http://lists.gnu.org/archive/html/help-gnu-emacs/2009-05/msg00167.html)

Explaining the problem: in recent versions of b72

```
Emacs, the normal way to use accent keys doesn't work as expected. Trying to accent a word like 'fiancé' will produce the message above.

```

A way to solve it is just put the line above on your startup file, `~/.emacs`:

```
  (require 'iso-transl)

```

And no, it isn't a bug, but a feature of new Emacs versions. Reading the subsequent messages about it on the mail list, we found it ([http://lists.gnu.org/archive/html/help-gnu-emacs/2009-05/msg00179.html](http://lists.gnu.org/archive/html/help-gnu-emacs/2009-05/msg00179.html)):

	*It seems that nothing is loaded automatically because there is a choice betwee iso-transl and iso-acc. Both seem to provide an input method with C-x 8 or Alt-<accent> prefix, but what you and I are doing is just pressing a dead key (^, ´, `, ~, ¨) for the accent and then another key to "compose" the accented character. And there is no Alt key used in this! And according to documentation it seems be appropriate for 8-bit encodings, so it should be pretty useless in UTF-8\. I reported this bug when it was introduced, but the bug seems to be*

a3b

```
classified as a feature ... Maybe it's just because the file is auto-loaded though pretty useless. 

```

### C-M-% and some other bindings do not work in emacs nox

This is because terminals are more limited than Xorg. Some terminals may handle more bindings than other, though. Two solutions:

*   either use the graphical version,
*   or change the binding to a supported one.

Example:

 `.emacs` 
```
(global-set-key (kbd "C-M-y") 'query-replace-regexp)

```

### Emacs client gets stuck when switching back to it

If you are using Emacs daemon, then you should know that input is blocking. If one Emacs instance is in the minibuffer (after an **M-x** for instance), then all other instance will wait for it to finish. Press **C-g** to cancel any input to make sure this Emacs session is not blocking.

### Emacs-nox output gets messy

When working in a terminal, the color, indentation, or anything related to the output might become crazy. This is (probably?) because Emacs was sent a special character at some point which may conflict with the current terminal. There is not much to be done but restarting emacs. If someone has a workaround or a more detailed explanation on the issue, feel free to contribute.

Graphical Emacs does not suffer from this issue.

### Shift + Arrow keys not working in emacs within tmux

First you must enable xterm-keys in your [tmux](/index.php/Tmux "Tmux") config.

 `.tmux.conf` 
```
setw -g xterm-keys on

```

But, this will break other key combinations. To fix them, put the following in your emacs config.

 `.emacs` 
```
;; handle tmux's xterm-keys
;; put the following line in your ~/.tmux.conf:
;;   setw -g xterm-keys on
(if (getenv "TMUX")
    (progn
      (let ((x 2) (tkey ""))
	(while (<= x 8)
	  ;; shift
	  (if (= x 2)
	      (setq tkey "S-"))
	  ;; alt
	  (if (= x 3)
	      (setq tkey "M-"))
	  ;; alt + shift
	  (if (= x 4)
	      (setq tkey "M-S-"))
	  ;; ctrl
	  (if (= x 5)
	      (setq tkey "C-"))
	  ;; ctrl + shift
	  (if (= x 6)
	      (setq tkey "C-S-"))
	  ;; ctrl + alt
	  (if (= x 7)
	      (setq tkey "C-M-"))
	  ;; ctrl + alt + shift
	  (if (= x 8)
	      (setq tkey "C-M-S-"))

	  ;; arrows
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d A" x)) (kbd (format "%s<up>" tkey)))
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d B" x)) (kbd (format "%s<down>" tkey)))
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d C" x)) (kbd (format "%s<right>" tkey)))
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d D" x)) (kbd (format "%s<left>" tkey)))
	  ;; home
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d H" x)) (kbd (format "%s<home>" tkey)))
	  ;; end
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d F" x)) (kbd (format "%s<end>" tkey)))
	  ;; page up
	  (define-key key-translation-map (kbd (format "M-[ 5 ; %d ~" x)) (kbd (format "%s<prior>" tkey)))
	  ;; page down
	  (define-key key-translation-map (kbd (format "M-[ 6 ; %d ~" x)) (kbd (format "%s<next>" tkey)))
	  ;; insert
	  (define-key key-translation-map (kbd (format "M-[ 2 ; %d ~" x)) (kbd (format "%s<delete>" tkey)))
	  ;; delete
	  (define-key key-translation-map (kbd (format "M-[ 3 ; %d ~" x)) (kbd (format "%s<delete>" tkey)))
	  ;; f1
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d P" x)) (kbd (format "%s<f1>" tkey)))
	  ;; f2
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d Q" x)) (kbd (format "%s<f2>" tkey)))
	  ;; f3
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d R" x)) (kbd (format "%s<f3>" tkey)))
	  ;; f4
	  (define-key key-translation-map (kbd (format "M-[ 1 ; %d S" x)) (kbd (format "%s<f4>" tkey)))
	  ;; f5
	  (define-key key-translation-map (kbd (format "M-[ 15 ; %d ~" x)) (kbd (format "%s<f5>" tkey)))
	  ;; f6
	  (define-key key-translation-map (kbd (format "M-[ 17 ; %d ~" x)) (kbd (format "%s<f6>" tkey)))
	  ;; f7
	  (define-key key-translation-map (kbd (format "M-[ 18 ; %d ~" x)) (kbd (format "%s<f7>" tkey)))
	  ;; f8
	  (define-key key-translation-map (kbd (format "M-[ 19 ; %d ~" x)) (kbd (format "%s<f8>" tkey)))
	  ;; f9
	  (define-key key-translation-map (kbd (format "M-[ 20 ; %d ~" x)) (kbd (format "%s<f9>" tkey)))
	  ;; f10
	  (define-key key-translation-map (kbd (format "M-[ 21 ; %d ~" x)) (kbd (format "%s<f10>" tkey)))
	  ;; f11
	  (define-key key-translation-map (kbd (format "M-[ 23 ; %d ~" x)) (kbd (format "%s<f11>" tkey)))
	  ;; f12
	  (define-key key-translation-map (kbd (format "M-[ 24 ; %d ~" x)) (kbd (format "%s<f12>" tkey)))
	  ;; f13
	  (define-key key-translation-map (kbd (format "M-[ 25 ; %d ~" x)) (kbd (format "%s<f13>" tkey)))
	  ;; f14
	  (define-key key-translation-map (kbd (format "M-[ 26 ; %d ~" x)) (kbd (format "%s<f14>" tkey)))
	  ;; f15
	  (define-key key-translation-map (kbd (format "M-[ 28 ; %d ~" x)) (kbd (format "%s<f15>" tkey)))
	  ;; f16
	  (define-key key-translation-map (kbd (format "M-[ 29 ; %d ~" x)) (kbd (format "%s<f16>" tkey)))
	  ;; f17
	  (define-key key-translation-map (kbd (format "M-[ 31 ; %d ~" x)) (kbd (format "%s<f17>" tkey)))
	  ;; f18
	  (define-key key-translation-map (kbd (format "M-[ 32 ; %d ~" x)) (kbd (format "%s<f18>" tkey)))
	  ;; f19
	  (define-key key-translation-map (kbd (format "M-[ 33 ; %d ~" x)) (kbd (format "%s<f19>" tkey)))
	  ;; f20
	  (define-key key-translation-map (kbd (format "M-[ 34 ; %d ~" x)) (kbd (format "%s<f20>" tkey)))

	  (setq x (+ x 1))
	  ))
      )
  )

```

## 替代方案

有很多Emacs的实现。GNU/Emacs 可能是最受欢迎的了。
更轻量的兼容性较好的Emacs可以在Arch仓库或在[AUR](https://aur.archlinux.org/)中找到。

### mg

**mg**（原来叫MicroGnuEmacs)，是用C语言实现的轻量级Emacs。

[mg](https://www.archlinux.org/packages/?name=mg) 在 [official repositories](/index.php/Official_repositories "Official repositories") 中，也可以从上游下载源码[page](http://homepage.boetes.org/software/mg/)。注意，**mg** 没有UTF-8支持。

### zile

引用官方网站[page](https://www.gnu.org/software/zile/)的描述，"GNU Zile is a lightweight Emacs clone. Zile is short for Zile Is Lossy Emacs. Zile has been written to be as similar as possible to Emacs; every Emacs user should feel at home."，意思是'GNU Zile'是一个轻量级的Emacs的克隆。Zile是'Zile Is Lossy Emacs'的缩写。 Zile的实现与Emacs如此相似以至于每个Emacs用户使用Zile一定会有一种宾至如归的感觉。

[zile](https://www.archlinux.org/packages/?name=zile) 可以在官方仓库中找到。

最新的tarball可以在GNU的官方源[mirrors](http://ftp.sh.cvut.cz/MIRRORS/gnu/pub/gnu/zile/)中找到。

### uemacs

**uemacs** 是由Linus Torvalds定制的微型Emacs版本。在 [AUR](/index.php/AUR "AUR") 中名为[uemacs-git](https://aur.archlinux.org/packages/uemacs-git/)。

### remacs

**remacs** 是一个用Rust写成的社区驱动的Emacs移植版。在 [AUR](/index.php/AUR "AUR") 中名为 [remacs-git](https://aur.archlinux.org/packages/remacs-git/)。

## 资源

*   [GNU Emacs home page](http://www.gnu.org/software/emacs/)
*   [GNU Emacs Manual](http://www.gnu.org/software/emacs/manual/emacs.html)
*   [Emacs Wiki](http://www.emacswiki.org/cgi-bin/wiki/)
*   [WikEmacs - a more readable, but less complete Emacs Wiki](http://wikemacs.org)
*   [Useful introduction to Emacs and its shortcuts](http://www2.lib.uchicago.edu/keith/tcl-course/emacs-tutorial.html)
*   [The Church of Emacs](http://www.dina.kvl.dk/~abraham/religion/)
*   [Official reference card](http://repo.or.cz/w/emacs.git/blob/HEAD:/etc/refcards/refcard.pdf)