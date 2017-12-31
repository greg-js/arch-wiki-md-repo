Related articles

*   [xdg-menu](/index.php/Xdg-menu "Xdg-menu")
*   [Default applications (简体中文)](/index.php/Default_applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Default applications (简体中文)")
*   [XDG Base Directory support](/index.php/XDG_Base_Directory_support "XDG Base Directory support")

**翻译状态：** 本文是英文页面 [XDG user directories](/index.php/XDG_user_directories "XDG user directories") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-02-22，点击[这里](https://wiki.archlinux.org/index.php?title=XDG+user+directories&diff=0&oldid=468815)可以查看翻译后英文页面的改动。

用户目录指位于 `$HOME` 下的一系列常用目录，例如 `Documents`，`Downloads`，`Music`，还有 `Desktop`。用户目录会在文件管理器中显示为不同的图标，且被多种应用程序所参照。可以使用 [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs) 自动生成这些目录。进一步信息请参照 [freedesktop.org](https://www.freedesktop.org/wiki/Software/xdg-user-dirs)。

**提示：** 对于那些想要用文件管理器来给 [Window manager (简体中文)](/index.php/Window_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Window manager (简体中文)")（例如 [Openbox (简体中文)](/index.php/Openbox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Openbox (简体中文)")）显示桌面的人来说这个程序尤其有用，因为它会自动创建 `~/Desktop` 目录。

## 创建默认目录

可以用 [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs) 在 `$HOME` 下创建一整套默认的经本地化的用户目录。请运行：

```
$ xdg-user-dirs-update

```

**提示：** 使用 `LC_ALL=C xdg-user-dirs-update` 命令可以强制创建英语目录。

运行后该命令还会自动地：

*   创建一个本地的 `~/.config/user-dirs.dirs` 配置文件：应用程序通过他来查找使用特定帐号指定的用户目录。
*   创建一个本地的 `~/.config/user-dirs.locale` 配置文件：根据使用的 locale 指定语言。

## 创建自定义目录

本地的 `~/.config/user-dirs.dirs` 和全局的 `/etc/xdg/user-dirs.defaults` 配置文件都使用如下的环境变量格式： `XDG_DIRNAME_DIR="$HOME/目录名"`。一个例子：

 `~/.config/user-dirs.dirs` 
```
XDG_DESKTOP_DIR="$HOME/桌面"
XDG_DOCUMENTS_DIR="$HOME/文档"
XDG_DOWNLOAD_DIR="$HOME/下载"
XDG_MUSIC_DIR="$HOME/音乐"
XDG_PICTURES_DIR="$HOME/图片"
XDG_PUBLICSHARE_DIR="$HOME/公共"
XDG_TEMPLATES_DIR="$HOME/模板"
XDG_VIDEOS_DIR="$HOME/视频"
```

因为 [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs) 会参照本地配置文件来了解正确的用户目录，所以可以自定义。比如若将 `~/.config/user-dirs.dirs` 下 `XDG_DOWNLOAD_DIR` 变量设为了 `$HOME/Internet`，那么任何参照了该变量的程序都会改用这个目录。

**注意:** 和其他的配置文件一样，本地设定覆盖全局设定。另外自定义的目录要自己创建。

或者也可以用命令行修改默认目录。下列命令会产生和上面一样的效果：

```
$ xdg-user-dirs-update --set DOWNLOAD ~/Internet

```

## 查询配置好的目录

可以用 [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs) 来查询配置好的目录路径。例如，下列命令可以查询 `模板` 目录的位置，对应于本地配置文件中 `XDG_TEMPLATES_DIR` 变量的值：

```
$ xdg-user-dir TEMPLATES

```