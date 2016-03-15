Reflector 是一个脚本程序，从[镜像状态](https://www.archlinux.org/mirrors/status/)页面获取镜像列表，过滤出还在更新的页面并根据速度排列，然后覆盖文件`/etc/pacman.d/mirrorlist`。

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")软件包 [reflector](https://www.archlinux.org/packages/?name=reflector)。

## 使用示例

先备份 `/etc/pacman.d/mirrorlist`::

```
# cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup

```

下面命令将过滤出 5 个镜像，按速度排列并覆盖 `/etc/pacman.d/mirrorlist`:

```
# reflector -l 5 --sort rate --save /etc/pacman.d/mirrorlist

```

要查看所有命令，请运行

```
# reflector --help

```

**警告:** 同步或者更新前请保证 mirrorlist 不包含任何奇怪的内容。

## 外部链接

*   项目官方页面: [http://xyne.archlinux.ca/projects/reflector/](http://xyne.archlinux.ca/projects/reflector/)