**翻译状态：** 本文是英文页面 [Google_Earth](/index.php/Google_Earth "Google Earth") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-2-14，点击[这里](https://wiki.archlinux.org/index.php?title=Google_Earth&diff=0&oldid=355374)可以查看翻译后英文页面的改动。

来自 [项目网站](http://support.google.com/earth/bin/answer.py?hl=en&answer=176145)：:

_"Google Earth可以让您在一个虚拟的地球上随意的旅行并观看卫星影像,地形,地图,3D建筑等元素. 随着Google earth中地理内容的丰富, 您将能探索更真实的世界，并能够飞到您最喜欢的地方, 搜索商户或者只是用于导航。"_

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 故障处理](#.E6.95.85.E9.9A.9C.E5.A4.84.E7.90.86)
    *   [2.1 启动时出现错误](#.E5.90.AF.E5.8A.A8.E6.97.B6.E5.87.BA.E7.8E.B0.E9.94.99.E8.AF.AF)
        *   [2.1.1 Startup tips 被启用](#Startup_tips_.E8.A2.AB.E5.90.AF.E7.94.A8)
        *   [2.1.2 ~/.drirc文件的结尾没有换行](#.7E.2F.drirc.E6.96.87.E4.BB.B6.E7.9A.84.E7.BB.93.E5.B0.BE.E6.B2.A1.E6.9C.89.E6.8D.A2.E8.A1.8C)
        *   [2.1.3 缓存文件损坏](#.E7.BC.93.E5.AD.98.E6.96.87.E4.BB.B6.E6.8D.9F.E5.9D.8F)
        *   [2.1.4 Another crash happened while handling crash!](#Another_crash_happened_while_handling_crash.21)
    *   [2.2 占用的内存过多](#.E5.8D.A0.E7.94.A8.E7.9A.84.E5.86.85.E5.AD.98.E8.BF.87.E5.A4.9A)
    *   [2.3 Panoramio上的照片无法使用](#Panoramio.E4.B8.8A.E7.9A.84.E7.85.A7.E7.89.87.E6.97.A0.E6.B3.95.E4.BD.BF.E7.94.A8)
    *   [2.4 地球除了黄色的边框以外什么都不显示](#.E5.9C.B0.E7.90.83.E9.99.A4.E4.BA.86.E9.BB.84.E8.89.B2.E7.9A.84.E8.BE.B9.E6.A1.86.E4.BB.A5.E5.A4.96.E4.BB.80.E4.B9.88.E9.83.BD.E4.B8.8D.E6.98.BE.E7.A4.BA)

## 安装

[AUR](/index.php/AUR "AUR")中已提供了Google earth 的安装包:

*   最新版本 - [google-earth](https://aur.archlinux.org/packages/google-earth/)
*   之前的版本 - [google-earth6](https://aur.archlinux.org/packages/google-earth6/)

## 故障处理

**Tip:** 参见 [官方支持社区](https://productforums.google.com/forum/#!categories/earth/linux) 来查阅本段中未包括的内容。

### 启动时出现错误

Google Earth可能会因多种错误而不能启动，下面列出了几个常见错误和错误的处理方法。

#### Startup tips 被启用

即使startup tips非常有用，但是它被人所更为了解的原因是startup tip容易造成软件的崩溃，所以请使它无效化，把以下字段加入 `~/.config/Google/GoogleEarthPlus.conf`中:

```
[General]
enableTips=false

```

#### `~/.drirc`文件的结尾没有换行

```
$ echo >> ~/.drirc

```

#### 缓存文件损坏

如果缓存文件已损坏并需要重建,请移除它:

```
$ rm -r ~/.googleearth/Cache/

```

#### Another crash happened while handling crash!

您可以尝试移除以下文件:

```
$ rm -f ~/.googleearth/Cache/cookies ~/.googleearth/instance-running-lock

```

### 占用的内存过多

您可以在 _Tools > Options > Cache_中调整最大缓存限制来控制内存的使用大小，或者您可以在_3D View_页面中通过降低画面质量来降低内存负荷。

### Panoramio上的照片无法使用

在[Google Earth forums](https://productforums.google.com/forum/#!categories/earth/linux)中有几个针对不同原因所给出的不同解决方案 [[1]](http://productforums.google.com/d/msg/earth/548PQIT8bKI/rbpVsbMawwIJ) [[2]](http://productforums.google.com/forum/#!msg/earth/_h4t6SpY_II/6O_DTry49pgJ) [[3]](http://productforums.google.com/d/msg/earth/tZfKSs2AaZc/r_rBDl5djIMJ)。 如果在[google-earth](https://aur.archlinux.org/packages/google-earth/)中的[PKGBUILD](https://aur.archlinux.org/packages/go/google-earth/PKGBUILD)设置`_attempt_fix` 变量仍不起作用，回滚到旧版的[google-earth6](https://aur.archlinux.org/packages/google-earth6/) 可能会解决这个问题.

### 地球除了黄色的边框以外什么都不显示

根据更新日志[7.0.3](https://support.google.com/earth/bin/answer.py?hl=en&answer=40901)这个问题已得到大幅改善，但是这个错误仍然会存在:

```
这个问题可能会出现在使用Intel系列GPU的Linux用户中

```

解决方法同样适用于 [google-earth6](https://aur.archlinux.org/packages/google-earth6/)。