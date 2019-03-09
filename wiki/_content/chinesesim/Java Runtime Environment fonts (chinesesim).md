Related articles

*   [Fonts (简体中文)](/index.php/Fonts_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fonts (简体中文)")
*   [Font configuration (简体中文)](/index.php/Font_configuration_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Font configuration (简体中文)")
*   [MS Fonts (简体中文)](/index.php/MS_Fonts_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "MS Fonts (简体中文)")
*   [X Logical Font Description](/index.php/X_Logical_Font_Description "X Logical Font Description")

**翻译状态：** 本文是英文页面 [Java Runtime Environment fonts](/index.php/Java_Runtime_Environment_fonts "Java Runtime Environment fonts") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-3-8，点击[这里](https://wiki.archlinux.org/index.php?title=Java+Runtime+Environment+fonts&diff=0&oldid=568119)可以查看翻译后英文页面的改动。

可能一部分人认为Java应用程序中的默认字体和字体的显示模式不大理想。下面有几种方法可以改进Oracle Java Runtime Environment (JRE)中的字体显示。这些方法可以单独使用，但是经过许多用户实践发现将它们组合使用可以获得更好的效果。

Java对于TrueType格式字体的支持似乎是最好的。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 抗锯齿](#抗锯齿)
    *   [1.1 基础设置](#基础设置)
    *   [1.2 OpenJDK 补丁](#OpenJDK_补丁)
*   [2 选择字体](#选择字体)
    *   [2.1 TrueType 字体](#TrueType_字体)
    *   [2.2 修复乱码 (For JRE8)](#修复乱码_(For_JRE8))

## 抗锯齿

### 基础设置

Linux上的Oracle Java 1.6和OpenJDK提供了字体的[抗锯齿](https://en.wikipedia.org/wiki/Font_rasterization "wikipedia:Font rasterization")功能。使用这个功能，请将以下内容添加到`/etc/environment`:

```
_JAVA_OPTIONS='-Dawt.useSystemAAFontSettings=*setting'*

```

`*setting*` 是下面内容的其中一项:

| 设置值 | 描述 |
| `off`, `false`, `default` | 不开启抗锯齿 |
| `on` | 全效抗锯齿 |
| `gasp` | 使用字体文件自带的配置信息 |
| `lcd`, `lcd_hrgb` | 为流行的显示器调整过的抗锯齿 |
| `lcd_hbgr`, `lcd_vrgb`, `lcd_vbgr` | 替代显示器的设置 |

`gasp` 和`lcd` 设置在大部分情况下表现良好。

选择使用GTK的显示风格，请将下面的内容添加到.bashrc：

```
_JAVA_OPTIONS='-Dswing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel' 

```

**Note:**

*   所描述的Java选项仅适用于使用Java绘制GUI的应用程序，如Jdownloader，而不适用于仅使用Java作为后端的应用程序，如Openoffice.org和Matlab。
*   “TrueType” 字体包含一个网格显示拟合和扫描转换过程的表(Grid-fitting And Scan-conversion Procedure “GASP”)，其中包含了字体作者对不同大小字体显示的建议。一些字号可以完全抗锯齿，一些只有部分提示，还有一些显示为位图。对于一些字号，上面的方法会组合使用。

在运行之前，在命令行中指定其他的变量，可以尝试别的配置:

```
_JAVA_OPTIONS=*options* *executable* 

```

你需要重新登陆使配置生效。

### OpenJDK 补丁

即使通过Java选项强制执行了抗锯齿，得到的抗锯齿效果也可能不如本机应用程序。可以通过OpenJDK的一个补丁来弥补，[AUR](/index.php/AUR "AUR")提供了这个补丁:

*   修补后的 **OpenJDK7** 可用 [jre7-openjdk-infinality](https://aur.archlinux.org/packages/jre7-openjdk-infinality/) (—enable-infinality=yes)
*   修补后的 **OpenJDK8** 可用 [jre8-openjdk-infinality](https://aur.archlinux.org/packages/jre8-openjdk-infinality/)

修补后的版本从fontconfig获得FreeType类型字体的渲染和加载标志，而不是使用OpenJDK的方法。虽然这是一个[Infinality](/index.php/Infinality "Infinality")包，但是补丁本身实际上并不依赖于[fontconfig-Infinality](https://aur.archlinux.org/packages/fontconfig-Infinality/)，因为只使用了普通的[fontconfig](https://www.archlinux.org/packages/?name=fontconfig) api。

## 选择字体

### TrueType 字体

使一些应用程序知道所需字体的目录路径，那么这些Java应用程序就会使用特定的TrueType字体。TrueType字体安装在`/usr/share/fonts/TTF`目录中。将以下内容添加到`/etc/environment`以启用这些字体。

```
JAVA_FONTS=/usr/share/fonts/TTF

```

你需要重新登陆使配置生效。

### 修复乱码 (For JRE8)

将字体文件放在下面的目录下。如果目录不存在，则创建该目录。

```
/usr/lib/jvm/java-8-openjdk/jre/lib/fonts/fallback/

```