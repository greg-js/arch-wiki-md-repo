**翻译状态：** 本文是英文页面 [Pkgfile](/index.php/Pkgfile "Pkgfile") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-06-15，点击[这里](https://wiki.archlinux.org/index.php?title=Pkgfile&diff=0&oldid=262598)可以查看翻译后英文页面的改动。

工具**pkgfile**可以查出文件是由哪一个包提供的。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 示例](#.E7.A4.BA.E4.BE.8B)
*   [3 其它示例](#.E5.85.B6.E5.AE.83.E7.A4.BA.E4.BE.8B)
*   [4 "Command not found" 钩子](#.22Command_not_found.22_.E9.92.A9.E5.AD.90)
*   [5 参阅](#.E5.8F.82.E9.98.85)

## 安装

可以从 [官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)") [安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")软件包[pkgfile](https://www.archlinux.org/packages/?name=pkgfile) , 或者从 [AUR](/index.php/AUR "AUR") 安装 [pkgfile-git](https://aur.archlinux.org/packages/pkgfile-git/)。

然后以 root 权限更新文件数据库:

```
# pkgfile --update

```

## 示例

查找哪个包包含名为 "makepkg" 的文件:

 `$ pkgfile _makepkg_`  `core/pacman           #搜索的文件在 [core] 源的 [pacman](https://www.archlinux.org/packages/?name=pacman) 包中。` 

## 其它示例

列出 [core] 源中 [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) 包包含的文件：

 `$ pkgfile --list _core/archlinux-keyring_` 

```
core/archlinux-keyring usr/
core/archlinux-keyring usr/share/
core/archlinux-keyring usr/share/pacman/
core/archlinux-keyring usr/share/pacman/keyrings/
core/archlinux-keyring usr/share/pacman/keyrings/archlinux-revoked
core/archlinux-keyring usr/share/pacman/keyrings/archlinux-trusted
core/archlinux-keyring usr/share/pacman/keyrings/archlinux.gpg
```

## "Command not found" 钩子

pkgfile 包含一个叫做 "command not found" 的钩子，它会在你键入一个未知命令的时候自动在官方源中搜索。

要在所有的shell中启用它，需要将钩子的 source 添加到你的 shell 的配置文件中。

*   在 [Bash](/index.php/Bash "Bash") 中启用:

 `~/.bashrc`  `source /usr/share/doc/pkgfile/command-not-found.bash` 

*   在 [Zsh](/index.php/Zsh "Zsh") 中启用:

 `~/.zshrc`  `source /usr/share/doc/pkgfile/command-not-found.zsh` 

## 参阅

*   [Bash#The_"command_not_found"_hook](/index.php/Bash#The_.22command_not_found.22_hook "Bash") - A section comparing [pkgfile](https://www.archlinux.org/packages/?name=pkgfile) and [command-not-found](https://aur.archlinux.org/packages/command-not-found/)