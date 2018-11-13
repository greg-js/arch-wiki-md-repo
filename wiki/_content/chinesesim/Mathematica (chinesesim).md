相关文章

*   [Scientific Applications (简体中文)](/index.php/Scientific_Applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Scientific Applications (简体中文)")
*   [Sage-mathematics](/index.php/Sage-mathematics "Sage-mathematics")
*   [Matlab (简体中文)](/index.php/Matlab_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Matlab (简体中文)")

**翻译状态：** 本文是英文页面 [Mathematica](/index.php/Mathematica "Mathematica") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-09-01，点击[这里](https://wiki.archlinux.org/index.php?title=Mathematica&diff=0&oldid=525644)可以查看翻译后英文页面的改动。

[Mathematica](http://www.wolfram.com/mathematica/) 是用于科学，工程和数学领域的商业软件。在这里我们说明如何安装它。

## Contents

*   [1 安装](#安装)
    *   [1.1 Mathematica 6](#Mathematica_6)
        *   [1.1.1 挂载 iso 文件](#挂载_iso_文件)
        *   [1.1.2 运行安装程序](#运行安装程序)
        *   [1.1.3 字体](#字体)
    *   [1.2 Mathematica 7](#Mathematica_7)
    *   [1.3 Mathematica 8](#Mathematica_8)
    *   [1.4 Mathematica 10](#Mathematica_10)
    *   [1.5 Mathematica 11](#Mathematica_11)
*   [2 故障排除](#故障排除)
    *   [2.1 "Missing symbols" 错误](#"Missing_symbols"_错误)
    *   [2.2 HiDPI / Retina 屏幕](#HiDPI_/_Retina_屏幕)
    *   [2.3 与系统库冲突导致的问题](#与系统库冲突导致的问题)
        *   [2.3.1 Symbol lookup error: /usr/lib/libfontconfig.so.1: undefined symbol: FT_Done_MM_Var](#Symbol_lookup_error:_/usr/lib/libfontconfig.so.1:_undefined_symbol:_FT_Done_MM_Var)
        *   [2.3.2 Mathematica/11.3/SystemFiles/Libraries/Linux-x86-64/libz.so.1: version `ZLIB_1.2.9' not found (required by /usr/lib/libpng16.so.16)](#Mathematica/11.3/SystemFiles/Libraries/Linux-x86-64/libz.so.1:_version_`ZLIB_1.2.9'_not_found_(required_by_/usr/lib/libpng16.so.16))
*   [3 参阅](#参阅)

## 安装

由于 Mathematica 是专有软件，升级可能会产生成本，因此本节列出了不同可用版本的说明。

### Mathematica 6

#### 挂载 iso 文件

挂载 Mathematica `.iso` 的一种方式是创建 `/media/iso` 目录用于挂载，并在 [fstab](/index.php/Fstab "Fstab") 中增加这几行：

```
/*location/of/mathematica.iso* /media/iso iso9660 exec,ro,user,noauto,loop=/dev/loop0   0 0

```

然后就可以这样挂载它：

```
# mount /media/iso

```

#### 运行安装程序

进入这个目录来启动安装程序：

```
/Unix/Installer

```

运行 *MathInstaller*：

```
sh ./MathInstaller

```

**注意:** 如果没有把 "sh" 放在前面，那么会得到一个关于解释器出错 (bad interpreter) 的错误信息。

#### 字体

向 FontPath 里添加包含 Type1 和 BDF 字体的目录。

### Mathematica 7

Mathematica 7 安装起来非常方便。

```
tar xf Mathematica-7.0.1.tar.gz
cd Unix/Installer
./MathInstaller

```

按照指示完成即可。

KDE 用户注意，Mathematica 的图标可能会出现在 *Lost & Found* 分类里面。解决方法是以 root 用户身份运行下列命令：

```
# ln -s /etc/xdg/menus/applications-merged /etc/xdg/menus/kde-applications-merged

```

### Mathematica 8

Mathematica 8 的一个问题是执行 WolframAlpha[ ] 函数时会出现崩溃，这个崩溃可以重现。Mathematica 的默认配置为，在设置如何连接到互联网以获取数据时，检测系统的代理设置。但是在调用库函数时存在一个 bug，最终会使 Mathematica 崩溃。解决方法是通过将 Mathematica 配置为“直接连接”到互联网来完全避免此库调用 (*Edit > Preferences > Internet Connectivity > Proxy Settings*)。这个错误已经报告给 Wolfram。

### Mathematica 10

[安装](/index.php/Install "Install") [mathematica](https://aur.archlinux.org/packages/mathematica/) （需要旧版本）。需要 `Mathematica_10.XX.YY_LINUX.sh` 安装脚本，从 Wolfram.com 或某大学的站点上下载。同时你还需要一个激活密钥。

### Mathematica 11

[安装](/index.php/Install "Install") [mathematica](https://aur.archlinux.org/packages/mathematica/)。从 Wolfram Research 获取 `Mathematica_11.XX.YY_LINUX.sh` 和激活密钥。成功的安装可能也会抛出一些不严重的错误：xdg-icon-resource, mkdir, xdg-desktop-menu 等。

Mathematica 11 在 [$UserDocumentsDirectory](https://reference.wolfram.com/language/ref/$UserDocumentsDirectory.html) 自动创建 'Wolfram Mathematica' 文件夹，Mathematica 根据 [XDG user directories](/index.php/XDG_user_directories "XDG user directories") 自动设置了这个变量。

## 故障排除

### "Missing symbols" 错误

如果出现字体渲染问题，某些符号无法显示（比如 `/` 显示为正方形），请尝试卸载 [font-mathematica](https://www.archlinux.org/packages/?name=font-mathematica)。

同时，尝试 [这种](http://mathematica.stackexchange.com/questions/1158/invisible-conjugate-glyph-in-the-linux-frontend) 方案。其中还说明了 Mathematica 版本 9 修复了这个问题。

尝试让应用程序使用抗锯齿。 对于 KDE 用户： *System Settings > Application Appearance > Fonts > Use anti-aliasing (Enabled)*

### HiDPI / Retina 屏幕

如果你有一块 [HiDPI](/index.php/HiDPI "HiDPI") 屏幕，比如 Apple Retina 屏幕，而且 Mathematica 里面的文字非常小，这样就能解决：

*   打开 *Edit → Preferences*
*   在 *Advanced* 选项卡里单击 *Open Option Inspector*
*   在右侧的树状列表中找到 *Formatting Options → Font Options → Font Properties*
*   改变 *"ScreenResolution"* 的值到它原来的两倍大小，比如 72 → 144。你也可以用 `xdpyinfo | grep resolution` 来获得一个更精确的数字（也要变成原来的两倍大小）。

### 与系统库冲突导致的问题

Mathematica 软件包包含了一系列其自有的库，存放在 <INSTALL_DIR>/SystemFiles/Libraries/Linux-x86-64 里面。它们可能会导致一些兼容性问题，并且可能需要将某些库回退到系统现有版本。

#### Symbol lookup error: /usr/lib/libfontconfig.so.1: undefined symbol: FT_Done_MM_Var

强制 Mathematica 使用系统自有的 freetype 库。

```
# cd <INSTALL_DIR>/SystemFiles/Libraries/Linux-x86-64
# mv libfreetype.so.6 libfreetype.so.6.old

```

#### Mathematica/11.3/SystemFiles/Libraries/Linux-x86-64/libz.so.1: version `ZLIB_1.2.9' not found (required by /usr/lib/libpng16.so.16)

强制 Mathematica 使用系统自有的 zlib 库。

```
# cd <INSTALL_DIR>/SystemFiles/Libraries/Linux-x86-64
# mv libz.so.1 libz.so.1.old

```

## 参阅

*   [Official site](http://www.wolfram.com/mathematica/)
*   [Official Support](http://www.wolfram.com/support/)