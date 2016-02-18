**翻译状态：** 本文是英文页面 [Python](/index.php/Python "Python") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-08-02，点击[这里](https://wiki.archlinux.org/index.php?title=Python&diff=0&oldid=326459)可以查看翻译后英文页面的改动。

根据[Wikipedia 页面](https://zh.wikipedia.org/wiki/Python): Python 是一种面向对象、直译式电脑编程语言，具有近二十年的发展历史，成熟且稳定。它包含了一组完善而且容易理解的标准库，能够轻松完成很多常见的任务。它的语法简捷和清晰，尽量使用无异义的英语单词，与其它大多数程序设计语言使用大括号不一样，它使用缩进来定义语句块。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 Python 3](#Python_3)
    *   [1.2 Python 2](#Python_2)
*   [2 正确设置编译脚本中的 Python 版本](#.E6.AD.A3.E7.A1.AE.E8.AE.BE.E7.BD.AE.E7.BC.96.E8.AF.91.E8.84.9A.E6.9C.AC.E4.B8.AD.E7.9A.84_Python_.E7.89.88.E6.9C.AC)
*   [3 在 Python Shell 中实现自动补全功能](#.E5.9C.A8_Python_Shell_.E4.B8.AD.E5.AE.9E.E7.8E.B0.E8.87.AA.E5.8A.A8.E8.A1.A5.E5.85.A8.E5.8A.9F.E8.83.BD)
*   [4 部件绑定](#.E9.83.A8.E4.BB.B6.E7.BB.91.E5.AE.9A)
*   [5 旧版本](#.E6.97.A7.E7.89.88.E6.9C.AC)
*   [6 更多资源](#.E6.9B.B4.E5.A4.9A.E8.B5.84.E6.BA.90)

## 安装

目前有2个版本的Python, Python 3 是默认的，Python 2 是较老版本。 从 [官方软件仓库](/index.php/Official_repositories "Official repositories") 中 [安装](/index.php/Pacman "Pacman") 软件包 [python3](https://www.archlinux.org/packages/?name=python3) 或者 [python2](https://www.archlinux.org/packages/?name=python2)。

[IPython](http://ipython.org/) 是改善了的 Python 命令行工具，可以从官方软件仓库安装 [ipython](https://www.archlinux.org/packages/?name=ipython) 和 [ipython2](https://www.archlinux.org/packages/?name=ipython2)。

### Python 3

Python 3 是语言的最新版本，而且**不兼容 Python 2**。语言. 语法基本上差不多，但是很多细节，尤其是一些内置对象，像字典和字符串，它们的工作方式已经改变了，一些不推荐使用的特性最终被移除了。同样，标准库也进行了整理。所有差别的列表，请访问 [Python2orPython3](http://wiki.python.org/moin/Python2orPython3) 和 Dive into Python 3 的相关 [章节](http://getpython3.com/diveintopython3/porting-code-to-python-3-with-2to3.html)。

要获得 Python 3，请从[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")中[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 软件包 [python](https://www.archlinux.org/packages/?name=python) 。

要从源代码编译测试版，请访问 [Python 下载](http://www.python.org/download/)。[AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 中同样包含 [PKGBUILDS](/index.php/PKGBUILD_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PKGBUILD (简体中文)") 。如果要安装 RC 版，请注意二进制文件默认安装到 `/usr/local/bin/python3.x`.

### Python 2

要获得 Python 2，请从[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")中[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 软件包 [python2](https://www.archlinux.org/packages/?name=python2) 。

Python 2 可以和 Python 3 同时运行，需要指定成`python2`才会运行此版本。

默认的`/usr/bin/python`是链接到 python 3 的，所以所有要求使用 python 2 的软件包应该用 `/usr/bin/python2` 替换 `/usr/bin/python`.

用文本编辑器打开程序或脚本，将第一行：

```
#!/usr/bin/env python

```

或

```
#!/usr/bin/python

```

中的 `python` 替换为 `python2`。

另一种强制使用 python2 而不修改脚本的方法是明确地使用 python2 调用它，即

 `python2 myScript.py` 

最后，你可能无法控制脚本调用哪一个，但还有一种方法。它仅在脚本使用 `#!/usr/bin/env python` 时有效，在用 `#!/usr/bin/python` 时无效。这种手法依赖于 `env` 在 PATH 变量中搜索第一个对应的条目。 首先创建一个目录。

```
$ mkdir ~/bin

```

然后添加一个名为 'python' 的链接指向 python2 以及一个名为 'python-config' 的链接指向 python2-config 。

```
$ ln -s /usr/bin/python2 ~/bin/python
$ ln -s /usr/bin/python2-config ~/bin/python-config

```

最后把新的目录添加到你的 PATH 变量的 *最前面*。

```
$ export PATH=~/bin:$PATH

```

注意到这个修改不是永久的，仅在当前终端会话中有效。 要检查 `env` 使用的是哪个 python 解释器，使用以下命令：

```
$ which python

```

另一个解决这个问题的方法是通过 [Virtualenv](/index.php/Virtualenv "Virtualenv") 来伪造一个脚本的运行环境。这要求脚本通过 `#!/usr/bin/env python` 来执行。当激活了 Virtualenv 之后，Python执行程序会被PATH变量指向到 Virtualenv 中。因此如果 Virtualenv 是用 Python 2创建的，那么`python`就会指向到 Python 2 。首先我们需要[安装](/index.php/Pacman "Pacman")[python2-virtualenv](https://www.archlinux.org/packages/?name=python2-virtualenv)：

然后创建 Virtualenv 环境：

```
$ virtualenv2 venv # 创建一个名为 venv 的目录，其中包含了 Virtualenv

```

激活这个Virtualenv，使`python`指向 Python 2 ：

```
$ source venv/bin/activate

```

**注意:** 这个激活只对当前终端会话有效。

之后的脚本就会用 Python 2 来启动。

## 正确设置编译脚本中的 Python 版本

许多项目的编译脚本认为 `python` 是 Python 2，如果这样编译会导致错误 - 例如 `print 'foo'` 是错误语法。幸运的是，很多编译脚本会使用 `$PATH` 中的`python` 而不是写死 `#!/usr/bin/python`，而且 Python 脚本都位于项目树中。所以，可以不修改脚本就解决此问题，只需创建`/usr/local/bin/python`：

 `/usr/local/bin/python` 
```
#!/bin/bash
script=$(readlink -f -- "$1")
case "$script" in (/path/to/project1/*|/path/to/project2/*|/path/to/project3*)
    exec python2 "$@"
    ;;
esac

exec python3 "$@"

```

其中 `/path/to/project1/*|/path/to/project2/*|/path/to/project3*` 是用`|` 分隔的项目匹配列表。

给脚本执行权限：

```
# chmod +x /usr/local/bin/python

```

完成后，指定的项目就会以 Python 2 运行脚本了。

## 在 Python Shell 中实现自动补全功能

把下面的内容复制到 Python Shell 中

 `/usr/bin/python` 
```
import rlcompleter
import readline
readline.parse_and_bind("tab: complete")

```

[Source](http://algorithmicallyrandom.blogspot.com.es/2009/09/tab-completion-in-python-shell-how-to.html)

## 部件绑定

有如下[部件工具](https://en.wikipedia.org/wiki/widget_toolkit "wikipedia:widget toolkit")的绑定:

*   **TkInter** — Tk 绑定

	[http://wiki.python.org/moin/TkInter](http://wiki.python.org/moin/TkInter) || 标准模块

*   **pyQt** — [Qt](/index.php/Qt "Qt") 绑定

	[http://www.riverbankcomputing.co.uk/software/pyqt/intro](http://www.riverbankcomputing.co.uk/software/pyqt/intro) || [python2-pyqt4](https://www.archlinux.org/packages/?name=python2-pyqt4) [python2-pyqt5](https://www.archlinux.org/packages/?name=python2-pyqt5) [python-pyqt4](https://www.archlinux.org/packages/?name=python-pyqt4) [python-pyqt5](https://www.archlinux.org/packages/?name=python-pyqt5)

*   **pySide** — [Qt](/index.php/Qt "Qt") bindings

	[http://www.pyside.org/](http://www.pyside.org/) || [python2-pyside](https://www.archlinux.org/packages/?name=python2-pyside)

*   **pyGTK** — [GTK+](/index.php/GTK%2B "GTK+") 绑定

	[http://www.pygtk.org/](http://www.pygtk.org/) || [pygtk](https://www.archlinux.org/packages/?name=pygtk)

*   **PyGObject** — [GTK+ 2/3](/index.php/GTK%2B "GTK+") 绑定通过 GObject Introspection

	[https://wiki.gnome.org/PyGObject/](https://wiki.gnome.org/PyGObject/) || [python2-gobject2](https://www.archlinux.org/packages/?name=python2-gobject2) [python2-gobject](https://www.archlinux.org/packages/?name=python2-gobject) [python-gobject2](https://www.archlinux.org/packages/?name=python-gobject2) [python-gobject](https://www.archlinux.org/packages/?name=python-gobject)

*   **wxPython** — [wxWidgets](/index.php?title=WxWidgets&action=edit&redlink=1 "WxWidgets (page does not exist)") 绑定

	[http://wxpython.org/](http://wxpython.org/) || [wxpython](https://www.archlinux.org/packages/?name=wxpython)

要和 Python 一同使用，需要先安装相应的组件。

## 旧版本

[AUR](/index.php/Arch_User_Repository "Arch User Repository")中有之前发布的 Python 版本，运行旧程序或测试程序的版本兼容性时可以使用：

*   [python15](https://aur.archlinux.org/packages/python15/): Python 1.5.2
*   [python16](https://aur.archlinux.org/packages/python16/): Python 1.6.1
*   [python24](https://aur.archlinux.org/packages/python24/): Python 2.4.6
*   [python25](https://aur.archlinux.org/packages/python25/): Python 2.5.6
*   [python26](https://aur.archlinux.org/packages/python26/): Python 2.6.8
*   [python30](https://aur.archlinux.org/packages/python30/): Python 3.0.1
*   [python31](https://aur.archlinux.org/packages/python31/): Python 3.1.5
*   [python32](https://aur.archlinux.org/packages/python32/): Python 3.2.5
*   [python33](https://aur.archlinux.org/packages/python33/): Python 3.3.5

2014年7月，Python 上游仅支持 Python 2.7, 3.2, 3.3, 和 3.4 的安全修复，老版本有安全隐患，不建议使用。AUR 中还有老版本使用的模块和库，可以通过带版本的 python 搜索。例如 "python26" 关键字可以搜索支持 2.6 的模块。

## 更多资源

*   [Learning Python](http://shop.oreilly.com/product/9780596158071.do) is one of the most comprehensive, up to date, and well-written books on Python available today.
*   [Dive Into Python](http://www.diveintopython.net/) 是极好的（免费）资源，但是可能更适合高级读者，且[已经升级为 Python 3](http://diveintopython3.ep.io/)。
*   [A Byte of Python](http://www.swaroopch.com/notes/Python) 适合新接触Python（以及编写脚本）的读者阅读。
*   [Learn Python The Hard Way](http://learnpythonthehardway.org) 最好的编程入门书。
*   [facts.learnpython.org](http://facts.learnpython.org) 学习 python 的好网站。
*   [Crash into Python](http://stephensugden.com/crash_into_python/) 也被称为**3小时认识 Python**，向其它编程语言的程序员介绍 Python。
*   [Beginning Game Development with Python and Pygame: From Novice to Professional](http://www.apress.com/book/view/9781590598726) 是游戏方面的书籍。