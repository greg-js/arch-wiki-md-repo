`gcc` 有一个非常有用的工具叫 `ccache`. 主页位于[这里](http://ccache.samba.org)。

如果总是不停的编译同一个程序 — 例如实验不同的内核补丁、测试自己的开发等 — 那么 `ccache` 是完美的选择。尽管第一次编译会花费长一点的时间，有了`ccache`，后续的编译将变得非常非常快。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 为 makepkg 启用 ccache](#.E4.B8.BA_makepkg_.E5.90.AF.E7.94.A8_ccache)
    *   [1.2 启用命令行](#.E5.90.AF.E7.94.A8.E5.91.BD.E4.BB.A4.E8.A1.8C)
    *   [1.3 启用 colorgcc 支持](#.E5.90.AF.E7.94.A8_colorgcc_.E6.94.AF.E6.8C.81)
*   [2 Misc](#Misc)
    *   [2.1 修改缓存目录](#.E4.BF.AE.E6.94.B9.E7.BC.93.E5.AD.98.E7.9B.AE.E5.BD.95)
    *   [2.2 CLI](#CLI)
*   [3 参见](#.E5.8F.82.E8.A7.81)

## 安装

[安装](/index.php/Pacman "Pacman") 位于 [官方软件仓库](/index.php/Official_repositories "Official repositories") 的 [ccache](https://www.archlinux.org/packages/?name=ccache) 软件包。

### 为 makepkg 启用 ccache

要在 makepkg 启用 ccache，请编辑 `/etc/makepkg.conf`. 在 `BUILDENV` 中删除 ccache 前的感叹号：

```
 BUILDENV=(fakeroot !distcc color ccache !xdelta)

```

**Note:** 如果要编译 KDE ，需要不要导出 CPP 而是导出 CXX — 这将会避免一些错误。

### 启用命令行

如果从命令行编译而不是生成软件包，也可以使用`ccache`提高速度。

先修改 `$PATH`，添加`ccache`所在路径。

```
export PATH="/usr/lib/ccache/bin/:$PATH"

```

可以将其加入 `~/.bashrc`，这样以后可以一直使用。

### 启用 colorgcc 支持

colorgcc 也是一个编译器外壳，所以需要确保外壳的调用顺序是正确的。

```
export PATH="/usr/lib/colorgcc/bin/:$PATH"    # As per usual colorgcc installation, leave unchanged (don't add ccache)
export CCACHE_PATH="/usr/bin"                 # Tell ccache to only use compilers here

```

colorgcc 需要调用 ccache 而不是真正的编译器。编辑`/etc/colorgcc/colorgccrc` 修改所有`/usr/bin` 路径为`/usr/lib/ccache/bin`：

 `/etc/colorgcc/colorgccrc` 

```
g++: /usr/lib/ccache/bin/g++
gcc: /usr/lib/ccache/bin/gcc
c++: /usr/lib/ccache/bin/g++
cc: /usr/lib/ccache/bin/gcc
g77:/usr/bin/g77
f77:/usr/bin/g77
gcj:/usr/bin/gcj
```

## Misc

### 修改缓存目录

可以将缓存目录 `~/.ccache` 配置到其它地方，例如 SSD 或 ramdisk:

```
export CCACHE_DIR=/ramdisk/ccache             # ccache 将使用这个环境变量给出的缓存目录

```

### CLI

此外可以使用 ccache 命令行工具。

显示统计数据:

```
$ ccache -s

```

清空缓存:

```
$ ccache -C

```

## 参见

*   [ccache 主页](http://ccache.samba.org/)
*   [ccache 手册](http://ccache.samba.org/manual.html)