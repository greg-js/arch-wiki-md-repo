[WPS Office for Linux](http://linux.wps.cn/) 是金山公司推出的、运行于 Linux 平台上的全功能办公软件。与 Microsoft Office 高度兼容，且更加尊重 Linux 用户特定的使用习惯，并自带方正字体集。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [2.1 修改 WPS 文件图标以及文件关联](#.E4.BF.AE.E6.94.B9_WPS_.E6.96.87.E4.BB.B6.E5.9B.BE.E6.A0.87.E4.BB.A5.E5.8F.8A.E6.96.87.E4.BB.B6.E5.85.B3.E8.81.94)
    *   [2.2 使用 GTK+ UI](#.E4.BD.BF.E7.94.A8_GTK.2B_UI)
*   [3 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [3.1 Office WPS for Linux 的启动命令是什么](#Office_WPS_for_Linux_.E7.9A.84.E5.90.AF.E5.8A.A8.E5.91.BD.E4.BB.A4.E6.98.AF.E4.BB.80.E4.B9.88)
    *   [3.2 Zip 模板压缩包乱码](#Zip_.E6.A8.A1.E6.9D.BF.E5.8E.8B.E7.BC.A9.E5.8C.85.E4.B9.B1.E7.A0.81)
    *   [3.3 公式无法正常显示](#.E5.85.AC.E5.BC.8F.E6.97.A0.E6.B3.95.E6.AD.A3.E5.B8.B8.E6.98.BE.E7.A4.BA)

## 安装

自alpha18开始，WPS已经有x86_64版本，故所有用户均可直接安装 [AUR (简体中文)](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)") 中的 wps-office 即可。

yaourt wps-office

当然，你也可以通过添加[archlinuxcn源](https://www.archlinuxcn.org/archlinux-cn-repo-and-mirror/)后用pacman安装(仅限64位arch用户）。

**注意:** 请留意自带字体的版权状况，可阅读 [WPS Office Linux 版最终用户协议](http://community.wps.cn/wiki/WPS_Office_Linux%E7%89%88%E6%9C%80%E7%BB%88%E7%94%A8%E6%88%B7%E5%8D%8F%E8%AE%AE) 第十四条

此外 [AUR (简体中文)](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)") 还包含了可自定义安装字体、模板的 [wpsforlinux](https://aur.archlinux.org/packages/wpsforlinux/)，不自带字体、模板的 [wps-office-split](https://aur.archlinux.org/packages/wps-office-split/)、提供 fcitx immodule 的 [fcitx-wps](https://aur.archlinux.org/packages/fcitx-wps/) 等。

## 提示与技巧

### 修改 WPS 文件图标以及文件关联

安装 WPS 后，您所用 icon-theme 中的 DOC、XLS、PPT 等文件会被替换成 WPS Office 所自带的 WPS 文字、ET 表格、WPP 演示等图标。如果您并不需要，可自行修改相关的 mime 配置文件：

```
/usr/share/mime/packages/wps-office-{wpp,wps,et}.xml
/usr/share/mime/packages/freedesktop.org.xml #(属于软件包shared-mime-info)

```

以及 desktop 文件：

```
/usr/share/applications/wps-office-{wpp,wps,et}.desktop

```

处理策略：WPS 自己的格式由 `wps-office-{wpp,wps,et}.xml` 定义，其他的用 `freedesktop.org.xml` 定义。同时修改 `desktop` 文件的 `MimeType` 项。

在 PKGBUILD 文件中的 `package` 函数添加以下语句：

```
##et wpp wps 支持的MimeType
    _etMT="MimeType=application\/wps-office.et;application\/wps-office.ett;application\/vnd.ms-excel;\
application\/vnd.openxmlformats-officedocument.spreadsheetml.template;\
application\/vnd.openxmlformats-officedocument.spreadsheetml.sheet;"
    _wppMT="MimeType=application\/wps-office.dps;application\/wps-office.dpt;application\/vnd.ms-powerpoint;\
application\/vnd.openxmlformats-officedocument.presentationml.presentation;\
application\/vnd.openxmlformats-officedocument.presentationml.slideshow;\
application\/vnd.openxmlformats-officedocument.presentationml.template;"
    _wpsMT="MimeType=application\/wps-office.wps;application\/wps-office.wpt;\
application\/msword;application\/rtf;application\/msword-template;\
application\/vnd.openxmlformats-officedocument.wordprocessingml.template;\
application\/vnd.openxmlformats-officedocument.wordprocessingml.document;"

    ##mime
    sed -i '3,31d' $pkgdir/usr/share/mime/packages/wps-office-et.xml
    sed -i '3,36d' $pkgdir/usr/share/mime/packages/wps-office-wpp.xml
    sed -i '3,30d' $pkgdir/usr/share/mime/packages/wps-office-wps.xml

    ##desktop
    #_et
    sed -i "s/^MimeType.*$/$_etMT/" $pkgdir/usr/share/applications/wps-office-et.desktop
    #_wpp
    sed -i "s/^MimeType.*$/$_wppMT/" $pkgdir/usr/share/applications/wps-office-wpp.desktop
    #_wps
    sed -i "s/^MimeType.*$/$_wpsMT/" $pkgdir/usr/share/applications/wps-office-wps.desktop
```

### 使用 GTK+ UI

WPS 默认的 UI 为 Qt，事实上其捆绑的 Qt 为 4.7.4，从而因为版本不符，无法正常加载 qtcurve 之类的主题。但我们可以改为 GTK+，直接加上参数 `-style gtk+` 即可。

可以修改`/usr/share/applications/wps-office-{wps,wpp,et}.desktop`一劳永逸设定：

```
Exec=/usr/bin/{wps,wpp,et} **-style gtk+** %f

```

## 疑难解答

### Office WPS for Linux 的启动命令是什么

`wps`、`et`、`wpp` 分别为启动 WPS 文字、WPS 表格、WPP 演示的命令。

### Zip 模板压缩包乱码

请先安装 [unzip-iconv](https://aur.archlinux.org/packages/unzip-iconv/)，解压时用参数 `-O gb18030` 即可。

### 公式无法正常显示

大部分数学公式的正常显示需要以下字体：

```
symbol.ttf webdings.ttf wingding.ttf wingdng2.ttf wingdng3.ttf monotypesorts.ttf MTExtra.ttf

```

[AUR (简体中文)](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)") 中的 [ttf-microsoft](https://aur.archlinux.org/packages/ttf-microsoft/) 包含了除以上后两者之外的字体，直接安装即可。