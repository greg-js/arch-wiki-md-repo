**翻译状态：** 本文是英文页面 [Pacman/Restore local database](/index.php/Pacman/Restore_local_database "Pacman/Restore local database") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-10-16，点击[这里](https://wiki.archlinux.org/index.php?title=Pacman%2FRestore+local+database&diff=0&oldid=489928)可以查看翻译后英文页面的改动。

如果遇到下面的问题，很可能需要恢复pacman本地数据库：

*   `pacman -Q`什么都不输出，`pacman -Syu`错误地报告系统已为最新。
*   使用`pacman -S`安装软件包时，很多已经安装过的依赖提示未安装。

pacman储存本地软件包的数据库`/var/lib/pacman/local`很可能已经损坏甚至丢失。这是很严重的问题，请按照如下步骤修复。

首先，确认pacman的日志文件还在：

```
$ ls /var/log/pacman.log

```

如果日志丢失了，那就*不能*使用本方法修复，可以尝试使用[Xyne的软件包检测脚本](https://bbs.archlinux.org/viewtopic.php?pid=670876)重建数据库。要是还行不通，很遗憾，最后的路就是重装系统。

## 日志过滤脚本

创建一个awk脚本文件，内容如下 ：

 `log2pkglist.awk` 
```
#!/bin/awk -f

i = 3 {}

$3 ~ /^\[[^]]+\]$/ {
  i = 4
}

$i ~ /^(installed|upgraded)$/ {
  pkg[$(i+1)] = 1
  next
} 

$i == "removed" {
  pkg[$(i+1)] = 0
} 

END {
  for (i in pkg) if (pkg[i]) print i
}

```

打上可执行标志：

```
$ chmod +x log2pkglist.awk

```

## 生成软件包列表

运行该脚本，输出到一个文本文件中：

```
$ ./log2pkglist.awk /var/log/pacman.log > pkglist.orig

```

（可选）手动检查`pkglist.orig`，删除所有不需要重新安装的软件包，例如：自己从ABS安装的软件包。

过滤掉无法从软件仓库中安装的软件包：

```
$ { cat pkglist.orig; pacman -Slq; } | sort | uniq -d > pkglist

```

**Note:** If this fails with `failed to initialise alpm library`, then check if `/var/lib/pacman/local/ALPM_DB_VERSION` exists - if not, then run `pacman-db-upgrade` as root followed by `pacman -Sy` and then **retry the previous command**.

检查**base**软件包组中的软件包是否缺失，并加入列表：

```
$ comm -23 <(pacman -Sgq base) pkglist.orig >> pkglist

```

当`pkglist`列表内容完备后，继续下一步，利用这个列表恢复数据库。

## 恢复数据库

建立临时的缓存、数据库以及根目录：

```
tmp=~/tmp
mkdir -p "${tmp}"

pushd "${tmp}"
dbpath=$(readlink -f ./dbpath)
root=$(readlink -f ./root)
cache=$(readlink -f ./cache)
log=/dev/null
mkdir -p "${dbpath}" "${cache}" "${root}"
popd

recovery-pacman() {
     sudo pacman "$@"  \
     --log /dev/null   \
     --noscriptlet     \
     --dbonly          \
     --force           \
     --nodeps          \
     --needed
 }
```

同步临时目录中的数据库：

```
$ recovery-pacman -Sy

```

或者复制系统的数据库：

```
$ cp -r /var/lib/pacman/sync "${dbpath}"

```

（可选）要避免下载和处理当前系统本地数据库中存在的软件包，复制本地数据库到临时目录：

```
$ cp -r /var/lib/pacman/local "${dbpath}"

```

从上一步获取的`pkglist`生成临时本地数据库：

```
$ recovery-pacman -S --nodeps --needed $(< pkglist)

```

**注意:** 由于`--noscriptlet`选项，fakeroot生成的文件不会被真正安装到系统中。

生成数据库后，复制到真正的系统中：

```
# cp -r "${dbpath}"/local /var/lib/pacman

```

最后，更新本地数据库，将不受其他软件包依赖的软件包标记为手动安装，剩下的标记为依赖安装：

```
# pacman -D --asdeps $(pacman -Qq)
# pacman -D --asexplicit $(pacman -Qtq)

```