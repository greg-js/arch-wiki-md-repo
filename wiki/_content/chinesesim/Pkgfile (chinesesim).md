**翻译状态：** 本文是英文页面 [Pkgfile](/index.php/Pkgfile "Pkgfile") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-03-13，点击[这里](https://wiki.archlinux.org/index.php?title=Pkgfile&diff=0&oldid=549364)可以查看翻译后英文页面的改动。

工具**pkgfile**是检查[官方软件仓库](/index.php/%E5%AE%98%E6%96%B9%E8%BD%AF%E4%BB%B6%E4%BB%93%E5%BA%93 "官方软件仓库")中软件包文件的工具。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 示例](#示例)
*   [3 "Command not found" 钩子](#"Command_not_found"_钩子)
*   [4 自动更新](#自动更新)

## 安装

[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")软件包[pkgfile](https://www.archlinux.org/packages/?name=pkgfile) 或 [pkgfile-git](https://aur.archlinux.org/packages/pkgfile-git/)。

更新文件数据库:

```
# pkgfile --update

```

## 示例

查找文件 "makepkg" 属于哪个软件包:

 `$ pkgfile makepkg`  `core/pacman` 

列出 [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) 包含的所有文件：

 `$ pkgfile -l archlinux-keyring` 
```
core/archlinux-keyring usr/
core/archlinux-keyring usr/share/
core/archlinux-keyring usr/share/pacman/
core/archlinux-keyring usr/share/pacman/keyrings/
core/archlinux-keyring usr/share/pacman/keyrings/archlinux-revoked
core/archlinux-keyring usr/share/pacman/keyrings/archlinux-trusted
core/archlinux-keyring usr/share/pacman/keyrings/archlinux.gpg
```

这个结果与 `pacman -Ql` 类似(参考[pacman#Querying package databases](/index.php/Pacman#Querying_package_databases "Pacman"))，只不过这个命令查询的是远程仓库中的软件包。

## "Command not found" 钩子

pkgfile 包含一个叫做 "command not found" 的钩子，它会在你键入一个未知命令的时候自动在官方源中搜索。

要在所有的shell中启用它，需要将钩子的 source 添加到你的 shell 的配置文件中。

*   在 [Bash](/index.php/Bash "Bash") 中启用:

 `~/.bashrc`  `source /usr/share/doc/pkgfile/command-not-found.bash` 

*   在 [Zsh](/index.php/Zsh "Zsh") 中启用:

 `~/.zshrc`  `source /usr/share/doc/pkgfile/command-not-found.zsh` 

## 自动更新

**pkgfile** 提供了 [systemd](/index.php/Systemd "Systemd") 服务和 [定时器](/index.php/Systemd/Timers "Systemd/Timers")，可以自动同步 pkgfile 数据库。要自动启动，请 [启用](/index.php/Enable "Enable") `pkgfile-update.timer`.

默认情况下 pkgfile 每天更新一次，可以通过 [编辑单元文件](/index.php/Systemd#Editing_provided_units "Systemd")进行配置。