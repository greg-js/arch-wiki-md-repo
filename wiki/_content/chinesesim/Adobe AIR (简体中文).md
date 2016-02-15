[Adobe Integrated Runtime (AIR)](https://en.wikipedia.org/wiki/Adobe_Integrated_Runtime "wikipedia:Adobe Integrated Runtime")(Adobe 集成运行环境) 是一个跨平台的运行环境，由 Adobe Systems 开发，用于编译使用 Adobe Flash, Adobe Flex, HTML, 或 Ajax 的富Internet应用程序，可以作为桌面应用程序部署。

## Contents

*   [1 安装 Adobe AIR](#.E5.AE.89.E8.A3.85_Adobe_AIR)
*   [2 安装一个 AIR 应用程序](#.E5.AE.89.E8.A3.85.E4.B8.80.E4.B8.AA_AIR_.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
    *   [2.1 使之可执行](#.E4.BD.BF.E4.B9.8B.E5.8F.AF.E6.89.A7.E8.A1.8C)
    *   [2.2 删除应用程序](#.E5.88.A0.E9.99.A4.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)

## 安装 Adobe AIR

从 [AUR](/index.php/AUR "AUR") 中安装 [adobe-air-sdk](https://aur.archlinux.org/packages.php?ID=25633&comments=all)。

## 安装一个 AIR 应用程序

下载应用程序，解压到 `/opt/airapps/<appname>`。使用下面的命令运行：

 `$ /opt/adobe-air-sdk/bin/adl -nodebug /opt/airapps/<Application name>/META-INF/AIR/application.xml /opt/airapps/<Application name>/` 

### 使之可执行

你也可以在 `/usr/bin` 创建一个可执行程序：

```
 #! /bin/sh
 /opt/adobe-air-sdk/bin/adl -nodebug /opt/airapps/wimp/META-INF/AIR/application.xml /opt/airapps/wimp/

```

这个应用程序可能需要参数 (voddler)，因此脚本可能类似于：

```
 #! /bin/sh
 /opt/adobe-air-sdk/bin/adl -nodebug /opt/airapps/wimp/META-INF/AIR/application.xml /opt/airapps/wimp/ -- $1 $2 $3 $4

```

然后 _chmod_ 这个文件使之可执行：

```
$ chmod +x filename

```

现在你安装好了一个 AIR 应用程序。很简单是吧 :P

### 删除应用程序

删除 `/opt/airapps` 中的应用程序文件夹。同时删除您自己创建的可执行文件。