使用 Bootchart 可以很方便地分析 Linux 启动流程，分析结果可以用来优化启动速度。包含的 bootchartd 服务负责记录及展示分析结果。

**注意:** Bootchart 已经成为 systemd 的一部分，请参考 [Improve boot performance#Analyzing the boot process](/index.php/Improve_boot_performance#Analyzing_the_boot_process "Improve boot performance") 页面。本文介绍的是合并之前的老版本和bootchart2。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装Bootchart](#安装Bootchart)
*   [2 运行Bootchart](#运行Bootchart)
    *   [2.1 启动引导器设置](#启动引导器设置)
*   [3 生成分析结果图表](#生成分析结果图表)
    *   [3.1 问题解决](#问题解决)
*   [4 参考资料](#参考资料)

## 安装Bootchart

安装 [bootchart](https://aur.archlinux.org/packages/bootchart/)。

## 运行Bootchart

要运行 bootchart，需要将他添加到引导器的初始化进程选项，或者手动在init脚本（通常是rc.sysinit）中手动添加。不过需要注意的是，如果你是手动添加到init脚本的，那么也要手动停止它，总之，这种情况需要特别留意！

### 启动引导器设置

下面我们介绍常用的方法，即将原有引导选项复制一份，并在内核项后面添加`init=/usr/bin/bootchartd`. 方法参阅[kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). 然后通过启动引导器引导bootchart。这样bootchart会在登录提示符出现的时候自动停止。

## 生成分析结果图表

你可以通过运行下面的命令来生成分析结果图：

```
bootchart-render

```

确保运行命令的目录有写权限，程序就会生成一个名为'bootchart.png'的图像，这就是分析结果图。

你需要事先安装Java运行环境并且在此之前设置正确。

### 问题解决

Bootchart-render 如果无法生成 'bootchart.png' 图片并显示如下错误信息：

```
/var/log/bootchart.tgz not found

```

主要原因是 bootchartd 无法检测到启动过程何时停止。如该使用非 KDM 或 GDM 的启动管理器如 [SLIM](/index.php/SLiM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SLiM (简体中文)") 或 entrance 时会发生这个问题。可以打开 `/sbin/bootchartd` 脚本并将这些程序加到 `exit_proc` 变量中：

```
# The processes we have to wait for
local exit_proc="gdmgreeter gdm-binary kdm_greet kdm slim"

```

如果没有使用启动管理器，修改 `exit_proc` 变量为：

```
# The processes we have to wait for
local exit_proc="login"

```

## 参考资料

*   [Bootchart主页](http://www.bootchart.org/)
*   [如何快速启动上网本的 LWN 文章](http://lwn.net/Articles/299483/) 写得很好，提供了许多快速启动的技巧，尽管许多不适合一般用户使用。(修改 X.org 内核 kernel 等)。