[WPS Office for Linux](http://linux.wps.cn/) 是金山公司推出的、运行于 Linux 平台上的全功能办公软件。与 Microsoft Office 高度兼容，且更加尊重 Linux 用户特定的使用习惯，并自带方正字体集。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 提示与技巧](#提示与技巧)
    *   [2.1 修改 WPS 文件图标以及文件关联](#修改_WPS_文件图标以及文件关联)
    *   [2.2 使用 GTK+ UI](#使用_GTK+_UI)
        *   [2.2.1 手动修复 金山 PDF 启动脚本](#手动修复_金山_PDF_启动脚本)
*   [3 疑难解答](#疑难解答)
    *   [3.1 Office WPS for Linux 的启动命令是什么](#Office_WPS_for_Linux_的启动命令是什么)
    *   [3.2 Zip 模板压缩包乱码](#Zip_模板压缩包乱码)
    *   [3.3 公式无法正常显示](#公式无法正常显示)
    *   [3.4 KDE中Microsoft Office文件格式被识别为Zip](#KDE中Microsoft_Office文件格式被识别为Zip)
*   [4 参见](#参见)

## 安装

自alpha18开始，WPS已经有x86_64版本，故所有用户均可直接安装 [AUR (简体中文)](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)") 中的 [wps-office](https://aur.archlinux.org/packages/wps-office/) 即可。

当然，你也可以通过添加[archlinuxcn源](https://www.archlinuxcn.org/archlinux-cn-repo-and-mirror/)后用pacman安装(仅限64位arch用户）。

**注意:** 请留意自带字体的版权状况，可阅读 [WPS Office Linux 版最终用户协议](http://community.wps.cn/wiki/WPS_Office_Linux%E7%89%88%E6%9C%80%E7%BB%88%E7%94%A8%E6%88%B7%E5%8D%8F%E8%AE%AE) 第十四条

此外可选安装wps需要的符号字体：[ttf-wps-fonts](https://aur.archlinux.org/packages/ttf-wps-fonts/)。

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

处理策略：WPS 自己的格式由 {{ic|wps-office-{wpp,wps,et}.xml}} 定义，其他的用 `freedesktop.org.xml` 定义。同时修改 `desktop` 文件的 `MimeType` 项。

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

可以修改 /usr/bin/ 目录下的 et、wpp、wps 文件，删除（如果有的话）：

```
gOpt=

```

然后，添加：

```
gOpt="-style=gtk+"
export GTK2_RC_FILES=/usr/share/themes/Breeze/gtk-2.0/gtkrc

```

#### 手动修复 金山 PDF 启动脚本

金山 PDF 提供的启动脚本缺失了对 GTK 的自定义配置 可以在其启动脚本 /usr/bin/wpspdf 开始位置添加：

```
gOpt="-style=gtk+"
export GTK2_RC_FILES=/usr/share/themes/Breeze/gtk-2.0/gtkrc

```

并在其后的 run 函数中添加 `${gOpt`}，修改后的 run 函数如下：

```
function run()
{
	if [ -e "${gInstallPath}/office6/${gApp}" ] ; then
		{ ${gInstallPath}/office6/${gApp} ${gOpt} "$@"; } >/dev/null 2>&1
	else
		echo "${gApp} does not exist!"
	fi
}

```

**Note:** 由于每次升级可能导致文件修改遗失，可以考虑将 et、wpp、wps 文件复制到其他目录（例如：`~/.local/bin/`），并将其添加到 [Environment variables](/index.php/Environment_variables "Environment variables")

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

[AUR (简体中文)](/index.php/AUR_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AUR (简体中文)") 中的 [ttf-wps-fonts](https://aur.archlinux.org/packages/ttf-wps-fonts/) 包含了除monotypesorts.ttf之外的字体，直接安装即可。

### KDE中Microsoft Office文件格式被识别为Zip

在安装完成wps之后，系统的Microsoft Office文件格式会被识别为zip，无法与wps关联，可以通过删除/usr/share/mime/packages/下的mime文件即可修改格式识别：

```
sudo rm /usr/share/mime/packages/wps-office-*.xml
sudo update-mime-database /usr/share/mime

```

## 参见

*   [How to associate all Microsoft office files to WPS office applications?](https://forum.manjaro.org/t/how-to-associate-all-microsoft-office-files-to-wps-office-applications/33528/6)