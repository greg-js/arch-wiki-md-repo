[Gamin](https://en.wikipedia.org/wiki/Gamin "wikipedia:Gamin") 是一个文件和目录监控系统，替代 FAM (File Alteration Monitor)。它是一个程序库提供的服务，用来检测文件和目录的改动。

Gamin 用 [inotify](https://en.wikipedia.org/wiki/inotify "wikipedia:inotify") 实现了 [FAM](/index.php/FAM "FAM") 标准，与 FAM 兼容，可以完全替代 FAM。它是一个[GNOME](/index.php/GNOME "GNOME")的项目，但它没有Gnome依赖。

## 安装

如果安装了 FAM，先要移除 [fam](https://aur.archlinux.org/packages/fam/) 包，忽略依赖：

```
# systemctl disable fam.service
# pacman -Rd fam

```

安装 [gamin](https://www.archlinux.org/packages/?name=gamin) 软件包。

## 外部链接

*   [FAM, Gamin and inotify](http://www.noah.org/wiki/FAM,_Gamin,_inotify)