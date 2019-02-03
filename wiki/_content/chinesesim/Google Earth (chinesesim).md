**翻译状态：** 本文是英文页面 [Google_Earth](/index.php/Google_Earth "Google Earth") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-2-14，点击[这里](https://wiki.archlinux.org/index.php?title=Google_Earth&diff=0&oldid=355374)可以查看翻译后英文页面的改动。

来自 [项目网站](http://support.google.com/earth/bin/answer.py?hl=en&answer=176145)：:

*"Google Earth可以让您在一个虚拟的地球上随意的旅行并观看卫星影像,地形,地图,3D建筑等元素. 随着Google earth中地理内容的丰富, 您将能探索更真实的世界，并能够飞到您最喜欢的地方, 搜索商户或者只是用于导航。"*

## Contents

*   [1 安装](#安装)
*   [2 故障处理](#故障处理)
    *   [2.1 启动时出现错误](#启动时出现错误)
        *   [2.1.1 Startup tips 被启用](#Startup_tips_被启用)
        *   [2.1.2 ~/.drirc文件的结尾没有换行](#~/.drirc文件的结尾没有换行)
        *   [2.1.3 缓存文件损坏](#缓存文件损坏)
        *   [2.1.4 Another crash happened while handling crash!](#Another_crash_happened_while_handling_crash!)
    *   [2.2 占用的内存过多](#占用的内存过多)
    *   [2.3 Panoramio上的照片无法使用](#Panoramio上的照片无法使用)
    *   [2.4 地球除了黄色的边框以外什么都不显示](#地球除了黄色的边框以外什么都不显示)

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

您可以在 *Tools > Options > Cache*中调整最大缓存限制来控制内存的使用大小，或者您可以在*3D View*页面中通过降低画面质量来降低内存负荷。

### Panoramio上的照片无法使用

在[Google Earth forums](https://productforums.google.com/forum/#!categories/earth/linux)中有几个针对不同原因所给出的不同解决方案 [[1]](http://productforums.google.com/d/msg/earth/548PQIT8bKI/rbpVsbMawwIJ) [[2]](http://productforums.google.com/forum/#!msg/earth/_h4t6SpY_II/6O_DTry49pgJ) [[3]](http://productforums.google.com/d/msg/earth/tZfKSs2AaZc/r_rBDl5djIMJ)。 如果在[google-earth](https://aur.archlinux.org/packages/google-earth/)中的[PKGBUILD](https://aur.archlinux.org/packages/go/google-earth/PKGBUILD)设置`_attempt_fix` 变量仍不起作用，回滚到旧版的[google-earth6](https://aur.archlinux.org/packages/google-earth6/) 可能会解决这个问题.

### 地球除了黄色的边框以外什么都不显示

根据更新日志[7.0.3](https://support.google.com/earth/bin/answer.py?hl=en&answer=40901)这个问题已得到大幅改善，但是这个错误仍然会存在:

```
这个问题可能会出现在使用Intel系列GPU的Linux用户中

```

解决方法同样适用于 [google-earth6](https://aur.archlinux.org/packages/google-earth6/)。