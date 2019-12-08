**翻译状态：** 本文是英文页面 [Vivaldi](/index.php/Vivaldi "Vivaldi") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-07-28，点击[这里](https://wiki.archlinux.org/index.php?title=Vivaldi&diff=0&oldid=576866)可以查看翻译后英文页面的改动。

[Vivaldi](http://vivaldi.com/) 是由前 [Opera](/index.php/Opera "Opera") 创立者和开发团队成员新近开发的一款浏览器。Vivaldi 基于 [Chromium](/index.php/Chromium "Chromium") 开发，专注于个性化体验。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 扩展程序](#扩展程序)
*   [3 媒体播放](#媒体播放)
*   [4 排错](#排错)
    *   [4.1 无法将 Vivaldi 设为默认浏览器](#无法将_Vivaldi_设为默认浏览器)
*   [5 参阅](#参阅)

## 安装

可以从 AUR 安装 Vivaldi 的正式版（[vivaldi](https://aur.archlinux.org/packages/vivaldi/)）或快照版（[vivaldi-snapshot](https://aur.archlinux.org/packages/vivaldi-snapshot/)）。 或者也可以添加 [herecura](/index.php/Unofficial_user_repositories#herecura "Unofficial user repositories") 的非官方源，安装预构建的包。

若需将 [GTK+](/index.php/GTK%2B "GTK+") 风格的文件选择对话框替换成 [Qt](/index.php/Qt "Qt") 风格，只要安装 [kdialog](https://www.archlinux.org/packages/?name=kdialog) 包即可。

## 扩展程序

Vivaldi 兼容 Chrome 的绝大部分扩展。可以从[Chrome 网上商店](https://https://chrome.google.com/webstore/category/extensions)直接安装。

查看已安装或启用的扩展，可以搜索：`vivaldi://extensions` 或 `extensions`。 另请参阅 [维基百科：谷歌 Chrome 扩展](https://en.wikipedia.org/wiki/Google_Chrome_Extension "wikipedia:Google Chrome Extension")

## 媒体播放

为支持额外的音视频播放功能，可以安装相应版本的 [vivaldi-ffmpeg-codecs](https://aur.archlinux.org/packages/vivaldi-ffmpeg-codecs/) 或 [vivaldi-snapshot-ffmpeg-codecs](https://aur.archlinux.org/packages/vivaldi-snapshot-ffmpeg-codecs/)。（***译者注：前述 [herecura](/index.php/Unofficial_user_repositories#herecura "Unofficial user repositories") 的非官方源里同样有预构建的包。***）

要播放 flash 媒体文件应当安装 [pepper-flash](https://www.archlinux.org/packages/?name=pepper-flash) 。

## 排错

### 无法将 Vivaldi 设为默认浏览器

请手工编辑 [default applications](/index.php/Default_applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Default applications (简体中文)") ，Vivaldi 不能自动配置。

## 参阅

*   [官方网站](http://vivaldi.com/)
*   [Vivaldi浏览器中文讨论区](https://vivaldi.club/)（由前*Opera中国*员工[@Csineneo](https://twitter.com/csineneo)创建的非官方中文论坛）