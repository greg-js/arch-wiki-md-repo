相关文章

*   [守护进程](/index.php/%E5%AE%88%E6%8A%A4%E8%BF%9B%E7%A8%8B "守护进程")

GPM（General Purpose Mouse，通用鼠标）是为 Linux 虚拟控制台（TTY）提供鼠标支持的守护进程。大多数 Linux 发行版中都有它。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 台式机](#.E5.8F.B0.E5.BC.8F.E6.9C.BA)
    *   [1.2 笔记本](#.E7.AC.94.E8.AE.B0.E6.9C.AC)
*   [2 配置](#.E9.85.8D.E7.BD.AE)

## 安装

### 台式机

用 [pacman](/index.php/Pacman "Pacman") 安装 [gpm](https://www.archlinux.org/packages/?name=gpm) 即可。

```
# pacman -S gpm

```

### 笔记本

用 [pacman](/index.php/Pacman "Pacman") 安装 [gpm](https://www.archlinux.org/packages/?name=gpm) 和 [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) 即可。

```
# pacman -S gpm xf86-input-synaptics

```

## 配置

`-m` 参数表示预定义要使用的鼠标。`-t` 参数表示预处理您使用的鼠标类型。要得到能被`-t`参数接受的类型的列表，用`-t help`运行`gpm`。

```
# gpm -m /dev/psaux -t help

```

如果鼠标只有两个键，将参数 `-2` 传递给 `GPM_ARGS`，这样第二个键就可以完成粘贴功能。

[gpm](https://www.archlinux.org/packages/?name=gpm) 软件包需要使用一些参数启动，这些参数可以添加到 `/etc/conf.d/gpm` 或者直接在运行 `gpm` 时使用。

*   对于 PS/2 鼠标，用下面这行替代已有的一行：

```
GPM_ARGS="-m /dev/psaux -t ps2"

```

*   对于 USB 鼠标应该使用：

```
GPM_ARGS="-m /dev/input/mice -t imps2"

```

*   对于 IBM Trackpoints 使用：

```
GPM_ARGS="-m /dev/input/mice -t ps2"

```

配置好合适的选项之后，在`/etc/rc.conf` 文件中把 `gpm` 添加至 `DAEMONS` 行里面。例如：

```
DAEMONS=(syslog-ng **gpm** network netfs crond)

```

更多信息见 [gpm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gpm.8)。