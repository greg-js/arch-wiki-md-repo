警告: The moon plugin is not fully functional yet. Not all pages with Silverlight will work correctly and some will force Firefox to die. Still looks pretty though.

Moonlight是一个开源的实现Microsoft's Silverlight运行环境. 目前它还在测试中并且有可能今年晚些时候正式发布. Moonlight currently still needs the mono and olive packages built from SVN to create a working plugin.

# 安装Moonlight

Moonlight需要从AUR中来构建. 你可以下载独立包或者使用[AUR helper scripts](/index.php/AUR_helpers "AUR helpers")其中的工具.

## 手动安装

需要mono-svn, monodocer-svn, olive-svn 和moon-svn这四个包. 使用这个顺序来构建和安装:

	[monodocer-svn](https://aur.archlinux.org/packages/monodocer-svn/)

	[olive-svn](https://aur.archlinux.org/packages/olive-svn/)

安装这四个包都使用相同的命令, 解压tarball,然后运行:

```
makepkg -i 

```

从新建的文件夹.