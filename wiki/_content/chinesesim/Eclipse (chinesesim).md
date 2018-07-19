**翻译状态：** 本文是英文页面 [Eclipse](/index.php/Eclipse "Eclipse") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-07-18，点击[这里](https://wiki.archlinux.org/index.php?title=Eclipse&diff=0&oldid=527415)可以查看翻译后英文页面的改动。

[Eclipse](https://eclipse.org) 是一个开源的社区项目，它致力于提供一个通用的开发平台。Eclipse 项目最广为人知的是它的跨平台集成开发环境(IDE). Arch Linux 软件包 (以及本文) 只针对于此 IDE。

Eclipse IDE 主要是用 Java 写成，但是可以用来用数种语言开发应用程序，包括 Java, C/C++, PHP 和 Perl. 此 IDE 也可以提供 subversion 支持(见下文) 以及任务管理。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 插件](#.E6.8F.92.E4.BB.B6)
    *   [2.1 添加默认更新站点](#.E6.B7.BB.E5.8A.A0.E9.BB.98.E8.AE.A4.E6.9B.B4.E6.96.B0.E7.AB.99.E7.82.B9)
    *   [2.2 Eclipse Marketplace](#Eclipse_Marketplace)
    *   [2.3 插件管理器](#.E6.8F.92.E4.BB.B6.E7.AE.A1.E7.90.86.E5.99.A8)
        *   [2.3.1 通过插件管理器升级](#.E9.80.9A.E8.BF.87.E6.8F.92.E4.BB.B6.E7.AE.A1.E7.90.86.E5.99.A8.E5.8D.87.E7.BA.A7)
    *   [2.4 插件列表](#.E6.8F.92.E4.BB.B6.E5.88.97.E8.A1.A8)
*   [3 启用 javadoc 集成](#.E5.90.AF.E7.94.A8_javadoc_.E9.9B.86.E6.88.90)
    *   [3.1 在线版本](#.E5.9C.A8.E7.BA.BF.E7.89.88.E6.9C.AC)
    *   [3.2 离线版本](#.E7.A6.BB.E7.BA.BF.E7.89.88.E6.9C.AC)
*   [4 疑难问题](#.E7.96.91.E9.9A.BE.E9.97.AE.E9.A2.98)
    *   [4.1 Ctrl+X 关闭了 Eclipse](#Ctrl.2BX_.E5.85.B3.E9.97.AD.E4.BA.86_Eclipse)
    *   [4.2 暗色主题](#.E6.9A.97.E8.89.B2.E4.B8.BB.E9.A2.98)
    *   [4.3 使用 Gnome 3.6 Adwaita 主题时"提示"显示为深色背景色](#.E4.BD.BF.E7.94.A8_Gnome_3.6_Adwaita_.E4.B8.BB.E9.A2.98.E6.97.B6.22.E6.8F.90.E7.A4.BA.22.E6.98.BE.E7.A4.BA.E4.B8.BA.E6.B7.B1.E8.89.B2.E8.83.8C.E6.99.AF.E8.89.B2)
    *   [4.4 切换按钮的选择/未选择状态是一样的](#.E5.88.87.E6.8D.A2.E6.8C.89.E9.92.AE.E7.9A.84.E9.80.89.E6.8B.A9.2F.E6.9C.AA.E9.80.89.E6.8B.A9.E7.8A.B6.E6.80.81.E6.98.AF.E4.B8.80.E6.A0.B7.E7.9A.84)
    *   [4.5 改变默认窗口标题字号](#.E6.94.B9.E5.8F.98.E9.BB.98.E8.AE.A4.E7.AA.97.E5.8F.A3.E6.A0.87.E9.A2.98.E5.AD.97.E5.8F.B7)
*   [5 参阅](#.E5.8F.82.E9.98.85)

## 安装

从下面列表中选择一个进行[安装](/index.php/Install "Install"):

*   [eclipse-jee](https://www.archlinux.org/packages/?name=eclipse-jee) - Java EE 开发
*   [eclipse-java](https://www.archlinux.org/packages/?name=eclipse-java) - Java 开发
*   [eclipse-cpp](https://www.archlinux.org/packages/?name=eclipse-cpp) - C/C++ 开发
*   [eclipse-php](https://www.archlinux.org/packages/?name=eclipse-php) - PHP 开发
*   [eclipse-javascript](https://www.archlinux.org/packages/?name=eclipse-javascript) - JavaScript 和网页开发

目前不支持同时安装多个版本 [FS#45577](https://bugs.archlinux.org/task/45577): 请选择最接近您需求的软件包，其它功能可以通过[插件](#Plugins)进行安装。

## 插件

大部分插件只需 **pacman** 就可安装 (更多信息见 [Eclipse 插件包参考](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines")). 这样同时能保证它们是最新的。另外，你也可以使用 [#Eclipse Marketplace](#Eclipse_Marketplace) 或内建的[#插件管理器](#.E6.8F.92.E4.BB.B6.E7.AE.A1.E7.90.86.E5.99.A8)。

### 添加默认更新站点

确保您已配置好针对当前版本的 Eclipse 的更新站点，这样它就能自动安装插件依赖。Eclipse 最新版本是 Luna ，它的更新站点是: [http://download.eclipse.org/releases/luna](http://download.eclipse.org/releases/luna). 转到 帮助 > 安装新软件 > 添加，填写名称后可以轻松地找到更新站点 - 比如，Luna 软件源 - 并填上网址。

### Eclipse Marketplace

**注意:** 确保您遵循了[#添加默认更新站点](#.E6.B7.BB.E5.8A.A0.E9.BB.98.E8.AE.A4.E6.9B.B4.E6.96.B0.E7.AB.99.E7.82.B9)部分。

要使用 Eclipse Marketplace, 首先要安装: 转到 帮助 > 安装新软件 > 切换到默认更新站点 > 通用工具 > Marketplace 客户端。重启 Eclipse, 之后在 帮助 > Eclipse Marketplace 可以找到。

### 插件管理器

**注意:** 确保您遵循了[#添加默认更新站点](#.E6.B7.BB.E5.8A.A0.E9.BB.98.E8.AE.A4.E6.9B.B4.E6.96.B0.E7.AB.99.E7.82.B9)部分。

使用 Eclipse 的插件管理器以从官方源下载并安装插件: 这种情况下你需要在插件网站上找到需要的源，然后转到 *帮助 > 安装新软件...*, 在 *Work with* 栏目里输入源地址，从下面的列表里选择要安装的插件并遵循教程。

**注意:**

*   如果你使用 Eclipse 的插件管理器，建议您以 root 身份运行 Eclipse: 这种方法插件会安装到 `/usr/lib/eclipse/plugins/`; 如果你以普通用户安装，它们会被存储在 `~/.eclipse/` 下的一个和版本号相关的文件夹里，并且升级 Eclipse 之后插件再也无法被识别。
*   日常工作时不要以 root 身份运行 Eclipse.

#### 通过插件管理器升级

运行 Eclipse 并执行 *帮助 > 检查更新*。如果你如上以 root 身份安装，那么需要以 root 身份来升级。

对于准备更新的插件，你应该确保已经启用它们的更新源 *窗口 > 首选项 > 安装/升级 > 可用软件站点*: 你可在各自的网站上找到插件的更新源。要添加/编辑/移除... 源只需使用*可用软件站点*面板右部的按钮。对于 Eclipse 4.5 (Mars), 检查你是否启用了:

```
[http://download.eclipse.org/releases/mars](http://download.eclipse.org/releases/mars)

```

要接受更新提示转到 *窗口 > 首选项 > 安装/升级 > 自动更新*. 如果你想接受以 root 身份安装插件的更新提示，你需要以 root 身份运行 Eclipse. 转到 *窗口 > 首选项 > 安装/升级 > 可用软件站点*, 选择插件相关的源并*导出*它们，然后以普通用户运行 Eclipse 并在同样的面板里*导入*它们。

### 插件列表

*   **AVR** — AVR 微控制器插件。

	[http://avr-eclipse.sourceforge.net/wiki/index.php/The_AVR_Eclipse_Plugin](http://avr-eclipse.sourceforge.net/wiki/index.php/The_AVR_Eclipse_Plugin) || [eclipse-avr](https://aur.archlinux.org/packages/eclipse-avr/)

*   **Aptana** — HTML5/CSS3/JavaScript/Ruby/Rails/PHP/Pydev/Django support. Also available as standalone application.

	[http://www.aptana.com/](http://www.aptana.com/) || [aptana-studio](https://aur.archlinux.org/packages/aptana-studio/)

*   **IvyDE** — IvyDE 依赖管理器

	[https://ant.apache.org/ivy/ivyde/](https://ant.apache.org/ivy/ivyde/) || [eclipse-ivyde](https://aur.archlinux.org/packages/eclipse-ivyde/)

*   **Markdown** — Eclipse 的 Markdown 编辑插件。

	[http://www.winterwell.com/software/markdown-editor.php](http://www.winterwell.com/software/markdown-editor.php) || [eclipse-markdown](https://aur.archlinux.org/packages/eclipse-markdown/)

*   **PyDev** — [Python](/index.php/Python "Python") 支持。

	[http://pydev.org/](http://pydev.org/) || [eclipse-pydev](https://aur.archlinux.org/packages/eclipse-pydev/)

*   **Subclipse** — [Subversion](/index.php/Subversion "Subversion") 支持。

	[https://github.com/subclipse/subclipse](https://github.com/subclipse/subclipse) || [eclipse-subclipse](https://aur.archlinux.org/packages/eclipse-subclipse/)

*   **Subversive** — 另一 Subversion 支持。

	[http://www.eclipse.org/subversive/](http://www.eclipse.org/subversive/) || [eclipse-subversive](https://aur.archlinux.org/packages/eclipse-subversive/)

*   **TestNG** — TestNG 支持。

	[http://testng.org/doc/eclipse.html](http://testng.org/doc/eclipse.html) || [eclipse-testng](https://aur.archlinux.org/packages/eclipse-testng/)

*   **TeXlipse** — [LaTeX](/index.php/LaTeX "LaTeX") 支持。

	[http://texlipse.sourceforge.net/](http://texlipse.sourceforge.net/) || [texlipse](https://aur.archlinux.org/packages/texlipse/)

*   **Checkstyle** — Eclipse Checkstyle support.

	[http://eclipse-cs.sourceforge.net/](http://eclipse-cs.sourceforge.net/) || [eclipse-checkstyle](https://aur.archlinux.org/packages/eclipse-checkstyle/)

## 启用 javadoc 集成

将鼠标指针放在标准 Java 方法的时候想看API条目？

### 在线版本

如果你的机器有不间断的互联网连接，您可以使用在线文档:

1.  转到 *窗口 > 首选项*, 然后转到 *Java > 已安装的 JRE*.
2.  应该会有一个类型为 "Standard VM" 的 "java". 选择它并点击 *Edit*.
3.  选择 "JRE system libraries:" 下的 `/opt/java/jre/lib/rt.jar` 条目然后点击 *Javadoc Location...*.
4.  在 "Javadoc location path:" 文本栏里键入 "[http://docs.oracle.com/javase/7/docs/api/](http://docs.oracle.com/javase/7/docs/api/)".

### 离线版本

你可安装 [openjdk8-doc](https://www.archlinux.org/packages/?name=openjdk8-doc) 软件包把文档存储到本地。Eclipse 能够自动找到 javadocs. 如果不起效，针对 rt.jar 把 Javadoc 设置到 `file:/usr/share/doc/java8-openjdk/api`.

## 疑难问题

### Ctrl+X 关闭了 Eclipse

是[这个](https://bugs.eclipse.org/bugs/show_bug.cgi?id=318177) bug 的一部分。只要看看 `~/workspace/.metadata/.plugins/org.eclipse.e4.workbench/workbench.xmi` 并删除错误的 `Ctrl+X` 组合。通常它是第一个。

### 暗色主题

Luna 提供了暗色主题，可在 首选项 > 外观 再选择 'Dark' 主题启用。

暗色主题使用它自己的颜色而不是 GTK 主题的，如果你想完全使用 GTK 颜色设定的话，从此处删除或移动所有 .css 文件到备份子文件夹: /usr/share/eclipse/plugins/org.eclipse.ui.themes_1.0.0.xxxx/css/

### 使用 Gnome 3.6 Adwaita 主题时"提示"显示为深色背景色

如下取消 `/usr/share/themes/Adwaita/gtk-2.0/gtkrc` 倒数第二行的注释

```
#widget "gtk-tooltip*"  style "tooltips"

```

相关 bug:

*   [https://bugzilla.gnome.org/show_bug.cgi?id=688285](https://bugzilla.gnome.org/show_bug.cgi?id=688285)
*   [https://bugs.eclipse.org/bugs/show_bug.cgi?id=381010](https://bugs.eclipse.org/bugs/show_bug.cgi?id=381010) (WONTFIX)

### 切换按钮的选择/未选择状态是一样的

如下取消 `/usr/share/themes/Adwaita/gtk-2.0/gtkrc` 最后一行的注释

```
#widget "*swt*toolbar*" style "null"

```

要应用修改后的主题，使用 `gnome-tweak-tool` 来选择另一主题之后切回 Adwaita.

相关 bug:

*   [https://bugzilla.gnome.org/show_bug.cgi?id=687519](https://bugzilla.gnome.org/show_bug.cgi?id=687519)

### 改变默认窗口标题字号

使用 Eclipse 配置并不能改变窗口字号，你必须编辑对应的 .css 文件。注意，当你更新 Eclipse 后必须再执行一遍。 它们位于

```
/usr/share/eclipse/plugins/org.eclipse.platform_4.3.<your version number>/css

```

Open the appropriate file with your text editor, ie e4_default_gtk.css if you are using the "GTK theme". 寻找 .MPartStack, 并把字号改成你想要的大小

```
.MPartStack {
       font-size: 9;
       swt-simple: false;
       swt-mru-visible: false;
}

```

## 参阅

*   [How to use Subversion with Eclipse](https://www.ibm.com/developerworks/library/os-ecl-subversion/)