## Contents

*   [1 介绍](#.E4.BB.8B.E7.BB.8D)
*   [2 风格](#.E9.A3.8E.E6.A0.BC)
    *   [2.1 QtCurve](#QtCurve)
    *   [2.2 其它](#.E5.85.B6.E5.AE.83)
*   [3 主题引擎](#.E4.B8.BB.E9.A2.98.E5.BC.95.E6.93.8E)
    *   [3.1 GTK-QT-Engine](#GTK-QT-Engine)
    *   [3.2 MetaTheme](#MetaTheme)
*   [4 其它策略](#.E5.85.B6.E5.AE.83.E7.AD.96.E7.95.A5)
    *   [4.1 GTK2程序拥有KDE的文件对话框](#GTK2.E7.A8.8B.E5.BA.8F.E6.8B.A5.E6.9C.89KDE.E7.9A.84.E6.96.87.E4.BB.B6.E5.AF.B9.E8.AF.9D.E6.A1.86)
*   [5 问题解决](#.E9.97.AE.E9.A2.98.E8.A7.A3.E5.86.B3)
    *   [5.1 怎样为每一个工具设置风格?](#.E6.80.8E.E6.A0.B7.E4.B8.BA.E6.AF.8F.E4.B8.80.E4.B8.AA.E5.B7.A5.E5.85.B7.E8.AE.BE.E7.BD.AE.E9.A3.8E.E6.A0.BC.3F)
        *   [5.1.1 KDE3 和 QT3 风格](#KDE3_.E5.92.8C_QT3_.E9.A3.8E.E6.A0.BC)
        *   [5.1.2 QT4 风格](#QT4_.E9.A3.8E.E6.A0.BC)
        *   [5.1.3 GTK2 风格](#GTK2_.E9.A3.8E.E6.A0.BC)
        *   [5.1.4 GTK1 风格](#GTK1_.E9.A3.8E.E6.A0.BC)
    *   [5.2 主题不作用于GTK程序](#.E4.B8.BB.E9.A2.98.E4.B8.8D.E4.BD.9C.E7.94.A8.E4.BA.8EGTK.E7.A8.8B.E5.BA.8F)

# 介绍

基于[Qt](https://en.wikipedia.org/wiki/Qt_(toolkit) 和 [GTK+](/index.php/GTK%2B "GTK+")的程序使用不同的工具包来渲染图形化用户界面，各自带有不同的主题、风格和图标，所以观感就明显有所不同。这篇文章将帮助你体验让你的Qt和GTK+程序看起来更现代化、集成化的桌面。

*"Qt (音："cute") 是一个跨平台应用开发框架，广泛应用于开发GUI程序(这种情况下是作为开发工具包)，也用于开发非GUI程序比如控制台工具和服务程序。"*

*   **主题** - 包含一套风格、图标主题和颜色主题。
*   **风格** - 图形布置，观感。
*   **图标主题** - 一套整体的图标。
*   **颜色主题** - 一套连接风格的整体配色。

# 风格

有很多集成程序都配置和提供可用于Qt和GTK+程序的整套风格，因此可以毫不费力应用于所以程序拥有一个统一的外观。

## QtCurve

可应用于 *qt4* (kde4), *qt3* (kde3), *gtk2*, 和 *gtk1* 在 **[community]** 仓库，这是一个非常流行的全方位应用的高可配置风格。它有很多不同选项用于控制按钮外观、边缘平滑等。 你可以安装所有包。

```
pacman -S qtcurve-gtk1 qtcurve-gtk2 qtcurve-kde3 qtcurve-kde4

```

在KDE3中改变Qt3风格：

```
Control Center (kcontrol) --> Appearance & Themes --> Style --> Widget Style = QtCurve

```

在KDE3中改变GTK+2风格：

```
pacman -S gtk-chtheme

```

运行它你就可以选择你想要的选项了。你还可以改变字体。请注意所有打开的应用程序必须重启动才能作用那些改变。另还可以应用于引擎，下面将会进一步提及。

## 其它

一些分别为Qt和GTK+配置提供的程序，他们看起来相似，不过分属于不同开发者，你可能需要自己作些小调整使它们看起来一致。比如：

*   klearlooks (qt3); clearlooks (gtk2)

# 主题引擎

主题引擎可以认为是从一个或多个工具翻译主题（图标除外）很小的API层。这些引擎为进程添加额外的代码，这种解决方案不是非常精致更多为本来风格优化。

## GTK-QT-Engine

这个是用于KDE平台中的GTK+程序的引擎。它作用于所有Qt设置（风格、字体，不包含图标）的GTK+程序并且直接使用风格插件。 请记住在部分Qt风格渲染有些问题。

```
pacman -S gtk-qt-engine

```

你可以从这里进入设置：

```
Control Center (kcontrol) --> Appearance & Themes --> GTK Styles and Fonts

```

如果你要移除所有包和设置，你还要删除以下文件：

*   ~/.gtkrc2.0-kde
*   ~/.kde/env/gtk-qt-engine.rc.sh
*   ~/gtk-qt-engine.rc

## MetaTheme

Metatheme引擎被设计为介于各工具箱且建立一套统一的API层，使每个主题引擎能绘图，最终可以利用相同的代码来为每个程序绘图。此引擎支持GTK2, QT/KDE, 还有Java toolkits。

```
pacman -S metatheme

```

安装..

```
metatheme-install

```

配置..

```
mt-config

```

卸载..

```
metatheme-install -u

```

# 其它策略

## GTK2程序拥有KDE的文件对话框

KGtk 是一个包装脚本以 LD_PRELOAD来强制GTK2程序为 KDE 文件对话框 (打开、保存等等）。如果你使用KDE环境且比较喜欢用它的文件对话框，可以从AUR安装kgtk来覆盖GTK程序. 安装后你可以用2种方法使GTK2程序运行kgtk-wrapper(以gimp为例).

直接打开kgtk-wrapper且以GTK2二进制包作为一个参数

```
/usr/local/bin/kgtk-wrapper gimp

```

或

创建一个符号链接到将kgtk链接到二进制GTK2程序，然后你可以运行/usr/local/bin/gimp 来使gimp拥有KDE对话框的。

```
ln -s /usr/local/bin/kgtk-wrapper /usr/local/bin/gimp
/usr/local/bin/gimp

```

# 问题解决

## 怎样为每一个工具设置风格?

你可以在各种桌面环境用以下方式改变主题文件。

#### KDE3 和 QT3 风格

*   Control Center (kcontrol) --> Appearance & Themes --> Style --> Widget Style
*   kde-config --style [name of style]
*   /opt/qt/bin/qtconfig

#### QT4 风格

*   /usr/bin/qtconfig

#### GTK2 风格

*   gtk-chtheme
*   gtk2_prefs
*   switch2 (gtk-theme-switch2 package)

#### GTK1 风格

*   switch (gtk-theme-switch package)

## 主题不作用于GTK程序

如果你安装的风格或主题引擎在某些GTK程序不能显示，很可能你的GTK设置文件因某些原因不能被加载。你可以检查你的系统找到那些文件作如下设置：

```
export | grep gtk

```

通常那些文件设置在 ~/.gtkrc （GTK1）, ~/.gtkrc2.0 或 ~/.gtkrc2.0-kde （GTK2）

新版gtk-qt-engine 使用 ~/.gtkrc2.0-kde 和 ~/.kde/env/gtk-qt-engine.rc.sh 设置输出变量 如果你最近移除了gtk-qt-engine然后试图设置GTK主题，你必有要移除 ~/.kde/env/gtk-qt-engine.rc.sh 然后重启。这样做会使GTK外观使用标准的设置 ~/.gtkrc2.0来代替 ~/.gtkrc2.0-kde